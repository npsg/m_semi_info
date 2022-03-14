# Azure Databricks でのデータの探索と変換

1. Azure Databricks の説明   
https://docs.microsoft.com/ja-jp/learn/modules/describe-azure-databricks/
2. Azure Databricks でデータの読み取りと書き込みを行う   
https://docs.microsoft.com/ja-jp/learn/modules/read-write-data-azure-databricks/    

>**やってみましょう！** <br>
>「03-Reading-and-writing-data-in-Azure-Databricks」ワークスペースにある「1.Reading Data - CSV」〜「6.Reading Data - Lab」を実行してみましょう。
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
3. Azure Databricks でデータフレームを操作する   
https://docs.microsoft.com/ja-jp/learn/modules/work-dataframes-azure-databricks/
4. Azure DatabricksでDataFramesの高度なメソッドを操作する   
https://docs.microsoft.com/ja-jp/learn/modules/work-dataframes-advanced-methods-azure-databricks/
