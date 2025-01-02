# 3.Node-REDでLINE Botにメッセージを送ろう

## このパートでやること

## 今回作るもの

## ハンズオン：一緒に作っていきましょう！

# LINEに通知する

## LINEのノードをインストールをする

Nodeの中でパレットの管理でnode-red-contrib-line-messaging-api と検索
![](https://storage.googleapis.com/zenn-user-upload/ced7848977a6-20241230.png)

追加されました
![](https://storage.googleapis.com/zenn-user-upload/ef516502f3da-20241230.png)

インストール完了！！

## LINE Botにプッシュメッセージを送るだけやってみる

injectノードと、「push」ノードをつなげる
![](https://storage.googleapis.com/zenn-user-upload/b886b530b957-20241230.png)

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