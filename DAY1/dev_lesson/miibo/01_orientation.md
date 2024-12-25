# 1.　オリエンテーション

## 今回の目標
- よく分からなくても何か作れたらOK！

## 心構え
- 今日この時間ですべてはできないです。
- 理論の理解をするのではなく、アプリや仕組みを作ってアウトプットすることに重きを置いています。  
（数学の公式を理解するのではなく、公式を使えることが大事です。）
- 人に見せることでコミュニケーションが発生します。  
恥ずかしがらずに披露して、クラスと繋がりましょう！

## 分からない言葉が出てきた時
- 同じグループの人同士で助け合いましょう！
- ハンズオン中はTAや講師に質問を積極的にしましょう！ 後で聞こうは取り返しがつきません。
- また、Google検索をしたり、ChatGPTに聞いてみたりして自分で解決しましょう。  
- 積極的に質問する姿勢は褒めますが、なんでも人に聞くのは違います。  
自分でも解決できないかトライする心意気でいましょう。

### 【ワーク】ChatGPTに聞いてみよう
1番最初のワークで振り分けたカードで、知らないサービスがあったと思います。  
そのうちの1つを聞いて、教えてもらいましょう！
[ChatGPT](https://chatgpt.com/)

## AIの話
### ノーコードツールを使ってAI搭載アプリを作る

5年くらい前の身近なAIツールは、iPhoneに搭載されたSiriだったように思います。  
2021年にOpenAI社がChatGPTを発表したのを皮切りに、今もなおAIが急速に進化しています。  
触ってみようと思いながら触ってない人も、触ってみたけどあまり活用できてない人も、今日を機に「AI使えるよ！」と言えるようになりましょう。  
触ってみたけどどうして良いか分からなくなってしまう人は、目的（企画）と手段（技術）をセットで考える訓練が必要です。

今日の仕事減らして！ではなく、
今日のこの書類仕事ワンクリックで終わらせて！ぐらい具体的な目的が必要です。

<img src="https://i.gyazo.com/f762cd8bbc5f757ea220db60bbbb7422.png" width="450px" alt="image from gyazo"/>

そしてAIだけでは現場で思うように使えません。  
なにかサービスやアプリになっていた方が使いやすいです。  
これまで私たちは業者に依頼して、何万円も支払ってHPやらアプリやらを作ってもらいました。  
（それも理想形態からなんとなく遠い仕上がりだったりするわけです。）

<img src="https://i.gyazo.com/079cd94ec6cc4d27de0495d5ea13bbbb.png" width="450px" alt="image from gyazo"/>

でも、miiboを使えば **無料で**、**自分で**、**自分が思い描く形に近い会話型AI**が作れちゃいます。  
アプリで採用するのは、日本でもっとも利用されているメッセージングアプリLINEです。  
今日は、「自分でも作れて嬉しい！」という体験をしてもらいたいのと、どんなことに応用できるか考えられるといいなと思います！


## 基礎知識
### 生成AI（Generative AI）
 生成AIは、人工知能の一分野で、テキスト、画像、音声、動画などの新しいデータやコンテンツを生成する技術です。
 - 動画生成:Runway 
 - 画像生成:Midjourney
 - 音楽:Suno 

<img src="https://i.gyazo.com/9fa38557e2abdcd459d0e9b841d7e83d.png" width="450px" alt="image from gyazo"/>

### モデル
脳みそのこと。何も学習していない状態は産まれたての赤ちゃんみたいなものです。
<img src="https://i.gyazo.com/854fdc0acc8cc4357265fa8e50d1deaa.png" width="450px" alt="image from gyazo"/>

### LLM（Large Language Model、大規模言語モデル）
LLMは生成AIの1つで、テキストを生成するのに特化したモデルです。  
膨大な量のテキストデータを学習して、高性能な脳みそに。

【代表的なLLM】
- GPT（Generative Pre-trained Transformer）: OpenAIが開発した一連のモデル、現在のバージョンはGPT-4
- Claude: Anthropicが開発した言語モデル、人間のフィードバックを取り入れて安全で信頼性の高い応答を目指す
- Gemini：Googleが開発したモデル、Google検索エンジンの情報を基にしているので情報が新しい傾向

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

# 今回使用するツール
## miibo
生成AIを簡単にアプリケーション化するためのサービスです。
- 「AIではじめて何かをしてみよう！」という人におススメ

miiboのメリット
- プログラミング不要で爆速でAI開発できる
- さまざまなLLMを選んで変更できる
- さまざまなサービスと連携できる
- 作成したAIをどこにでも組み込める
- 開発と運用の費用を最小化できる
- 個別化された会話ができるAIを構築できる
- 汎用的な機能を備えている

## LINE Bot
LINEは日本でもっとも利用されているメッセージングアプリです。  
直感的な見た目と操作性により、初心者でも利用しやすいのが特徴です。

LINE Botは、そのLINE上で動作するチャットボット（ロボット）です。  
日頃使っているLINEとはすこし違うものだと思っていてください。

【会話型AIの活用例】
- カスタマーサポート: 企業の顧客サポート、問い合わせ対応の効率化
- ヘルスケア: 健康アドバイス、予約管理、医療機関との連携
- 予約管理: レストランやクリニックの予約
- 情報提供: ニュース、天気予報、イベント情報の提供
- リマインダー: 薬の服用やアポイントメントのリマインダー
- 教育: 学習支援や教材の提供

## 活用事例
### もいせん卒業生
- [鼻洗太郎bot](https://sho-k.my.canva.site/dagqv-x6nqu)
<img src="https://i.gyazo.com/1832edfa0a041fdbd5d8cf052c3bce11.jpg" width="450px" alt="image from gyazo"/>

### 他社製品
- [医療機関のお問い合わせ対応にmiiboを導入する効果](https://www.docswell.com/s/daitoku0110/57VJNJ-miibo#p1)
<img src="https://i.gyazo.com/061cd9695af32226947e329d0a8d2763.png" width="450px" alt="image from gyazo"/>


- [AI毎日物語](https://camp-fire.jp/projects/view/683245?list=channel_sparks)
<img src="https://i.gyazo.com/b1c38322d6c0272b077f13b0dc800281.png" width="450px" alt="image from gyazo"/>

# 今日のゴール
- 自分の会話型AIを作成できる
- 作った会話型AIをカスタマイズできる
- 職場での活用を検討できる
<img src="https://i.gyazo.com/7d86f01c0c57e9920611820a42b5a9c3.png" width="450px" alt="image from gyazo"/>