# 2.Webサイトからニュースデータを取得してみよう

## このパートでやること

- Webサイトからニュースデータを取得する   
YahooのWebサイトから岩手県の最新ニュースデータを取得してみます。

## このパートで作るもの

- ブロック（ノード）を繋げていき、右側のデバックパネルに岩手県の最新ニュースデータを表示させます。
  - 補足:デバックパネル  
  作った仕組みが正しく動いているかを確認し、問題があるか確認できる場所です。

<img src="https://i.gyazo.com/516f5146219ccfd47dd03963bad17b18.png" width="450px" alt="image from gyazo"/>


## 1.Node-REDの環境について

### 1-1.ノードとは何か

- ノード（Node）とは？
Node-REDを構成する基本的な構成要素で、処理をする機能（プログラム）のかたまりです。
<img src="https://i.gyazo.com/4209abfa226dca0d1a4c1d3421768bbe.png" width="250px" alt="image from gyazo"/>

- ノードは前方のノードからメッセージを受け取るか、外部イベントを受け取ることで動き出します。  
ノードは受け取ったメッセージまたはイベントを処理し、 次のノードにメッセージを送ります。  
処理は左から右に実行され、各ノードで処理された内容がバケツリレーのようにやり取りされていきます。

<img src="https://i.gyazo.com/ac72b467278872701170501f629731ef.png" width="450px" alt="image from gyazo"/>

- メッセージはJSONというデータで構成されます。  
<img src="https://i.gyazo.com/b2e38a11e61da1ad55ff387493b71891.png" width="450px" alt="image from gyazo"/>


### 1-2.画面の構成

前のパートでNode-REDを立ち上げることができました。  
実際の画面を一緒に見てみましょう。

- パレット：ノードが置かれているエリアです。  
インストールしてノードを増やすこともできます。

<img src="https://i.gyazo.com/4e4f325615d23c2a56929fc767ce4327.png" width="450px" alt="image from gyazo"/>

- ワークスペース：パレットからノードを配置してフロー（データの流れ）を作るエリアです。

<img src="https://i.gyazo.com/47f080539655f431df2bc6afbf2eb845.png" width="450px" alt="image from gyazo"/>

- サイドバー：エディター（ブラウザ上で表示しているNode-RED）の中で使える便利なツールがまとめられたエリアです。
  - ノードについてのさらなる情報
  - ヘルプを確認するパネル
  - デバッグメッセージを確認するパネル
  - フローの設定ノードを確認するパネル　などがあります。

<img src="https://i.gyazo.com/2b44b8d4535ed54a2ce46629fec8f96f.png" width="450px" alt="image from gyazo"/>

### 1-3.実際にどんなイメージで作っていくのか見てみましょう
gif動画になっています。

<img src="https://i.gyazo.com/9f29274f6b038b421de3817f321b9dce.gif" width="450px" alt="image from gyazo"/>


## 2.ブロック（ノード）を繋げる

- 現在はこのような画面になっているかと思います。
<img src="https://storage.googleapis.com/zenn-user-upload/3ff23066e145-20241229.png" width="450px" alt="image from gyazo"/>

- パレット内 `共通`の中にある`injectノード`をワークスペースに入れます。  
ノードを長押ししながら移動させるイメージです。

<img src="https://storage.googleapis.com/zenn-user-upload/974fb1f435f7-20241229.png" width="450px" alt="image from gyazo"/>

- パレット内`ネットワーク`の中にある`http requestノード`をワークスペースに入れます。  
先ほどのinjectノードの右側に配置します。 

<img src="https://storage.googleapis.com/zenn-user-upload/46441f5b74ab-20241229.png" width="450px" alt="image from gyazo"/>

- パレット内`機能`の中にある`functionノード`をワークスペースに入れます。  
先ほどのhttp requestノードの右側に配置します。 

<img src="https://storage.googleapis.com/zenn-user-upload/6cb078a62397-20241229.png" width="450px" alt="image from gyazo"/>

- パレット内`共通`の中にある`debugノード`をワークスペースに入れます。  
先ほどのfunctionノードの右側に配置します。 

<img src="https://storage.googleapis.com/zenn-user-upload/a981684dfbba-20241229.png" width="450px" alt="image from gyazo"/>

- 各ノードの間を線で繋げていきます。  
左側のノードの終わり（小さな四角の部分）から、右側のノードの始まり（小さな四角の部分）を長押しして線を引っ張るイメージです。
  - 補足：繋ぐものは「ワイヤー」と言います。

<img src="https://storage.googleapis.com/zenn-user-upload/8f5733678747-20241229.png" width="450px" alt="image from gyazo"/>


## 3.Webサイトのデータを取得する

今回は、Yahooサイトから岩手県の最新ニュースデータを取得してみます。

### 3-1.http requestノードを設定していく

まずは、Yahooニュースの岩手日報のデータを取る準備をします。

- Yahooニュースの岩手日報のURLをコピーします。  
https://news.yahoo.co.jp/media/iwatenpv

<img src="https://storage.googleapis.com/zenn-user-upload/fe7916b1e7b1-20241229.png" width="450px" alt="image from gyazo"/>

- Node-REDの画面に戻り、http requestノードをダブルクリックします。  
プロパティ内の`URL`部分に岩手日報のURLを貼り付けます。  
下記のようになっていたらOKです。

  - 補足：プロパティとは設定のようなものです。

<img src="https://storage.googleapis.com/zenn-user-upload/3e746113176c-20241230.png" width="350px" alt="image from gyazo"/>

- 右上の`完了`ボタンを押します。  
これでhttp requestノードの設定はOKです。

### 3-2.Functionノードを設定していく

Yahooニュースの岩手日報のデータを取る準備ができたので、その中から１番上に表示される最新ニュースだけを抽出していきます。  
補足：Webサイトから必要な情報をプログラムを使って自動的に抽出してくることをスクレイピングと言います。

- Functionノードをダブルクリックすると、プロパティが出てきます。

<img src="https://storage.googleapis.com/zenn-user-upload/289d743b549a-20241229.png" width="350px" alt="image from gyazo"/>

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

<img src="https://storage.googleapis.com/zenn-user-upload/08060f08dd23-20241229.png" width="350px" alt="image from gyazo"/>

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