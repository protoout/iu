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
- Difyのチャットアプリを作っておく  
  - 公開されてる必要があります。
    - <img src="/Photo/CleanShot 2026-01-17 at 11.49.03@2x.png">
---

### 2-1. Difyにプラグインを追加

Difyにはプラグインという外部サービスと連携しやすい仕組みがあります。  
LINE Bot以外にもSlackやNotion、スプレットシートなど主要なツールと連携できます。  
プラグインはOSS開発となっていて割と最近追加された機能なので、選択肢はまだ少ない印象です。

#### プラグインの検索
プラグインページから、マーケットプレイスへいきLINEのプラグインをインストールしましょう。

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

### 2-3. LINE DevelopersでWebhookの設定

最後、WebhookURLの設定です。

ここまでトラブルなく進むと、URLが発行されます。

![Webhook URLが発行される](https://storage.googleapis.com/zenn-user-upload/3a113c10e68c-20250809.png)

LINE Developersのコンソールで先ほどのURLをWebhook URLに設定します。

![LINE DevelopersでWebhook URLを設定](https://i.gyazo.com/16e353c1a68a3a0fd92d9b9d7a83bfd9.png)

問題なく連携できると、検証ボタンを押したときに成功と表示されます。

![検証が成功](https://i.gyazo.com/c1e4975d249ca4863a82288495990af4.png)

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

https://i.gyazo.com/669a86b1940aa84ba5da6098e37057b0.png
---

## 5. まとめ

この資料では、Difyで作成したAIをLINE Botとして利用できるようにする手順を学びました。ポイントを整理すると以下の通りです。

- DifyのAIをLINE Bot化できる  
  Difyで公開したチャットアプリを、LINEの公式アカウントと接続することで、身近なLINE上で利用可能になります。

- プラグインを活用した連携  
  Difyのプラグイン機能を使うと、LINEをはじめとした外部サービスと簡単に連携可能です。  
  今回はLINEプラグインを導入し、設定を行うことでAIをLINE Botとして動かせました。  
  ※安定稼働のため、LINEプラグインはバージョン0.0.4を利用するのが推奨です。

- Webhookの設定でLINEと接続完了  
  LINE Developersに発行されたWebhook URLを設定し、検証で成功が表示されれば、実際にLINE Botとして利用可能になります。

- 応用と拡張性  
  リッチメニューを設定することでUIを改善したり、他のノーコードツールやプログラムを組み合わせて拡張することもできます。  
  Difyを中核に据えれば、SlackやNotionなど他サービスとの連携も広がります。

今回のハンズオンで、DifyとLINE Botの連携の基本的な流れを体験できました。  
今後はリッチメニューや追加機能を試しながら、より使いやすいBotを作っていきましょう。

- [前の資料へ](/IU25/02_Dify.md))