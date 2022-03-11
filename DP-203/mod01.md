# データエンジニアリングワークロードのコンピューティングおよびストレージオプションを確認する
1. Azure Synapse Analytics の 概要  
https://docs.microsoft.com/ja-jp/learn/modules/introduction-azure-synapse-analytics/    
2. Azure Databricks の説明  
https://docs.microsoft.com/ja-jp/learn/modules/describe-azure-databricks/
3. Azure Databricks Delta Lake のアーキテクチャについて  
https://docs.microsoft.com/ja-jp/learn/modules/describe-azure-databricks-delta-lake-architecture/
4. Azure Data Lake Storage の概要   
https://docs.microsoft.com/ja-jp/learn/modules/introduction-to-azure-data-lake-storage/
5. Azure Stream Analytics を使用したデータ ストリームの処理    
https://docs.microsoft.com/ja-jp/learn/modules/introduction-to-data-streaming/

>**やってみましょう！** <br>
>ここで確認しておきたい操作は以下の点です。
>1. Azure Synapse Analyticsのワークスペースの作成<br>（モジュール2の終わりの「やってみましょう！」でも行うので、操作手順のみの確認でOKです）<br>
>https://docs.microsoft.com/ja-jp/learn/modules/survey-components-of-azure-synapse-analytics/3-exercise-create-manage-workspace
>2. Databricksワークスペースの作成
>以下、ご参照

## Databricksワークスペースの作成
### Azure Databricksワークスペースを展開する
1. 「Azure Databricks」を検索します。
2. [作成]をクリックします。
3. 以下の情報を入力します。
   - リソースグループ:（任意の名前)
   - ワークスペース名:（任意の名前）
   - リージョン: ここでは、East US2を選択します。
   - 価格レベル:「試用版」
4. [確認および作成]をクリックし、検証後、[作成]をクリックします。 [リソースに移動]をクリックします。
5. 作成したDatabricksを開き、[ワークスペースの起動]をクリックします。
### クラスターを作成する
1. 左側のメニューから[＋]をクリックし、「Cluster」を選択します。
2. 以下を設定して、[Create Cluster]をクリックします。
   - Cluster name:　（一意の名前）
   - Cluster mode:　Single Node
   - Databricks runtime version: 既定値
   - Node Type: 既定値（Standard_DS3_v2） 
<img width="560" alt="image" src="https://user-images.githubusercontent.com/69043643/157821957-b5c1e322-461e-49f4-9bbf-f82a72951f09.png">
3. 作成中はインジケーターが回転します。緑色の実線に変わるまで待ちます。
<img width="560" alt="image" src="https://user-images.githubusercontent.com/69043643/157823137-c09f638a-e153-4032-8904-c86b5f58dae3.png">

### データをアップロードする
