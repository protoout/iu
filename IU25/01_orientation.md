# オリエンテーション

このパートでは、授業の進め方を確認し、授業で扱う基礎用語（生成AI / LLM / ノーコード）を最低限おさえます。  
この後のハンズオン（Dify → RAG → LINE Bot）を迷子にならずに進めるための準備です。

<details>
  <summary>準備確認（アカウント）</summary>

この授業は、以下の3つのアカウント準備ができているところからスタートします。

- Googleアカウント
- Difyアカウント
- LINE公式アカウント
  - LINE公式アカウントは、STEP3-5のLINE公式アカウントと友達になるところまでが準備です。
  - 準備できてない方は、この後の冒頭説明を聞きながら作業を進めてください!
</details>

## 1. 授業の進み方（ハンズオンの進行）

- 進行
  - 最初は資料を見ながら、講師と一緒にハンズオンを進めます
  - 全体の6〜7割程度の進捗を確認しながら進めます

- 早く進んでいる時は
  - 資料を読み進めて、どんどん作業を進めてみましょう

- 質問があったら
  - 声を出して質問していただいて大丈夫です
  - わからないときは遠慮なく質問してください

- 分からない言葉が出てきたら
  - Google検索をしたり、[ChatGPT](https://chatgpt.com/)に聞くなど、自分で解決できないかトライしてみましょう  
    - 補足: ChatGPTとは？  
      AI（データをもとに人のように考えたり学ぶことができ、提案などもしてくれるコンピュータの技術）と会話しながら質問や調べ物を解決できる便利なサービスです

- 迷子予防
  - このページは固定しておき、リンクは新規タブで開くのがおすすめです

---

## 2. 基礎知識（今日の前提）

5年くらい前の身近なAIツールは、iPhoneに搭載されたSiriだったように思います。  
2021年にOpenAI社がChatGPTを発表したのを皮切りに、今もなおAIが急速に進化しています。

### 3-1. 生成AI（Generative AI）

生成AIとは、文章・画像・音声・動画などのデータやコンテンツを新しく作り出す技術です。
<details>
  <summary>【生成AIツール例】 </summary>
  
  - 動画生成：[Runway](https://runwayml.com/) ・[Sora](https://openai.com/sora/)
  - 画像生成：[Midjourney](https://www.midjourney.com/home)・[DALL-E(GPT-4o)](https://openai.com/index/dall-e/) ・[ImageFX](https://labs.google/fx/tools/image-fx) 
  - 音楽：[Suno](https://suno.com/) 
</details>
<img src="https://i.gyazo.com/9fa38557e2abdcd459d0e9b841d7e83d.png" width="450px" alt="image from gyazo"/>

生成AIの中でも、テキスト生成に特化したモデルが **LLM（Large Language Model / 大規模言語モデル）** です。

#### LLMとは

膨大な量のテキストデータを学習した、高性能なモデルのことです。  
補足: モデルとは脳みそのこと。何も学習していない状態は産まれたての赤ちゃんみたいなものです。

<img src="https://i.gyazo.com/854fdc0acc8cc4357265fa8e50d1deaa.png" width="450px" alt="image from gyazo"/>

【LLM例】
  
- [GPT（Generative Pre-trained Transformer）](https://chatgpt.com/)  
OpenAIが開発した一連のモデル。
- [Claude](https://claude.ai/login?returnTo=%2F%3F)  
Anthropicが開発した言語モデル。
- [Gemini](https://gemini.google.com/app?hl=ja)  
Googleが開発したモデル。

---

### 3-2. ノーコードツール

ノーコードツールとは、プログラムを書かなくても直感的に操作できるシステムです。

<details>
  <summary>ノーコードツールの例</summary>

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
</details>

<details>
  <summary>ノーコードツールを使った活用事例（ChatBot）</summary>

- [学内のタスクや共同作業を「見える化」して、共有をスムーズにする](https://protoout.studio/24c6077e4887800cb750cca5d55cd487)
  - 参考事例：ノーコードツールで制作！タスク管理＆共有アプリ「TASK BOARD」で現場の困りごとを解決！
    - 例：課題・制作・イベント準備の進捗を、スマホで更新できるタスクボード

- [申請・承認・管理などの「事務作業」をスマホで簡単にする](https://protoout.studio/71ad29b2ffa5444f9cf7602368b6763c)
  - 参考事例：事務的な作業をスマホ1つで楽ちんに！
    - 例：備品の貸出管理、ゼミ備品の管理、申請の承認フローなど
   
【その他活用例】
- 学内施設の案内（図書館の開館時間、PCルーム、食堂の混雑時間など）
- 授業/ゼミのFAQ（レポート提出方法、持ち物、出欠ルール、参考資料）
- 学生向けイベント案内（学内イベント、オープンキャンパス、サークルの説明）
※Difyの詳しい説明（エージェント/ワークフロー/RAGなど）は、後の「Difyパート」でまとめて扱います。

</details>
---

### 3-3. ノーコードツールで会話型AIを作る意味

AIだけでは日常で思うように使えません。  
何らかのサービスやアプリになっていた方が使いやすいのです。

<img src="https://i.gyazo.com/f762cd8bbc5f757ea220db60bbbb7422.png" width="450px" alt="image from gyazo"/>

これまで私たちは、業者に依頼して何万円も支払いHPやアプリなどを作ってもらうことがありました。  
（完成したものを確認すると、なんとなく理想と異なっている仕上がりだということもあります。）

外注という選択肢もありますが、最近は **自分たちで作れる領域** もかなり広がっています。  
たとえば **Dify** のようなツールを使うと、AIチャットや業務用のミニアプリを、まずは小さく試作して改善していく流れが作れます。  

---

## 4. 今回のゴール

- DifyとLINE Botを連携し、自分のRAG活用型AIができる
- 作ったLINE Botをカスタマイズできる
- 日常生活や職場での活用を検討できる


初めてAIを触る方も、触ってみたけど活用しきれていないという方でも、  
今日は「自分でも作れて嬉しい！」と感じてもらい、どんなことに応用できるか考えられる体験になることを目指します。
理論の理解よりも、仕組みを作ってアウトプットすることが大切です！

---

このページの内容は以上です。

このページの内容は以上です。  

[◀ 目次ページ](./readme.md)
