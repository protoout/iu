# LINEと連携をした「盛岡の観光アドバイザーLINE Bot」を作ろう

このパートでは、Difyで作ったBot（盛岡の知識に強いAI）を、LINE上で動くBotとして利用できる形にします。  
- LINEはみなさんの身の回りにある身近なアプリなので、触れることがイメージしやすいのが強みです。
- Bot（ボット）は、**人の代わりに自動でやり取りや処理を行うプログラム**のことです。
  - 例えば「質問に自動で返事をする」「案内をする」「予約や申請の受付をする」などを、ルールやAIを使って実行します。
- LINE Botは、LINE上で動作するチャットボットです。お店の公式アカウントをイメージしてもらえると良いです。
  - [郵便局LINE「ぽすくま」](https://www.post.japanpost.jp/send/line/index.html)

    <img src="https://i.gyazo.com/584ad087677f0a94caa5649177ab6ec8.png" width="300px" alt="image from gyazo"/>

  - [スターバックスLINEでモバイルオーダー](https://www.starbucks.co.jp/mobileorder/line/?srsltid=AfmBOorlyDn1F7MMv6uCnyz6CYoa5a_jU0I6oGPBmkvy8f7bk-ZygOum)

    <img src="https://i.gyazo.com/23d8488beab27b4d1ddb28f1f7d0bc28.png" width="300px" alt="image from gyazo"/>

- 個人のLINEアカウントとは別物です（個人アカウントをBot化するわけではありません）
- LINE公式アカウントは複数作れるので、用途別にBotを作って試せます  
  （例：盛岡観光Bot / 大学案内Bot / サークル新歓Bot など）

## 1. このパートで作るもの

### 1-1. 盛岡の観光情報について質問すると、AIが回答してくれるLINE Bot

  <img src="https://i.gyazo.com/b132065325a9792bb0a1fc7a5c8004b8.png" width="300px" alt="image from gyazo"/>

### 1-2. フロー画面
- [DIfy](https://cloud.dify.ai/)のフロー画面をひらいておきましょう

    <img src="https://i.gyazo.com/b2c0d6c458f5c309f29c5ba43cc9621a.png" width="300px" alt="image from gyazo"/>

## 2. ハンズオン：盛岡の観光アドバイザーLINE Botを作ろう

### 2-1. Difyのチャットアプリを準備する

- 先ほど制作したDifyのチャットアプリは公開になっている必要があります。
- アプリが公開されているか確認しておきましょう。

    <img src="https://i.gyazo.com/b66569ab623f4d957cd11406afea8a0d.png" width="300px" alt="image from gyazo"/>

### 2-2. DifyにLINEプラグインを追加

Difyには外部サービスと連携しやすい「プラグイン」機能があります。  
LINE以外にも、Slack/Notion/スプレッドシートなどと連携できます。

1. 右上にある`プラグイン`ボタンをクリックします。

    <img src="https://i.gyazo.com/73b39427cd085ff89b46f7eb900a8d3b.png" width="300px" alt="image from gyazo"/>

2. 様々なプラグイン機能が載っている「マーケットプレイス」が開かれます。

    <img src="https://i.gyazo.com/ab4e2c1421386436eeb7df03bd1ac7e1.png" width="300px" alt="image from gyazo"/>

3. `検索プラグイン`の検索バーで「LINE」や「LINE Bot」と検索をします。

    <img src="https://i.gyazo.com/1c2ca1961d889788eb3dd60a156c81db.png" width="300px" alt="image from gyazo"/>

4. 右下の`インストール`ボタンをクリックしてインストールしましょう。

    <img src="https://i.gyazo.com/11c6ade0c1750586be03eda3bb3950ce.png" width="300px" alt="image from gyazo"/>

### 2-3. 重要: LINEプラグインのバージョンを0.0.4に下げる

- コミュニティ知見として、最新の0.0.5だとバグで動かないケースがあるため、0.0.4にダウングレードします。

1. マーケットプレイスを探索するタブから、以下画像左上の「プラグイン」タブに移動しましょう。

    <img src="https://i.gyazo.com/4d9b98ca1138fb9bbd056622db32314e.png" width="300px" alt="image from gyazo"/>

2. 先ほどインストールしたLINE Botの枠内をクリックすると、右側にバージョン設定が出てきます。
  
    <img src="https://i.gyazo.com/7942431bf430e4d551d8af4e771d3920.png" width="300px" alt="image from gyazo"/>

3. このバージョン部分をクリックして、0.0.4にダウングレードします。

    <img src="https://i.gyazo.com/c158e3c8746e232ac13663f1166f4ab7.png" width="300px" alt="image from gyazo"/>

### 2-4. エンドポイントの設定

1. インストールしたらエンドポイントの設定へ進みます。

    <img src="https://i.gyazo.com/62cfd349da465c94475dc743162ada9c.png" width="300px" alt="image from gyazo"/>

3. `+` ボタンから作成します。

    <img src="https://i.gyazo.com/3c1b027ae1be6071db87d0273d7fa7fc.png" width="300px" alt="image from gyazo"/>
  
3. 各項目に必要事項を入力します。
  - エンドポイント名: `dify-line-bot`
  - チャネルシークレット: 事前に準備したwordやメモ帳などに控えているチャネルシークレットをコピーして貼り付ける
  - チャネルアクセストークン: 事前に準備したwordやメモ帳などに控えているチャネルアクセストークンをコピーして貼り付ける
  - アプリ: 作成したチャットフローを選択

    <img src="https://i.gyazo.com/bb04e337be5b9c4d8807a651ba58b9fe.png" width="300px" alt="image from gyazo"/>

### 2-5. LINE DevelopersでWebhook URLの設定（連携の仕上げ）

1. ここまで問題なく進むと、Dify側でWebhook URLが発行されます。
  - 発行したWebhookURLの上にカーソルを持っていき、下記画像の赤枠のマークをクリックしてコピーしましょう。

    <img src="https://i.gyazo.com/d91b9ded1ee5b6cd464cc616a4d04886.png" width="300px" alt="image from gyazo"/>

  - 補足: Webhookとは？  
    サービス（アプリケーション）の何らかのアクションを他のアプリケーションへリアルタイムに通知する仕組みのことです。

    < img src="https://i.gyazo.com/245a3596028af63c4b7e5c352d07ff6c.png" width="450px" alt="image from gyazo"/>

2. [LINE Developersのコンソール](https://developers.line.biz/ja/docs/line-developers-console/)を開きます。
  - `LINEアカウントでログイン`をクリックします。
    
    <img src="https://i.gyazo.com/e925062eb2d104283343de71c105b1f5.png" width="300px" alt="image from gyazo"/>

  - `ログイン`をクリックします。
    
    <img src="https://i.gyazo.com/bb04e337be5b9c4d8807a651ba58b9fe.png" width="300px" alt="image from gyazo"/>

3. `盛岡の観光アドバイザー`を開きます。
    
    <img src="https://i.gyazo.com/b017a2e5fa6151556fbec1770fece089.png" width="300px" alt="image from gyazo"/>

4. `Messaging API設定`タブを開きます。
    
    <img src="https://i.gyazo.com/483fba01e56b7afda6a5df29379db70a.png" width="300px" alt="image from gyazo"/>

5. `Webhook設定`の`編集`ボタンをクリックします。

    <img src="https://i.gyazo.com/54330709801aabf9f5fe63ff6c96a58f.png" width="300px" alt="image from gyazo"/>

6. 先ほどコピーしたURLをWebhook URLに設定します。

    <img src="https://i.gyazo.com/42c018ea53c79da753ad2b342ca85de3.png" width="300px" alt="image from gyazo"/>

7. その下にある`Webhookの利用`ボタンをクリックし、オンにします

    <img src="https://i.gyazo.com/88de95e073afa7218f78e883e8fa3d4d.png" width="300px" alt="image from gyazo"/>

8. 検証ボタンを押して成功と表示されればOKです。

    <img src="https://i.gyazo.com/c1e4975d249ca4863a82288495990af4.png" width="300px" alt="image from gyazo"/>

### 2-6. LINEから会話してみよう

- スマートフォンで、友達になったLINE Botへ何かメッセージを送信し、返答がくるのを確認しましょう。

    <img src="https://i.gyazo.com/b132065325a9792bb0a1fc7a5c8004b8.png" width="300px" alt="image from gyazo"/>
    
- DifyとLINE Botが連携され、AIと会話ができるLINE Botが完成しました！  
ここからオリジナリティを出していきましょう。

## 3. Tips
### 3-1. Dify以外のLINE Bot連携方法

- LINE BotはDifyとは別の仕組みなので、ほかにも色々な連携方法があります。

  例
  - プログラムを書いて連携する（自前サーバー）
  - 他のノーコードツールと組み合わせる
  - 外部APIと連携してリアルタイム情報を扱う

  興味がある人は調べてみましょう。

### 3-2. 応答メッセージについて

- 今回は、LINE公式アカウント側の「応答設定」を以下のように調整しました。  
  これは、**LINEの自動応答ではなく、Difyからの返信をメインにするため**です。
  - チャット：オフ  
  - 挨拶メッセージ：オン  
  - Webhook：オフ（Webhook URL設定後にオンにします）  
  - 応答メッセージ：オフ  

- 各項目の意味を詳しく知りたい人は、以下を開いて確認してください。

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

  - **応答メッセージ**  
  ユーザーが送信したメッセージに対して、LINE公式アカウントが自動で返信を行う機能です。
  
    - LINE公式アカウントの基本的な自動応答機能として活用されており管理画面から設定できます。
    - 設定できるメッセージは「固定文」のみで、事前に設定した内容の応答を自動で返します。
 
      - 例：設定した文章「こんにちは！お問い合わせありがとうございます。」  
      ユーザー：「こんにちは」  
      LINE公式アカウント：「こんにちは！お問い合わせありがとうございます。」  

  > 今回は、応答をカスタマイズしてユーザーのニーズに合わせた返信を実現するため、オフにしています。

  </details>

## 4. チャレンジ

### 4-1. 自分のLINE Botを共有する/他の人のLINE Botも試す

  - QRコードを共有することで他の人にも使ってもらえます。
  - 他の人のLINE Botも試して、動作を確認してみましょう。

### 4-2. リッチメニュー

- リッチメニューという機能を使うと、LINE Botの見栄えと操作性が格段に上がります。  
- 管理画面の設定で、プログラムなどは使わずに作ることができます。

<img src="https://i.gyazo.com/831101cd49d0d302d5a2fb51ded99988.jpg" width="200px" alt="image from gyazo"/>

参考
- ノーコード：[LINE公式アカウント（LINE Official Account Manager）リッチメニューを作成するマニュアル｜LINEヤフー for Business](https://www.lycbiz.com/jp/manual/OfficialAccountManager/rich-menus/)

- 【発展】プログラムで制御したい人：[リッチメニューを使う（LINE Developers）](https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/)

### 4-3 色々な公式アカウントを検索して共有する

- お店やサービスのLINE公式アカウントで、使いやすいと思ったアカウントを2〜3個探して、次の観点で見てみましょう。
  - どんな導線で会話が始まるか？
  - どんな機能が使われているか？
    - リッチメニュー / クーポン / 予約 / ポイントカード など
  - 「使いやすい」と感じた理由は？
- 見つけた「使いやすさ」を、後で作る自分のオリジナルLINE Botに取り入れたり、最後の発表タイムで共有したりしましょう！

## 5. まとめ

このパートでは、**Difyで作ったAIをLINE Botとして使える形にする**ところまで作成しました。

LINE Botは、研究室・サークル・ゼミのFAQ、学内施設案内など、**身近な情報を答えるアシスタント**として、幅広く活用できます。

LINEは普段使っている人も多いので、**登録者が増えやすく、改善のフィードバックが集めやすい**のも利点です。

---

このページの内容は以上です。  

[◀ 目次ページ](./readme.md)
