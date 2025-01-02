# 1.Node-REDを立ち上げてみよう

## 1.このパートでやること

- Node-REDについて触れてみる
  - 理論の理解をするのではなく、仕組みを作ってアウトプットすることを大切にしています。  
  　（数学の公式を理解するのではなく、公式を使えることが大事です。）

- GitHub Codespacesを使ってNode-REDを立ち上げる
  - 補足:GitHub Codespacesとは？  
  インターネット上にパソコンを借りて、コーディングができるサービスです。  
  GitHubのアカウントがあれば利用できます。  

- よく分からなくても、**何か作れたらOK**です！

## 2.授業の進み方

- 進行
  - 最初は資料を見ながら講師と共にハンズオンを進めていきます。  
  - 全体の6~7割程度の進捗を確認しながら進めます。

- 早く進んでいる時は
  - 早く進んでいる場合、資料を読み進めてどんどん作業を進めてみましょう。

- 質問があったら
  - 声を出して質問していただいて大丈夫です。
  - わからないときは遠慮なく質問してくださいね。

- 分からない言葉が出てきたら
  - Google検索をしたり、[ChatGPT](https://chatgpt.com/)に聞くなど、自分で解決できないかトライしてみましょう。
  - 補足:ChatGPTとは？  
  質問に答えたり、アイデアを手伝ったりする、AIと会話ができるサービスです。

## 3.基礎知識

- Node-REDとは？
ブラウザ上で動作するビジュアルプログラミングツールです。
プログラムのコードを書く代わりに、ブロック（ノード）を線でつないでシステムやアプリを作成します。

<img src="https://i.gyazo.com/4ab37c349c161a9067a4f9ad30995267.png" width="450px" alt="image from gyazo"/>





### ノーコードツール
言葉通りNO CODEツールです。  
プログラムを書かなくても直感的に操作できるシステムです。  
色々なサービスがすごく速い速度で開発されているので、こまめに情報をキャッチできるといいですね！

【サービス同士を繋げる系】
- [Make](https://www.make.com/en)
- [Zapier](https://zapier.com/)

【Webサイトやアプリを作れる系】
- [STUDIO](https://studio.design/ja)
- [Adalo](https://ja.adalo.com/)

【AI系】
- miibo
- [Dify](https://dify.ai/jp)
- [Coze](https://www.coze.com/)

### 事例
- [店舗従業員業務支援AI](https://protoout.studio/43d4f52ee1c744d3a22c3bf7857bc4b1)

<img src="https://i.gyazo.com/b385192df760f0aa76805f64d195b414.png" width="450px" alt="image from gyazo"/>

- [サービスカウンターが楽しくなるマニュアル検索ChatBotです。](https://protoout.studio/1ea4f6a646df4e30ac8c834e2b1d86a9)

<img src="https://i.gyazo.com/d03dd7580268744fbbd3a4bb0c8bae0e.png" width="450px" alt="image from gyazo"/>

## 3.今回使用するツール（ここも必ず入れる！）

### Node-RED
Node-REDは、フローベース（処理の流れを「線」でつなぐことで動きを表現する方法）のプログラミングツールです。  
直感的に操作ができ、初心者でも利用しやすいのが特徴です。

**Node-REDのメリット**
- プログラミング不要で素早く開発できる
- WindowsやMacなどの環境の差でのトラブルを気にしなくてよい
- Node.jsなど必要なソフトウェアが最初からインストールされている
- 前に作ったプログラムがちゃんとログに残る
- 講師側が学生の状況を把握しやすく、学生もトラブル発生時に講師側に状況を共有しやすい

ローカル（自分のPC）上で動かす場合には、オープンソースとして無料でインストールすることができます。  
DockerやKubernetesといった仮想環境での提供もなされています。  
パブリッククラウド上での提供もされており、こちらは基本有償ですが自分のPCにインストールする手間がありません。  
ユーザー登録後30日間は、クレジットカード情報の入力も必要なく無償試用ができます。

### LINE Bot
LINEは日本でもっとも利用されているメッセージングアプリです。  
直感的な見た目と操作性により、初心者でも利用しやすいのが特徴です。  
LINE Botは、そのLINE上で動作するチャットボット（ロボット）です。  
日頃使っているLINEとはすこし違うものだと思っていてください。



# 4.今日のゴール（ここを明確に！！）ここに向かっていこうね！

- 自分の会話型AIを作成できる
- 作った会話型AIをカスタマイズできる


# 5.ハンズオン：Node-REDを立ち上げてみよう

## 5-1.GitHub CodespacesでNode-REDを実行する方法

https://github.com/kazuhitoyokoi/node-red-codespaces

## 5-2.GitHub Codespacesの始め方

https://zenn.dev/protoout/articles/68-github-codespaces-setup#1.-github-codespaces%E3%81%A3%E3%81%A6%EF%BC%9F

## 5-3.GitHub Codespacesの再開とタイムアウト時間の設定

https://zenn.dev/protoout/articles/77-github-codespaces-restart

- [次の資料へ](./02_agent_publish.md)
- [トップページへ](./readme.md)