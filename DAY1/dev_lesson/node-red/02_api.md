# 2.Webサイトからニュースデータを取得してみよう

## このパートでやること

- Webサイトからニュースデータを取得する   
YahooのWebサイトから岩手県の最新ニュースデータを取得してみます。

## このパートで作るもの

- ノードを繋げていき、右側のデバックパネルに岩手県の最新ニュースデータを表示させます。
  - 補足:デバックパネル  
  作った仕組みが正しく動いているかを確認し、問題があるか確認できる場所です。

<img src="https://i.gyazo.com/516f5146219ccfd47dd03963bad17b18.png" width="450px" alt="image from gyazo"/>


## 2.ブロック（ノード）を繋げる

- 現在、「1.Node-REDを立ち上げてみよう」で行ったinjectノードとdebugノードを繋げた画面になっていると思います。

<img src="https://i.gyazo.com/abc62548060782192d4b4312fb5e392c.png" width="450px" alt="image from gyazo"/>

- このパートでは、新しい作業場所を作ります。  
右上の「＋」ボタン（フローを追加）をクリックし、作業するスペースを変えます。

<img src="https://i.gyazo.com/0cf1b8dcdf636bc54cdf74620a83eee1.png" width="450px" alt="image from gyazo"/>


- 新しい作業場所ができたら、パレット内 `共通`の中にある`injectノード`をワークスペースに入れます。  

<img src="https://i.gyazo.com/cc9ddfec339a497fd5ed6691f6d82a76.png" width="450px" alt="image from gyazo"/>

- パレット内`ネットワーク`の中にある`http requestノード`をワークスペースに入れます。  
先ほどのinjectノードの右側に配置します。 

<img src="https://i.gyazo.com/bbf4d2dc2deb62ce0ef1dda3021346b1.png" width="450px" alt="image from gyazo"/>

- パレット内`機能`の中にある`functionノード`をワークスペースに入れます。  
先ほどのhttp requestノードの右側に配置します。 

<img src="https://i.gyazo.com/0c15b0c8efbd7b2f5f459bf13d6f8aa0.png" width="450px" alt="image from gyazo"/>

- パレット内`共通`の中にある`debugノード`をワークスペースに入れます。  
先ほどのfunctionノードの右側に配置します。 

<img src="https://i.gyazo.com/e8ac2f47d88e99c05f7465a918287252.png" width="450px" alt="image from gyazo"/>

- 各ノードの間を線で繋げていきます。  
左側のノードの終わり（小さな四角の部分）から、右側のノードの始まり（小さな四角の部分）を長押しして線を引っ張るイメージです。

<img src="https://i.gyazo.com/915159e20d4565c71891d3daea04238d.png" width="450px" alt="image from gyazo"/>


## 3.Webサイトのデータを取得する

今回は、Yahooサイトから岩手県の最新ニュースデータを取得してみます。

### 3-1.http requestノードを設定していく

まずは、Yahooニュースの岩手日報のデータを取る準備をします。

- Yahooニュースの岩手日報のURLをコピーします。  
https://news.yahoo.co.jp/media/iwatenpv

<img src="https://i.gyazo.com/63f2ed005cf6873b321abcd1dff28c84.png" width="450px" alt="image from gyazo"/>

- Node-REDの画面に戻り、http requestノードをダブルクリックします。  
プロパティ内の`URL`部分に岩手日報のURLを貼り付けます。  
下記のようになっていたらOKです。

  - 補足：プロパティとは設定のようなものです。

<img src="https://i.gyazo.com/4ef6e10c0946c055d826acd76b8555dd.png" width="250px" alt="image from gyazo"/>

- 右上の`完了`ボタンを押します。  
これでhttp requestノードの設定はOKです。

### 3-2.Functionノードを設定していく

Yahooニュースの岩手日報のデータを取る準備ができたので、その中から１番上に表示される最新ニュースだけを抽出していきます。  
補足：Webサイトから必要な情報をプログラムを使って自動的に抽出してくることをスクレイピングと言います。

- Functionノードをダブルクリックすると、プロパティが出てきます。

<img src="https://i.gyazo.com/df6cbf4afa383d1f9754fea2089bf0c1.png" width="350px" alt="image from gyazo"/>

- プロパティ内のコードにあるものを１度全部クリアにし、真っ白な状態にします。

<img src="https://i.gyazo.com/22230be508f31ba18ab5cffe6d78c341.png" width="350px" alt="image from gyazo"/>

- コードの中に下記のコードをコピーして貼り付けていきます。

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

- コードを貼り付けて、このような画面になればOkです。

<img src="https://i.gyazo.com/f9cb6fab69fb5ddc5ea4766c022fd8e8.png" width="350px" alt="image from gyazo"/>

### 3-3.データを取得できているか確認する

岩手の最新ニュースデータが抽出できているか確認していきます。

- サイドバー内にある虫のようなアイコン`デバックパネル`を開いておきます。

- 右上の`デプロイ`を押す  
これにより、作成してきたノードが実際に動かせられる状態になります。

<img src="https://i.gyazo.com/15918eeb56df1237713759b2ae31a558.png" width="450px" alt="image from gyazo"/>

- injectノードの左側にある四角いボタンを１度押します。  
これにより左から右へ処理が実行されていきます。

<img src="https://i.gyazo.com/7eeebde966317282ad8fa5f020faf0be.png" width="250px" alt="image from gyazo"/>

- デバックパネルを確認する  
うまくデータが抽出できると下記のような画面になります。

<img src="https://i.gyazo.com/516f5146219ccfd47dd03963bad17b18.png" width="450px" alt="image from gyazo"/>

※ 抽出したデータは`▶︎`を押していくと開かれていきます。

<img src="https://i.gyazo.com/bd9157702b6999343a1aa12e010fd3a1.png" width="350px" alt="image from gyazo"/>


- [次の資料へ](./03_linebot.md)
- [トップページへ](./readme.md)
