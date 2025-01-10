# 4.取得したデータをLINE Botに通知しよう

## このパートでやること

- 前のパートで作ったものを組み合わせていき、ノードの設定の違いによって起こる挙動を確認する。

## このパートで作るもの

- LINE Botに岩手県の最新ニュース1件を通知する仕組みを作ります。

- 応用で、LINE Botに岩手県の最新ニュース3件を通知する仕組みを作ります。

<img src="https://i.gyazo.com/8af5a416925fbfd4f2173d07b002ef59.png" width="450px" alt="image from gyazo"/>


## 1.最新のニュース1件をLINEに通知させる

### 1-1.ノードを繋げる

- [03.Node-REDでLINE Botにメッセージを送ろう](./03_api.md)で作ったノードたちは次の作業がしやすいように、下記のように少し開けて置いておいてください。

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
その中に、実際に扱うデータを入れる場所`payload`というものがあります。  
現在ではhttp requestで取得した岩手のニュースデータが、payloadに入っているイメージです。  

そこで今回新たにchangeノードを使い、ニュースデータから最新のニュース１件だけを抽出します。  
- changeノードとは？  
ノードの間を流れるメッセージ(msg)の特定のプロパティ値を書き換えたり、新規に作成できます。
  
イメージはこちらです。  
左側に岩手のWebサイト、右側にNode-REDのデバックタブを載せています。  
それぞれのニュースのURLや名前などが載っていますね。

<img src="https://i.gyazo.com/d366f6f6c90a5bdd559c0e30db895429.png" width="350px" alt="image from gyazo"/>

今回は１番上のニュースだけを抽出したいので、`代入する値`の右側に`payload[0].url`を入れます。  
※[0] は「配列の1番目の要素を取り出す」書き方になります。  

- 補足：上記の画像でいうと、1番目のニュースが[0]、2番目のニュースが[1]、3番目のニュースが[2]と表します。

<img src="https://i.gyazo.com/d7e93814cba78d11ac6506e9dda179e3.png" width="450px" alt="image from gyazo"/> 



### 1-3.Pushノードを設定していく

- [03.Node-REDでLINE Botにメッセージを送ろう](./03_linebot.md) ）と同じようにLINEノードのプロパティを入れていきます。

- Pushノードのプロパティに必要な情報を入れた画面は下記のようになります。  

プロパティの画面   
- 先ほどLINEの鉛筆マークの画面の中は設定しているので、開くだけでアカウントを選択できます。

<img src="https://i.gyazo.com/9d638034b74858773f8c0acb62d7c888.png" width="450px" alt="image from gyazo"/>

- Access TokenにLINE DevelopersのMessaging APIから`チャネルアクセストークン`を貼り付けてください。
- User IdにLINE Developersのチャネル基本設定から`あなたのユーザーID`を貼り付けてください。

<img src="https://i.gyazo.com/a40c79af5b8e55b1faef0ef7e6124ec0.png" width="450px" alt="image from gyazo"/>


  ### 1-4.LINE Botで岩手県の最新ニュースが1件来ているか通知の確認をする

- 必要な情報を入れることができたか確認できたら`完了`ボタンを選択します。
- `デプロイ`ボタンを押します。
- injectノードの左側にある四角いボタンを１度押します。  
これにより左から右へ処理が実行されていきます。

- LINE Botに、最新ニュースが1件通知が来ていたらOKです！

<img src="https://i.gyazo.com/8af5a416925fbfd4f2173d07b002ef59.png" width="450px" alt="image from gyazo"/>

※YahooのWebサイトも見てみると、最新ニュースがLINE Botに抽出されていることが確認できます！
https://news.yahoo.co.jp/media/iwatenpv


## 2.最新のニュース3件をLINEに通知させる

LINE Botに最新ニュース1件を通知する仕組みは作れましたね。  
次に少しチャレンジとして、最新ニュース3件を同時にLINEに通知する仕組みを作ってみましょう！

実際に作るとこのような仕組みになります。  
先ほどとノードの配置は変わりませんが、ノード内の設定が少し変わってきます。

<img src="https://i.gyazo.com/d19da52370ea3c1c786e40d060dae99e.png" width="450px" alt="image from gyazo"/>

### 2-1.ノードの準備をする

- 先ほど作ったノードをコピペして、「＋」ボタンから新しいフローを追加して作業場所を変えましょう。

<img src="https://i.gyazo.com/fe3432fff021e255c2af1235c4057e77.gif" width="450px" alt="image from gyazo"/>

- ノードを繋げたあとは、Functionノードとchangeノードの設定を変える必要があります。  

  - **自分で作ってみたい方は[ChatGPT](https://chatgpt.com/)に聞きながらトライしてみましょう！**
    - 【ヒント】  
      -  1件の場合と複数件ある場合ではデータの扱い方や最終的にどのような形式で使いたいのかで設定が変わってきます。
      -  Functionノードのコードの変更：最新ニュース1件から3件へ変える必要があり、同時にLINEに表示できるようにします。  
      -  changeノード：代入する値を変える必要があります。

<details>
<summary>詳しい手順はこちら</summary>

### 2-2.Functionノードを変更する

- 最新のニュース1件の場合のNode-REDデバックタブを見てみましょう。   
1番目のニュースの中のurlというところをLINEに表示されていました。

<img src="https://i.gyazo.com/d366f6f6c90a5bdd559c0e30db895429.png" width="350px" alt="image from gyazo"/>

ただ今回の3件という複数件表示することになります。  
この場合、データを全部まとめて表示するのか、複数回に分けて表示するのかなど設定次第で変わってきます。

今回は同時に3件表示するため、下記のようなコードになります。

<details>
<summary>Function内のコード</summary>

```js
// (1) HTMLを文字列化
msg.payload = msg.payload.toString();

// (2) 記事を格納する配列
let articles = [];

// (3) Yahoo!ニュースページで記事を含む区切りを split
let items = msg.payload.split('<li class="sc-1u4589e-0 kKmBYF">');

// (4) 先頭( i=1 )から順に、最大3件をパース
for (let i = 1; i < items.length; i++) {
    // すでに3件取得済みなら終了
    if (articles.length >= 3) {
        break;
    }

    let item = items[i];
    let article = {};

    try {
        // -------------------
        // URL抽出
        // -------------------
        let urlStart = item.indexOf('href="') + 'href="'.length;
        let urlEnd = item.indexOf('"', urlStart);
        if (urlStart > -1 && urlEnd > -1) {
            article.url = item.substring(urlStart, urlEnd).trim();
        }

        // -------------------
        // タイトル抽出
        // -------------------
        let titleStart = item.indexOf('class="sc-3ls169-0 dHAJpi">') + 'class="sc-3ls169-0 dHAJpi">'.length;
        let titleEnd = item.indexOf('</div>', titleStart);
        if (titleStart > -1 && titleEnd > -1) {
            article.title = item.substring(titleStart, titleEnd).trim();
        }

        // -------------------
        // 日付抽出
        // -------------------
        let dateStart = item.indexOf('class="sc-16vsoxb-1 cPSkfe">') + 'class="sc-16vsoxb-1 cPSkfe">'.length;
        if (dateStart > -1) {
            let dateText = item.substring(dateStart);
            let dateMatch = dateText.match(/([0-9]{1,2}\/[0-9]{1,2}\([日月火水木金土]\))\s*<!-- -->\s*<!-- -->\s*([0-9]{1,2}:[0-9]{2})/);
            if (dateMatch) {
                // 例: "12/31(土) 10:02"
                article.date = dateMatch[1] + " " + dateMatch[2];
            }
        }

        // -------------------
        // メディア名の抽出
        // -------------------
        let mediaStart = item.indexOf('class="sc-1t7ra5j-9 dIJJqB">') + 'class="sc-1t7ra5j-9 dIJJqB">'.length;
        let mediaEnd = item.indexOf('</span>', mediaStart);
        if (mediaStart > -1 && mediaEnd > -1) {
            article.media = item.substring(mediaStart, mediaEnd).trim();
        }

        // -------------------
        // 有効なタイトルとURLがある場合のみ追加
        // -------------------
        if (article.title && article.url) {
            articles.push(article);
        }

    } catch (err) {
        node.error("Error while parsing article: " + err.message);
        // スキップ
        continue;
    }
}

// (5) 先頭3件の配列を msg.payload に
msg.payload = articles;
return msg;
```
</details>

こちらで3件のデータを次のchangeノードへと送ることができました。

### 2-3.changeノードを変更する

それぞれのニュースからURLだけを取り出し、同時にLINEへ送る設定をしていきます。  
短い式だけで配列の要素を取り出したり、結合できるJSONata式を使います。

今回はプロパティの代入する値にJSONataを選択し、`$join(payload[ ].url, "\n")`を入れます。

【$join(payload[ ].url, "\n`】

- \n：改行です。
- ニュースのURLを3つこのように表示する　という意味になります。

<img src="https://i.gyazo.com/b19cffe4e6a31ed4e45fb79958a80d7c.png" width="250px" alt="image from gyazo"/>

これで最新のニュース3つを同時に送る準備ができました。

<img src="https://i.gyazo.com/c558c08d0b7c0f9c3af84c21705c9702.png" width="250px" alt="image from gyazo"/>

後の設定は変えず、デプロイしてinjectノードの小さい四角ボタンをクリックします。  
LINEに最新のニュースが同時に３件送られているか見てみましょう！

</details>

LINEに最新のニュースが３件送られてきました。完成です！

<img src="https://i.gyazo.com/4f3ae69be01cd23e961eb2569ef8e7b7.png" width="350px" alt="image from gyazo"/>


## チャレンジ課題

- 時間がある方は、他の都道府県のニュースデータを取得してLINE Botに通知する仕組みを作ってみましょう！  
  - 通知する件数なども変えてトライしてみてください。

- [次の資料へ](./05_conclusion.md)
- [トップページへ](./readme.md)
