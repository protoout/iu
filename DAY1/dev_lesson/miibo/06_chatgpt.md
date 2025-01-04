# 6.GPTsに触れてみよう

## このパートでやること

- GPTsに触れてみる


## 1.GPTとは？

### 1-1.ChatGPTとGPT（Generative Pre-trained Transformer）

- ChatGPTとは  
2022年11月にOpenAIが発表した「高性能なチャットボット（人間の代わりに機械が対話してくれるシステム）」です。  
あらかじめ用意された回答をするのではなく、**人が使う言語を解釈し、応答を生成して返答する**ところがポイントです。

<img src="https://i.gyazo.com/1863f39bee726930036ec36329ef03e2.png" width="450px" alt="image from gyazo"/>

- GPTとは  
**「文章生成モデル」** です。  
ChatGPTがとても喋る赤ちゃんだとしたら、GPTは赤ちゃんの脳みそというイメージです。  
モデルは年々進化していて、今の最新モデルは「GPT-4o」です。  
（無料版では5時間あたり10回までの回数制限があります。）


### 1-2. GPTを使ったアプリケーションの作り方は大きく分けて2パターンある

ChatGPT周りの課金形態は、`ChatGPT Plus`と`Open API`の2種類ありますが、別物です。  
ChatGPT Plusの契約をしていてもOpenAIのAPIを無料で使えるわけではありません。

#### GPTsで作る  
ChatGPT Plus（定額）と契約するとGPTsが作れるようになります。   
**【✅下記の一文相談・確認する】**
今回準備してもらったのはこちらです。

  - GPTs 
  読み方は「ジーピーティーズ」です。  

  自分でカスタマイズして業務や特定の領域に特化させたGPTを作ることができます。  
  対話的に質問していくだけで作れるので、サクッと試す分にはプログラムを書く必要もなく、カスタマイズできます。  

　生成AIでありがちなハルシネーションを防ぐこともできます。  
　自身で用意したファイルなどの情報を元に会話させたり、外部のAPIにアクセスもできたりするので、可能性は無限大です。

- GPTStore  
各自が開発したGPTsを探してインストールできる（公開できる）場所です。  
参考: https://www.robothink.jp/post/chatgpt-gpts-read

ストアに公開したGPTsは収益化できるようになるよ！と発表されていますが、2025年1月現在、日本ではまだできません。

- OpenAIのAPI  
OpenAIのAPI（基本従量課金）と契約すると、GPTに限らず色々な機能を利用できます。

  - Wisper(音声認識AI)
  - Vison（画像分析）
  - Text to Speech（テキストから音声合成）　　など

APIアクセスで機能を使える状態なので、アプリケーションとして組み込むためには、別のプラットホームの開発や準備も必要になります。

【作例】
- [OpenAI Embedding API（テキストやデータをベクトルに変換する）の利用](https://speakerdeck.com/n0bisuke2/iottotian-zhong-noju-li-number-iotlt-number-tian-zhong-number-openai)  

- [OpenAI Vision APIの利用](https://qiita.com/n0bisuke/items/1dc99747d31316df6c44)


## 2.GPTsに触れてみる

### 2-1.GPT Storeで検索して、カスタムされたGPTアプリ(GPTs)を使ってみよう

- ChatGPT左のメニューバーからストアにアクセスできます。  
GPT Storeとは書かれていないので分かりにくいですね。

<img src="https://i.gyazo.com/8100d38e4ba689d949f50418f585c0a0.png" width="250px" alt="image from gyazo"/>

- ストアの中で、「福井観光情報GPT」と検索をしてみましょう。  
見つからない場合は下記のリンクからアクセスしましょう。  
[福井観光情報GPT](https://chatgpt.com/g/g-673987a84654819193753ff59d612605-fu-jing-guan-guang-qing-bao-gpt)

<img src="https://i.gyazo.com/449d269b7c22e436e9b95f6a8d89fb92.png" width="450px" alt="image from gyazo"/>

- 「2024年12月のニュースを教えてください」など、何かメッセージを送信してみましょう。  
はじめは「常に許可をする」もクリックします。  
ニュースを教えてもらえましたか？

<img src="https://i.gyazo.com/5aecb8a10db3c190d0d04272614d53bb.png" width="350px" alt="image from gyazo"/>


### 2-1.さまざまなGPTs

以前はGPTsから画像生成やWebサイト検索をするものでした。  
ですが、1年前ChatGPTに画像生成機能が搭載され、2024年5月頃web検索機能が搭載されました。

ChatGPTでできることが増えているため、GPTsはよりニッチなものや自分の特定の何かのために作られているといいかなと思います。

【作例】  
- [一貫したキャラクターを絵本様に生成するGPTs](https://chatgpt.com/g/g-XCZL60HQq-yi-guan-sitakiyarakutawohui-ben-yong-nisheng-cheng-surugpts)
- [Travel Buddy](https://chatgpt.com/g/g-qnCECVGXn-travel-buddy)

- コラム：[実際に触ってみないと分からない](https://note.com/shu223/n/nd80662dc9fc6)


### 2-3.GPT mentionsで複数のGPTsを連携して使ってみよう

複数の「GPTs」を会話の切り替えなしで、チャット内で呼び出して使うことができる機能です。      
GPTs Aに問い合わせして返ってきた内容をもとにGPTs Bに問い合わせができます。  
それを体感してみましょう。

@でメンションしてメッセージ毎にGPTsを切り替えられます。  
ChatGPTの入力フォームで@を入力すると候補が出てきます。

<img src="https://i.gyazo.com/3465f79bc3549e0a2c8553435dbf8715.png" width="450px" alt="image from gyazo"/>

- 「GPTsを探す」から「DALL-E」を検索して、チャットを開始します。  
一度呼び出したGPTsをメンションできるので事前準備。

<img src="https://i.gyazo.com/25f38ca8b75384d73de0e39e0661fc72.png" width="450px" alt="image from gyazo"/>

- 1つ目のGPTsから情報を取得します。
「福井観光情報GPT」で最新のニュースを聞いてみましょう。

<img src="https://i.gyazo.com/89e21cc6047f0631fe357d8d35c7351c.png" width="350px" alt="image from gyazo"/>

- 1つ目の返答をもとに、2つ目のGPTsに情報を渡します。 
出力されたニュースを元にサムネイル画像を作ってみます。  
「DALL-E」をメンションして呼び出し、画像生成をしてもらいましょう。  
（@daなど入れると候補が出ると思います。）

<img src="https://i.gyazo.com/c1011bcb8eb8aefc77e2e7920549773e.png" width="450px" alt="image from gyazo"/

- 「先ほどのニュースの内容からブログを書きたいのでサムネイルを作成してください。」など問い合わせをしてみましょう。  

<img src="https://i.gyazo.com/f79d7de44fcc9024984969badd724b58.png" width="350px" alt="image from gyazo"/>

- [次の資料へ](./07_original.md)
- [トップページへ](./readme.md)