# 4.取得したデータをLINE Botに通知しよう

## このパートでやること

- 前のパートで作ったLINE Botにメッセージを送る仕組みと組み合わせる

## 今回作るもの

- LINE Botに岩手県の最新ニュース1件を通知する仕組みを作ります。

<img src="https://i.gyazo.com/34f75775036a4e0b40a7e5d45253ec3f.png" width="450px" alt="image from gyazo"/>

## ハンズオン：一緒に作っていきましょう！

## 1.最新のニュース1件をLINEに通知させる

### 1-1.ノードを繋げる

「02. Webサイトからニュースデータを取得してみよう」で作ったノードに追加していきます。

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

### 1-2.http requestのノードのプロパティを入れていく






<img src="" width="450px" alt="image from gyazo"/>
<img src="" width="450px" alt="image from gyazo"/>
<img src="" width="450px" alt="image from gyazo"/>
<img src="" width="450px" alt="image from gyazo"/>
<img src="" width="450px" alt="image from gyazo"/>





・
メソッド：GET
URL：https://news.yahoo.co.jp/media/iwatenpv
![](https://storage.googleapis.com/zenn-user-upload/7bb8a11548ac-20241230.png)

・Functionノードに入れていく

```js

```
![](https://storage.googleapis.com/zenn-user-upload/90d1367c7198-20241230.png)

・changeノードに入れていく
payload[0].url
![](https://storage.googleapis.com/zenn-user-upload/93911cafabfd-20241230.png)

・Pushノードに入れていく
→さっきとLINEの設定一緒
![](https://storage.googleapis.com/zenn-user-upload/62ebb20ec383-20241230.png)

・最新のニュース表示できた（パソコンの画面）
![](https://storage.googleapis.com/zenn-user-upload/edf6c9d05daa-20241230.png)
→スマホだと画像もついていい感じ
![](https://storage.googleapis.com/zenn-user-upload/309323a8f29a-20241230.jpg)

YahooのWEBサイトも見る。このページが１番上に来ていたことを確認。OK
![](https://storage.googleapis.com/zenn-user-upload/7ef951eb03f1-20241230.png)








## チャレンジ課題

最新のニュース5件通知する仕組みを作る



- [次の資料へ](./05_conclusion.md)
- [トップページへ](./readme.md)