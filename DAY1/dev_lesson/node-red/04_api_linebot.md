# 4.取得したデータをLINE Botに通知しよう

## このパートでやること

- 前のパートで作ったLINE Botにメッセージを送る仕組みと組み合わせる

## 今回作るもの

- LINE Botに岩手県の最新ニュース1件を通知する仕組みを作ります。

<img src="https://i.gyazo.com/34f75775036a4e0b40a7e5d45253ec3f.png" width="450px" alt="image from gyazo"/>

## ハンズオン：一緒に作っていきましょう！

## 1.最新のニュース1件をLINEに通知させる

### 1-1.ノードを繋げる

- 新しくノードを繋げていきます。  
「inject」→「http request」→「function」→「change」→「Push」の順番です。  
自分でノードを繋げられそうな方は、トライしてみましょう。

  - 補足：ノードの場所を探す時には、下記のパレット内のキーワードを参考にしてみてください。
    - inject：共通
    - http request：ネットワーク
    - function：機能
    - change：機能
    - Push：LINE

<img src="https://storage.googleapis.com/zenn-user-upload/6ec8f08e2590-20241230.png" width="450px" alt="image from gyazo"/>







<img src="" width="450px" alt="image from gyazo"/>
<img src="" width="450px" alt="image from gyazo"/>
<img src="" width="450px" alt="image from gyazo"/>
<img src="" width="450px" alt="image from gyazo"/>
<img src="" width="450px" alt="image from gyazo"/>
<img src="" width="450px" alt="image from gyazo"/>
<img src="" width="450px" alt="image from gyazo"/>






・デバックノード追加した（http requestとfunctionのところ）
![](https://storage.googleapis.com/zenn-user-upload/28af669c29b8-20241230.png)

・http requestのノードのプロパティに入れていく
メソッド：GET
URL：https://news.yahoo.co.jp/media/iwatenpv
![](https://storage.googleapis.com/zenn-user-upload/7bb8a11548ac-20241230.png)

・Functionノードに入れていく

```js
msg.payload = msg.payload.toString();
let articles = [];

// 記事リストを分割
let items = msg.payload.split('<li class="sc-1u4589e-0 kKmBYF">');

// 各記事の情報を抽出
for (let i = 1; i < items.length; i++) {
    let item = items[i];
    let article = {};

    try {
        // URLの抽出
        let urlStart = item.indexOf('href="') + 'href="'.length;
        let urlEnd = item.indexOf('"', urlStart);
        if (urlStart > -1 && urlEnd > -1) {
            article.url = item.substring(urlStart, urlEnd).trim();
        }

        // タイトルの抽出
        let titleStart = item.indexOf('class="sc-3ls169-0 dHAJpi">') + 'class="sc-3ls169-0 dHAJpi">'.length;
        let titleEnd = item.indexOf('</div>', titleStart);
        if (titleStart > -1 && titleEnd > -1) {
            article.title = item.substring(titleStart, titleEnd).trim();
        }

        // 日付の抽出 - 新しい方法
        let dateStart = item.indexOf('class="sc-16vsoxb-1 cPSkfe">') + 'class="sc-16vsoxb-1 cPSkfe">'.length;
        if (dateStart > -1) {
            let dateText = item.substring(dateStart);
            let dateMatch = dateText.match(/([0-9]{1,2}\/[0-9]{1,2}\([日月火水木金土]\))\s*<!-- -->\s*<!-- -->\s*([0-9]{1,2}:[0-9]{2})/);
            if (dateMatch) {
                article.date = dateMatch[1] + " " + dateMatch[2];
            }
        }

        // メディア名の抽出
        let mediaStart = item.indexOf('class="sc-1t7ra5j-9 dIJJqB">') + 'class="sc-1t7ra5j-9 dIJJqB">'.length;
        let mediaEnd = item.indexOf('</span>', mediaStart);
        if (mediaStart > -1 && mediaEnd > -1) {
            article.media = item.substring(mediaStart, mediaEnd).trim();
        }

        // 記事が有効な情報を持っている場合のみ追加
        if (article.title && article.url) {
            articles.push(article);
        }
    } catch (e) {
        // エラーが発生した場合はその記事をスキップ
        node.error("Error processing article: " + e.message);
        continue;
    }
}

msg.payload = articles;
return msg;
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