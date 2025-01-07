# 2.Node-REDを立ち上げてみよう

## このパートでやること

- GitHub Codespacesを使ってNode-REDを立ち上げる　　
  - 補足:GitHub Codespacesとは？  
  インターネット上にパソコンを借りて、コーディングができるサービスです。  
  GitHubのアカウントがあれば利用できます。  

## このパートで作るもの

- Node-REDとGitHub Codespacesを下記の画面まで一緒に作っていきます。

Node-REDの画面  
<img src="https://i.gyazo.com/522659c78c07734d1cd4f30ce1b47764.png" width="450px" alt="image from gyazo"/>


## 1.GitHub Codespacesを使う

### 1-1. GitHub Codespacesの始め方

[参考：GitHub Codespacesの始め方](https://zenn.dev/protoout/articles/68-github-codespaces-setup#1.-github-codespaces%E3%81%A3%E3%81%A6%EF%BC%9F)

### 1-2. GitHub CodespacesでNode-REDを実行する方法

[参考：GitHub CodespacesでNode-REDを実行する方法](https://qiita.com/kazuhitoyokoi/items/7a41e7c7aee684815cf0)

**補足**
[参考：GitHub Codespacesの再開とタイムアウト時間の設定](https://zenn.dev/protoout/articles/77-github-codespaces-restart)


## 2.Node-REDの環境について

### 2-1.ノードとは何か

- ノード（Node）とは？
Node-REDを構成する基本的な構成要素で、処理をする機能（プログラム）のかたまりです。
<img src="https://i.gyazo.com/4209abfa226dca0d1a4c1d3421768bbe.png" width="250px" alt="image from gyazo"/>

- ノードは前方のノードからメッセージを受け取るか、外部イベントを受け取ることで動き出します。  
ノードは受け取ったメッセージまたはイベントを処理し、 次のノードにメッセージを送ります。  
処理は左から右に実行され、各ノードで処理された内容がバケツリレーのようにやり取りされていきます。

<img src="https://i.gyazo.com/ac72b467278872701170501f629731ef.png" width="450px" alt="image from gyazo"/>

- メッセージはJSONというデータで構成されます。  
<img src="https://i.gyazo.com/b2e38a11e61da1ad55ff387493b71891.png" width="450px" alt="image from gyazo"/>


### 2-2.画面の構成

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

### 2-3.実際にどんなイメージで作っていくのか見てみましょう
gif動画になっています。

<img src="https://i.gyazo.com/9f29274f6b038b421de3817f321b9dce.gif" width="450px" alt="image from gyazo"/>


## 3.ノードを繋げてみよう

まずはじめに、`inject`というノードでボタンクリックをきっかけにメッセージを送り、送られてきたメッセージをサイドバーのデバッグタブに表示する`debug`というノードを繋げて挙動を見ていきます。


### 3-1.inject ノードと debug ノードをつなげていく

- injectノードをワークスペースにドラックアンドドロップします。  
※ ノードを長押ししながら移動させるイメージです。
<img src="https://i.gyazo.com/69d9424ea7db4779794c1d39e1d0a44f.png" width="450px" alt="image from gyazo"/>

- injectノードの横にdebugノードをドラックアンドドロップします。
<img src="https://i.gyazo.com/4ab5cd15ee540f8b2181cafc29cf9377.png" width="450px" alt="image from gyazo"/>

- injectノードとdebugノードをつなぎます。
  - つなぐものはワイヤーといいます。  
  左側のノードの終わり（小さな四角の部分）から、右側のノードの始まり（小さな四角の部分）を長押しして線を引っ張るイメージです。
<img src="https://i.gyazo.com/b8eb34fb3296018ddae614e01bd47a50.png" width="450px" alt="image from gyazo"/>

- デプロイボタンをクリックするとボタンの色が変わって、今作ったものが反映されます。
<img src="https://i.gyazo.com/58de57346d51b7620c32562f9c8690bf.png" width="450px" alt="image from gyazo"/>

ボタンの色が変わる様子です。  

<img src="https://i.gyazo.com/6d69e6990487e06533edba753d67904e.png" width="450px" alt="image from gyazo"/>

- debugノードのデータはサイドバーのデバッグタブをクリックすると見ることができます。  
右上の4つのマークのうち虫の形をしたものが、デバックタブです。  
<img src="https://i.gyazo.com/6efbc1b0671669a3e5201e23e7298216.png" width="450px" alt="image from gyazo"/>

- debugノードでデータがきてるか確認します。  

  - injectノードの横のボタンを押すとdebugノードにデータが送られます。  
  今回のinjectノードは日付（タイムスタンプ）を送っています。  
  
  デバッグタブでdebugノードが受け付けたデータを確認できます。
<img src="https://i.gyazo.com/f99e3989db06dd84900022d8be76cb75.png" width="450px" alt="image from gyazo"/>


## 3-2.injectノードで送るデータを変更

- injectノードをダブルクリックしてデータを変更しましょう。  
各ノードはダブルクリックすると細かな設定ができます。

<img src="https://i.gyazo.com/05dc870ae85c44d1be74d97b1a474b41.png" width="450px" alt="image from gyazo"/>

- payload（ペイロード）がデータの内容です。  
▼を押して数値に変更しましょう。
<img src="https://i.gyazo.com/6416484adf11e2410f0e5e1042da7f53.png" width="450px" alt="image from gyazo"/>

- `msg.payload=50`に設定して完了をクリックします。
<img src="https://i.gyazo.com/290cce9c52a9736289eb3317a8f18f36.png" width="450px" alt="image from gyazo"/>

- デプロイボタンをクリックすると今作ったものが反映されます。
<img src="https://i.gyazo.com/6d69e6990487e06533edba753d67904e.png" width="450px" alt="image from gyazo"/>

- 動かして、`inject`ノードから送られるデータが`50`の数値になっているか確認します。
<img src="https://i.gyazo.com/5ce3b9ec73285db932270eabfab4ac63.png" width="450px" alt="image from gyazo"/>


基本の動作は、メッセージを変えて表示することです。


### チャレンジ

- 時間がある方は`数値`を`文字列`に変えて`こんにちは`なども表示させてみましょう。


### その他の使い方
  
公式WEBサイトには参考になるドキュメントがたくさんあります。  
今回のフロー以外の方法は以下の公式から学んでください。

[エディタガイド : Node\-RED日本ユーザ会](https://nodered.jp/docs/user-guide/editor/)


- [次の資料へ](./03_api.md)
- [トップページへ](./readme.md)
