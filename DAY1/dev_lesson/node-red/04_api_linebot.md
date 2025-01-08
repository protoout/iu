# 4.取得したデータをLINE Botに通知しよう

## このパートでやること

- 前のパートで作ったものを組み合わせていく。

## このパートで作るもの

- LINE Botに岩手県の最新ニュース1件を通知する仕組みを作ります。

<img src="https://i.gyazo.com/34f75775036a4e0b40a7e5d45253ec3f.png" width="450px" alt="image from gyazo"/>


## 1.最新のニュース1件をLINEに通知させる

### 1-1.ノードを繋げる

- [03.Node-REDでLINE Botにメッセージを送ろう](./03_api.md)で作ったノードたちは次の作業がしやすいように、下記のように少し開けて、下においてください。

<img src="https://i.gyazo.com/22f1447e5ce30f08e69712d492674ed6.png" width="450px" alt="image from gyazo"/>

- [02.Webサイトからニュースデータを取得してみよう](./02_api.md)で作ったノードに追加していきます。
- こちらのノードの下付近で、下記の画面のようにノードを繋げてみてください。  
`inject`→`http request`→`function`→`change`→`Push`の順番です。  
自分でノードを繋げられそうな方は、トライしてみましょう。

  - 参考：ノードの場所を探すときに、下記のパレット内のキーワードを見てみてください。
    - 共通：inject・debug
    - ネットワーク：http request
    - 機能：function・change

<img src="https://i.gyazo.com/4ac23238afde63958bdcc15f77c477d6.png" width="450px" alt="image from gyazo"/>

- 次に`debug`ノードを２つ追加して、繋げていきます。  
  - `http requestノード`と`debugノード`を繋ぐ
  - `functionノード`と`debugノード`を繋ぐ

<img src="https://i.gyazo.com/4062fd5750bfd347a152c40106359730.png" width="450px" alt="image from gyazo"/>

### 1-2.changeノードを設定していく

Node-REDでは、各ノード同士がデータを受け渡す際に「メッセージオブジェクト（msg）」という箱のようなものを使います。  
その中に、実際に扱いたいデータを入れる場所として`payload`というものがあります。  
現在ではhttp requestで取得した岩手のニュースデータが、payloadに入っているイメージです。  

そこで今回新たにchangeノードを使って、岩手のニュースデータの全体から最新の１番上のニュースだけを抽出したいと思います。  
- changeノードとは？  
ノードの間を流れるメッセージ(msg)の特定のプロパティ値を書き換えたり、新規に作成できます。
  
イメージはこちらです。  
左側に岩手のWebサイト、右側にNode-REDのデバックタブを載せています。  
上から1番目のニュース、2番目のニュース...と続いていきます。

<img src="https://i.gyazo.com/d366f6f6c90a5bdd559c0e30db895429.png" width="350px" alt="image from gyazo"/>

今回は１番上のニュースだけを抽出したいので、`代入する値`の右側に`payload[0].url`を入れます。  
※[0] は「配列の1番目の要素を取り出す」書き方になります。  

<img src="https://i.gyazo.com/d7e93814cba78d11ac6506e9dda179e3.png" width="450px" alt="image from gyazo"/> 


### 1-3.Pushノードを設定していく

- [03.Node-REDでLINE Botにメッセージを送ろう](./03_linebot.md) ）と同じようにLINEノードのプロパティを入れていきます。

- Pushノードのプロパティに必要な情報を入れることができた画面は下記のようになります。  

プロパティの画面  
先ほどLINEの鉛筆マークの画面の中は設定しているので、開くだけでアカウントを選択できます。

  <img src="https://i.gyazo.com/3dc4b2a6063fae9863af90d6443e8562.png" width="450px" alt="image from gyazo"/>

  ### 1-4.LINE Botで岩手県の最新ニュースが1件来ているか通知の確認をする

- 必要な情報を入れることができたか確認できたら`完了`ボタンを選択します。
- `デプロイ`ボタンを押します。
- injectノードの左側にある四角いボタンを１度押します。  
これにより左から右へ処理が実行されていきます。

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
