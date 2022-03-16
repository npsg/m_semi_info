# Azure Synapse Link を使用してハイブリッドトランザクション分析処理 (HTAP) に対応する

1. Azure Synapse Analytics を使用したハイブリッド トランザクションおよび分析処理ソリューションの設計    
https://docs.microsoft.com/ja-jp/learn/modules/design-hybrid-transactional-analytical-processing-using-azure-synapse-analytics/  
2. Azure Cosmos DB を使用して Azure Synapse Link を構成する   
https://docs.microsoft.com/ja-jp/learn/modules/configure-azure-synapse-link-with-azure-cosmos-db/  

>**やってみましょう！** <br>
> Azure Cosmos DB SQL (Core) API アカウントで Synapse Link を有効にする   
> [ラボファイルのセットアップが必要](lab.md)    
> https://docs.microsoft.com/ja-jp/learn/modules/configure-azure-synapse-link-with-azure-cosmos-db/2-enable-cosmos-db-account-to-use    
> 分析ストアが有効なコンテナーを作成する      
> https://docs.microsoft.com/ja-jp/learn/modules/configure-azure-synapse-link-with-azure-cosmos-db/3-create-analytical-store-enabled-container    
> ※下記、「分析ストアが有効なコンテナーを作成する」を参照してください。

3. Azure Synapse Analytics で Apache Spark を使用して Azure Cosmos DB に対してクエリを実行する    
https://docs.microsoft.com/ja-jp/learn/modules/query-azure-cosmos-db-with-apache-spark-for-azure-synapse-analytics/   
4. Azure Synapse Analytics の SQL サーバーレスを使用して Azure Cosmos DB に対するクエリを実行する   
https://docs.microsoft.com/ja-jp/learn/modules/query-azure-cosmos-db-with-sql-serverless-for-azure-synapse-analytics/   

## 分析ストアが有効なコンテナーを作成する
- サンプルデータは以下を利用してください。    
```json
{
    "customerId": 101,
    "firstname": "Orlando",
    "lastname": "Gee",
    "email": "orlando.gee@adventure-works.com",
    "addresses": [
        { "addressline1" : "660 Lindbergh", "city" : "Saint Louis", "stateprovince" : "Missouri", "countryregion" : "United States", "postalcode" : "63103" },
        { "addressline1" : "Ontario Mills", "city" : "Ontario", "stateprovince" : "California", "countryregion" : "United States", "postalcode" : "91764" }
    ]
}
```
```json
{
    "customerId" : 122,
    "title" : "Ms.",
    "firstname" : "Caroline",
    "middlename" : "A.",
    "lastname" : "Vicknair",
    "companyname" : "World of Bikes",
    "salesperson" : "adventure-works\\jillian0",
    "addresses": [
        { "addressline1" : "72540 Blanco Rd.", "addressline2" : "South Side", "city" : "San Antonio", "stateprovince" : "Texas", "countryregion" : "United States", "postalcode" : "78204" }
    ]
}
```
- また、「7.次のようにして、このデータに対してクイック クエリを実行し、特定の顧客の顧客プロファイルと販売注文情報を取得してみましょう。…」の部分では、以下のコードを実行してください。
```sql
SELECT * FROM c WHERE c.customerId = 101
```
![image](https://user-images.githubusercontent.com/69043643/158559887-c45d2b9e-5e22-427a-ba2e-8650bd062fa0.png)     

- 「a. 「New Shell」(新しいシェル) をクリックします (A)」の部分では、以下のように入力してください。
```PowerShell
show collection
db.Sales.find({customerId:122})
```

