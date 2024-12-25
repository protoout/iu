# 6.　GPTsに触れてみよう"

## 1.GPTとは？

## ChatGPTとGPT（Generative Pre-trained Transformer）
ChatGPTは、2022年11月にOpenAIが発表した「高性能なチャットボット（人間の代わりに機械が対話してくれるシステム）」です。  
あらかじめ用意された回答をするのではなく、**人が使う言語を解釈し、応答を生成して返答する**ところがポイントです。

<img src="https://i.gyazo.com/1863f39bee726930036ec36329ef03e2.png" width="450px" alt="image from gyazo"/>

GPTは **「文章生成モデル」** です。  
ChatGPTがめちゃ喋る赤ちゃんだとしたら、GPTは赤ちゃんの脳みそのイメージでしょう。  
モデルは年々進化していて、今の最新モデルは「GPT-4o」です。無料版では5時間あたり10回までの回数制限があります。


## GPTを使ったアプリケーションの作り方は大きく分けて2パターン
ChatGPT周りの課金形態は、ChatGPT PlusとOpen APIの2種類ありますが、別物なので注意が必要です。
ChatGPT Plusの契約をしていてもOpenAIのAPIを無料で使えるわけではありません。

## 1. GPTsで作る
ChatGPT Plus（定額）と契約するとGPTsが作れるようになります。  
今回準備してもらったのはこちら。

### GPTs
読み方はジーピーティーズです。
自分でカスタマイズして業務や特定の領域に特化させたGPTを作れます。  
対話的に質問していくだけで作れるので、サクッと試す分にはプログラムを書く必要もなく、カスタマイズできます。
生成AIでありがちなハルシネーションを防ぐこともできます。
自身で用意したファイルなどの情報を元に会話させたり、外部のAPIにアクセスもできたりするので可能性は無限大です。

### GPTStore
各自が開発したGPTsを探してインストールできる（公開できる）場所です。  
参考: https://www.robothink.jp/post/chatgpt-gpts-read

ストアに公開したGPTsは収益化できるようになるよ！と発表されていますが、2024年11月現在、日本ではまだできません。


### 2. OpenAIのAPIを使う
OpenAIのAPI（基本従量課金）と契約すると、GPTに限らず色々な機能を利用できます。

- Wisper(音声認識AI)
- Vison（画像分析）
- Text to Speech（テキストから音声合成）
など

APIアクセスで機能を使える状態なので、アプリケーションとして組み込むためには、別のプラットホームの開発や準備も必要になります。

【作例】
- [OpenAI Embedding API（テキストやデータをベクトルに変換する）の利用](https://speakerdeck.com/n0bisuke2/iottotian-zhong-noju-li-number-iotlt-number-tian-zhong-number-openai)  
- [OpenAI Vision APIの利用](https://qiita.com/n0bisuke/items/1dc99747d31316df6c44)

# 2. GPTsに触れてみる

## GPT Storeで検索して、カスタムされたGPTアプリ(GPTs)を使ってみよう
1. ChatGPT左のメニューバーからストアにアクセスできます。  
GPT Storeとは書かれていないので分かりにくいですね。
<img src="https://i.gyazo.com/8100d38e4ba689d949f50418f585c0a0.png" width="450px" alt="image from gyazo"/>
<img src="https://i.gyazo.com/89bd1525cb8b0d27342558d085211baa.png" width="450px" alt="image from gyazo"/>

1. ストアの中で、「福井観光情報GPT」と検索をしてみましょう。  
見つからない場合はこちらからアクセスしましょう。
[福井観光情報GPT](https://chatgpt.com/g/g-673987a84654819193753ff59d612605-fu-jing-guan-guang-qing-bao-gpt)
<img src="https://i.gyazo.com/449d269b7c22e436e9b95f6a8d89fb92.png" width="450px" alt="image from gyazo"/>

1. 「11月16日のニュースを教えて」などなにかメッセージを送信してみましょう。  
はじめは「常に許可をする」もクリックします。  
ニュースを教えてもらえましたか？
<img src="https://i.gyazo.com/4056e9f7c5ef822f876250c289bfb6f7.png" width="450px" alt="image from gyazo"/>

### いろいろなGPTs
以前はGPTsから画像生成やWebサイト検索をするものでしたが、1年前ChatGPTに画像生成機能が搭載され、2024年5月頃web検索機能が搭載されました。

ChatGPTでできることが増えているため、GPTsはよりニッチなものや自分の特定の何かのために作られているといいかなと思います。

- [一貫したキャラクターを絵本様に生成するGPTs](https://chatgpt.com/g/g-XCZL60HQq-yi-guan-sitakiyarakutawohui-ben-yong-nisheng-cheng-surugpts)
- [Travel Buddy](https://chatgpt.com/g/g-qnCECVGXn-travel-buddy)


コラム：[実際に触ってみないと分からない](https://note.com/shu223/n/nd80662dc9fc6)


## GPT mentionsで複数のGPTsを連携して使ってみよう
複数の「GPTs」を会話の切り替えなしで、チャット内で呼び出して使うことができる機能です。  
GPTs Aに問い合わせして返ってきた内容をもとにGPTs Bに問い合わせができます。  
それを体感してみましょう。

@でメンションしてメッセージ毎にGPTsを切り替えられます。  
> ChatGPTの入力フォームで@を入力すると候補が出てきます。
<img src="https://i.gyazo.com/3465f79bc3549e0a2c8553435dbf8715.png" width="450px" alt="image from gyazo"/>

1. 「GPTsを探す」から「DALL-E」を検索して、チャットを開始する。  
一度呼び出したGPTsをメンションできるので事前準備。
<img src="https://i.gyazo.com/25f38ca8b75384d73de0e39e0661fc72.png" width="450px" alt="image from gyazo"/>

1. 1つ目のGPTsから情報を取得する  
「福井観光情報GPT」で最新のニュースを聞いてみましょう。
<img src="https://i.gyazo.com/89e21cc6047f0631fe357d8d35c7351c.png" width="450px" alt="image from gyazo"/>

1. 1つ目の返答をもとに、2つ目のGPTsに情報を渡す  
出力されたニュースを元にサムネイル画像を作ってみます。「DALL-E」をメンションして呼び出し、画像生成をしてもらいましょう。
<img src="https://i.gyazo.com/c1011bcb8eb8aefc77e2e7920549773e.png" width="450px" alt="image from gyazo"/>
    @daなど入れると候補が出ると思います。

1. 「先ほどのニュースの内容からブログを書きたいのでサムネイルを作成してください。」など問い合わせをしましょう。  
<img src="https://i.gyazo.com/f79d7de44fcc9024984969badd724b58.png" width="450px" alt="image from gyazo"/>