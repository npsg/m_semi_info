# ラボURL   
https://github.com/MicrosoftLearning/DP-203JA-Data-Engineering-on-Microsoft-Azure

## ラボファイルのセットアップ（時間がかかります）
1. Azure Az PowerShell moduleのインストール
```powershell
Install-Module -Name Az -Scope CurrentUser -Repository PSGallery -Force
```
2. Azure CLIのインストール
```powershell
$ProgressPreference = 'SilentlyContinue'; Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; rm .\AzureCLI.msi
```
> 注：インストールが完了したら、Azure CLI を使用するには PowerShell を再度開く必要があります。
3. Windows検索ボックスを使用してWindows PowerShellを検索し、管理者として実行します。
4. Windows PowerShellで、次のコマンドを実行して、必要なコースファイルをダウンロードします。これには数分かかる場合があります。
```powershell
mkdir c:\dp-203

cd c:\dp-203

git clone https://github.com/microsoftlearning/dp-203-data-engineer.git data-engineering-ilt-deployment
```
5. Windows PowerShellで、次のコマンドを実行して実行ポリシーを設定し、ローカルPowerShellスクリプトファイルを実行できるようにします。
```powershell
Set-ExecutionPolicy Unrestricted
```
6. Windows PowerShellでは、次のコマンドを使用して、ディレクトリをオートメーションスクリプトを含むフォルダに変更します。
```powershell
cd C:\dp-203\data-engineering-ilt-deployment\Allfiles\00\artifacts\environment-setup\automation\
```
7. Windows PowerShellで、次のコマンドを入力してセットアップスクリプトを実行します。画面の指示に従って、Azureのサインインを行ったり、データベースパスワードを新規登録します。
```powershell
.\dp-203-setup-Part01.ps1
```
## 専用のSQLプールとPowerShellスクリプトの実行
### 専用のSQLプール
1. Synapse Studio (https://web.azuresynapse.net/) を開きます。
1. 左側のメニューから管理／SQLプールを選択し、[+新規]を選択します。
1. 専用SQLプールの作成ページで、プール名にSQLPool01（ここに表示されている名前を正確に使用する必要があります）を入力し、パフォーマンスレベルをDW100cに設定します（スライダーを左いっぱいに移動します）。<br><img width="800" alt="image" src="https://user-images.githubusercontent.com/69043643/158264235-0df92a14-9986-471b-8f67-466062384754.png">
1. [レビュー + 作成] をクリックします。次に、検証ステップで [作成] を選択します。
1. 専用のSQLプールが作成されるまで待ちます。
### PowerShellスクリプト
1. Windows PowerShellで、次のコマンドを実行して実行ポリシーを設定し、ローカルPowerShellスクリプトファイルを実行できるようにします。
```powershell
Set-ExecutionPolicy Unrestricted
```
2. Windows PowerShellでは、次のコマンドを使用して、ディレクトリをオートメーションスクリプトを含むフォルダに変更します。
```powershell
cd C:\dp-203\data-engineering-ilt-deployment\Allfiles\00\artifacts\environment-setup\automation\
```
3. Windows PowerShellで、次のコマンドを入力して、SqlServerのコマンドをインストールします。
```powershell
Install-Module -Name SqlServer
```
4. Windows PowerShellで、次のコマンドを入力してセットアップスクリプトを実行します。画面の指示に従って、Azureのサインインを行います。また、Synapseワークスペースが入っているリソースグループ名を入力します。
```powershell
.\setup-sql.ps1
```

## Data Lakeへのコピー
1. C:\dp-203\data-engineering-ilt-deployment\Allfiles\00\artifacts\environment-setup\automation\にある「dp-203-setup-Part02.ps1」をメモ帳などで開きます。必要に応じて、情報書き換えて保存します。Synapseワークスペースの内容を参考にします。
```powershell
$selectedSub = ""
$suffix = "（書き換える）"
$subscriptionId = "（書き換える）"
$resourceGroupName = "data-engineering-synapse-（書き換える）"
$workspaceName = "asaworkspace（書き換える）"
$global:logindomain = "5bb6d01d-4c6a-4b16-9979-24855af65690"
$global:sqlEndpoint = "asaworkspace（書き換える）.sql.azuresynapse.net"
$global:sqlUser = "asa.sql.admin"
$global:synapseToken = ""
$global:synapseSQLToken = ""
$global:managementToken = ""
$global:powerbiToken = ""
$global:tokenTimes = [ordered]@{
        Synapse = (Get-Date -Year 1)
        SynapseSQL = (Get-Date -Year 1)
        Management = (Get-Date -Year 1)
        PowerBI = (Get-Date -Year 1)
}
```
<img width="900" alt="image" src="https://user-images.githubusercontent.com/69043643/158268462-6bab68be-337b-47ca-bb23-3acf9ce43343.png">

2. Windows PowerShellで、次のコマンドを実行して実行ポリシーを設定し、ローカルPowerShellスクリプトファイルを実行できるようにします。
```powershell
Set-ExecutionPolicy Unrestricted
```

3. Windows PowerShellでは、次のコマンドを使用して、ディレクトリをオートメーションスクリプトを含むフォルダに変更します。
```powershell
cd C:\dp-203\data-engineering-ilt-deployment\Allfiles\00\artifacts\environment-setup\automation\
```

4. Windows PowerShellで、次のコマンドを入力してセットアップスクリプトを実行します。画面の指示に従って、Azureのサインインを行ったり、データベースパスワードを新規登録します。
```powershell
.\dp-203-setup-Part02.ps1
```
