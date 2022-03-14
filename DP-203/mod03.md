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

>**やってみましょう！** <br>
>「日付と時刻の操作を実行する」で登場する「07-Dataframe-Advanced-Methods」ワークスペースにある「1.DateTime-Manipulation」〜「3.Exercise-Deduplication-of-Data」を実行してみましょう。
>最後の演習では、ETL（Extract/Transform/Load,抽出/変換/ロード）を実施します。重複するレコードや大文字・小文字の混在、ハイフンの混在があるため、103,000レコードになっています。
>この重複を排除し、100,000レコードにした上で、Parquetファイルに書き出します。以下を参考にセルの結果を確認しながら、実行するようにしましょう。
```python
# 入力データのパスと出力先を指定します。
# すでに出力先が存在すれば、削除します。
sourceFile = "dbfs:/mnt/training/dataframes/people-with-dups.txt"
destFile = userhome + "/people.parquet"
dbutils.fs.rm(destFile, True)
# 指定されたファイルの最大バイト数を返す
print(dbutils.fs.head(sourceFile))
```
```python
# Sparkでは、データを「パーティション」という単位で並列処理します。HDFSから読み出したブロック数がパーティション数です。
# groupByやjoinなどの処理は、パーティション間のデータ交換が生じます（シャッフル処理）。
# spark.sql.shuffle.partitions= Shuffle Stage Input Size / Target Size(100MB~200MB)
spark.conf.set("spark.sql.shuffle.partitions", 8)
# CSVファイル読み込み
df = (spark
    .read
    .option("header", "true")
    .option("inferSchema", "true")
    .option("sep", ":")
    .csv(sourceFile)
)

from pyspark.sql.functions import *
# 解答の一部を修正、dropDuplicatesで重複した行を取り除けばいい、
# "lcFirstName", "lcMiddleName", "lcLastName", "ssnNums"は変換後の正しい列だからdropしなくてよい。
dedupedDF = (df
  .select(col("*"),
      lower(col("firstName")).alias("lcFirstName"),
      lower(col("lastName")).alias("lcLastName"),
      lower(col("middleName")).alias("lcMiddleName"),
      # translate(col("ssn"), "-", "").alias("ssnNums")
      # regexp_replace(col("ssn"), "-", "").alias("ssnNums")
      regexp_replace(col("ssn"), """^(\d{3})(\d{2})(\d{4})$""", "$1-$2-$3").alias("ssnNums")
   )
  .dropDuplicates(["lcFirstName", "lcMiddleName", "lcLastName", "ssnNums", "gender", "birthDate", "salary"])
  #.drop("lcFirstName", "lcMiddleName", "lcLastName", "ssnNums")
)
dedupedDF.show()
```
<img width="800" alt="image" src="https://user-images.githubusercontent.com/69043643/158163795-aef7dc69-e5f9-49b7-805c-05240665e503.png">

```python   
(dedupedDF.write
   .mode("overwrite")
   .option("compression", "snappy")
   .parquet(destFile)
)
dedupedDF = spark.read.parquet(destFile)
print("Total Records: {0:,}".format( dedupedDF.count() ))
display( dbutils.fs.ls(destFile) )
```

```python
finalDF = spark.read.parquet(destFile)
finalCount = finalDF.count()

clearYourResults()
validateYourAnswer("01 Expected 100000 Records", 972882115, finalCount)
summarizeYourResults()
```
<img width="682" alt="image" src="https://user-images.githubusercontent.com/69043643/158163929-bc56b5d3-bdbc-4f50-82cb-fb75c24dda3d.png">
