# Apache Spark を使用してデータの探索と変換を行い、データウェアハウスに読み込む

1. Azure Synapse Analytics のApache Spark を使用したビッグデータのエンジニアリングについて   
https://docs.microsoft.com/ja-jp/learn/modules/understand-big-data-engineering-with-apache-spark-azure-synapse-analytics/

>**やってみましょう！** <br>
>「Azure Synapse Analytics で Apache Spark プールが機能するしくみ」にあるAzure Synapse Analytics で Apache Spark プールを作成を実施しておきましょう。   
> <img width="744" alt="image" src="https://user-images.githubusercontent.com/69043643/158170048-e405626a-1e7f-48c3-be58-2c7f6f625382.png">

2. Azure Synapse AnalyticsでApache Sparkノートブックを使用してデータを取り込む    
https://docs.microsoft.com/ja-jp/learn/modules/ingest-data-with-apache-spark-notebooks-azure-synapse-analytics/

>**やってみましょう！** <br>
>以下の演習が実施可能です。
>- 演習: Azure Synapse Analytics で Spark ノートブックを作成する
>- 演習: Spark ノートブックを開発する
>- 演習: Spark ノートブックを実行する
>- 演習: Spark ノートブックにデータを読み込む（準備に時間がかかります）
>    - [ラボファイルのセットアップが必要](lab.md) また、「Data Lakeへのコピー」も行います。
>    - 「data-engineering-synapse-ランダムな文字列」のリソースグループ内にあるSynapse Analytics ワークスペースからSynapse Studioを起動
>    - sale-small/Year=2016/Quarter=Q4/Month=12/Day=20161231を選択します。2016年です。右クリックし、新しいノートブックから「DatazFrameに読み込む」をクリックします。 
>    - <img width="905" alt="image" src="https://user-images.githubusercontent.com/69043643/158269316-1beaa71f-fbce-4407-84e8-ba2058717075.png">

>**注：**　自動生成すると、変数名がdata_pathではなく、dfになるので、読みかえてください。
><img width="905" alt="image" src="https://user-images.githubusercontent.com/69043643/158270789-4ed40b40-6969-4f80-a087-6f230422a062.png">


3. Azure Synapse AnalyticsのApache Sparkプールで DataFrameを使用してデータを変換する    
https://docs.microsoft.com/ja-jp/learn/modules/transform-data-with-dataframes-apache-spark-pools-azure-synapse-analytics/

>**やってみましょう！** <br>
>以下の演習が実施可能です。
>- **「Spark DataFrame にデータを読み込む」から、「次のような手順を実行します。」部分**。「COPY」という文字列は不要です。下記に置き換えてください。
> ```python
> %%pyspark
> df = spark.read.load('abfss://wwi-02@asadatalake1kp89zr.dfs.core.windows.net/sale-small/Year=2016/Quarter=Q4/Month=12/Day=20161231/sale-small-20161231-snappy.parquet', format='parquet')
> # display(df.limit(10))
> spark.sql("CREATE DATABASE IF NOT EXISTS nyctaxi")
> df.write.mode("overwrite").saveAsTable("nyctaxi.trip")
> ```
>- **演習: Spark ノートブックを開発する**<br>
> 以下のように、ストレージアカウントは結合しても構いません。
> ```python
> df = (spark.read \
>        .option('inferSchema', 'true') \
>        .json('abfss://wwi-02@asadatalake1kp89zr.dfs.core.windows.net/online-user-profiles-02/*.json', multiLine=True)
>    )
>
> df.printSchema()
> ```
> - **演習: Spark テーブルを作成する**<br>
> もう１度、データを読み直してから、実行しましょう。変数dfに注意です。
> ```python
> %%pyspark
> df = spark.read.load('abfss://wwi-02@asadatalake1kp89zr.dfs.core.windows.net/sale-small/Year=2016/Quarter=Q4/Month=12/Day=20161231/sale-small-20161231-snappy.parquet', format='parquet')
> df.printSchema()
> ```
> - **演習: Synapse の Apache Spark で入れ子構造をフラット化し、配列を分解する**<br>
> 「Spark ノートブックを開発する」で読み込んだjsonファイルを使います。手順5以降では、以下のimportが必要です。
> ```python
> from pyspark.sql.types import *
> from pyspark.sql.functions import *
> ```

4. Azure Synapse Analytics で SQL プールと Apache Spark プールを統合する   
https://docs.microsoft.com/ja-jp/learn/modules/integrate-sql-apache-spark-pools-azure-synapse-analytics/  
演習略
