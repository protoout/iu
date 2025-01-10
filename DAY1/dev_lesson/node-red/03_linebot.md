# 3.Node-REDでLINE Botにメッセージを送ろう

## このパートでやること

- LINEのノードをNode-REDにインストールする
- Node-REDからLINE Botにメッセージを送る

## このパートで作るもの

- injectノードで設定した言葉をLINE Botに通知する簡単な仕組みを作ります。  

<img src="https://i.gyazo.com/4f03f6e5b697f2e2e15c645911e5a923.png" width="450px" alt="image from gyazo"/>


## 1.LINEのノードをインストールをする

パレット内にLINEのノードを追加していきます。

- Node-REDの画面の右上にある三本線のメニューを開きます。  
`パレットの管理`を選択します。

<img src="https://i.gyazo.com/591e2aec34439626d298134a52b1e674.png" width="250px" alt="image from gyazo"/>

- ノードを検索という欄で`node-red-contrib-line-messaging-api`と検索します。  
右下の`ノード追加`を選択します。

<img src="https://i.gyazo.com/1f3e1e532ccfb87867402b1b1007f067.png" width="450px" alt="image from gyazo"/>

- パレット内にLINEのノードが追加されました。  
追加が確認できたら、無事にインストール完了です！

<img src="https://i.gyazo.com/10793eb4490b9f01a15038b05b6f7168.png" width="250px" alt="image from gyazo"/>


## 2.LINE Botにメッセージを送る

ノードを繋げていき、LINE Botに簡単なメッセージを送ってみます。

### 2-1.ノードを繋げる

- このパートでは、新しい作業場所を作らずに進めていきます。  
[02.Webサイトからニュースデータを取得してみよう](./02_api.md)で作ったノードたちの下付近で新しくノードを繋げていきます。

- パレット内`共有`の中にある`injectノード`をワークスペースに入れます。 

<img src="https://i.gyazo.com/3600262f56396bc765ba15fbf0d3b2bb.png" width="450px" alt="image from gyazo"/>

- パレット内で先ほど追加した`LINE`の中にある`Pushノード`をinjectノードの右側に配置します。  

<img src="https://i.gyazo.com/fc8dd351197293fcb8c87106e17525b8.png" width="450px" alt="image from gyazo"/>

- 2つのノードを繋げます。

<img src="https://i.gyazo.com/d446fc49180360a5775f9c64e65d7cfa.png" width="450px" alt="image from gyazo"/>

### 2-2.injectノードを設定する 
 
- injectノードをダブルクリックして、プロパティを開きます。

- `文字列`を選択します。

<img src="https://i.gyazo.com/da266a9513cec2f01fffb21bbb476ede.png" width="450px" alt="image from gyazo"/>

- 送りたいメッセージを入れる。（LINE Botに通知されるメッセージになります。）  
`Node-REDから文字の送信`と入れてみましょう。

<img src="https://i.gyazo.com/147e07ef805fe52b44c6ab1e56cb135f.png" width="450px" alt="image from gyazo"/>


### 2-2.Pushノードの設定準備をする

- Pushノードをダブルクリックして、プロパティを開きます。

<img src="https://i.gyazo.com/6b1ec08ca8672b8ab1ec53a06dc21483.png" width="450px" alt="image from gyazo"/>

- プロパティ内の`LINE Bot`欄の右側にある`鉛筆マーク`を押します。  
下記のような画面になります。

<img src="https://i.gyazo.com/0ce0faaf32848bbe7d45a2697248dcb5.png" width="450px" alt="image from gyazo"/>

LINE Botと連携するため、チャネルシークレットやアクセストークン、IDなど必要な情報を入れる必要があります。

### 2-3.LINE Developersから連携に必要な情報をとり、プロパティに設定する

LINE Developersを開きます。  
[LINE Developers](https://developers.line.biz/ja/)

<img src="https://i.gyazo.com/c271fcc9e3b7959f3ea6fc2fa1b157e3.png" width="350px" alt="image from gyazo"/>

**miiboの時に使用したLINE Botと一緒のチャネルで大丈夫です。**

- LINE Developersから必要な情報をコピーし、Pushノードのプロパティに貼り付けていきます。
  - 必要な情報  
    -  チャネル名（LINE Developers内のチャネル基本設定の中にあります）
    -  チャネルシークレット（LINE Developers内のチャネル基本設定の中にあります）
    -  チャネルアクセストークン（LINE Developers内のMessaging API設定の中にあります）
    -  ユーザーID（LINE Developers内のチャネル基本設定の中にあります）

<details>

<summary>必要な情報をコピペする詳しい手順はこちらから</summary>

- LINE Developers内のチャネル基本設定から`チャネル名`をコピーします。

<img src="https://i.gyazo.com/b24acd3299f6d61c3a5f1a549ef33c6d.png" width="350px" alt="image from gyazo"/>

- Node-RED内のプロパティの中の`Bot Name`に貼り付けます。

<img src="https://i.gyazo.com/d9035e226b634a9ba552771fbb88c1ef.png" width="450px" alt="image from gyazo"/>

- LINE Developers内のチャネル基本設定から`チャネルシークレット`をコピーします。

<img src="https://i.gyazo.com/2bd69c910eaac992f64b2664da8a4eff.png" width="450px" alt="image from gyazo"/>

- Node-RED内のプロパティの中の`Channel Secret`に貼り付けます。

<img src="https://i.gyazo.com/7f6e7dfba12af8211ecaeccff77d7120.png" width="350px" alt="image from gyazo"/>

- LINE Developers内のMessaging API設定から`チャネルアクセストークン`をコピーします。

<img src="https://i.gyazo.com/854e4cf8b1b0c4040de56f19466c18dd.png" width="450px" alt="image from gyazo"/>

- Node-RED内のプロパティの中の`Channel Access Token`に貼り付けます。

<img src="https://i.gyazo.com/f9f06aa4d337f8473df7db4f60076305.png" width="350px" alt="image from gyazo"/>

- 右上の「更新」を選択します。  
再び`AccessToken`内に`チャネルアクセストークン`を貼り付けます。

<img src="https://i.gyazo.com/420d0311ab63dd1725e445c8417376e5.png" width="450px" alt="image from gyazo"/>

- LINE Developers内のチャネル基本設定から`あなたのユーザーID`をコピーします。

<img src="https://i.gyazo.com/7fa8219ea2b7a9d6c2f6e3885c8d9faa.png" width="450px" alt="image from gyazo"/>

- Node-RED内のプロパティの中の`User Id or Group ID`に貼り付けます。

<img src="https://i.gyazo.com/9d638034b74858773f8c0acb62d7c888.png" width="450px" alt="image from gyazo"/>

</details>

- Pushノードのプロパティに必要な情報を入れることができた画面は下記のようになります。  
  - 鉛筆マーク画面

<img src="https://i.gyazo.com/f9f06aa4d337f8473df7db4f60076305.png" width="450px" alt="image from gyazo"/>

  - プロパティ最初の画面

  <img src="https://i.gyazo.com/9d638034b74858773f8c0acb62d7c888.png" width="450px" alt="image from gyazo"/>

### 2-4.LINE Botでメッセージの通知確認をする

- 必要な情報を入れることができたか確認できたら`完了`ボタンを選択します。
- `デプロイ`ボタンを押します。
- injectノードの左側にある四角いボタンを１度押します。  
これにより左から右へ処理が実行されていきます。

<img src="https://i.gyazo.com/3c87c9982ac101777e433a568d5293c1.png" width="250px" alt="image from gyazo"/>

- LINE Botに`Node-REDから文字の送信`というメッセージが通知されていたらOKです！

<img src="https://i.gyazo.com/4f03f6e5b697f2e2e15c645911e5a923.png" width="450px" alt="image from gyazo"/>


## チャレンジ課題

- LINE Botに通知するメッセージを変えてみましょう。

- [次の資料へ](./04_api_linebot.md)
- [トップページへ](./readme.md)
