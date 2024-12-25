# 2.miiboを触ってエージェントを公開しよう

## miiboで会話型AIをつくる
### 1-1.miiboにサインインする
https://mebo.work/

###  1-2.新規エージェントの作成
miiboでは会話型AIの1単位を「エージェント」と呼びます。  
エージェントに対してさまざまな設定や会話コンテンツの登録をすることで会話可能な状態にします。

- 「新規作成して開始する」のボタンをクリックする

<img src="https://i.gyazo.com/5460a41fcd073e57015371f39b9b8ea5.png" width="450px" alt="image from gyazo"/>

- 「新規作成する」のボタンをクリックする

<img src="https://i.gyazo.com/cde3a43294e6010800129b1ac5180709.png" width="450px" alt="image from gyazo"/>

- 名前を入力する

<img src="https://i.gyazo.com/d0c0d56162aad885ef67dcc55b4018bc.png" width="450px" alt="image from gyazo"/>

- 提供者名を入力する

<img src="https://i.gyazo.com/449f036b4101a2068de306020fea9d4a.png" width="450px" alt="image from gyazo"/>

- イメージの設定をする（設定しなくても大丈夫）

<img src="https://i.gyazo.com/1d2bccaf78ecd9bb0c5b8013467901f2.png" width="450px" alt="image from gyazo"/>
<img src="https://i.gyazo.com/d03dd7580268744fbbd3a4bb0c8bae0e.png" width="450px" alt="image from gyazo"/>

- 紹介文の設定をする

<img src="https://i.gyazo.com/06a6019934164764d9b4aa4a56e5e72d.png" width="450px" alt="image from gyazo"/>

- 言語モデルを選択する

<img src="https://i.gyazo.com/c6bd34489ede11f9c516cdc4c76c952e.png" width="450px" alt="image from gyazo"/>
    GPT-4o-miniを選びましょう。

 
利用する言語モデルによって、精度や会話の消費回数が異なります。  
会話の消費回数とは、miiboのプランに割り当てられた、1ヵ月あたりの会話上限クレジットの消費ポイントです。  
会話上限を超えると、その月は会話ができなくなります。  

有料プランでアップグレードできます。  
参考：GPT-4の消費ポイント50、GPT-4o-miniの消費ポイント5  
個人のAPIキーを利用ができるAIは、APIキーを割り当てることで消費回数を一律1回にできます。  

- プロンプトの設定をする
プロンプト（Prompt）とは、AIモデルに対して指示をするためのテキストです。  
AIはこの入力をもとに応答を生成します。  
プロンプトテンプレートから「デフォルトテンプレート」や「お問い合わせ対応AI」などを選びます。

<img src="https://i.gyazo.com/bb96585984785a649fd9e2a7be446f6f.png" width="450px" alt="image from gyazo"/>
<img src="https://i.gyazo.com/daa33b1330986a8c7050fcae73339dab.png" width="450px" alt="image from gyazo"/>

- エージェントの完成
「登録して開始する」をクリックして完了しましょう。

<img src="https://i.gyazo.com/3b79cdda4ccb7e33b0ec37936afbbca0.png" width="450px" alt="image from gyazo"/>
<img src="https://i.gyazo.com/45ba65dfdb8daa267c51f9bc0f99e61a.png" width="450px" alt="image from gyazo"/>

    
### 1-3.会話を試す
「会話をテストする」ボタンをクリックします。  
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

- 左のメニューバーから「公開設定」をクリックする

<img src="https://i.gyazo.com/e5a256aee68ad63dd2822c96d86c5032.png" width="450px" alt="image from gyazo"/>

- 公開の範囲を決めて、「利用規約に同意して公開」ボタンをクリックする
「限定公開」で大丈夫です。

<img src="https://i.gyazo.com/74c4edf33b05081cef5e58c691233f82.png" width="450px" alt="image from gyazo"/>

#### 使ってみよう
完成したエージェントを会場の人と共有し、公開できているか試してみましょう。

<img src="https://i.gyazo.com/a745adb42a26d2e77c498b84731099d7.png" width="450px" alt="image from gyazo"/>