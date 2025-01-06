# 2.miiboを触ってエージェントを公開しよう

## このパートでやること

- miiboでエージェントを作成し、公開する  
作成したエージェントを、他の人やサービスが利用できる状態にしていきます。

  - 補足：エージェントとは  
  特定の役割に特化している会話型AIの1つの機能のことです。


## このパートで作るもの

- 公開したエージェントとチャット画面で会話をすることができる

<img src="https://i.gyazo.com/ee451187efa4e0d0116b11229ea570aa.png" width="450px" alt="image from gyazo"/>

（注：今回は、福井県の研修で使用した資料を利用しています。）

## 1.miiboで会話型AIをつくる

### 1-1.miiboにサインインする

miibo：https://mebo.work/


### 1-2.新規エージェントの作成

エージェントに対して、さまざまな設定や会話コンテンツの登録をすることで会話可能な状態にします。 

- `新規作成して開始する`のボタンをクリックする

<img src="https://i.gyazo.com/5460a41fcd073e57015371f39b9b8ea5.png" width="250px" alt="image from gyazo"/>

- `通常モードで新規作成する`のボタンをクリックする

<img src="https://i.gyazo.com/cde3a43294e6010800129b1ac5180709.png" width="450px" alt="image from gyazo"/>

- 名前を入力する  

<img src="https://i.gyazo.com/d0c0d56162aad885ef67dcc55b4018bc.png" width="450px" alt="image from gyazo"/>

- 提供者名を入力する  

<img src="https://i.gyazo.com/449f036b4101a2068de306020fea9d4a.png" width="450px" alt="image from gyazo"/>

- イメージの設定をする（設定しなくても大丈夫です。）

<img src="https://i.gyazo.com/1d2bccaf78ecd9bb0c5b8013467901f2.png" width="450px" alt="image from gyazo"/>

- 紹介文の設定をする  
例：「ワークショップ用です。」

<img src="https://i.gyazo.com/ec0f17b22ca288ad651773b155b3653b.png" width="450px" alt="image from gyazo"/>

- 言語モデルを選択する  
**GPT-4o-mini**を選びましょう。
<img src="https://i.gyazo.com/1bb1015e3d282d31a1e8ad4bec660b78.png" width="450px" alt="image from gyazo"/>

> - 利用する言語モデルによって、精度や会話の消費回数が異なります。  
会話の消費回数：miiboのプランに割り当てられた、1ヵ月あたりの会話上限クレジットの消費ポイントのことです。  
    会話上限を超えると、その月は会話ができなくなります。  

> - 有料プランでアップグレードできます。  
参考：GPT-4」の消費ポイント→50、「GPT-4o-mini」の消費ポイント→5  
個人のAPIキーを利用ができるAIは、APIキーを割り当てることで消費回数を一律1回にできます。  

### 1-3.プロンプトの設定する

プロンプト（Prompt）とは、AIモデルに対して指示をするためのテキストです。  
AIはこの入力をもとに応答を生成しています。  

- `プロンプトテンプレートから選ぶ`をクリックします。

<img src="https://i.gyazo.com/4a594bfb9ca427ae5b134255ad632646.png" width="450px" alt="image from gyazo"/>

- `デフォルトテンプレート`や`お問い合わせ対応AI`などを選びます。

<img src="https://i.gyazo.com/52aa16fea892396fb7a1c1feb97b51d3.png" width="450px" alt="image from gyazo"/>

- エージェントの完成  
`登録して開始する`をクリックしましょう。

<img src="https://i.gyazo.com/3b79cdda4ccb7e33b0ec37936afbbca0.png" width="450px" alt="image from gyazo"/>


### 1-4.会話を試す

- Botの設定・管理ページが開かれました。

<img src="https://i.gyazo.com/ac29834a593ddaa781998ad63eaafc8c.png" width="450px" alt="image from gyazo"/>

- 作成したbotで会話を試してみましょう。  
`会話をテストする`ボタンをクリックします。  
チャット画面が表示されますので、1度だけ何かメッセージを送信し、返答が返ってくるのを確かめましょう。

**1回送るごとに5回分の会話回数を消費してしまうので、 ここで会話クレジットを使いすぎないよう注意してください。**

<img src="https://i.gyazo.com/ee451187efa4e0d0116b11229ea570aa.png" width="450px" alt="image from gyazo"/>


###  1-5.エージェントを公開する

- エージェントは、プレビュー版と公開版があります。  
公開したエージェントは、他のユーザーに共有し、会話をしてもらえるようになります。

  - 一般公開
    - 発行されたURLを共有することで、誰でもチャット画面で会話ができます
    - 外部サービスとの連携やWebサイトへの埋め込みも可能です
  - 限定公開
    - チャット画面を他のユーザーに共有はできませんが、外部サービス連携は可能です
    - 作成者がログインしている間だけ、エージェントと会話ができます

- 左のメニューバーから`公開設定`をクリックします。

<img src="https://i.gyazo.com/e5a256aee68ad63dd2822c96d86c5032.png" width="250px" alt="image from gyazo"/>

- 公開の範囲を決めて、`利用規約に同意して公開`ボタンをクリックします。  
`限定公開`で大丈夫です。

<img src="https://i.gyazo.com/30a4540fc37e680f8c9ee3b910b6078c.png" width="450px" alt="image from gyazo"/>

- `公開する`ボタンをクリックします。

<img src="https://i.gyazo.com/0d17d938a8ed2add83539eb8f8e720fb.png" width="450px" alt="image from gyazo"/>


## 2.完成したエージェントを使ってみよう

**【✅検討事項・確認してから】**
完成したエージェントを他の方と共有し、公開できているか試してみましょう。

<img src="https://i.gyazo.com/a745adb42a26d2e77c498b84731099d7.png" width="450px" alt="image from gyazo"/>

- [次の資料へ](./03_line_api.md)
- [トップページへ](./readme.md)
