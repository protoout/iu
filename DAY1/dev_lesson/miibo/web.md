### 【付録】v0またはClaudeを使ってWebサイトに埋め込んでみる

今回はLINEに組み込みましたが、Webサイトにチャットボットを埋め込むこともできます。  
チャレンジしたい方は見てみてください。

## 作るもの

- Webサイトにmiiboのチャットを入れ込んだもの

<img src="https://i.gyazo.com/c9efc0f324a9a571735f9d20fd2ad29c.gif" width="350px" alt="image from gyazo"/>


### miiboの埋め込み用のタグをコピー

`公開設定`→`一般公開`→埋め込みタグから`埋め込み用のタグ`をコピーします。

<img src="https://i.gyazo.com/263743f5b95fe5c99a2bdd9abdd92327.png" width="350px" alt="image from gyazo"/>

<img src="https://i.gyazo.com/c9efc0f324a9a571735f9d20fd2ad29c.gif" width="350px" alt="image from gyazo"/>


### v0にmiiboのタグを埋め込んだWebサイトを作ってもらう

ChatGPTにコードを書いてもらうのも良いですが、`v0`や`Claude（Claude Artifact）`を使うというのも良いです。  
Webサイトの作成、プレビュー、公開まで一緒にできます。（無料だと利用制限が掛かるので適度に）

#### 今回は`v0`を使います。

- v0にアクセスする  
v0：https://v0.dev/

- 入力画面にプロンプトを以下のように書き、続けてmiiboからコピーしてきた埋め込みタグを貼り付けます。

```
福井の観光情報をまとめるWebサイトを作りたいです。 ホーム画面はシンプルにしてください。

HTML/CSS/JavaScriptで記述し、外部ライブラリなどは基本使わないバニラJSの状態でかいてください。 
以下の埋め込みコードを入れるようにしてください。

 ↓↓↓ここは自分でとってきたmiiboのタグを貼り付ける

 <script> // CSSとアイコンのリンクを追加する関数 function addStylesheet(href) { let link = document.createElement('link'); link.href = href; link.rel = 'stylesheet'; document.head.appendChild(link); } // トグルボタンを作成し、追加する関数 function createToggleButton() { const toggleBtn = document.createElement('div'); toggleBtn.id = 'chatbot-toggle_button'; const anchor = document.createElement('a'); anchor.id = 'chat-button';

＞＞＞＞タグが続きます
```

<img src="https://i.gyazo.com/9e64e3678d32670875c8d0caa6126ed1.png" width="450px" alt="image from gyazo"/>

- サクッと完成しました。  
見た目の変更等があれば、プロンプトに追記しましょう。

<img src="https://i.gyazo.com/5f1e6f2b78fbc11903ff5578b60c4ece.png" width="250px" alt="image from gyazo"/>

- 右上の「共有」を押して「公開」できます。

<img src="https://i.gyazo.com/02b6645a6dd3ab288b782a4456b2f6a0.png" width="450px" alt="image from gyazo"/>

v0のエディターでは、miiboのチャットページを開くとブロックされてしまいます。  
そこで、コードをコピーして公開できるサイトへ移動しましょう。

- コードをコピーする

<img src="https://i.gyazo.com/986f725453363e4c53f9c508a257ec39.png" width="450px" alt="image from gyazo"/>

## CodePenでWebサイトを作る

Webサイトとして表示させるためには、どこかのサーバーにHTML/CSS/JavaScriptを載せる必要があります。  
コピペですぐに試せるCodePenを使ってWebサイトを作って公開してみましょう。

- CodePenにアクセスする  
CodePen：https://codepen.io/

- CodePenのアカウントを作成する

- ログインしたら右上のメニューから`New Pen`を選択する

<img src="https://i.gyazo.com/bcb613e67aed2b9e3702ed42b366bf71.png" width="250px" alt="image from gyazo"/>

- エディター画面が表示されるので、HTMLと書いてある箇所にv0が書いてくれたコードをまるっとコピペします。  
すると下のプレビューエリアにWebサイトが表示されます！

<img src="https://i.gyazo.com/6ceffa2a5eaeed73d544cb06262857fc.png" width="450px" alt="image from gyazo"/>


### 公開

- 左上で`名前`をつけて、右上の`Save`を押して、右下の`Share`からリンクを取得すると、公開できます。

<img src="https://i.gyazo.com/43ac8d5626087ca79fa0cb19d8d9a7de.gif" width="250px" alt="image from gyazo"/>
 
[表示エリアを大きくする方法](https://zenn.dev/protoout/articles/40-codepen-live-preview)

### チャレンジ

時間がある方は、他の方にも共有してみましょう！

- 授業連絡用チャット内に、作ったWebサイトのURLを共有してみてください。  
- 他の方が作成したものも見にいってみましょう！

- 機能がついたサイトも作れます。  
[やるだけえらい](https://codepen.io/ka5ha4/pen/WNqLgqd)


### 補足：HTML/CSS/JavaScriptをまとめてコピペする

- Webサイトを作るときには「HTML/CSS/JavaScript」の3つの要素が重要です。  
CodePenではそれぞれ別々に記載できますが、まとめてHTMLのエディターの箇所に入れています。  
1回試して良い出来になるか分からないのでコピペして微妙だったら、またChatGPTにオーダーをして、またコピペしてと「PDCAサイクル」を早く回せるようにするための工夫だったりもします。

エンジニアっぽい人に見せると「一緒に書かないで」と言ってくる方もいるかもしれませんが、まとめて入れる方がプロトタイピング的には合理的だと思っています。

- [次の資料へ](./06_conclusion.md)
- [トップページへ](./readme.md)