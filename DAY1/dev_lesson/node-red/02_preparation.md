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

## 2.ブロックを繋げていく





✅ここから修正！

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





- [次の資料へ](./03_api.md)
- [トップページへ](./readme.md)
