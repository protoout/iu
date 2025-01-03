# 4.取得したデータをLINE Botに通知しよう

## このパートでやること

- 前のパートで作ったLINE Botにメッセージを送る仕組みと組み合わせる

## 今回作るもの

- LINE Botに岩手県の最新ニュース1件を通知する仕組みを作ります。

<img src="https://i.gyazo.com/34f75775036a4e0b40a7e5d45253ec3f.png" width="450px" alt="image from gyazo"/>

## ハンズオン：一緒に作っていきましょう！

## 1.最新のニュース1件をLINEに通知させる

### 1-1.ノードを繋げる

[02.Webサイトからニュースデータを取得してみよう](./02_api.md)で作ったノードに追加していきます。

- 02.で繋げたノードを見てください。  
現在はこのような画面になっていると思います。

<img src="https://i.gyazo.com/47a78c1833c907317452702e576508fe.png" width="450px" alt="image from gyazo"/>

- ここから下記の画面のようにノードを繋げてみてください。  
「inject」→「http request」→「function」→「change」→「Push」の順番です。  
自分でノードを繋げられそうな方は、トライしてみましょう。

  - 参考：ノードの場所を探すときに、下記のパレット内のキーワードを見てみてください。
    - 共通：inject・debug
    - ネットワーク：http request
    - 機能：function・change

<img src="https://i.gyazo.com/4ac23238afde63958bdcc15f77c477d6.png" width="450px" alt="image from gyazo"/>

- 次に「debug」ノードを２つ追加して、繋げていきます。  
  - 「http requestノード」と「debugノード」を繋ぐ
  - 「functionノード」と「debugノード」を繋ぐ

<img src="https://i.gyazo.com/4062fd5750bfd347a152c40106359730.png" width="450px" alt="image from gyazo"/>

### 1-2.changeノードを設定していく

- 「代入する値」の右側に「payload[0].url」を入れます。

<img src="https://storage.googleapis.com/zenn-user-upload/93911cafabfd-20241230.png" width="450px" alt="image from gyazo"/>

### 1-3.Pushノードを設定していく

- [03.Node-REDでLINE Botにメッセージを送ろう](./03_linebot.md) ）と同じようにLINEノードのプロパティを入れていきます。

- Pushノードのプロパティに必要な情報を入れることができた画面は下記のようになります。  
  - 鉛筆マーク画面

<img src="https://i.gyazo.com/1b4ea98a979088fc91279347b0241793.png" width="450px" alt="image from gyazo"/>

  - プロパティ最初の画面

  <img src="https://i.gyazo.com/3a6824536c4f04f23a715c8cc869b809.png" width="450px" alt="image from gyazo"/>

  ### 1-4.LINE Botで岩手県の最新ニュースが1件来ているか通知の確認をする

- 必要な情報を入れることができたか確認できたら「完了」ボタンを選択します。
- 「デプロイ」ボタンを押します。

- LINE Botに、岩手県の最新ニュースが1件通知が来ていたらOKです！

<img src="https://i.gyazo.com/34f75775036a4e0b40a7e5d45253ec3f.png" width="450px" alt="image from gyazo"/>

※YahooのWebサイトも見てみると、最新ニュースがLINE Botに抽出されていることが確認できます！
https://news.yahoo.co.jp/media/iwatenpv


- いかがでしたか？  
LINE Botに岩手県の最新ニュース1件を通知する仕組みは作れたでしょうか？


## チャレンジ課題

- 最新のニュース5件通知する仕組みを作る
- 他のWebサイトからスクレイピングしてLINE Botに通知する仕組みを作る

- [次の資料へ](./05_conclusion.md)
- [トップページへ](./readme.md)