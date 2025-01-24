# 3.miiboを用いてLINE Botを作ろう

## このパートでやること

- LINEの情報を取得してmiiboに登録していきます。


## このパートで作るもの

- miiboとLINEを連携して、会話型AIのLINE Botを作る  
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

> 今回は、miibo側で自動応答をメインで活用し、人による手動応答は不要になるため、オフに設定しています。


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

## 2.miiboにLINEの情報を登録する

- miiboのエージェントページに移動します  
左側のメニューバーから「外部サービス連携」をクリックします。

<img src="https://i.gyazo.com/87a6864e9fb3985633eb5157cf319229.png" width="250px" alt="image from gyazo"/>

- 「LINE上で会話する」ボタンをクリックします。

<img src="https://i.gyazo.com/6e68d6cc6ed5508a108822ee279ad150.png" width="450px" alt="image from gyazo"/>

- 先ほど取得した「チャネルシークレット」と「チャネルアクセストークン」を貼り付けます。  
貼り付けた後は「LINEと連携する」ボタンをクリックします。

<img src="https://i.gyazo.com/6605f9740f9a5facd581c72bf07d2037.png" width="450px" alt="image from gyazo"/>


## 3.LINEにWebhook URLを登録する

- miiboで発行された「Webhook URL」をコピーします  
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

## 4.ひとまず完成！

### LINEから会話をしてみる

- スマートフォンで、友達になったLINE Botへ何かメッセージを送信し、返答がくるのを確認しましょう。  

<img src="https://i.gyazo.com/7b3929bf5dd796a84f81600102e18709.png" width="250px" alt="image from gyazo"/>

- miiboとLINE Botが連携され、会話型AIが完成しました！  
ここからオリジナリティを出していきましょう。

---

- [次の資料へ](./04_custom.md)
- [トップページへ](./readme.md)


