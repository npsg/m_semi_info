# サーバーレスSQLプールを使用してインタラクティブなクエリを実行する
1. Azure Synapse サーバーレス SQL プールの機能を確認する   
https://docs.microsoft.com/ja-jp/learn/modules/explore-azure-synapse-serverless-sql-pools-capabilities/
3. Azure Synapse サーバーレス SQL プールを使用してレイク内のデータのクエリを実行する   
https://docs.microsoft.com/ja-jp/learn/modules/query-data-lake-using-azure-synapse-serverless-sql-pools/
5. Azure Synapse サーバーレス SQL プールにメタデータ オブジェクトを作成する   
https://docs.microsoft.com/ja-jp/learn/modules/create-metadata-objects-azure-synapse-serverless-sql-pools/
7. Azure Synapse サーバーレス SQL プールでデータを保護し、ユーザーを管理する   
https://docs.microsoft.com/ja-jp/learn/modules/secure-data-manage-users-azure-synapse-serverless-sql-pools/

>**やってみましょう！** <br>Azure Synapseワークスペースの作成は、以下の演習が参考になります。<br>モジュール01とモジュール02が終わった後に行うと良いでしょう。    
>https://docs.microsoft.com/ja-jp/learn/modules/explore-azure-synapse-analytics/6-exercise-azure-synapse    
> - リージョンは、「US West 2」を選択すると良いでしょう。   
> - 名前: 「AdventureWorks 製品」は、「AdventureWorksProducts」に変更するなど、日本語で入力できないところは、適宜、英語にしてください。

## サーバーレスと専用の選択
- 専用SQLプール（一般的なDWH）：DWU（データウェアハウスユニット）で課金、CPU・メモリおよび IO の組み合わせ、手動でDWUを調整しなければいけない
- サーバーレスSQLプール：処理量で課金、クエリの負荷に応じて自動で調整   

DWUや処理量以外に、データストレージの課金も加わる。   
https://azure.microsoft.com/ja-jp/pricing/details/synapse-analytics/#pricing
