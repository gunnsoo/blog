---
title: "Airflow Docker ImageのEntrypointの挙動"
date: 2021-12-12T20:32:05+09:00
draft: false
tags: [ "Airflow" ]
---

Airflow公式の[Docker Image](https://hub.docker.com/r/apache/airflow)を使って、Airflowクラスターを構築しようとした際に、Docker Entrypointの挙動に少しハマったので記事にします。

&nbsp;

### 遭遇した事象
Airflowでは、クラスタとバックエンドDBの接続後にdb initコマンドを叩いてスキーマを作る必要があります。
これはDBとの接続設定さえされていれば、SchedulerやWebserver、どのコンポーネントから叩いても良いです。
```shell
airflow db init
```

&nbsp;

また、デフォルトのAuth設定ではWebserverにアクセスするよりも前に、ユーザをパスワードとともに作っておく必要があります。
```shell
# create an admin user
airflow users create \
  --username admin \
  --firstname Peter \
  --lastname Parker \
  --role Admin \
  --email spiderman@superhero.org
```

&nbsp;

そのため、クラスタ立ち上げ時にこの２つの初期化コマンドを実行したいと思って、docker-compose.ymlに以下のようにコマンドを書いてました。

```yml
services:
  airflow-scheduler:
    image: apache/airflow
    ...
    command: >
        sh -c '
        airflow db init &&
        airflow users create \
            --username admin \
            --firstname Peter \
            --lastname Parker \
            --role Admin \
            --email spiderman@superhero.org
        '
```

しかし上のymlだと以下のようなエラーになります。

```shell
airflow command error: argument GROUP_OR_COMMAND: invalid choice: 'sh' (choose from 'celery',
 'cheat-sheet', 'config', 'connections', 'dags', 'db', 'info', 'jobs', 'kerberos',
 'kubernetes', 'plugins', 'pools', 'providers', 'roles', 'rotate-fernet-key', 'scheduler',
 'standalone', 'sync-perm', 'tasks', 'triggerer', 'users', 'variables', 'version',
 'webserver'), see help above.
usage: airflow [-h] GROUP_OR_COMMAND ...

...
```

&nbsp;

### 原因
エラーを見るに、どうやらcommandに渡した文字列がairflowコマンドの引数として渡っているようです。

これには心当たりがあって、そもそもAirflow公式が提供しているdocker-compose.ymlを見ると、
```yml
...
services:
  airflow-webserver:
    ...
    command: webserver
  airflow-scheduler:
    ...
    command: scheduler
  airflow-worker:
    ...
    command: celery worker
...
```
とあり、「なんでairflowコマンド省略できるん？」と前から疑問でした。

&nbsp;

というわけで、airflow imageの[Dockerfile](https://github.com/apache/airflow/blob/main/Dockerfile)を見ると、
```yml
ENTRYPOINT ["/usr/bin/dumb-init", "--", "/entrypoint"]
```
とENTRYPOINTが定義してあり、コンテナ立ち上げ時に/entrypointが実行されるであろうことが見て取れます。

&nbsp;

ENTRYPOINTとCMDの両方が定義されている場合、CMDはENTRYPOINTに引数として渡されるので、docker-compose.ymlでcommandとして定義した文字列が/entrypointに引数として渡っていることが判明しました。\
(ENTRYPOINTとCMDについてはこちらの記事が参考になりました。　[DockerfileのCMDとENTRYPOINTを読み解く(2/3) — CMD命令とENTRYPOINT命令の基礎 #docker #dockerfile](https://www.creationline.com/lab/39705))

&nbsp;

じゃあ次はということで、[/entrypointの中身](https://github.com/apache/airflow/blob/main/scripts/in_container/prod/entrypoint_prod.sh)を見てみると、
```shell
exec "airflow" "${@}"
```
と/entrypointに対する引数が全てairflowコマンドに渡されていることがわかります。

&nbsp;

また、第１引数に'bash'もしくは'python'が指定された際には、/bin/bashかpythonコマンドにたいして引数が渡されるようになっています。
```shell
AIRFLOW_COMMAND="${1:-}"

function exec_to_bash_or_python_command_if_specified() {
    # If one of the commands: 'bash', 'python' is used, either run appropriate
    # command with exec
    if [[ ${AIRFLOW_COMMAND} == "bash" ]]; then
       shift
       exec "/bin/bash" "${@}"
    elif [[ ${AIRFLOW_COMMAND} == "python" ]]; then
       shift
       exec "python" "${@}"
    fi
}

exec_to_bash_or_python_command_if_specified "${@}"
```

&nbsp;

また、第１引数に'airflow'が指定された際は、shiftして第２引数以降をairflowコマンドに渡すようになっています。
```shell
AIRFLOW_COMMAND="${1:-}"

# Remove "airflow" if it is specified as airflow command
# This way both command types work the same way:
#
#     docker run IMAGE airflow webserver
#     docker run IMAGE webserver
#
if [[ ${AIRFLOW_COMMAND} == "airflow" ]]; then
   AIRFLOW_COMMAND="${2:-}"
   shift
fi

exec "airflow" "${@}"
```

そのため、コンテナ起動時にコマンドとしてairflow webserverで指定しようが、単にwebserverのみで指定しようが同じ動きをするようになってます。

&nbsp;

### 解決策
commandに'sh -c'を指定していると、sh -cごとairflowコマンドの引数として渡されてしまうので、'bash -c'を指定するようにしたら解決しました。
```yml
services:
  airflow-scheduler:
    image: apache/airflow
    ...
    command: >
        bash -c '
        airflow db init &&
        airflow users create \
            --username admin \
            --firstname Peter \
            --lastname Parker \
            --role Admin \
            --email spiderman@superhero.org
        '
```

&nbsp;

### おわりに
[公式のEntrypointのページ](https://airflow.apache.org/docs/docker-stack/entrypoint.html#executing-commands)見ればすぐわかったねってお話でした。

\
&nbsp;