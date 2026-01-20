# 03. LINE Bot

このパートでは、Difyで作ったBot（盛岡の知識に強いAI）を、LINE上で動くBotとして利用できる形にします。  
- LINEは普段使っているアプリなので、ユーザーにとって「使い始めるハードルが低い」のが強みです。
- LINE Botは、そのLINE上で動作するチャットボット（ロボット）です。日頃使っているLINEとはすこし違うものだと思っていてください。
  - お店の公式アカウントをイメージしてもらえると良いです。

---

## 1. このパートで作るもの「AIと会話ができるLINE Bot」

### 1-1. 作成するものの概要

- Difyで作成したAIをLINEに接続し、LINEでメッセージを送ると返信が返ってくるBotを作ります
- 作成イメージ:
- [盛岡の観光情報を教えてくれるチャットBot](https://x.com/T_taisyou/status/1954062259132792958)

<img src="https://i.gyazo.com/2973c4d251732e7e08b43885580d3268.png" width="250px" alt="image from gyazo"/>

参考リンク
- [LINE公式アカウント作成 / LINE Botの初め方](https://zenn.dev/protoout/articles/16-line-bot-setup)

---

## 2. DifyとLINE Botを連携する

### 2-1. LINE側の応答設定を整える（応答メッセージ）

LINE Official Account Managerで応答設定を確認します。  
「Messaging API設定」タブの「応答メッセージ」から、右側の `編集` ボタンで設定します。

<img src="https://i.gyazo.com/d9a707b5b85c3401cc2b9b536ba71104.png" width="450px" alt="image from gyazo"/>

応答メッセージは下記のように設定します。

- チャット: オフ
- 挨拶メッセージ: オン
- Webhook: オフ（現時点では選択できない仕様の場合があります。後でWebhook URLを設定するとオンにできます）
- 応答メッセージ: オフ

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

---

### 2-2. Difyのチャットアプリを準備する（公開状態）

- Dify側でチャットアプリ（チャットフロー or ワークフロー）を作成しておきます
- 公開（外部から呼べる状態）になっている必要があります

---

### 2-3. DifyにLINEプラグインを追加（インストール）

Difyには外部サービスと連携しやすい「プラグイン」機能があります。  
LINE以外にも、Slack/Notion/スプレッドシートなどと連携できます。

手順
- Difyのプラグインページからマーケットプレイスへ移動
- LINEプラグインを検索してインストールします

![利用イメージ](https://storage.googleapis.com/zenn-user-upload/9ce7b1c6f375-20250808.png)

![プラグインページからマーケットプレイスへ](https://storage.googleapis.com/zenn-user-upload/8e7fcaff702f-20250808.png)

検索
- `LINE Bot` や `LINE` などで検索すると候補が出てきます

![LINEプラグイン検索結果](https://storage.googleapis.com/zenn-user-upload/25229f4a8016-20250808.png)

インストール

![インストール画面](https://storage.googleapis.com/zenn-user-upload/f77caa9fc15a-20250808.png)

---

### 2-4. 重要: LINEプラグインのバージョンを0.0.4に下げる

コミュニティ知見として、最新の0.0.5だとバグで動かないケースがあります。  
その場合は0.0.4にダウングレードします。

![0.0.4にダウングレード](https://i.gyazo.com/c158e3c8746e232ac13663f1166f4ab7.png)

---

### 2-5. プラグインの設定（LINEのキーとDifyアプリを紐づけ）

インストールしたら設定へ進みます。

![設定へ進む](https://storage.googleapis.com/zenn-user-upload/37fcea0365b9-20250808.png)

`+` ボタンから作成します。

![+ボタン](https://storage.googleapis.com/zenn-user-upload/977fd2fc499e-20250808.png)

入力項目
- エンドポイント名: 任意（わかりやすい名前）
- チャンネルシークレット: LINE Bot管理画面から取得
- チャンネルアクセストークン: LINE Bot管理画面から取得
- アプリ: 作成したチャットフロー（またはワークフロー）を選択

キー取得の参考
- https://zenn.dev/protoout/articles/16-line-bot-setup

![各項目を入力](https://storage.googleapis.com/zenn-user-upload/8a29256a2282-20250808.png)

---

### 2-6. LINE DevelopersでWebhook URLの設定（連携の仕上げ）

ここまで問題なく進むと、Dify側でWebhook URLが発行されます。
  補足: Webhookとは？  
  サービス（アプリケーション）の何らかのアクションを他のアプリケーションへリアルタイムに通知する仕組みのことです。

![Webhook URLが発行される](https://storage.googleapis.com/zenn-user-upload/3a113c10e68c-20250809.png)

LINE Developersのコンソールで、先ほどのURLをWebhook URLに設定します。

![LINE DevelopersでWebhook URLを設定](https://i.gyazo.com/16e353c1a68a3a0fd92d9b9d7a83bfd9.png)

- Webhookの利用ボタンをクリックし、オンにします

<img src="https://i.gyazo.com/88de95e073afa7218f78e883e8fa3d4d.png" width="450px" alt="image from gyazo"/>

検証ボタンを押して成功と表示されればOKです。

![検証が成功](https://i.gyazo.com/c1e4975d249ca4863a82288495990af4.png)

---

### 2-7. ひとまず完成！

- LINEから会話をしてみる
    - スマートフォンで、友達になったLINE Botへ何かメッセージを送信し、返答がくるのを確認しましょう。  
- DifyとLINE Botが連携され、AIと会話ができるLINE Botが完成しました！  
ここからオリジナリティを出していきましょう。

<img src="https://i.gyazo.com/2973c4d251732e7e08b43885580d3268.png" width="350px" alt="image from gyazo"/>

---

### 2-8. 試す / 他の人のLINE Botも試す

試す際はLINEで話しかけて動作を確認してみましょう。

QRコードを共有することで他の人にも使ってもらえます。  
他の人のLINE Botも使ってみましょう。

---

## 3. Tips: ほかの作り方もある

LINE BotはDifyとは別の仕組みなので、ほかにも色々な連携方法があります。

例
- プログラムを書いて連携する（自前サーバー）
- 他のノーコードツールと組み合わせる
- 外部APIと連携してリアルタイム情報を扱う

興味がある人は調べてみましょう。

---

## 4. チャレンジ課題（応用: リッチメニュー）

リッチメニューという機能を使うと、LINE Botの見栄えと操作性が格段に上がります。  
特にプログラムが必要なわけではなく、管理画面の設定から作れるので、余裕がある人はチャレンジしてアプリケーションとしての使い勝手を上げましょう。

参考リンク（ノーコード）
- LINE公式アカウント（LINE Official Account Manager）リッチメニューを作成するマニュアル｜LINEヤフー for Business  
  https://www.lycbiz.com/jp/manual/OfficialAccountManager/rich-menus/

プログラムで制御したい人（発展）
- リッチメニューを使う（LINE Developers）  
  https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/

![LINEリッチメニュー](https://i.gyazo.com/669a86b1940aa84ba5da6098e37057b0.png)

やってみること（例）
- `課題1.` リッチメニューを作成してBotに表示する
- `課題2.` よく使う質問をボタン化する（例: おすすめ/モデルコース/子連れ/グルメ）
- `課題3.` ボタン文言を「ユーザーのやりたいこと」ベースに調整する（迷わない導線にする）

### まだ時間がある方向け
- `課題4.` LINE Botの挨拶メッセージを、自分のBot用に書き換える
- `課題5.` QRコードを共有して、他の人に使ってもらう（フィードバックを集める）
- `課題6.` 他の人のLINE Botも試して、良いUI/返答の設計を真似する

---

## 5. まとめ

- Difyで作ったAIは、プラグインを使ってLINE Botとして提供できます
- 連携に必要なのは「チャンネルシークレット」「チャンネルアクセストークン」「Webhook URL設定」です
- まずは動くところまで作り、改善（プロンプト/ナレッジ/体験設計）で精度と満足度を上げていきましょう




---

このページの内容は以上です。  
[◀ 目次ページ](./readme.md)

- [次の資料へ](./04_rag.md)
- [前の資料へ](./02_dify_chat.md)
