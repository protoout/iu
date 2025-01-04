# 3.miiboを用いてLINE Botを作ろう

## このパートでやること

- LINEの情報を取得してmiiboに登録していきます。


## このパートで作るもの

- miiboとLINEを連携して、会話型AIのLINE Botを作る  
何かメッセージを送信すると、返答が来る仕組みになります。

<img src="https://i.gyazo.com/078e7398d19084061828cae7c8934f8c.png" width="350px" alt="image from gyazo"/>


## 1.LINEの情報を取得する

### 1-1.LINEのチャネルを開く

- LINE Developersにログインします。  
`コンソールからログイン`→`LINEアカウントでログイン`→`ログイン`  
LINE Developers：https://developers.line.biz/ja/

- コンソールから事前に作ったプロバイダーの中のチャネルを開きます  
<img src="https://i.gyazo.com/904ada972e3f14c175986f1bf56556de.png" width="450px" alt="image from gyazo"/>


### 1-2.LINEの情報を取得する

- 「チャネル基本設定」のタブから「チャネルシークレット」を取得します
  - 発行されていなければ、`発行`ボタンをクリックして文字列をコピーします。  
  コピーしたら、パソコンに搭載されているメモ帳、付箋、Wordなどに貼り付けて控えておきましょう。

<img src="https://i.gyazo.com/ba1324e1744b946075b6c431bd27a16a.png" width="450px" alt="image from gyazo"/>

<img src="https://i.gyazo.com/f13b828514fb92fc40b7ac400dcf7788.png" width="450px" alt="image from gyazo"/>

- 「Messageing API設定」のタブから「チャネルアクセストークン」を取得します  
  - 発行されていなければ、`発行`ボタンをクリックして文字列をコピーします。  
  こちらもコピーしたら、メモ帳、付箋、Wordなどに貼り付けて控えておきましょう。

<img src="https://i.gyazo.com/c87e8d9e659aae5a400d061d805f62a8.png" width="450px" alt="image from gyazo"/>
<img src="https://i.gyazo.com/47f9f55878de22f875eeaa25c49bcd97.png" width="450px" alt="image from gyazo"/>

- 応答機能を確認します  
  - あいさつメッセージは有効になっていることがおすすめです。  
  右側の`編集`ボタンから下記のように設定しておきます。

<img src="https://i.gyazo.com/d9a707b5b85c3401cc2b9b536ba71104.png" width="450px" alt="image from gyazo"/>

<img src="https://i.gyazo.com/9ea92e7237b87af7e59feb8b3d576c0e.png" width="450px" alt="image from gyazo"/>


## 2.miiboにLINEの情報を登録する

- miiboのエージェントページに移動します  
左側のメニューバーから「外部サービス連携」をクリックします。

<img src="https://i.gyazo.com/3b998db521042669c0d4157fc2e2ff19.png" width="250px" alt="image from gyazo"/>

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

<img src="https://i.gyazo.com/c87e8d9e659aae5a400d061d805f62a8.png" width="450px" alt="image from gyazo"/>

- Webhook URLの `編集`ボタンをクリックします。

<img src="https://i.gyazo.com/2dc501d6a7c30fe75ce8d6572657ecf0.png" width="350px" alt="image from gyazo"/>

- 先ほどコピーしたWebhook URLを貼り付け、`更新`ボタンをクリックします。

<img src="https://i.gyazo.com/57486cb575b3d8fd6b6615929d644bab.png" width="450px" alt="image from gyazo"/>

- Webhookの利用ボタンをクリックし、オンにします。

<img src="https://i.gyazo.com/88de95e073afa7218f78e883e8fa3d4d.png" width="450px" alt="image from gyazo"/>

- `検証`ボタンをクリックし、「成功」の表示がでたら連携完了です。

<img src="https://i.gyazo.com/2699f7e4370f7140e2b8ff2e12e9a805.png" width="250px" alt="image from gyazo"/>

## 4.ひとまず完成！

### LINEから会話してみましょう

- スマートフォンで、友達になったLINE Botへ何かを送信し、返答がくるのを確認しましょう。  

<img src="https://i.gyazo.com/078e7398d19084061828cae7c8934f8c.png" width="350px" alt="image from gyazo"/>

- miiboとLINE Botが連携され、会話型AIが完成しました！
ここからオリジナリティを出していきましょう。

- [次の資料へ](./04_custom.md)
- [トップページへ](./readme.md)


