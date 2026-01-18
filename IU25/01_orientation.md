# 01.オリエンテーション

### 0-1. 今日作るもの
- 盛岡の情報に詳しいAIを作ってみる
- DifyとLINEを連携してLINE Botを作る

### 0-2. 流れ
- STEP1: Difyを用いて、盛岡の情報に強いAIチャットアプリを作る
- STEP2: 制作したAIチャットアプリをLINEで動かす
  - LINE公式アカウントの事前準備チェック

### 0-3. 準備確認
Googleアカウント、Difyアカウント、LINE公式アカウントの3つのアカウント準備が出来ているところからスタートします。

LINE公式アカウントは `チャンネルシークレット` と `アクセストークン` の取得までが準備です。

**LINE公式アカウントの準備（イベントページ記載）**
- 以下のURLの記事の「4-2. Messaging APIの有効化」まで  
  https://zenn.dev/protoout/articles/16-line-bot-setup
- 準備できてない方はこの後冒頭で話をしていくので、その話を聴きながら作業を進めましょう。

## 1.授業の進み方

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
  AI（データをもとに人のように考えたり学ぶことができ、提案などもしてくれるコンピュータの技術）と会話しながら質問や調べ物を解決できる便利なサービスです。

- このページは固定してリンクは新規タブで開くなど迷子予防を工夫してください。

### 用語チェック

今回学習するツールや技術の用語リストです！
タスクタブをコピペして、ステータスを更新してみてください。
[用語チェックリスト](https://docs.google.com/spreadsheets/d/1IuFcXTJYjVJeuBQK-15VeinFWJonUwvU_vVtmkiNglg/edit?usp=sharing)


## 2.基礎知識

5年くらい前の身近なAIツールは、iPhoneに搭載されたSiriだったように思います。  
2021年にOpenAI社がChatGPTを発表したのを皮切りに、今もなおAIが急速に進化しています。 

### 2-1.生成AI

- 生成AI（Generative AI）とは  
AIの一つで文章、画像、音声、動画などのデータやコンテンツを新しく作り出す技術です。  
【生成AI（ツール）の例】 
  - 動画生成：[Runway](https://runwayml.com/) ・[Sora](https://openai.com/sora/)
  - 画像生成：[Midjourney](https://www.midjourney.com/home)・[DALL-E(GPT-4o)](https://openai.com/index/dall-e/) ・[ImageFX](https://labs.google/fx/tools/image-fx) 
  - 音楽：[Suno](https://suno.com/) 

<img src="https://i.gyazo.com/9fa38557e2abdcd459d0e9b841d7e83d.png" width="450px" alt="image from gyazo"/>

  - 生成AIの中の１つにテキストを生成するのに特化したモデルがあります。  
  **LLM**(Large Language Model、大規模言語モデル)です。  

#### LLMとは  
膨大な量のテキストデータを学習した、高性能なモデルのことです。  

- 補足：モデルとは脳みそのこと。何も学習していない状態は産まれたての赤ちゃんみたいなものです。

<img src="https://i.gyazo.com/854fdc0acc8cc4357265fa8e50d1deaa.png" width="450px" alt="image from gyazo"/>

【LLMの例】
- [GPT（Generative Pre-trained Transformer）](https://chatgpt.com/)  
OpenAIが開発した一連のモデル。
- [Claude](https://claude.ai/login?returnTo=%2F%3F)  
Anthropicが開発した言語モデル。人間のフィードバックを取り入れて安全で信頼性の高い応答を目指しています。
- [Gemini](https://gemini.google.com/app?hl=ja)  
Googleが開発したモデル。Google検索エンジンの情報を基にしているので情報が新しい傾向です。


### 2-2.ノーコードツール

言葉通り「NO CODEツール」です。  
プログラムを書かなくても、直感的に操作できるシステムです。  

#### ノーコードツールの例
【サービス同士を繋げるもの】
- [Make](https://www.make.com/en)
- [Zapier](https://zapier.com/)

【Webサイトやアプリを作れるもの】
- [STUDIO](https://studio.design/ja)
- [Adalo](https://ja.adalo.com/)

【AI系のもの】
- [miibo](https://miibo.ai/)
- [Dify](https://dify.ai/jp)
- [Coze](https://www.coze.com/)


#### ノーコードツールを使った活用事例
ノーコードツールを使って作成したChatBotの例をご紹介します。

- [店舗従業員業務支援AI](https://protoout.studio/43d4f52ee1c744d3a22c3bf7857bc4b1)

<img src="https://i.gyazo.com/b385192df760f0aa76805f64d195b414.png" width="450px" alt="image from gyazo"/>

- [サービスカウンターが楽しくなるマニュアル検索ChatBot](https://protoout.studio/1ea4f6a646df4e30ac8c834e2b1d86a9)

<img src="https://i.gyazo.com/d03dd7580268744fbbd3a4bb0c8bae0e.png" width="450px" alt="image from gyazo"/>


### 2-3.ノーコードツール使った会話型AI

AIだけでは日常で思うように使えません。  
何らかのサービスやアプリになっていた方が使いやすいのです。  

<img src="https://i.gyazo.com/f762cd8bbc5f757ea220db60bbbb7422.png" width="450px" alt="image from gyazo"/>

これまで私たちは、業者に依頼して何万円も支払いHPやアプリなどを作ってもらうことがありました。  
（完成したものを確認すると、なんとなく理想と異なっている仕上がりだということもあります。）  

外注という選択肢もありますが、最近は**自分たちで作れる領域**もかなり広がっています。たとえば**Dify**のようなツールを使うと、AIチャットや業務用のミニアプリを、まずは小さく試作して改善していく流れが作れます。Difyは エージェント的なワークフローやRAG（自社資料を参照して答える仕組み） を、画面上でプロセス設計しながら構築し、アプリとしてデプロイまで進められるオープンソースの開発プラットフォームです。

## 3.今回やること

- DIfyを使ってAIに触れてみる
  - 理論の理解をするのではなく、仕組みを作ってアウトプットすることを大切にしています。  
  （数学の公式を理解するのではなく、公式を使えることが大事です。）

- DifyとLINE Botを連携し、RAG活用型AIを作る
  - より会話の性能を上げるため、カスタマイズもしていきます。
  - よく分からなくても、**何か作れたらOK**です！

## 4.今回使用するツール

授業では主に2つのツールを使っていきます。
- Dify
- LINE Bot

## 5.今回のゴール

- DifyとLINE Botを連携し、自分のRAG活用型AIができる
- 作ったLINE Botをカスタマイズできる
- 日常生活や職場での活用を検討できる  

  - 補足：AIをどのように使えば良いのか迷った場合、**目的（企画）と手段（技術）をセットで考える**と良いです。  
  例えば、「今日の仕事減らして！」ではなく、「今日のこの書類仕事をワンクリックで終わらせて！」というぐらい**具体的な目的**を設定をします。  

初めてAIを触る方も、触ってみたけど活用しきれていないという方でも！  
今日は「自分でも作れて嬉しい！」と感じてもらい、どんなことに応用できるか考えられる体験になると良いなと思っています。

---

このページの内容は以上です。  

- [次の資料へ](./02_dify.md)
- [前の資料へ](./00_preparation.md)

[◀ 目次ページ](./readme.md)
