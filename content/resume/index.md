---
title: "Resume"
date: 2022-10-06T09:11:05+09:00
draft: false
---

# Summary
データパイプラインの開発とかしてきて、最近はデータ基盤どう作るかとか戦略考えたりとか実際の開発したりとかしてる。
TBD

&nbsp;

# Work Experience
### [2019/04-Now]　Software Engineer　Rakuten Group, Inc.

- __[2022/01-Now] DWH Improvement Promotion__  
<役割>  
企画立案者として、草案作りや調整などを担当  
<概要>  

戦略考えたりとかデータ基盤のデザインとかしてる

&nbsp;

- __[2020/03-Now] Personalization Optimization Platform__  
<役割>  
メンバーから入り、後にリーダーとして、開発全般を担当  
<使用技術>  
Python, Go, Luigi, Airflow, PySpark, Apache Iceberg, Great Expectations, DataRobot  
<概要>  
社内のマーケティング担当者向けに、機械学習を用いてどの顧客にリーチすると施策効果が高いかを予測するシステムを開発。  
プロジェクト初期では、エンジニア３人チームの内のメンバーとして、草案の状態からリリースまでの開発を担当。  
その後は、エンジニア４人チームの内のリーダーとして、開発業務全般を担当した。  
Goでスケジューラー、Pythonでデータパイプラインを記述し、Luigiでワークフロー管理をする構成をプロジェクト初期では取っており、デザインから実装まで行なった。  
1年近く運用を続ける中で、データパイプラインの拡張性と特徴量管理に課題が出てきたため、システム基盤をリプレイスした。  
新基盤では、ワークフロー管理にAirflowを採用し、ユースケースごとに記述していたデータパイプラインを、テンプレートと定義ファイルにより記述できるように変えた。    
また、Apache Icebergを用いて特徴量管理をする構成に変え、ユースケースごとに都度生成していた特徴量を１箇所に集約させるようにした。  

&nbsp;

- __[2019/07-2020/02] Blockchain Based System__  
<役割>  
メンバーとして、主にCI/CD整備を担当  
<使用技術>  
Bash, Hyperledger Fabric, Docker Swarm  
<概要>  
エンジニア４人チームの内のメンバーとして、データ保持コストを抑える目的でブロックチェーン技術を用いて金融データを長期的に管理するシステムを開発。  
[Hyperledger Fabric](https://github.com/hyperledger/fabric "GitHubへ移動")というOSSの分散台帳フレームワークをコア技術として用いた。  
Docker Swarmを用いて複数ノードにHyperledger Fabricの各コンポーネントをデプロイする構成の中で、テスト自動化や各環境へのデプロイを行うパイプラインの開発を主に担当した。  

&nbsp;

# Education
- 2015年 - 2019年　学士・経済学　慶應義塾大学

&nbsp;

# Skills
1~3
- 1 : 使ったことがある
- 2 : 業務で導入を検討し調査などを行なった
- 3 : 業務で使用している/本番環境で運用している

項目別に数値化した方がよさそう

&nbsp;

## Languages
Python : 3
Go : 3
Java : 3
SQL : 

&nbsp;

## Data Processing Tools
1~3
- 1 : 使ったことがある
- 2 : 業務で導入を検討し調査などを行なった
- 3 : 業務で使用している/本番環境で運用している

Hadoop
Apahce Spark
Pandas
Dask

Apahce Iceberg

Apahce Airflow
Luigi

CliskHouse

&nbsp;

# Communication Languages
Japanese : Native
English  : Business Intermediate

&nbsp;

# Area of Interests
- Data Engineering
- MLOps
- Analytics

- Golf
- Tennis
