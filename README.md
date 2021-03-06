# 研修受講の前に

## 研修全般
- https://github.com/npsg/m_semi_info/
- デジタルテキスト（Skillpipe）のコードは届いておりますでしょうか？
- 研修の間で、ラボ（実習問題のこと）が用意されています。<br>お手持ちのローカル環境もしくはlearnondemandが用意しているラボ環境から実習できます。<br>ラボ環境は、小さな仮想マシンが起動し、ブラウザから操作できるようになっています。講師からも画面を見ながらサポートできます。
- いずれにしてもMicrosoft Azureへは、研修特典であるAzure Pass（サブスクリプション）を利用してアクセスします。<br>[https://docs.microsoft.com/ja-jp/learn/certifications/mocazurepass](https://docs.microsoft.com/ja-jp/learn/certifications/mocazurepass)
- Azure Passの使用量に注意します。<br>余分なAzure コンポーネントを実行しないように、ラボの最後にリソースグループを削除します。
- ラボによっては、次のラボでも同じコンポーネントを使う場合もあるので注意してください。
- 次のリンクでラボの使用量を確認できます。<br>[https://www.microsoftazuresponsorships.com/Balance](https://www.microsoftazuresponsorships.com/Balance)

## ①デジタルテキスト（Skillpipe）の有効化
Skillpipeは、ブラウザで閲覧するデジタル教科書です。<br>コースが終わった後でもアクセスできます。
1. 事前登録後、noreply@skillpipe.com からメールが届いているはず
1. https://www.skillpipe.com へアクセス
1. Skillpipeのアカウントでログイン(Skillpipeのアカウントがない方は「Join now」から新規作成します)
![image](https://user-images.githubusercontent.com/69043643/122666855-bd18be80-d1ea-11eb-8bc3-1453605cc5d4.png)
1. ログインしたら、[Menu]をクリックします。
1. ［+Add course］ボタンをクリックします。
1. メール内のコードを入力し、［Redeem License Key］をクリックします。
- メールがない場合は、ゴミ箱やスパムのメールボックスを確認
- 見つからない場合は教えて下さい
- 「Table of Contents」で目次が表示されます。コースによっては、章末のチェック問題「レビューの質問」という項目があります。
- テキストは範囲選択して、右クリックすると、ハイライトやノートが記録できます。

## ②Microsoftアカウントの新規作成
学校や職場のアカウントを利用すると、ラボが進行できない場合があります。研修用として、新しくMicrosoftアカウントを作成してください。<br>
後ほど、作成したMicrosoftアカウントにAzure Passを関連付け、有効化します。１度Azure Passを有効化するとそのAzure Passは使用できません。
1. InPrivateモードに切り替えます。
1. [https://signup.live.com/signup](https://signup.live.com/signup)にアクセスします。
1. 「新しいメールアドレスを取得」をクリックします。
1. メールアドレスを入力します。
1. パスワードを入力します。
1. お名前を入力します（任意のもので結構です）
1. 生年月日を入力します（任意のもので結構です）
1. スパムチェックの問題をクリアします（うまく正解できない場合は、InPrivateモードを確認したり、別のブラウザでやってみてください）

## ③ラボ環境へのアクセス
1. [https://esi.learnondemand.net/User/Login](https://esi.learnondemand.net/User/Login)にアクセスします。<br>イベントによっては、こちらhttps://cloudweeks.learnondemand.net/    
1. ［Sign In］をクリックします
1. 「Microsoft Account」をクリックして、②で作成した新しいMicrosoftアカウントでサインインします
![image](https://user-images.githubusercontent.com/69043643/122667123-35cc4a80-d1ec-11eb-995b-0b36a35472f4.png)
1. 操作を行う許可の画面が表示されます。［はい］をクリックします。
1. 「トレーニングキーを利用する」をクリックします。
1. 講師から得たトレーニングキーを入力し、［トレーニングキーを利用する］ボタンをクリックします。画面はこのままで④に進みます。

## ④Azure Passの有効化
1. スクロールして、アクティビティのリストを表示します。このリストが、ラボ（演習問題）のリストです。
1. 最初のラボにある［起動］ボタンをクリックします。
1. ラボ環境が構築されます。数分かかります。少しラボ環境を操作してみましょう！
1. 左側が仮想マシンの画面、右側がラボの手順が表示されます。右下の［次へ］をクリックします。
1. 仮想マシンの画面がサインイン画面になっています。Passwordにカーソルがあることを確認したら、<br>右側にあるラボの手順の「ラボのセットアップ」2.パスワード［T］マークをクリックします。<br>すると、自動的にタイプされます。［T］マークは、ラボ環境では、自動入力のボタンと覚えてください。<br>（注）単にコピーアンドペーストするときは、仮想マシンの左上の稲妻アイコン／テキストを入力／クリップボードの…を選択します。
1. 仮想マシンの画面から、→（Submit）ボタンを押して、サインインします。
3. 右側にあるラボの手順から「ラボファイルをDドライブ」をクリックして、演習データを仮想マシンに取り込みます（ローカルで実習する場合は不要）。［次へ］をクリックします。
5. Azure Passの有効化に必要なPromo codeは、ラボの手順の上部にある「リソース」タブにあります。<br>もしくは右側にあるラボの手順をスクロールすると、手順1-5にプロモコードがあります。<br>これをローカルの環境にコピーするかメモします。
1. ここからは、ラボ環境で実習を続行しても、ローカルで実習しても構いません。<br>ラボ環境を終了して閉じる場合は、最後まで右下の［次へ］をクリックして、「ラボをキャンセルする」にチェックを付け、［へい］ボタンをクリックします。[ウィンドウを閉じる]をクリックして、ラボ環境を閉じます。
1. ラボ環境の仮想マシンの中、あるいはローカル環境において、InPrivateモードでWebブラウザを起動します。
1. [https://www.microsoftazurepass.com/](https://www.microsoftazurepass.com/)にアクセスします。
![image](https://user-images.githubusercontent.com/69043643/122667798-a9238b80-d1ef-11eb-92e8-35817bf36eba.png)
1. ［Start>］をクリックします。
1. ②で取得したMicrosoftアカウントが表示されていることを確認したら、［Confirm Microsoft Account］をクリックします。
1. 「Enter Promo code:」にPromo Codeを貼り付け、［Claim Promo Code］をクリックします。数分かかります（何もせずにじっとお待ちください）。
1. Azure Pass スポンサープランの情報入力画面が開くので、どんどん質問にチェックして、［サインアップ］をクリックします。<br>「電話番号」「姓名」「「サブスクリプション契約、オファーの詳細、プライバシーに関する声明に同意します。」のチェックが必要です。
1. このサインアップ エクスペリエンスに満足していますか?の評価をクリックして、［送信］をクリックします。
1. '''最終的には、Azure Portalへ遷移したら、成功です。「サブスクリプション」画面に「Azure Passスポンサープラン」が表示されています。
![image](https://user-images.githubusercontent.com/69043643/122668192-f274da80-d1f1-11eb-9679-50c924a5116a.png)

ここまで、デジタルテキスト（Skillpipe）、Azure Pass が紐付いたMicrosoftアカウント、ラボ環境をセットアップしました。準備完了です！
