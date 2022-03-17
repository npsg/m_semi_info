# Stream Analytics によるリアルタイムのストリーム処理    
1. Azure Event Hubs を使用してビッグ データ アプリケーションの信頼性の高いメッセージングの有効にする   
https://docs.microsoft.com/ja-jp/learn/modules/enable-reliable-messaging-for-big-data-apps-using-event-hubs/    
2. Azure Stream Analytics を使用したデータ ストリームの処理   
https://docs.microsoft.com/ja-jp/learn/modules/introduction-to-data-streaming/    
3. Azure Stream Analytics を使用してデータを変換する   
https://docs.microsoft.com/ja-jp/learn/modules/transform-data-with-azure-stream-analytics/    

## EventHubにPOSTする方法
1. Event HubにPOSTするときには、トークンの生成が必要です。PowerShellなどでできます。
```powershell
[Reflection.Assembly]::LoadWithPartialName("System.Web")| out-null
$URI="myNamespace.servicebus.windows.net/myEventHub"
$Access_Policy_Name="RootManageSharedAccessKey"
$Access_Policy_Key="myPrimaryKey"
#Token expires now+300
$Expires=([DateTimeOffset]::Now.ToUnixTimeSeconds())+300
$SignatureString=[System.Web.HttpUtility]::UrlEncode($URI)+ "`n" + [string]$Expires
$HMAC = New-Object System.Security.Cryptography.HMACSHA256
$HMAC.key = [Text.Encoding]::ASCII.GetBytes($Access_Policy_Key)
$Signature = $HMAC.ComputeHash([Text.Encoding]::ASCII.GetBytes($SignatureString))
$Signature = [Convert]::ToBase64String($Signature)
$SASToken = "SharedAccessSignature sr=" + [System.Web.HttpUtility]::UrlEncode($URI) + "&sig=" + [System.Web.HttpUtility]::UrlEncode($Signature) + "&se=" + $Expires + "&skn=" + $Access_Policy_Name
$SASToken
```
2. URLとHeader、bodyを用意します。API Testerなどブラウザの拡張機能を用意すると便利です。   
- URL:<br>
https://[Event Hub名前空間].servicebus.windows.net/[イベントハブ名]/messages     
- Header<br>
Authorization:[上記PowerShellで生成されたトークン]    
Content-Type:application/json 
- Talend API Tester - Free Edition    
https://chrome.google.com/webstore/detail/talend-api-tester-free-ed/aejoelaoggembcahagimdiliamlcdmfm?hl=ja    <br><br>
![image](https://user-images.githubusercontent.com/69043643/158722081-de69e62d-f908-4dcf-bba9-7f4159472b74.png)

   
