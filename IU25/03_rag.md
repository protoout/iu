# 5.Difyのナレッジデータを設定しよう

## このパートでやること

- 作った会話型AIにオリジナリティを追加し、精度をあげる


## このパートで作るもの

- 自分の職場や施設などの情報を答えてくれるQ＆Aチャットボット

<img src="https://i.gyazo.com/7d86f01c0c57e9920611820a42b5a9c3.png" width="250px" alt="image from gyazo"/>



## 1.会話型AIの精度をあげる

作った会話型AIでもそれなりに情報は返してくれますが、自分の業務に即した情報や特定の領域の情報には弱いままです。  
会話型AIにオリジナリティを追加し、自分にとって使えるものにしていきましょう。 

### ハルシネーション

- ハルシネーションとは  
もっともらしい嘘の情報を返してくる**本来存在しない情報をAIが勝手に生成してしまう現象**のことです。

【例】  
あなた：「岩手県で今日実施されているイベントを教えて。」  
AI：「今日は以下の5件のイベントが開催されています。」  
あなた：（ホームページを見に行ったらこのイベントは来週からだ...違うなぁ？）

### RAG(Retrieval-augmented Generation)を構築し、AIの嘘を防ぐ

- RAGは、LLM（大規模言語モデル）が持つ知識を補うため、検索によって取得した外部の知識をモデルに与えて回答の質を向上させる手法です。  

  - 今回はナレッジデータストアの利用をします。  
  【手法一覧】  
    - ナレッジデータストアの利用  
    - データソース（Web検索）の利用
    - データコネクターの利用
    - 外部API・DB連携
    - 検索クエリー生成プロンプト

## 3. RAGアプリを作成

ナレッジ機能を使い、検索拡張機能を付与しましょう。

盛岡のナレッジや組織内のナレッジなどローカル情報には生成AIは弱く、学習してない情報に対してそれっぽい間違った回答を生成することがあります。ハルシネーションと言います。

これを回避するために、AIに情報と検索機能を持たせてあげて、回答精度を上げる手法をRAGと呼びます。

### 3-0. RAGの解説

https://note.com/preview/nbcd4a100e8c7?prev_access_key=a430d90f75599f57e6ee9654730312d2 

### 3-1. 利用するナレッジをDL

https://gist.githubusercontent.com/n0bisuke/a6d77572f3b55e9755e0580ebea2414d/raw/c37cb9a96318eb9b1615b7276628230dbb5dd88e/morioka-oyako.md

↑こちらのテキストを`morioka.txt`か`morioka.md`などのファイル名で手元に保存しましょう。

> ![CleanShot 2025-08-09 at 13.07.42.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/8f596432-2369-44c1-90a1-81a2ec0d7954.png)

直接DLしたい人は[こちら](https://gist.github.com/n0bisuke/a6d77572f3b55e9755e0580ebea2414d)からzipでDLできます。

### 3-2. ナレッジデータを登録


ナレッジのメニューに移動します。

https://cloud.dify.ai/datasets

> ![CleanShot 2025-08-09 at 13.04.14.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/a232ab96-931d-44dd-a156-6dad13b79f2b.png)

- `ナレッジベースを作成`を選択

> ![CleanShot 2025-08-09 at 13.05.07.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/45581e87-f847-459a-8336-b858db709364.png)

- ここで先ほどのファイルをアップロードします

> ![CleanShot 2025-08-09 at 13.10.43.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/1ec9dfc1-da34-4b18-ad18-df8084f7cb91.png)

### 3-2. 埋め込み（親子分割モード）と検索設定

#### 埋め込み: チャンク設定

汎用の方が簡単ですが、親子の方が基本的には精度高いので、`親子分割モード`にします

> ![CleanShot 2025-08-09 at 13.11.33.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/14fcb934-1650-48c3-b4cf-14087fbfac5f.png)

- チャンク識別子: `##`
- 検索用子チャンク識別子: `=====`

### 埋め込み: インデックス方法

Geminiの埋め込みモデルを利用

> ![CleanShot 2025-08-09 at 13.13.47.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/b37e6244-940e-4983-b8d6-3f46dd376173.png)

### 検索: 検索設定

ハイブリッドのリランク設定が一番良い。リランカーはAPIキーが欲しいので今回はウェイトで。

`ハイブリッド検索` > `ウェイト設定`

> ![CleanShot 2025-08-09 at 13.14.26.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/8db80470-3233-419d-bfd1-3d2db5c3817f.png)

`保存して処理`で完了

> ![CleanShot 2025-08-09 at 13.16.37.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/4c21bf65-f640-4815-ac84-5dd48b8c6d90.png)

### 3-3. チャットフローで設定

チャットフローに機能追加してみましょう。

- 最初に作ったチャットフローの画面に戻ります
- 開始ノードとLLMノードの間に知識検索ノードを入れます。

> ![CleanShot 2025-08-09 at 13.17.31.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/41289a68-44c8-4c42-a8a2-01058dbad42c.png)

知識検索ノードの設定 > ナレッジベースの項目の`+` > 先ほど作成したナレッジを選択 > 追加

> ![CleanShot 2025-08-09 at 13.18.15.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/32c4664a-c862-46d1-a4a1-8c09159d8080.png)

無事に追加されました。

> ![CleanShot 2025-08-09 at 13.19.12.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/c73c3ac7-6f2d-4136-baea-272084df7ba0.png)

- LLMモジュールの設定

`Gemini 1.5 Flash`などちょっと昔のあまり頭がよくないモデルを利用してみます。（頭の良いモデルを使うとRAG関係なくちゃんと回答してくれる懸念）

> ![CleanShot 2025-08-09 at 13.19.40.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/60553d4e-1d4e-4889-b733-e53342547bac.png)

`コンテキスト`の箇所に`知識検索のresult`を設定します。

> ![](https://i.gyazo.com/ee6d974dbc4cc9e9353a09f3cad6e90d.gif)

> ![CleanShot 2025-08-09 at 13.20.02.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/05790de1-f138-42ee-a085-2a9e1317f021.png)

プロンプトを調整します。

以下を貼り付け。

```
## 役割
- あなたは盛岡の観光アドバイザーです。
- ユーザーからの質問に対して盛岡観光に役立つ情報を提供してください。
- コンテキストに基づいて回答してください。

{{#context#}}

## 制約事項
- ユーザーが不快に思う返信は禁止です。
```

こんな感じ。これでOKです。

> ![CleanShot 2025-08-09 at 13.24.36.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/fea93677-0673-40fe-93e5-d3008d69cda6.png)

### 3-4.会話をしてみる

HPの情報のみを答えるようにプロンプトを調整すると、より自分の職場のための会話型AIになるでしょう。  
夜間の緊急対応リストなどを読みこませれば、夜間バイトさんが困ったときの手助けになることもあるかもしれません。  
あくまでもサポートという視点は忘れずに活用してくださいね。

<img src="https://i.gyazo.com/7d86f01c0c57e9920611820a42b5a9c3.png" width="250px" alt="image from gyazo"/>


### 取り込めるデータ
社内リソース、エクセルファイル、Notionの内部ページなど、Difyは扱えるデータが多く搭載されています。  
必要に応じて読みこんでください。

<img src="https://i.gyazo.com/2e15069a236dd7193bf98e701a30c773.png" width="250px" alt="image from gyazo"/>


#### 余談：APIという手もある

RAGでは事前に登録した情報しか扱えません。  
リアルタイム性が高い情報や更新性が高い情報を扱うためにはそういったデータを提供している外部サービス（API）と連携する必要があります。   
「Webhookを利用して外部サービスと連携する」というものもあります。  

[お天気API](https://weather.tsukumijima.net/)が手始めにはいいかもしれません。   
JSONという書き方が少し難しいですが、チャレンジすると応用の幅が広がると思います！


## 【チャレンジ】オリジナル会話型AIを作ってみよう

プロンプトを書き換えてみたり、自分の大学のHPを読みこんでみるなど、オリジナリティを出してみましょう。

【アイデア】
- 自分の職場や施設のHPを読みこんだQ＆Aチャットボット
- 経営に関するアドバイスやガイドラインを提供し、資金調達やビジネスプラン作成のサポートをするチャットボット
- 商工会議所が提供する最新のビジネス関連ニュースをリアルタイムで提供するチャットボット
- セミナーやイベントの予約をサポートするチャットボット

---

- [次の資料へ](/IU25/04_liinebot.md)
- [前の資料へ](/IU25/02_dify.md)