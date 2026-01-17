# DifyでLINE Botを作る

## 1. DifyでLINE Botを作ってみよう

Difyで作成した盛岡の知識に強いAIをLINE Botにしていきます。

### 1-1. 利用イメージ

- Dify x RAG
https://x.com/martina1_111/status/1960588508495503636?s=20

- 今回の制作イメージ
    - 盛岡の観光情報教えてくれるチャットbot 
https://x.com/T_taisyou/status/1954062259132792958

---

## 2. ハンズオン：DifyのAIをLINE Bot化

### 2-0. 準備

- LINE公式アカウントの準備  
  LINE公式アカウントの作成 / LINE Botの初め方
  https://zenn.dev/protoout/articles/16-line-bot-setup

- チャンネルアクセストークン と チャンネルシークレット の二つのキーを取得して下さい。
## このパートでやること

- LINEの情報を取得してDifyに登録していきます。


## このパートで作るもの

- DifyとLINEを連携して、会話型AIのLINE Botを作る  
何かメッセージを送信すると、返答が来る仕組みになります。

<img src="https://i.gyazo.com/7b3929bf5dd796a84f81600102e18709.png" width="250px" alt="image from gyazo"/>

## 事前準備の確認

参考：[事前準備資料](https://zenn.dev/protoout/articles/16-line-bot-setup)

LINEの公式アカウントの登録ができている状態か見てみましょう！

- [LINE Official Acount Manager](https://manager.line.biz/)にアクセスをして自分の作ったアカウントが表示され選べる状態になっている。

<img src="https://i.gyazo.com/18b2af51de0816270f5d3cb1ad7747b0.png" width="350px" alt="image from gyazo"/>

- アカウントを選んで開くと下記の画面になっている。

<img src="https://i.gyazo.com/546cf492038cee6962d9b8dfa4ca2c04.png" width="350px" alt="image from gyazo"/>

- スマートフォンでLINEの公式アカウントが友達追加されている。

<img src="https://i.gyazo.com/222275d75045bed314557e8526f3750d.png" width="250px" alt="image from gyazo"/>

確認できたら早速作っていきましょう！

## 1.LINEの情報を取得する

- [こちらの資料](https://zenn.dev/protoout/articles/16-line-bot-setup)にアクセスをします。  
`4. Messaging APIの有効化`〜`5-2. チャネルアクセストークンの取得`まで作ります。

- 次に、応答機能を確認します  
  「Messaging API設定」のタブの「応答メッセージ」で、右側の`編集`ボタンから設定していきます。

<img src="https://i.gyazo.com/d9a707b5b85c3401cc2b9b536ba71104.png" width="450px" alt="image from gyazo"/>

応答メッセージは下記のように設定しておきます。  
- チャット：オフ　
- 挨拶メッセージ：オン
- Webhook：オフ（現時点では選択できない仕様になっています ※理由は下記「応答メッセージの機能について」に参照）
- 応答メッセージ：オフ

<img src="https://i.gyazo.com/9ea92e7237b87af7e59feb8b3d576c0e.png" width="450px" alt="image from gyazo"/>

<details>

<summary>応答メッセージの機能について</summary>

- **チャット**  
  アカウント管理画面からユーザーと手動でメッセージのやり取りができます。
  
   - オンにした場合：自動応答を使わず、直接人が対応する場合に活用できます。
     
   - オフにした場合：手動応答が不要でBotなどの自動応答に専念したい時に活用できます。

> 今回は、Dify側で自動応答をメインで活用し、人による手動応答は不要になるため、オフに設定しています。


- **挨拶メッセージ**  
  ユーザーがLINE公式アカウントを友だち追加したときに1度だけ自動的に送信されるメッセージです。
  
  - オンにした場合  
  自動でBotが表示され初めのメッセージが送られてくるので、アカウントの存在が認識できます。  
  ユーザーが会話を始めるきっかけとして有効です。
    
  - オフにした場合  
  最初のメッセージが送られてこないので、追加したBotの存在が自動で表示されず、認識しづらくなります。

> 今回は、追加したBotの存在を認識してスムーズに会話を始めるため、オンにしています。


- **Webhook**  
  LINE公式アカウントと外部サーバーを連携させる機能です。
  
  - WebhookのURLが未設定の場合
    LINE公式アカウント側でどこにメッセージを送るべきか分からないため、Webhookを有効にする選択肢が出てきません。  
    WebhookのURLを設定した場合にオンまたはオフが選べるようになります。

> 今回は現時点で選択できないのですが、後のパートでにWebhookの検証をして連携します。  
> その時点でオンに設定していきます。


- **応答メッセージ**  
  ユーザーが送信したメッセージに対して、LINE公式アカウントが自動で返信を行う機能です。
  
  - LINE公式アカウントの基本的な自動応答機能として活用されており管理画面から設定できます。
  - 設定できるメッセージは「固定文」のみで、事前に設定した内容の応答を自動で返します。
 
    - 例：設定した文章「こんにちは！お問い合わせありがとうございます。」  
      ユーザー：「こんにちは」  
      LINE公式アカウント：「こんにちは！お問い合わせありがとうございます。」  

> 今回は、応答をカスタマイズしてユーザーのニーズに合わせた返信を実現するため、オフにしています。

</details>


- Difyのチャットアプリを作っておく  
  - 公開されている必要があります。
![Dify公開](/仮/CleanShot%202026-01-17%20at%2012.57.14@2x.png)
---

### 2-1. Difyにプラグインを追加

Difyにはプラグインという外部サービスと連携しやすい仕組みがあります。  
LINE Bot以外にもSlackやNotion、スプレットシートなど主要なツールと連携できます。  
プラグインはOSS開発となっていて割と最近追加された機能なので、選択肢はまだ少ない印象です。

#### プラグインの検索
プラグインページから、マーケットプレイスに行きLINEのプラグインをインストールしましょう。

![利用イメージ](https://storage.googleapis.com/zenn-user-upload/9ce7b1c6f375-20250808.png)

![プラグインページからマーケットプレイスへ](https://storage.googleapis.com/zenn-user-upload/8e7fcaff702f-20250808.png)

LINE BotやLINEなどで検索すると候補が出てきます。

![LINEプラグイン検索結果](https://storage.googleapis.com/zenn-user-upload/25229f4a8016-20250808.png)

#### インストール

![インストール画面](https://storage.googleapis.com/zenn-user-upload/f77caa9fc15a-20250808.png)



---

### 2-3. 重要: LINEプラグインのバージョンを0.0.4に下げる

これはコミュニティの知見で発見されましたが、最新の0.0.5だとバグで動きません。  
0.0.4にダウングレードしましょう。

![0.0.4にダウングレード](https://i.gyazo.com/c158e3c8746e232ac13663f1166f4ab7.png)

---

### 2-2. プラグインの設定

インストールしたら設定へ進みます。

![設定へ進む](https://storage.googleapis.com/zenn-user-upload/37fcea0365b9-20250808.png)

+ボタンから進んでください。

![+ボタン](https://storage.googleapis.com/zenn-user-upload/977fd2fc499e-20250808.png)

- エンドポイント名: 適宜名前を入れましょう。
- チャンネルシークレット: LINE Botの管理画面から取得
- チャンネルアクセストークン: LINE Botの管理画面から取得
- アプリ: 作ったチャットフロー（かワークフロー）を設定

※LINEのトークンなどは[こちら](https://zenn.dev/protoout/articles/16-line-bot-setup)から

![各項目を入力](https://storage.googleapis.com/zenn-user-upload/8a29256a2282-20250808.png)

---

### 2-3. LINE DevelopersでWebhook URLの設定

最後、WebhookURLの設定です。

ここまでトラブルなく進むと、URLが発行されます。

![Webhook URLが発行される](https://storage.googleapis.com/zenn-user-upload/3a113c10e68c-20250809.png)

LINE Developersのコンソールで先ほどのURLをWebhook URLに設定します。

![LINE DevelopersでWebhook URLを設定](https://i.gyazo.com/16e353c1a68a3a0fd92d9b9d7a83bfd9.png)

問題なく連携できると、検証ボタンを押したときに成功と表示されます。

![検証が成功](https://i.gyazo.com/c1e4975d249ca4863a82288495990af4.png)

- Difyで発行された「Webhook URL」をコピーします  
  - 補足：Webhookとは？  
  サービス（アプリケーション）の何らかのアクションを他のアプリケーションへリアルタイムに通知する仕組みのことです。

<img src="https://i.gyazo.com/4c05804099dcc6f93f49862b2ebff05b.png" width="450px" alt="image from gyazo"/>


- LINEのチャネルページへ移動し、「messageing API設定」のタブからWebhook設定をします。

<img src="https://i.gyazo.com/7f302b0956c1aad41c0bc2a4de975328.png" width="450px" alt="image from gyazo"/>

- Webhook URLの `編集`ボタンをクリックします。

<img src="https://i.gyazo.com/2dc501d6a7c30fe75ce8d6572657ecf0.png" width="350px" alt="image from gyazo"/>

- 先ほどコピーしたWebhook URLを貼り付け、`更新`ボタンをクリックします。

<img src="https://i.gyazo.com/57486cb575b3d8fd6b6615929d644bab.png" width="450px" alt="image from gyazo"/>

- Webhookの利用ボタンをクリックし、オンにします。

<img src="https://i.gyazo.com/88de95e073afa7218f78e883e8fa3d4d.png" width="450px" alt="image from gyazo"/>

- `検証`ボタンをクリックし、「成功」の表示がでたら連携完了です。

<img src="https://i.gyazo.com/2699f7e4370f7140e2b8ff2e12e9a805.png" width="250px" alt="image from gyazo"/>

## 3.ひとまず完成！

### LINEから会話をしてみる

- スマートフォンで、友達になったLINE Botへ何かメッセージを送信し、返答がくるのを確認しましょう。  

<img src="https://i.gyazo.com/7b3929bf5dd796a84f81600102e18709.png" width="250px" alt="image from gyazo"/>

- DifyとLINE Botが連携され、会話型AIが完成しました！  
ここからオリジナリティを出していきましょう。

---

### 2-4. 試す / 他の人のLINE Botも試す

試す際はLINEで話しかけて動作を確認してみましょう。

QRコードを共有することで他の人にも使ってもらえます。  
他の人のLINE Botも使ってみましょう。

![LINEで動作確認](https://i.gyazo.com/2973c4d251732e7e08b43885580d3268.png)

---

## 3. Tips: LINE Bot連携は色々

LINE Bot自体はDifyとは全く別物なので、プログラムを書いて連携したり他のノーコードツールと連携したりと様々な作り方があります。

興味がある人は他のやり方も調べてみましょう。

---

## 4. チャレンジ課題

リッチメニューという機能を使うとLINE Botの見栄えが格段に上がります。  
特にプログラムが必要とかでもなく設定からいけるので、やれる人はチャレンジしてアプリケーションとしての使い勝手を上げましょう。

- LINE公式アカウント（LINE Official Account Manager）リッチメニューを作成するマニュアル｜LINEヤフー for Business  
  https://www.lycbiz.com/jp/manual/OfficialAccountManager/rich-menus/

プログラム的に制御もできます

- リッチメニューを使う（LINE Developers）  
  https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/

![LINEリッチメニュー](https://i.gyazo.com/669a86b1940aa84ba5da6098e37057b0.png)
---

- [前の資料へ](/IU25/02_Dify.md))