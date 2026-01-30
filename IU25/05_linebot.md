# LINEと連携をした「盛岡の観光アドバイザーLINE Bot」を作ろう

このパートでは、Difyで作った盛岡観光AIチャットボットを、LINE上で動くBotとして利用できる形にします。  
LINEはみなさんの身の回りの（もはや生活の基盤になっている）アプリなので、触れることがイメージしやすいのが強みです。  
- [LINE1億人突破](https://x.com/itm_mobile/status/2016734324117459255?s=46)

    <img src="https://i.gyazo.com/355989836f8dec83fd666346ef7a9868.png" width="300px" alt="image from gyazo"/>


- LINE Botは、LINE上で動作するチャットボットです。
- お店の公式アカウントをイメージしてもらえると良いです。
  - [郵便局LINE「ぽすくま」](https://www.post.japanpost.jp/send/line/index.html)

    <img src="https://i.gyazo.com/584ad087677f0a94caa5649177ab6ec8.png" width="300px" alt="image from gyazo"/>

- 個人のLINEアカウントとは別物です。
- LINE公式アカウントは複数作れるので、用途別にBotを作って試すことができます   
  - 例：盛岡観光Bot / 大学案内Bot / サークル新歓Bot など

<br>

参考：Bot（ボット）は、**人の代わりに自動でやり取りや処理を行うプログラム**のことです。
  - 例えば「質問に自動で返事をする」「案内をする」「予約や申請の受付をする」などを、ルールやAIを使って実行します。

  - [スターバックスLINEでモバイルオーダー](https://www.starbucks.co.jp/mobileorder/line/?srsltid=AfmBOorlyDn1F7MMv6uCnyz6CYoa5a_jU0I6oGPBmkvy8f7bk-ZygOum)

    <img src="https://i.gyazo.com/23d8488beab27b4d1ddb28f1f7d0bc28.png" width="300px" alt="image from gyazo"/>

## 1. 作るアプリケーション

### 1-1. 盛岡の観光情報について質問すると、AIが回答してくれるLINE Bot

  <img src="https://i.gyazo.com/b132065325a9792bb0a1fc7a5c8004b8.png" width="450px" alt="image from gyazo"/>

## 2. ハンズオン：盛岡の観光アドバイザーLINE Botを作ろう

### 2-1. Difyのチャットアプリを準備する

- 盛岡観光AIチャットボットが公開になっているか確認しておきましょう。

    <img src="https://i.gyazo.com/b66569ab623f4d957cd11406afea8a0d.png" width="450px" alt="image from gyazo"/>

### 2-2. DifyにLINEプラグインを追加する

Difyには外部サービスと連携しやすい「プラグイン」機能があります。  

1. 右上にある`プラグイン`ボタンをクリックします。

    <img src="https://i.gyazo.com/73b39427cd085ff89b46f7eb900a8d3b.png" width="450px" alt="image from gyazo"/>

2. 様々なプラグイン機能が載っている「マーケットプレイス」が開かれます。

    <img src="https://i.gyazo.com/ab4e2c1421386436eeb7df03bd1ac7e1.png" width="450px" alt="image from gyazo"/>

3. `検索プラグイン`の検索バーで「LINE」や「LINE Bot」と検索をして、`LINE Bot`をクリックします。

    <img src="https://i.gyazo.com/1c2ca1961d889788eb3dd60a156c81db.png" width="450px" alt="image from gyazo"/>

4. 右下の`インストール`ボタンをクリックしてインストールしましょう。

    <img src="https://i.gyazo.com/11c6ade0c1750586be03eda3bb3950ce.png" width="450px" alt="image from gyazo"/>

重要: LINEプラグインのバージョンを0.0.4に下げる  
コミュニティ知見として、最新の0.0.5だとバグで動かないケースがあるため、0.0.4にダウングレードします。

5. マーケットプレイスを探索するタブから、画面左上の`プラグイン`タブに移動しましょう。

    <img src="https://i.gyazo.com/4d9b98ca1138fb9bbd056622db32314e.png" width="450px" alt="image from gyazo"/>

6. 先ほどインストールしたLINE Botの枠内をクリックすると、右側にバージョン設定が出てきます。
  
    <img src="https://i.gyazo.com/7942431bf430e4d551d8af4e771d3920.png" width="450px" alt="image from gyazo"/>

7. バージョン0.0.4部分をクリックします。

    <img src="https://i.gyazo.com/9ef2508191d68e068ad2e25ea5bbc5b7.png" width="450px" alt="image from gyazo"/>

8. `とにかくダウングレードする`をクリックします。

    <img src="https://i.gyazo.com/efc7555d54335a5ac8a2dfb69411e527.png" width="450px" alt="image from gyazo"/>

9. 0.0.4にダウングレードできました

    <img src="https://i.gyazo.com/eaef1b8231978dec905c7bb6b4d79cc7.png" width="450px" alt="image from gyazo"/>

### 2-3. エンドポイントを設定する

1. インストールしたらエンドポイントの設定へ進みます

    <img src="https://i.gyazo.com/62cfd349da465c94475dc743162ada9c.png" width="450px" alt="image from gyazo"/>

3. `+` ボタンから作成します。

    <img src="https://i.gyazo.com/3c1b027ae1be6071db87d0273d7fa7fc.png" width="450px" alt="image from gyazo"/>
  
3. 各項目に必要事項を入力します。
  - **エンドポイント名**: `dify-line-bot`
  - **チャネルシークレット**: 事前に準備したwordやメモ帳などに控えているチャネルシークレットをコピーして貼り付ける
  - **チャネルアクセストークン**: 事前に準備したwordやメモ帳などに控えているチャネルアクセストークンをコピーして貼り付ける
  - **アプリ**: 作成したチャットフローを選択

    <img src="https://i.gyazo.com/bb04e337be5b9c4d8807a651ba58b9fe.png" width="450px" alt="image from gyazo"/>

### 2-4. Webhook URLを設定する（連携の仕上げ）  

WebhookURLをつかってDify側とLINEを連携します。  

> [!TIP]
> Webhookとは？：サービス（アプリケーション）の何らかのアクションを他のアプリケーションへリアルタイムに通知する仕組みのこと  

1. Dify側でWebhook URLが発行されたら、下記画像の赤枠のマークをクリックしてコピーしましょう。

    <img src="https://i.gyazo.com/d91b9ded1ee5b6cd464cc616a4d04886.png" width="450px" alt="image from gyazo"/>

2. [LINE Developers](https://developers.line.biz/ja/docs/line-developers-console/)を開き、`LINEアカウント`をクリックします。
    
    <img src="https://i.gyazo.com/e925062eb2d104283343de71c105b1f5.png" width="300px" alt="image from gyazo"/>

3. `ログイン`をクリックします。
    
    <img src="https://i.gyazo.com/92c3f1a38b11b069b1d62aca419acd1f.png" width="300px" alt="image from gyazo"/>

4. ご自身で登録したチャネル（例：`盛岡の観光アドバイザー`）を開きます。
    
    <img src="https://i.gyazo.com/b017a2e5fa6151556fbec1770fece089.png" width="450px" alt="image from gyazo"/>

5. `Messaging API設定`タブを開きます。
    
    <img src="https://i.gyazo.com/483fba01e56b7afda6a5df29379db70a.png" width="450px" alt="image from gyazo"/>

6. `Webhook設定`の`編集`ボタンをクリックします。

   > <img src="https://i.gyazo.com/b2926bfddcc5faa8b594094c97744c4f.png" width="300px" alt="image from gyazo"/>

7. 先ほどコピーしたURLをWebhook URLに設定します。

    <img src="https://i.gyazo.com/42c018ea53c79da753ad2b342ca85de3.png" width="450px" alt="image from gyazo"/>

8. その下にある`Webhookの利用`ボタンをクリックし、オン（緑色の状態）にします。

    <img src="https://i.gyazo.com/88de95e073afa7218f78e883e8fa3d4d.png" width="450px" alt="image from gyazo"/>

9. `検証`ボタンを押して成功と表示されればOKです。

    <img src="https://i.gyazo.com/c1e4975d249ca4863a82288495990af4.png" width="450px" alt="image from gyazo"/>

### 2-5. LINEから会話してみよう

スマートフォンで、友達になったLINE Botへ何かメッセージを送信し、返答がくるのを確認しましょう。

<img src="https://i.gyazo.com/149e85e5b9dbe16946f7441f44a7df2e.png" width="450px" alt="image from gyazo"/>
    
- DifyとLINE Botが連携され、AIと会話ができるLINE Botが完成しました！  
ここからオリジナリティを出していきましょう

## 3. Tips
### 3-1. Dify以外のLINE Bot連携方法

LINE BotはDifyとは別の仕組みで、ほかにも色々な連携方法があるので興味がある人は調べてみましょう。

  例
  - プログラムを書いて連携する（自前サーバー）
  - 他のノーコードツールと組み合わせる
  - 外部APIと連携してリアルタイム情報を扱う

### 3-2. Difyのプラグイン機能

- Difyのプラグイン機能では、LINE以外にも、Slack/Notion/スプレッドシートなどと連携できます。

    <img src="https://i.gyazo.com/2212299629f5be33c9c29f27829ee582.png" width="450px" alt="image from gyazo"/>

### 3-3. リッチメニュー

- リッチメニューという機能を使うと、LINE Botの見栄えと操作性が格段に上がります  
- 管理画面の設定で、プログラムなどは使わずに作ることができます。

  <img src="https://i.gyazo.com/831101cd49d0d302d5a2fb51ded99988.jpg" width="200px" alt="image from gyazo"/>

参考
- ノーコード：[LINE公式アカウント（LINE Official Account Manager）リッチメニューを作成するマニュアル｜LINEヤフー for Business](https://www.lycbiz.com/jp/manual/OfficialAccountManager/rich-menus/)

- 【発展】プログラムで制御したい人：[リッチメニューを使う（LINE Developers）](https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/)


### 3-4. 応答メッセージについて

今回は、LINE公式アカウント側の「応答設定」を以下のように調整しました。  
これは、**LINEの自動応答ではなく、Difyからの返信をメインにするため**です。　　
>  - チャット：オフ  
>  - 挨拶メッセージ：オン  
>  - Webhook：オフ（Webhook URL設定後にオンにします。）  
>  - 応答メッセージ：オフ  

  <details>
  <summary>補足：各項目の応答メッセージの機能について</summary>

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
  最初のメッセージが送られてこないので、追加したBotの存在が自動で表示されず、認識しづらくなります

  > 今回は、追加したBotの存在を認識してスムーズに会話を始めるため、オンにしています。


  - **Webhook**  
  LINE公式アカウントと外部サーバーを連携させる機能です。
  
    - WebhookのURLが未設定の場合
    LINE公式アカウント側でどこにメッセージを送るべきか分からないため、Webhookを有効にする選択肢が出てきません  
    WebhookのURLを設定した場合にオンまたはオフが選べるようになります

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
    - QRコードはLINE DevelopersのMessagingAPIにあります。

      <img src="https://i.gyazo.com/e85d3e270be31bf7fd6354bdc1d1f4f2.png" width="200px" alt="image from gyazo"/>
  
  - 他の人のLINE Botも試して、動作を確認してみましょう。

### 4-2. 色々な公式アカウントを検索して共有する

- お店やサービスのLINE公式アカウントで、使いやすいと思ったアカウントを2〜3個探して、次の観点で見てみましょう
  - どんな導線で会話が始まるか？
  - どんな機能が使われているか？
    - リッチメニュー / クーポン / 予約 / ポイントカード など
  - 「使いやすい」と感じた理由は？
- 見つけた「使いやすさ」を、後で作る自分のオリジナルLINE Botに取り入れたり、最後の発表タイムで共有しましょう。！

## 5. まとめ

このパートでは、**Difyで作ったAIをLINE Botとして使える形にする**ところまで作成しました。

Dify上で動かすだけでもプロトタイプはできますが、**LINEに載せることで普段使っているアプリからすぐ開ける**ようになります。  
その結果、日常の中で使うハードルが下がり、試したり改善したりするサイクルを回しやすくなります。  

LINE Botは、たとえば**研究室・サークル・ゼミ内の連絡窓口**や、**学内施設の案内**など、身近なシーンの導線としても使えます。  
思いついたアイデアを素早く形にする手段の1つとして、**Dify × LINE**もぜひ活用してみてください。
<br>
さらに外部サービスと連携することで、データの記録や参照できるLINE Botも作成できます。  
[LINE Developers Communityの作成事例](https://www.youtube.com/@linedevelopercommunity9922/search?query=LINE%20Bot)や[QiitaのLINE Bot作成事例](https://qiita.com/search?q=LINEBot&sort=like)を見てどんなことができるか自分で探して幅を広げてみてください。


---

このページの内容は以上です。  

[◀ 目次ページ](./readme.md)
