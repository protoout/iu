# 2.miiboを触ってエージェントを公開しよう

## このパートでやること

- miiboでエージェントを作成し、公開する  
作成したエージェントを、他の人やサービスが利用できる状態にしていきます。

  - 補足：エージェントとは  
  特定の役割に特化している会話型AIの1つの機能のことです。


## このパートで作るもの

- 公開したエージェントとチャット画面で会話をすることができる

【✅作るもの画像貼っていく（エージェント公開するところ）】
<img src="" width="450px" alt="image from gyazo"/>


## 1.miiboで会話型AIをつくる

### 1-1.miiboにサインインする

miibo：https://mebo.work/


### 1-2.新規エージェントの作成

エージェントに対して、さまざまな設定や会話コンテンツの登録をすることで会話可能な状態にします。 

- `新規作成して開始する`のボタンをクリックする

<img src="https://i.gyazo.com/5460a41fcd073e57015371f39b9b8ea5.png" width="450px" alt="image from gyazo"/>

- `通常モードで新規作成する`のボタンをクリックする

<img src="https://i.gyazo.com/cde3a43294e6010800129b1ac5180709.png" width="450px" alt="image from gyazo"/>

- 名前を入力する  
例：「岩手ワークショップ」 ※文字の色は薄く表示されます。

<img src="https://i.gyazo.com/cd21c4ebada67622b425838b2dbb29c5.png" width="450px" alt="image from gyazo"/>

- 提供者名を入力する  
例：「岩手botくん」

<img src="https://i.gyazo.com/6e08b8112f9e22209a7a5528e2f6443a.png" width="450px" alt="image from gyazo"/>

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

有料プランでアップグレードできます。  
参考：GPT-4の消費ポイント50、GPT-4o-miniの消費ポイント5  
個人のAPIキーを利用ができるAIは、APIキーを割り当てることで消費回数を一律1回にできます。  

- プロンプトの設定をする
プロンプト（Prompt）とは、AIモデルに対して指示をするためのテキストです。  
AIはこの入力をもとに応答を生成します。  
プロンプトテンプレートから`デフォルトテンプレート`や`お問い合わせ対応AI`などを選びます。

<img src="https://i.gyazo.com/bb96585984785a649fd9e2a7be446f6f.png" width="450px" alt="image from gyazo"/>
<img src="https://i.gyazo.com/daa33b1330986a8c7050fcae73339dab.png" width="450px" alt="image from gyazo"/>

- エージェントの完成
`登録して開始する`をクリックして完了しましょう。

<img src="https://i.gyazo.com/3b79cdda4ccb7e33b0ec37936afbbca0.png" width="450px" alt="image from gyazo"/>
<img src="https://i.gyazo.com/45ba65dfdb8daa267c51f9bc0f99e61a.png" width="450px" alt="image from gyazo"/>

    
### 1-3.会話を試す
`会話をテストする`ボタンをクリックします。  
チャット画面が表示されますので、1度だけ何かを送信し、返答が返ってくるのを確かめましょう。

1回送るごとに5回分の会話回数を消費します。  
ここで会話クレジットを消費しすぎないよう注意してください。

<img src="https://i.gyazo.com/10dca318c3d93a8eeef868f3a78e012a.png" width="450px" alt="image from gyazo"/>

###  1-4.エージェントを公開する
エージェントは、プレビュー版と公開版があります。  
公開したエージェントは、他のユーザーに共有し、会話をしてもらえるようになります。

- 一般公開
    - 発行されたURLを共有することで、誰でもチャット画面で会話ができます
    - 外部サービスとの連携やWebサイトへの埋め込みも可能です
- 限定公開
    - チャット画面を他のユーザーに共有できませんが、外部サービス連携は可能です
    - 作成者がログインしている間だけエージェントと会話ができます

- 左のメニューバーから`公開設定`をクリックする

<img src="https://i.gyazo.com/e5a256aee68ad63dd2822c96d86c5032.png" width="450px" alt="image from gyazo"/>

- 公開の範囲を決めて、`利用規約に同意して公開`ボタンをクリックする
`限定公開`で大丈夫です。

<img src="https://i.gyazo.com/74c4edf33b05081cef5e58c691233f82.png" width="450px" alt="image from gyazo"/>

#### 使ってみよう
完成したエージェントを会場の人と共有し、公開できているか試してみましょう。

<img src="https://i.gyazo.com/a745adb42a26d2e77c498b84731099d7.png" width="450px" alt="image from gyazo"/>

- [次の資料へ](./03_line_api.md)
- [トップページへ](./readme.md)
