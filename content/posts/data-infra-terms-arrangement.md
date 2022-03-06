---
title: "データ基盤周りの用語整理"
date: 2022-02-05T16:35:37+09:00
draft: true
tags: [ "data" ]
---

仕事でデータ基盤関連のことについて資料作りすることになったので、自分の理解の整理ように改めて用語をまとめておく。

&nbsp;

### 用語一覧
**データレイク (Data Lake)**    
データソースからデータをそのままコピーして１つのシステムに集約したもの。  
データが適切に整理されていなくて検索できず利用できない状態になったものを、Lake(湖)に対しSwamp(沼)でデータスワンプ(Data Swamp)という。  
そうならないように、データに対してのメタデータを適切に管理する仕組み(データカタログ(Data Catalog))が必要。  

>A data lake is a central location that holds a large amount of data in its native, raw format. Compared to a hierarchical data warehouse, which stores data in files or folders, a data lake uses a flat architecture and object storage to store the data.‍ Object storage stores data with metadata tags and a unique identifier, which makes it easier to locate and retrieve data across regions, and improves performance. By leveraging inexpensive object storage and open formats, data lakes enable many applications to take advantage of the data. (出典 : https://databricks.com/jp/discover/data-lakes/introduction/)

>データレイクは、規模にかかわらず、すべての構造化データと非構造化データを保存できる一元化されたリポジトリです。データをそのままの形で保存できるため、データを構造化しておく必要がありません。また、ダッシュボードや可視化、ビッグデータ処理、リアルタイム分析、機械学習など、さまざまなタイプの分析を実行し、的確な意思決定に役立てることができます。(出典 : https://aws.amazon.com/jp/big-data/datalakes-and-analytics/what-is-a-data-lake/)

>データレイクは、多数のソースからのビッグデータを元のままの多様な形式で保持する中央ストレージリポジトリです。構造化データ、半構造化データ、非構造化データを格納できるので、将来の使用のためにデータをより柔軟な形式に保持できます。データレイクは、データを格納する際に識別子とメタデータタグを関連付けることで、検索を高速化します。(出典 : https://www.talend.com/jp/resources/what-is-data-lake/)

&nbsp;

**データウェアハウス (Data Ware House/DWH)**   
組織内の様々なデータを統合・蓄積して、意思決定に活用できるように整理したもの。  
 
>データウェアハウスとは、レポート作成や分析に利用するために、組織内の業務システムや外部データソースから発生したデータを収集するシステムです。データウェアハウスは、情報の中央リポジトリとして、従来の運用データストアではアクセスや存在が困難な現在および過去の意思決定支援情報をユーザーに提供します。その主な焦点は、異なるシステムからのデータを相関させることです。(出典 : https://databricks.com/jp/glossary/data-warehouse)

>データウェアハウスは、より多くの情報に基づく意思決定を行うための、分析可能な情報のセントラルリポジトリです。データは、通常一定の周期で、トランザクションシステム、リレーショナルデータベース、その他のソースからデータウェアハウスに移されます。ビジネスアナリスト、データエンジニア、データサイエンティスト、および意思決定者は、ビジネスインテリジェンス (BI) ツール、SQL クライアント、その他の分析アプリケーションを通してそのデータにアクセスします。(出典 : https://aws.amazon.com/jp/data-warehouse/)

>データウェアハウス（Data Ware House）とは、組織の意思決定を支援するために使用される大規模なビジネスデータを指します。データウェアハウスの概念自体は1980年代からありました。当初のデータウェアハウスは、データを業務で使用するだけでなく、ビジネスインテリジェンスを明らかにする意思決定支援システムで活用できるように支援するために開発されたものでした。データウェアハウスに含まれる大量のデータは、マーケティング/営業/財務/顧客向けアプリといった社内のアプリケーション、外部のパートナーシステムなど、さまざまな場所からもたらされる特徴があります。(出典 : https://www.talend.com/jp/resources/what-is-data-warehouse/)

&nbsp;

**データマート (Data Mart)**  
特定の利用者・ユースケースに特化した形で、データを加工・整理したもの。  
DWHに従属して作られるものもあれば、独立して作られるものもあるし、その両方を合わせた形で作られるものもある。  

>データマートは、特定のチームや部署 (財務、マーケティング、営業など) のニーズに対応したデータウェアハウスです。規模が小さく、的が絞られており、ユーザーのコミュニティにとって最適なデータの概要が保存されています。データマートがデータウェアハウスの一部である場合もあります。(出典 : https://aws.amazon.com/jp/data-warehouse/)

>データマートは、特定ユーザーグループのニーズに対応するサブジェクト指向のデータベースです。エンタープライズデータウェアハウス内のパーティションに分割されたセグメントである場合もあります（常にそうではありません）。データウェアハウスやオペレーショナルデータストア内の情報へのアクセスを（数か月以上もかけずに）数日で実現するデータマートは、ビジネスプロセスを加速します。迅速に知見を得るための費用対効果の高い方法です。(出典 : https://www.talend.com/jp/resources/what-is-data-mart/)

&nbsp;

**データカタログ (Data Catalog)**  
組織内のデータに対するメタデータを一元化し整理したもの。  
メタデータには、データの発生元やデータ定義、導出方法などが含まれ得る。  

>A Data Catalog is a collection of metadata, combined with data management and search tools, that helps analysts and other data users to find the data that they need, serves as an inventory of available data, and provides information to evaluate fitness data for intended uses. (出典 : https://www.alation.com/blog/what-is-a-data-catalog/)

&nbsp;

**データマイニング**  
ビッグデータから新たな知見や規則性を発見する手法やプロセスのこと。おむつとビールの話が有名。  
>データマイニングとは、企業がビジネスニーズに関連する知見を得るために、データ内のパターン検出を行うためのプロセスを指します。 これはビジネスインテリジェンスとデータサイエンスの双方にとって不可欠です。 企業が生データを実用的な知見に変換するのに利用できる、データマイニング手法は数多く存在します。 その中には、最先端の人工知能からデータプレパレーションの基本まで、あらゆるもの含まれており、どちらもデータへの投資の価値を最大化するための鍵となります。(出典 : https://www.talend.com/jp/resources/data-mining-techniques/)

&nbsp;

**DAMA**  
>データ管理を実践する国際的な非営利団体　国際データマネジメント協会（Data Management Association International(略称：DAMA-I)) の日本支部です。DAMAでは、データマネジメント知識体系ガイド（DMBOK)やデータマネジメント辞書などのベストプラクティスリソースを提供しています。(出典 : https://www.dama-japan.org/)

&nbsp;

**DMBOK**  
データマネジメント知識体系ガイド(Data Management Body of Knowledge)の略称。  

{{< amazon asin="4296100491" title="データマネジメント知識体系ガイド 第二版" >}}

&nbsp;

**FeatureStore**

>The Feature Store is where the features are stored and organized for the explicit purpose of being used to either train models (by Data Scientists) or make predictions (by applications that have a trained model). It is a central location where you can either create or update groups of features created from multiple different data sources, or create and update new datasets from those feature groups for training models or for use in applications that do not want to compute the features but just retrieve them when it needs them to make predictions.(出典 : https://www.featurestore.org/what-is-a-feature-store)


**MLOps**





**ETL/ELT**