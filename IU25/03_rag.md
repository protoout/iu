# 03. RAG

このパートでは、会話型AIに「検索機能」を追加して、ローカル情報（盛岡/社内/施設/大学など）にも強いQ&Aチャットボットを作ります。  
生成AIがそれっぽい嘘を返すハルシネーションを減らし、「根拠のある回答」に寄せるのが目的です。

---

## 1. このパートで作るもの「ローカル情報に強いQ&Aチャットボット」

### 1-1. 作成するものの概要

- Difyのナレッジ（Dataset）機能を使ってRAGを構築します
- 事前に用意した資料を検索して、その内容を根拠に回答できるチャットボットを作ります
- 今回作成するのは盛岡の観光情報ですが、自分の職場や施設の情報にも応用できます

参考リンク
- [漫画で理解するRAGの説明](https://note.com/preview/nbcd4a100e8c7?prev_access_key=a430d90f75599f57e6ee9654730312d2)


---

## 2. DifyでRAGアプリを作るハンズオン

### 2-1. 準備: Difyアカウントと事前注意

- 前のパートで作ったチャットフロー（盛岡の観光アドバイザー）を使います  
  まだ作っていない場合は、先に前の資料（Dify）を完了してください。
- 作った会話型AIでもそれなりに情報は返してくれますが、自分の業務に即した情報や特定の領域の情報には弱いままです。  
- 会話型AIにオリジナリティを追加し、自分にとって使えるものにしていきましょう。 

---

### 2-2. 利用するナレッジをダウンロードして保存

以下のテキストを、手元にファイルとして保存します。

- 保存するURL  
  https://gist.githubusercontent.com/n0bisuke/a6d77572f3b55e9755e0580ebea2414d/raw/c37cb9a96318eb9b1615b7276628230dbb5dd88e/morioka-oyako.md
> ![CleanShot 2025-08-09 at 13.07.42.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/8f596432-2369-44c1-90a1-81a2ec0d7954.png)

- 保存名（例）  
  `morioka.md` または `morioka.txt`

補足: zipでまとめてDLしたい人  
- https://gist.github.com/n0bisuke/a6d77572f3b55e9755e0580ebea2414d

---

### 2-3. ナレッジデータを登録（Dataset作成）

ナレッジ機能（Datasets）に移動します。  
- https://cloud.dify.ai/datasets
> ![CleanShot 2025-08-09 at 13.04.14.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/a232ab96-931d-44dd-a156-6dad13b79f2b.png)

手順
- `ナレッジベースを作成` を選択
> ![CleanShot 2025-08-09 at 13.05.07.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/45581e87-f847-459a-8336-b858db709364.png)
- 先ほど保存したファイル（`morioka.md` など）をアップロード
> ![CleanShot 2025-08-09 at 13.10.43.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/1ec9dfc1-da34-4b18-ad18-df8084f7cb91.png)

---

### 2-4. 埋め込み（親子分割モード）と検索設定

#### 2-4-1. 埋め込み: チャンク設定（親子分割モード）

汎用設定より手間は増えますが、精度を優先して `親子分割モード` を使います。
> ![CleanShot 2025-08-09 at 13.11.33.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/14fcb934-1650-48c3-b4cf-14087fbfac5f.png)

- 分割モード: `親子分割モード`
- チャンク識別子: `##`
- 検索用子チャンク識別子: `=====`

#### 2-4-2. 埋め込み: インデックス方法

- 埋め込みモデル: Geminiの埋め込みモデルを利用（Dify側の選択肢に従って選択）
> ![CleanShot 2025-08-09 at 13.13.47.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/b37e6244-940e-4983-b8d6-3f46dd376173.png)

#### 2-4-3. 検索: 検索設定（ハイブリッド検索）

本来は「ハイブリッド + リランカー」が強いですが、リランカーは別途APIキーが必要な場合があります。  
今回はウェイト設定で進めます。

- `ハイブリッド検索` を選択
> ![CleanShot 2025-08-09 at 13.14.26.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/8db80470-3233-419d-bfd1-3d2db5c3817f.png)

- `ウェイト設定` を選択
- `保存して処理` を押して完了
> ![CleanShot 2025-08-09 at 13.16.37.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/4c21bf65-f640-4815-ac84-5dd48b8c6d90.png)

---

### 2-5. チャットフローに「知識検索ノード」を追加

手順
- 最初に作ったチャットフローの画面に戻る
- `開始ノード` と `LLMノード` の間に `知識検索` ノードを追加する
> ![CleanShot 2025-08-09 at 13.17.31.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/41289a68-44c8-4c42-a8a2-01058dbad42c.png)
- `知識検索ノード` の設定でナレッジを紐づける
  - ナレッジベース項目の `+` を押す
  - 先ほど作成したナレッジを選択
  - `追加`
> ![CleanShot 2025-08-09 at 13.18.15.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/32c4664a-c862-46d1-a4a1-8c09159d8080.png)
> ![CleanShot 2025-08-09 at 13.19.12.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/c73c3ac7-6f2d-4136-baea-272084df7ba0.png)

---

### 2-6. LLMノードの設定（コンテキストに検索結果を渡す）

RAGが効いていることを分かりやすくするため、あえて少し古めのモデルを使います。  
（賢すぎるモデルだと、RAGなしでも答えてしまうことがあります）

- 例: `Gemini 1.5 Flash` など
> ![CleanShot 2025-08-09 at 13.19.40.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/60553d4e-1d4e-4889-b733-e53342547bac.png)

設定
- LLMノードの `コンテキスト` に `知識検索の result` を設定する
> ![](https://i.gyazo.com/ee6d974dbc4cc9e9353a09f3cad6e90d.gif)
> ![CleanShot 2025-08-09 at 13.20.02.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/05790de1-f138-42ee-a085-2a9e1317f021.png)

---

### 2-7. プロンプトをRAG用に調整

LLMノードのプロンプトを、コンテキスト参照前提にします。


```txt
## 役割
- あなたは盛岡の観光アドバイザーです。
- ユーザーからの質問に対して盛岡観光に役立つ情報を提供してください。
- コンテキストに基づいて回答してください。

{{#context#}}

## 制約事項
- ユーザーが不快に思う返信は禁止です。
``` 
> ![CleanShot 2025-08-09 at 13.24.36.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/fea93677-0673-40fe-93e5-d3008d69cda6.png)
---

### 2-8. 動かしてみる（会話テスト）

例
- 盛岡で親子で行けるスポットを教えて
- この資料に書かれているおすすめの回り方は？

チェックポイント
- 回答が「資料の内容」に寄っていれば成功です
- 資料にないことを断定する場合は、プロンプトを調整して「コンテキスト外はわからない」と言わせましょう
<img src="https://i.gyazo.com/2973c4d251732e7e08b43885580d3268.png" width="250px" alt="image from gyazo"/>

---

## 3. Tips: RAGの限界と応用

### 3-1. ハルシネーションとは

ハルシネーションとは、もっともらしい嘘の情報を返してくる  
「本来存在しない情報をAIが勝手に生成してしまう現象」です。

例
- あなた: 岩手県で今日実施されているイベントを教えて
- AI: 今日のイベントは5件あります
- あなた: 調べたら来週開催だった…など

### 3-2. RAG（Retrieval-Augmented Generation）で嘘を減らす

- RAGは、検索によって取得した外部の知識をLLMに与えて回答の質を上げる手法です
- Difyではナレッジ機能（Datasets）と知識検索ノードで実現できます
https://note.com/preview/nbcd4a100e8c7?prev_access_key=a430d90f75599f57e6ee9654730312d2 

参考: 手法の例（今回やるのはナレッジデータストア）
- ナレッジデータストアの利用
- データソース（Web検索）の利用
- データコネクターの利用
- 外部API・DB連携
- 検索クエリー生成プロンプト

### 3-3. 余談: APIという手もある

- RAGは「事前に登録した情報」が中心です
- リアルタイム性が高い情報や更新性が高い情報を扱うためにはそういったデータを提供している外部サービス（API）と連携する必要があります。   
「Webhookを利用して外部サービスと連携する」というものもあります。  

- [お天気API](https://weather.tsukumijima.net/)が手始めにはいいかもしれません。   
  - JSONという書き方が少し難しいですが、チャレンジすると応用の幅が広がると思います！

---

## 4. チャレンジ課題

時間が余っている人はこちら。
プロンプトを書き換えてみたり、自分の大学のHPを読みこんでみるなど、オリジナル会話型AIを作ってみよう！

- `課題1.` 盛岡ではなく「自分の大学/職場/施設」の情報でナレッジを作り直す
<img src="https://i.gyazo.com/7d86f01c0c57e9920611820a42b5a9c3.png" width="250px" alt="image from gyazo"/>

- `課題2.` プロンプトを調整して「コンテキスト外は回答しない」を徹底する
- `課題3.` 最新のビジネス関連ニュースをリアルタイムで提供するチャットボット
- `課題4.` セミナーやイベントの予約をサポートするチャットボット

---

## 5. まとめ

- ローカル情報は生成AI単体だと弱く、ハルシネーションが起きやすいです
- RAGは、検索した資料を根拠として回答させることで精度を上げる方法です
- Difyでは「ナレッジ機能 + 知識検索ノード」で比較的かんたんにRAGを組み込めます

### 取り込めるデータ
社内リソース、エクセルファイル、Notionの内部ページなど、Difyは扱えるデータが多く搭載されています。  
必要に応じて読みこんでください。

<img src="https://i.gyazo.com/2e15069a236dd7193bf98e701a30c773.png" width="250px" alt="image from gyazo"/>
---

このページの内容は以上です。  

- [次の資料へ](./04_linebot.md)
- [前の資料へ](./02_dify.md)

[◀ 目次ページ](./readme.md)
