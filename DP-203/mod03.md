# Azure Databricks でのデータの探索と変換

1. Azure Databricks の説明   
https://docs.microsoft.com/ja-jp/learn/modules/describe-azure-databricks/
2. Azure Databricks でデータの読み取りと書き込みを行う   
https://docs.microsoft.com/ja-jp/learn/modules/read-write-data-azure-databricks/    

>**やってみましょう！** <br>
>「CSV 形式でデータを読み取る」で登場する「03-Reading-and-writing-data-in-Azure-Databricks」ワークスペースにある「1.Reading Data - CSV」〜「6.Reading Data - Lab」を実行してみましょう。
>ただし、ユニット「CSV 形式でデータを読み取る-1.Reading Data - CSV」を完了しないと、最後の演習「6.Reading Data - Lab」まで進みません。演習の解答は「Solutions」サブフォルダー内にあります。
> - 6.Reading Data - Labでは、「testDF = <<FILL_IN>>」となっている部分を以下のように置き換えます。最後は、データフレームになっていることを確認してください。
```python
from pyspark.sql.types import *

schema = StructType([
    StructField("prev_id", IntegerType(), False),
    StructField("curr_id", IntegerType(), False),
    StructField("n", IntegerType(), False),
    StructField("prev_title", StringType(), False),
    StructField("curr_title", StringType(), False),
    StructField("type", StringType(), False)
])

testDF = (spark.read
  .option("sep", "\t")
  .option("header", "true")
  .schema(schema)
  .csv(fileName)
)

testDF.printSchema()
``` 

> **DBFSの中身を見たい？**
> 1. 設定／管理コンソール／Workspace Settings／Advancedから「DBFS File Browser」をEnabledに変更します。
> 2. 全体をリロードし、データをクリックすると、「データベーステーブル」と「DBFS」が選択できるようになります。

3. Azure Databricks でデータフレームを操作する   
https://docs.microsoft.com/ja-jp/learn/modules/work-dataframes-azure-databricks/

>**やってみましょう！** <br>
>「データフレームについて説明する」で登場する「04-Working-With-Dataframes」ワークスペースにある「1.Describe-a-dataframe」〜「4.Exercise: Distinct Articles」を実行してみましょう。
>演習の解答は「Solutions」サブフォルダー内にあります。
> - 4.Exercise: Distinct Articlesでは、「<<FILL_IN>>」となっている部分を以下のように置き換えます。


Parquet ファイルを読み取り、必要な変換を適用して、レコードの合計数を実行し、すべてのデータが正しく読み込まれたことを確認
```python
from pyspark.sql.types import *

parquetDir = "/mnt/training/wikipedia/pagecounts/staging_parquet_en_only_clean/"

df = (spark
  .read
  .parquet(parquetDir)
  .select("article")
  .distinct()
)
totalArticles = df.count()

print("Distinct Articles: {0:,}".format( totalArticles ))
``` 
おまけとして、データを照合するスキーマを定義してみて、このスキーマを使用するように読み取り操作を更新
```python
from pyspark.sql.types import *

schema = StructType([
  StructField("project", StringType(), False),
  StructField("article", StringType(), False),
  StructField("requests", IntegerType(), False),
  StructField("bytes_served", LongType(), False)
])

totalArticles = (spark.read
  .schema(schema)
  .parquet(parquetDir)
  .select("article")
  .distinct()
  .count()
)

print("Distinct Articles: {0:,}".format( totalArticles ))
``` 
>**考えてみましょう！** <br>
>前の演習で行った「03-Reading-and-writing-data-in-Azure-Databricks」ワークスペースの「6.Reading Data - Lab」を再度開きます。最後のセルでtestDFを操作していることを確認します。        
>① 変数testDFの件数を求めてください。     
>② Apache Spark でパフォーマンスを向上させるための 1 つの手法であるキャッシュ機能を使い、①の結果を素早く求めてください。
>[解答例](mod03_ans1.md)

4. Azure DatabricksでDataFramesの高度なメソッドを操作する   
https://docs.microsoft.com/ja-jp/learn/modules/work-dataframes-advanced-methods-azure-databricks/
