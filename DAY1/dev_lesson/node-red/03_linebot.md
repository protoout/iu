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
「パレットの管理」を選択します。

<img src="https://i.gyazo.com/591e2aec34439626d298134a52b1e674.png" width="450px" alt="image from gyazo"/>

- ノードを検索という欄で「node-red-contrib-line-messaging-api」と検索します。  
右下の「ノード追加」を選択します。

<img src="https://storage.googleapis.com/zenn-user-upload/ced7848977a6-20241230.png" width="450px" alt="image from gyazo"/>

- パレット内にLINEのノードが追加されました。  
追加が確認できたら、無事にインストール完了です！

<img src="https://storage.googleapis.com/zenn-user-upload/ef516502f3da-20241230.png" width="450px" alt="image from gyazo"/>


## 2.LINE Botにメッセージを送る

ノードを繋げていき、LINE Botに簡単なメッセージを送ってみます。

### 2-1.ノードを繋げる

- パレット内「共有」の中にある**injectノード**をワークスペースに入れます。 

<img src="https://i.gyazo.com/3600262f56396bc765ba15fbf0d3b2bb.png" width="450px" alt="image from gyazo"/>

- パレット内で先ほど追加した「LINE」の中にある**Pushノード**をinjectノードの右側に配置します。  

<img src="https://i.gyazo.com/fc8dd351197293fcb8c87106e17525b8.png" width="450px" alt="image from gyazo"/>

- 2つのノードを繋げます。

<img src="https://i.gyazo.com/d446fc49180360a5775f9c64e65d7cfa.png" width="450px" alt="image from gyazo"/>

### 2-2.injectノードを設定する 
 
- injectノードをダブルクリックして、プロパティを開く。

- 「文字列」を選択する

<img src="https://i.gyazo.com/da266a9513cec2f01fffb21bbb476ede.png" width="450px" alt="image from gyazo"/>

- 送りたいメッセージを入れる。（LINE Botに通知されるメッセージになります。）  
「Node-REDから文字の送信」と入れてみましょう。

<img src="https://i.gyazo.com/147e07ef805fe52b44c6ab1e56cb135f.png" width="450px" alt="image from gyazo"/>


### 2-2.Pushノードを設定する 

- Pushノードをダブルクリックして、プロパティを開く。

<img src="https://i.gyazo.com/6b1ec08ca8672b8ab1ec53a06dc21483.png" width="450px" alt="image from gyazo"/>

- プロパティ内の「LINE Bot」欄の右側にある「鉛筆マーク」を押します。  
下記のような画面になります。

<img src="https://i.gyazo.com/0ce0faaf32848bbe7d45a2697248dcb5.png" width="450px" alt="image from gyazo"/>

LINE Botと連携するため、チャネルシークレットやアクセストークン、IDなど必要な情報を入れる必要があります。

**LINE Developersを開く**
[LINE Developers](https://developers.line.biz/ja/)

<img src="https://storage.googleapis.com/zenn-user-upload/c34f46811fe4-20241230.png" width="450px" alt="image from gyazo"/>

- チャネル基本設定から「チャネル名」をコピーします。

<img src="https://i.gyazo.com/40a7c0f4b44070dbb4c9e9809fbb0044.png" width="450px" alt="image from gyazo"/>

- Node-RED内のプロパティの中の「Bot Name」に貼り付けます。

<img src="https://i.gyazo.com/70fa3e4b92cdcb175bdc3299182a4f8b.png" width="450px" alt="image from gyazo"/>

- チャネル基本設定から「チャネルシークレット」をコピーします。

<img src="https://i.gyazo.com/2bd69c910eaac992f64b2664da8a4eff.png" width="450px" alt="image from gyazo"/>

- Node-RED内のプロパティの中の「Channel Secret」に貼り付けます。

<img src="https://i.gyazo.com/3a0f5e724390eea86e4f9672024a326a.png" width="450px" alt="image from gyazo"/>

- Messaging API設定から「チャネルアクセストークン」をコピーします。

<img src="https://i.gyazo.com/854e4cf8b1b0c4040de56f19466c18dd.png" width="450px" alt="image from gyazo"/>

- Node-RED内のプロパティの中の「Channel Access Token」に貼り付けます。

<img src="https://i.gyazo.com/1b4ea98a979088fc91279347b0241793.png" width="450px" alt="image from gyazo"/>

- 右上の「更新」を選択する。






<img src="" width="450px" alt="image from gyazo"/>


<img src="" width="450px" alt="image from gyazo"/>


![](https://storage.googleapis.com/zenn-user-upload/d8474b4529fd-20241230.png)

完了ボタン押す



Pushノードの設定
![](https://storage.googleapis.com/zenn-user-upload/d5c4a92f83fe-20241230.png)

デプロイしてみる

LINEにメッセージが送れた！プッシュメッセージできた
![](https://storage.googleapis.com/zenn-user-upload/1685ed3f0709-20241230.png)



## チャレンジ課題

送るメッセージを変えて挙動を確認しよう。

- [次の資料へ](./04_api_linebot.md)
- [トップページへ](./readme.md)