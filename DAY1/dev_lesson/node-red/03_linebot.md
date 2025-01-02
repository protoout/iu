# 3.Node-REDでLINE Botにメッセージを送ろう

## このパートでやること

- LINEのノードをNode-REDにインストールする
- Node-REDからLINE Botにメッセージを送る

## 今回作るもの

- injectノードで設定した言葉をLINE Botに通知する簡単な仕組みを作ります。  

<img src="https://storage.googleapis.com/zenn-user-upload/1685ed3f0709-20241230.png" width="450px" alt="image from gyazo"/>


## ハンズオン：一緒に作っていきましょう！

## 1.LINEのノードをインストールをする

パレット内にLINEのノードを追加していきます。

- Node-REDの画面の右上にある三本線のメニューを開きます。

<img src="https://i.gyazo.com/591e2aec34439626d298134a52b1e674.png" width="450px" alt="image from gyazo"/>

- 「パレットの管理」を選択します。
- ノードを検索という欄で「node-red-contrib-line-messaging-api」と検索します。  
右下の「ノード追加」を選択します。

<img src="https://storage.googleapis.com/zenn-user-upload/ced7848977a6-20241230.png" width="450px" alt="image from gyazo"/>

- パレット内にLINEのノードが追加されました。  
追加が確認できたら、無事にインストール完了です！

<img src="https://storage.googleapis.com/zenn-user-upload/ef516502f3da-20241230.png" width="450px" alt="image from gyazo"/>


## 2.LINE Botにメッセージを送る

ノードを繋げていき、LINE Botに簡単なメッセージを送ってみます。

- パレット内「共有」の中にある**injectノード**をワークスペースに入れます。 
- パレット内で先ほど追加した「LINE」の中にある**Pushノード**をinjectノードの右側に配置します。  
　2つのノードを繋げます。

<img src="https://storage.googleapis.com/zenn-user-upload/b886b530b957-20241230.png" width="450px" alt="image from gyazo"/>




<img src="" width="450px" alt="image from gyazo"/>
<img src="" width="450px" alt="image from gyazo"/>



LINE Developers　ページから
・secret：チャネル基本設定→チャネルシークレットをコピーしてノードへ貼り付ける
・AccessToken：Messaging API設定→アクセストークンをコピーしてノードへ貼り付ける
・ID：Messaging API設定→ボットのベーシックIDをコピーしてノードへ貼り付ける
![](https://storage.googleapis.com/zenn-user-upload/c34f46811fe4-20241230.png)
![](https://storage.googleapis.com/zenn-user-upload/d8474b4529fd-20241230.png)

完了ボタン押す

injectノードの設定
![](https://storage.googleapis.com/zenn-user-upload/ceab5a9654a0-20241230.png)

Pushノードの設定
![](https://storage.googleapis.com/zenn-user-upload/d5c4a92f83fe-20241230.png)

デプロイしてみる

LINEにメッセージが送れた！プッシュメッセージできた
![](https://storage.googleapis.com/zenn-user-upload/1685ed3f0709-20241230.png)



## チャレンジ課題

- [次の資料へ](./04_api_linebot.md)
- [トップページへ](./readme.md)