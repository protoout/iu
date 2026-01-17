## 1. Difyで簡単なチャットアプリを作る
まずはDifyでチャットを作っていきましょう。以下の資料を元に進めます。

記事内にあるプロンプトは秋葉原ではなく **「盛岡の観光アドバイザー」** というプロンプトにして試してみましょう。
https://zenn.dev/protoout/articles/81-start-dify-chatflow

---

## 2. モデルプロバイダーをGeminiへ

無料枠があるGeminiのAPIキーを設定しましょう。
デフォルトだとGPT系ちょっとは使えるけどすぐ制限来てしまう。

### 2-1. GeminiのAPI取得

[Google AI Studio](https://aistudio.google.com/apikey)からAPIキーを取得します。

### 2-2. Difyのモデルプロバイダー設定

Difyはモデルプロバイダーという画面から各種AIモデルを追加できます。

> ![CleanShot 2025-08-09 at 12.39.07.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/ec511155-8374-433c-a275-3295daaf9111.png)

OpenAIのAPIキーがある人はOpenAIを使うなど、他のAPIでもOKです。

> ![CleanShot 2025-08-09 at 12.55.39.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/4f4ab1f6-9d74-421d-917e-60e5c9b2b349.png)

モデルプロバイダー > Gemini > `セットアップ`と進みAPIキーをセットします。

> ![CleanShot 2025-08-09 at 12.57.02.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/672eb24d-f237-433a-adf5-198e9fd459bc.png)

セット成功

> ![CleanShot 2025-08-09 at 12.57.09.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/c16bba01-bce4-4cd1-a98b-5e5f5c65b170.png)

これである程度使っても無料で制限も緩和されてAIが利用できます。

制限が来ないとは言い切れないのでその場合は[Groq](https://console.groq.com/home)のAPIとモデルプロバイダーを利用するのがお勧めです。余裕ある人はGroqのAPIキーも発行しておくと後で遊べるかもです。

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


### 3-4. 試す

プレビューでチャットして試しましょう。

## 4. 追加機能も入れてみる（時間次第）

- 何かプラグイン使ってみましょう。
- スクレイピング?

