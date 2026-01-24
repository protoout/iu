# 盛岡の観光アドバイザーLINE Botを作ろう

このパートでは、Difyで作ったBot（盛岡の知識に強いAI）を、LINE上で動くBotとして利用できる形にします。  
- LINEはおそらく皆さんが普段使っているアプリなので、使い始めるハードルが低いのが強みです。
- LINE Botは、そのLINE上で動作するチャットボットです。日頃使っているLINEとはすこし違うものだと思っていてください。
  - お店の公式アカウントをイメージしてもらえると良いです。

## 1. このパートで作るもの「AIと会話ができるLINE Bot」

- Difyで作成したAIをLINEに接続し、LINEでメッセージを送ると返信が返ってくるBotを作ります
- 作成イメージ:
- [盛岡の観光情報を教えてくれるチャットBot](https://x.com/T_taisyou/status/1954062259132792958)

<img src="https://i.gyazo.com/2973c4d251732e7e08b43885580d3268.png" width="250px" alt="image from gyazo"/>

参考リンク
- [LINE公式アカウント作成 / LINE Botの初め方](https://zenn.dev/protoout/articles/16-line-bot-setup)

## 2. DifyとLINE Botを連携する

### 2-1. Difyのチャットアプリを準備する

- 先ほど制作したDifyのチャットアプリは公開になっている必要があります。
<img src="https://i.gyazo.com/b66569ab623f4d957cd11406afea8a0d.png" width="450px" alt="image from gyazo"/>

### 2-2. DifyにLINEプラグインを追加

Difyには外部サービスと連携しやすい「プラグイン」機能があります。  
LINE以外にも、Slack/Notion/スプレッドシートなどと連携できます。

手順
- Difyのプラグインページからマーケットプレイスへ移動

<img src="https://i.gyazo.com/73b39427cd085ff89b46f7eb900a8d3b.png" width="450px" alt="image from gyazo"/>

<img src="https://i.gyazo.com/ab4e2c1421386436eeb7df03bd1ac7e1.png" width="450px" alt="image from gyazo"/>

検索
- `LINE Bot` や `LINE` などで検索すると候補が出てきます

<img src="https://i.gyazo.com/7f544df4463b7b4c50ec9a6de07899a5.png" width="450px" alt="image from gyazo"/>

- LINEプラグインを検索してインストールします

<img src="https://i.gyazo.com/11c6ade0c1750586be03eda3bb3950ce.png" width="450px" alt="image from gyazo"/>

### 2-3. 重要: LINEプラグインのバージョンを0.0.4に下げる

コミュニティ知見として、最新の0.0.5だとバグで動かないケースがあるため、0.0.4にダウングレードします。

<img src="https://i.gyazo.com/c158e3c8746e232ac13663f1166f4ab7.png" width="450px" alt="image from gyazo"/>

### 2-4. プラグインの設定（LINEのキーとDifyアプリを紐づけ）

インストールしたら設定へ進みます。

<img src="https://i.gyazo.com/62cfd349da465c94475dc743162ada9c.png" width="450px" alt="image from gyazo"/>

`+` ボタンから作成します。

<img src="https://i.gyazo.com/bce59781f3dbe0a83993d49a5ffe0f2e.png" width="450px" alt="image from gyazo"/>

入力項目
- エンドポイント名: 任意（わかりやすい名前）
- チャンネルシークレット: LINE Bot管理画面から取得
- チャンネルアクセストークン: LINE Bot管理画面から取得
- アプリ: 作成したチャットフロー（またはワークフロー）を選択

キー取得の参考
- https://zenn.dev/protoout/articles/16-line-bot-setup

<img src="https://i.gyazo.com/bb04e337be5b9c4d8807a651ba58b9fe.png" width="450px" alt="image from gyazo"/>

### 2-5. LINE DevelopersでWebhook URLの設定（連携の仕上げ）

ここまで問題なく進むと、Dify側でWebhook URLが発行されます。
  補足: Webhookとは？  
  サービス（アプリケーション）の何らかのアクションを他のアプリケーションへリアルタイムに通知する仕組みのことです。

<img src="https://i.gyazo.com/245a3596028af63c4b7e5c352d07ff6c.png" width="450px" alt="image from gyazo"/>

LINE Developersのコンソールで、先ほどのURLをWebhook URLに設定します。

<img src="https://i.gyazo.com/16e353c1a68a3a0fd92d9b9d7a83bfd9.png" width="450px" alt="image from gyazo"/>

- Webhookの利用ボタンをクリックし、オンにします

<img src="https://i.gyazo.com/88de95e073afa7218f78e883e8fa3d4d.png" width="450px" alt="image from gyazo"/>

検証ボタンを押して成功と表示されればOKです。

<img src="https://i.gyazo.com/c1e4975d249ca4863a82288495990af4.png" width="450px" alt="image from gyazo"/>

### 2-6. ひとまず完成！

- LINEから会話をしてみる
    - スマートフォンで、友達になったLINE Botへ何かメッセージを送信し、返答がくるのを確認しましょう。  
- DifyとLINE Botが連携され、AIと会話ができるLINE Botが完成しました！  
ここからオリジナリティを出していきましょう。

<img src="https://i.gyazo.com/2973c4d251732e7e08b43885580d3268.png" width="450px" alt="image from gyazo"/>

### 2-7. 試す / 他の人のLINE Botも試す

試す際はLINEで話しかけて動作を確認してみましょう。

QRコードを共有することで他の人にも使ってもらえます。  
他の人のLINE Botも使ってみましょう。

## 3. Tips
### 3-1. ほかの作り方もある

LINE BotはDifyとは別の仕組みなので、ほかにも色々な連携方法があります。

例
- プログラムを書いて連携する（自前サーバー）
- 他のノーコードツールと組み合わせる
- 外部APIと連携してリアルタイム情報を扱う

興味がある人は調べてみましょう。

### 3-2. 応答メッセージ

- それぞれの機能について気になる方は下記を参照ください。

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

## 4. 参考: リッチメニュー

リッチメニューという機能を使うと、LINE Botの見栄えと操作性が格段に上がります。  
特にプログラムが必要なわけではなく、管理画面の設定から作れるので、余裕がある人は、後ほど応用課題の際にチャレンジしてアプリケーションとしての使い勝手を上げましょう。

参考リンク（ノーコード）
- [LINE公式アカウント（LINE Official Account Manager）リッチメニューを作成するマニュアル｜LINEヤフー for Business](https://www.lycbiz.com/jp/manual/OfficialAccountManager/rich-menus/)

プログラムで制御したい人（発展）
- [リッチメニューを使う（LINE Developers）](https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/)

<img src="https://i.gyazo.com/669a86b1940aa84ba5da6098e37057b0.png" width="450px" alt="image from gyazo"/>
<img src="https://i.gyazo.com/d9a707b5b85c3401cc2b9b536ba71104.png" width="450px" alt="image from gyazo"/>

## 5. まとめ

- Difyで作ったAIは、プラグインを使ってLINE Botとして提供できます。
- 連携に必要なのは「チャンネルシークレット」「チャンネルアクセストークン」「Webhook URL設定」です。
- まずは動くところまで作り、プロンプトや体験設計を改善しながら精度と満足度を上げていきましょう！

---

このページの内容は以上です。  

[◀ 目次ページ](./readme.md)
