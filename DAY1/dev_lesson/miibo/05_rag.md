# 2.Webサイトからニュースデータを取得してみよう

## このパートでやること

- Webサイトからニュースデータを取得する   
YahooのWebサイトから岩手県の最新ニュースデータを取得してみます。

## 今回作るもの

- ブロック（ノード）を繋げていき、右側のデバックパネルに岩手県の最新ニュースデータを表示させます。
  - 補足:デバックパネル  
  作った仕組みが正しく動いているかを確認し、問題があるか確認できる場所です。

<img src="https://i.gyazo.com/516f5146219ccfd47dd03963bad17b18.png" width="450px" alt="image from gyazo"/>


## 1.Node-REDの環境について

### 1-1.ノードとは何か


ーーーーーーーーーーーーーー









# 5.miiboのナレッジデータを設定しよう

# 会話型AIの精度をあげる
このままでもそれなりに情報は返してくれますが、自分の業務に即した情報や特定の領域の情報には弱いままです。  
会話型AIにオリジナリティを追加し、自分にとって使えるものにしていきましょう。

次は、自分の職場や施設などの情報を答えてくれるQ＆Aチャットボットへ仕上げていきます。

## 1.Retrieval-augmented Generation(RAG)を構築し、AIの嘘を防ぐ
RAGは、LLM（大規模言語モデル）が持つ知識を補うため、検索によって取得した外部の知識をモデルに与えることで、回答の質を向上させる手法です。

今回はナレッジデータストアの利用をします。

手法一覧
- ナレッジデータストアの利用
- データソース（Web検索）の利用
- データコネクターの利用
- 外部API・DB連携
- 検索クエリー生成プロンプト

参考：[位置情報と連動した会話AIを作る！miibo✖️Google Places APIの繋ぎ方](https://note.com/miibo_takumori/n/n36d9bc45325b?magazine_key=ma82aceda74a8)

### ハルシネーション
もっともらしい嘘の情報を返してくる、「本来存在しない情報をAIが勝手に生成してしまう現象」のことをハルシネーションといいます。

例
あなた：「福井県で今日実施されているイベントを教えて。」
AI：「今日は以下の5件のイベントが開催されています。」
あなた：（ホームページを見に行ったらこのイベントは来週からだな…？違うなぁ。）

miiboではハルシネーションが起きにくいように調整されているようですが、起きないわけではありません。


## 2.ナレッジデータストアの利用
ナレッジデータストアは、miiboがサービス内で所有する、AIに与える専門知識を保持するためのデータベースです。

- 左のメニューバーから「会話の設定」をクリックする

<img src="https://i.gyazo.com/576052a39e39aef74bf5864318facfdf.png" width="450px" alt="image from gyazo"/>

- 「ナレッジデータストア」をクリックする

<img src="https://i.gyazo.com/be255307b99881e2cd7b0b8b6cb00aca.png" width="450px" alt="image from gyazo"/>

- 「ナレッジデータストアを作成する」ボタンをクリックする

<img src="https://i.gyazo.com/cb29f77acc81d0213451c5060108c2d4.png" width="450px" alt="image from gyazo"/>

- 右下に表示された「データを追加する」ボタンをクリックする

<img src="https://i.gyazo.com/38f3a6778780a4c226a8c09df9748937.png" width="450px" alt="image from gyazo"/>

- 「URLを指定してデータを追加する」をクリックする

<img src="https://i.gyazo.com/6c379185559a18ac0fb42a49fb021713.png" width="450px" alt="image from gyazo"/>

- データの入稿をする
    福井商工会議所のHPをお借りします。  
    複数ページある場合は、URLを1つずつ入れましょう。   
    `https://www.fcci.or.jp/`  
    入力したら「登録をリクエストをする」をクリックします。

    ナレッジ登録可能数に限りがあります。  
    HPの1階層（1ページ目）の文字のみを拾っています。  
    リンクされた先の情報は入っていないことがあるので注意してください。

<img src="https://i.gyazo.com/57186dec0e7e6d1cf42a8d23f2991061.png" width="450px" alt="image from gyazo"/>

   「登録のリクエストに失敗しました。」などとエラーが出ることがあります。  
    数分置いてリロード（ページの再読み込み）してみましょう。  
    成功していることがあります。

## 3.会話の様子

<img src="https://i.gyazo.com/7d86f01c0c57e9920611820a42b5a9c3.png" width="450px" alt="image from gyazo"/>

HPの情報のみを答えるようにプロンプトを調整すると、より自分の職場のための会話型AIになるでしょう。  
夜間の緊急対応リストなどを読みこませれば、夜間バイトさんが困ったときの手助けになることもあるかもしれません。  
あくまでもサポートという視点は忘れずに活用してくださいね。

### 取り込めるデータ
社内リソース、エクセルファイル、Notionの内部ページなど、miiboは扱えるデータが多く搭載されています。  
必要に応じて読みこんでください。

<img src="https://i.gyazo.com/2e15069a236dd7193bf98e701a30c773.png" width="450px" alt="image from gyazo"/>

#### 余談：APIという手もある

RAGでは事前に登録した情報しか扱えません。  
リアルタイム性が高い情報や更新性が高い情報を扱うためにはそういったデータを提供している外部サービス（API）と連携する必要があります。  
「Webhookを利用して外部サービスと連携する」というものもあります。
[お天気API](https://weather.tsukumijima.net/)が手始めにはいいかもしれません。  
JSONという書き方が少し難しいですが、チャレンジすると応用の幅が広がると思います！

# 【チャレンジ】オリジナル会話型AIを作ってみよう

プロンプトを書き換えてみたり、自分の職場のHPを読みこんでみたり、オリジナリティを出してみましょう。

【アイデア】
- 自分の職場や施設のHPを読みこんだQ＆Aチャットボット
- 経営に関するアドバイスやガイドラインを提供し、資金調達やビジネスプラン作成のサポートをするチャットボット
- 商工会議所が提供する最新のビジネス関連ニュースをリアルタイムで提供するチャットボット
- セミナーやイベントの予約をサポートするチャットボット

### 【付録】v0またはClaudeを使ってWebサイトに埋め込んでみる
今回はLINEに組み込みましたが、Webサイトにチャットボットを埋め込むこともできます。

チャレンジしたい人は見てみよう

## 作るもの 

Webサイトにmiiboのチャットを入れ込んだ連携
<img src="https://i.gyazo.com/c9efc0f324a9a571735f9d20fd2ad29c.gif" width="450px" alt="image from gyazo"/>

### miiboの埋め込み用のタグをコピー

`公開設定` → `一般公開` →  `埋め込みタグ` から埋め込み用の"タグ"をコピーします。
<img src="https://i.gyazo.com/263743f5b95fe5c99a2bdd9abdd92327.png" width="450px" alt="image from gyazo"/>
<img src="https://i.gyazo.com/c9efc0f324a9a571735f9d20fd2ad29c.gif" width="450px" alt="image from gyazo"/>

### v0にmiiboのタグを埋め込んだWebサイトを作ってもらう

ChatGPTにコードを書いてもらうのもいいですが、`v0`や`Claude（Claude Artifact）`を使うというのも良いです。  
Webサイトの作成、プレビュー、公開まで一緒にできます。（無料だと利用制限が掛かるので適度に）

今回は`v0`を使います。

- v0にアクセスする
https://v0.dev/

- 入力画面にプロンプトを以下のように書き、下にmiiboのコビーしてきたタグを貼り付ける
`ありがとう`って言っておくの大事です。

    ```
    福井の観光情報をまとめるWebサイトを作りたいです。 ホーム画面はシンプルにしてください。

    HTML/CSS/JavaScriptで記述し、外部ライブラリなどは基本使わないバニラJSの状態でかいてください。 
    以下の埋め込みコードを入れるようにしてください。

    ↓↓↓ここは自分でとってきたmiiboのタグを貼り付ける

    <script> // CSSとアイコンのリンクを追加する関数 function addStylesheet(href) { let link = document.createElement('link'); link.href = href; link.rel = 'stylesheet'; document.head.appendChild(link); } // トグルボタンを作成し、追加する関数 function createToggleButton() { const toggleBtn = document.createElement('div'); toggleBtn.id = 'chatbot-toggle_button'; const anchor = document.createElement('a'); anchor.id = 'chat-button';

    ＞＞＞＞タグが続きます

    ```

<img src="https://i.gyazo.com/9e64e3678d32670875c8d0caa6126ed1.png" width="450px" alt="image from gyazo"/>

- サクッと完成  
見た目の変更等があれば、プロンプトに追記しましょう。

<img src="https://i.gyazo.com/5f1e6f2b78fbc11903ff5578b60c4ece.png" width="450px" alt="image from gyazo"/>

- 右上の「共有」を押して「公開」できます。

<img src="https://i.gyazo.com/02b6645a6dd3ab288b782a4456b2f6a0.png" width="450px" alt="image from gyazo"/>

v0のエディターでは、miiboのチャットページを開くとブロックされてしまいます。  
そこで、コードをコピーして公開できるサイトへ移動しましょう。

- コードをコピーする

<img src="https://i.gyazo.com/986f725453363e4c53f9c508a257ec39.png" width="450px" alt="image from gyazo"/>

## CodePenでWebサイトを作る

Webサイトとして表示させるためにはどこかのサーバーにHTML/CSS/JavaScriptを載せる必要があります。  
コピペですぐに試せるCodePenを使ってWebサイトを作って公開してみましょう。

- CodePenにアクセスする  
https://codepen.io/

- CodePenのアカウントを作成する

- ログインしたら右上のメニューから`New Pen`を選択する

<img src="https://i.gyazo.com/bcb613e67aed2b9e3702ed42b366bf71.png" width="450px" alt="image from gyazo"/>

- エディター画面が表示されるので、HTMLと書いてある箇所にv0が書いてくれたコードをまるっとコピペします。

<img src="https://i.gyazo.com/6ceffa2a5eaeed73d544cb06262857fc.png" width="450px" alt="image from gyazo"/>

そうすると下のプレビューエリアにWebサイトが表示されます。 簡単！

## 公開

左上で`名前をつけて`、右上の`Save`を押して、右下の`Share`からリンクを取得で公開できます。

<img src="https://i.gyazo.com/43ac8d5626087ca79fa0cb19d8d9a7de.gif" width="450px" alt="image from gyazo"/>
 
ちなみに表示エリアを大きくするやり方。

https://zenn.dev/protoout/articles/40-codepen-live-preview

### 作れたらURLをオープンチャットに投稿してみましょう。

機能がついたサイトも作れます。　https://codepen.io/ka5ha4/pen/WNqLgqd


### Tips: HTML/CSS/JavaScriptをまとめてコピペ

Webサイトを作るときにはこの3つの要素が重要です。

CodePenではそれぞれ別々に記載できますが、まとめてHTMLのエディターの箇所に入れちゃってます。  
1回試して良い出来になるか分からないので、コピペして微妙だったらまたChatGPTにオーダーをしてまたコピペしてとPDCAサイクルを早く回せるようにするための工夫だったりします。

エンジニアっぽい人に見せると一緒に書くなって言ってくる人もいるかもですがこっちの方がプロトタイピング的には合理的だと思っています。


# まとめ
なんだか分からないうちにできてしまった！という感じでしょうか？簡単でしたね。  
デジタルの力を導入することで「楽になったり、便利になったり」するのが目的で、使いにくかったり仕事が増えたりしては意味がありません。  
「あったらいいはず」というアイデアから、「誰が」「どのタイミングで」使えるものなのか、も考えていけるといいですね。

- [次の資料へ](./06_chatgpt.md)
- [トップページへ](./readme.md)