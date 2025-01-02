# 2.Webサイトからニュースデータを取得してみよう

## このパートでやること

- Webサイトからニュースデータを取得する  
今回は、Yahooサイトから岩手県の最新ニュースデータを取得してみます。

## 今回作るもの

<img src="https://storage.googleapis.com/zenn-user-upload/aeeab14c68ff-20241230.png" width="450px" alt="image from gyazo"/>



## ハンズオン：一緒に作っていきましょう！

## スクレイピング　Yahoo　


スクレイピング：Webサイトやデータベース上のデータから特定の情報を抽出・収集する技術や行為
function：関数、与えられた値(引数)を元に何らかの計算や処理を行い、結果を呼び出し元に返すもののこと

Node-RED立ち上げ後
![](https://storage.googleapis.com/zenn-user-upload/3ff23066e145-20241229.png)
![](https://storage.googleapis.com/zenn-user-upload/974fb1f435f7-20241229.png)
![](https://storage.googleapis.com/zenn-user-upload/46441f5b74ab-20241229.png)
![](https://storage.googleapis.com/zenn-user-upload/6cb078a62397-20241229.png)
![](https://storage.googleapis.com/zenn-user-upload/a981684dfbba-20241229.png)
　
 ・線で繋げる
![](https://storage.googleapis.com/zenn-user-upload/8f5733678747-20241229.png)

・Yahooニュースの岩手日報のURLをコピー
![](https://storage.googleapis.com/zenn-user-upload/fe7916b1e7b1-20241229.png)

・ダブルクリックでプロパティにURL入れていく
![](https://storage.googleapis.com/zenn-user-upload/987a6ba15b0a-20241229.png)

メソッド：GET
URL：https://news.yahoo.co.jp/media/iwatenpv
出力形式：変えない

・出力形式も入れておく
![](https://storage.googleapis.com/zenn-user-upload/3e746113176c-20241230.png)

→完了ボタンを押す

・Functionノードをダブルクリック
![](https://storage.googleapis.com/zenn-user-upload/289d743b549a-20241229.png)

・コード入れていく

```js
msg.payload = msg.payload.toString();
let articles = [];

// 記事リストを分割
let items = msg.payload.split('<li class="sc-1u4589e-0 kKmBYF">');

// 各記事の情報を抽出
for(let i=1; i<items.length; i++) {
    let item = items[i];
    let article = {};
    
    try {
        // URLの抽出
        let urlStart = item.indexOf('href="') + 'href="'.length;
        let urlEnd = item.indexOf('"', urlStart);
        if(urlStart > -1 && urlEnd > -1) {
            article.url = item.substring(urlStart, urlEnd).trim();
        }

        // タイトルの抽出
        let titleStart = item.indexOf('class="sc-3ls169-0 dHAJpi">') + 'class="sc-3ls169-0 dHAJpi">'.length;
        let titleEnd = item.indexOf('</div>', titleStart);
        if(titleStart > -1 && titleEnd > -1) {
            article.title = item.substring(titleStart, titleEnd).trim();
        }
        
        // 日付の抽出 - 新しい方法
        let dateStart = item.indexOf('class="sc-16vsoxb-1 cPSkfe">') + 'class="sc-16vsoxb-1 cPSkfe">'.length;
        if(dateStart > -1) {
            let dateText = item.substring(dateStart);
            let dateMatch = dateText.match(/([0-9]{1,2}\/[0-9]{1,2}\([日月火水木金土]\))\s*<!-- -->\s*<!-- -->\s*([0-9]{1,2}:[0-9]{2})/);
            if(dateMatch) {
                article.date = dateMatch[1] + " " + dateMatch[2];
            }
        }
        
        // メディア名の抽出
        let mediaStart = item.indexOf('class="sc-1t7ra5j-9 dIJJqB">') + 'class="sc-1t7ra5j-9 dIJJqB">'.length;
        let mediaEnd = item.indexOf('</span>', mediaStart);
        if(mediaStart > -1 && mediaEnd > -1) {
            article.media = item.substring(mediaStart, mediaEnd).trim();
        }
        
        // 記事が有効な情報を持っている場合のみ追加
        if(article.title && article.url) {
            articles.push(article);
        }
    } catch(e) {
        // エラーが発生した場合はその記事をスキップ
        node.error("Error processing article: " + e.message);
        continue;
    }
}

msg.payload = articles;
return msg;
```

・コピペして入れたところ
![](https://storage.googleapis.com/zenn-user-upload/08060f08dd23-20241229.png)

・デプロイしてInjectノードの横の小さな四角のボタン押す
・デバックを見る
![](https://storage.googleapis.com/zenn-user-upload/aeeab14c68ff-20241230.png)








## チャレンジ課題

- [次の資料へ](./03_linebot.md)
- [トップページへ](./readme.md)