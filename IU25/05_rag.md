# RAGを使った「盛岡の観光アドバイザーAIチャットボット」を作ろう

生成AIは、事前にある程度の知識を学習していますが、ニッチな情報に対応していない時に、もっともらしい嘘の情報を返してくる（（=ハルシネーション））ことがあります。
本来存在しない情報をAIが勝手に生成しないように、RAG（Retrieval-Augmented Generation）を使用して、ローカル情報（盛岡/社内/施設/大学など）にも強いQ&Aチャットボットを作ってみましょう。



## 2. 現在の状態

現時点で、Difyが以下の状態になっていればOKです。

- 前のパートで作った **盛岡の観光アドバイザーチャットボット** がある
- そのチャットボットが **プレビューで会話できる**状態になっている

<img src="https://i.gyazo.com/5dff5672c3a73f6332d0efb8ae885c61.png" width="450px" alt="image from gyazo"/>

### 2-1. RAG導入前に試してみる

- RAGを入れる前に、質問を送ってみましょう。
- あとでRAGを入れた後にもう一度同じ質問をして、差分が分かるようにします。

```txt
直利庵本店の最低予約人数、大人料金と小学生料金は？
```

<img src="https://i.gyazo.com/4e0fbe8f32b7a4ee10a0ac2418140fc8.png" width="450px" alt="image from gyazo"/>

参考リンク
- [漫画で理解するRAGの説明](https://note.com/preview/nbcd4a100e8c7?prev_access_key=a430d90f75599f57e6ee9654730312d2)


## 1. このパートで作るもの「ローカル情報に強いQ&Aチャットボット」

### 1-1. 作成するものの概要

- Difyのナレッジ機能を使ってRAGを構築します
- 事前に用意した資料を検索して、その内容を根拠に回答できるチャットボットを作ります

### 2-2. DifyでRAGアプリを作る

以下のテキストを、手元にファイルとして保存します。

- 保存するURL  
  https://gist.githubusercontent.com/n0bisuke/a6d77572f3b55e9755e0580ebea2414d/raw/c37cb9a96318eb9b1615b7276628230dbb5dd88e/morioka-oyako.md
<img src="https://i.gyazo.com/4feb99d8c10610fa4cf5e2b1663ef129.png" width="450px" alt="image from gyazo"/>

- 保存名（例）  
  `morioka.md` または `morioka.txt`

補足: zipでまとめてDLしたい人  
- https://gist.github.com/n0bisuke/a6d77572f3b55e9755e0580ebea2414d

### 2-3. ナレッジデータを登録（Dataset作成）

ナレッジ機能（Datasets）に移動します。  
- https://cloud.dify.ai/datasets
<img src="https://i.gyazo.com/9dd2d3dd9f181ef1be8cd24240814366.png" width="450px" alt="image from gyazo"/>

手順
- `ナレッジベースを作成` を選択
<img src="https://i.gyazo.com/00293973083117c298714eb8c38e4236.png" width="450px" alt="image from gyazo"/>

- 先ほど保存したファイル（`morioka.md` など）をアップロード
<img src="https://i.gyazo.com/44b34ca32a8699bbced5a4b206601d51.png" width="450px" alt="image from gyazo"/>

### 2-4. 埋め込み（親子分割モード）と検索設定

#### 1. 埋め込み: チャンク設定（親子分割モード）

汎用設定より手間は増えますが、精度を優先して `親子分割モード` を使います。
<img src="https://i.gyazo.com/609e339e1339dd94154e381a12c0d2a9.png" width="450px" alt="image from gyazo"/>

- 分割モード: `親子分割モード`
- チャンク識別子: `##`
- 検索用子チャンク識別子: `=====`
- 埋め込みモデル: Geminiの埋め込みモデルを利用

<img src="https://i.gyazo.com/0d8b6fa8585a7ecf14009edf38094822.png" width="450px" alt="image from gyazo"/>

#### 2. 検索: 検索設定

本来は「ハイブリッド + リランカー」の方が精度が高いですが、リランカーは別途APIキーが必要な場合があるため、今回はウェイト設定で進めます。

- `ハイブリッド検索` を選択
- `ウェイト設定` を選択

<img src="https://i.gyazo.com/3bef14cf02e97912eb0eb98bf40b4388.png" width="450px" alt="image from gyazo"/>

- `保存して処理` を押して完了

<img src="https://i.gyazo.com/dc0e2f09993bfa6630b1e3d672127518.png" width="450px" alt="image from gyazo"/>

### 2-5. チャットフローに「知識検索ノード」を追加

手順
- 最初に作ったチャットフローの画面に戻る
- `開始ノード` と `LLMノード` の間に `知識検索` ノードを追加する
<img src="https://i.gyazo.com/f1b31a4a0ce4a2294c650d1bdb5170cd.png" width="450px" alt="image from gyazo"/>

- `知識検索ノード` の設定でナレッジを紐づける
  - ナレッジベース項目の `+` を押す
  - 先ほど作成したナレッジを選択
  - `追加`
<img src="https://gyazo.com/ade47fb9b54a1a765aa20514aef8b83c.png" width="450px" alt="image from gyazo"/>

<img src="https://gyazo.com/6e0fe598a6be8a8cd889a368e2a40e05.png" width="450px" alt="image from gyazo"/>



### 2-6. LLMノードの設定

RAGが効いていることを分かりやすくするため、あえて少し古めのモデルを使います。  
（賢すぎるモデルだと、RAGなしでも答えてしまうことがあります）

- 例: `Gemini 2.0 Flash-Lite 001` など
<img src="https://i.gyazo.com/93a33031303a9e50de4d3d5a4e57142e.png" width="450px" alt="image from gyazo"/>

設定
- LLMノードの `コンテキスト` に `知識検索の result` を設定する
<img src="https://i.gyazo.com/7a2138ec292a26b29c610dc949c8bb5e.png" width="450px" alt="image from gyazo"/>
<img src="https://i.gyazo.com/b1299412977579fcb86909c8b44ee624.png" width="450px" alt="image from gyazo"/>

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
<img src="https://i.gyazo.com/1868c1034865e2ffec19e8314a59bb3e.png" width="450px" alt="image from gyazo"/>

### 2-8. 会話テストをしてみる

ここで **2-1で送ったものと同じ質問** をもう一度聞きます。  
RAGを入れたことでの差を体験しましょう。

```txt
直利庵本店の最低予約人数、大人料金と小学生料金は？
```

チェックポイント
- 回答が「資料の内容」に寄っていれば成功です
- 資料にないことを断定する場合は、プロンプトを調整しましょう
<img src="https://i.gyazo.com/e8cb69a64fbb355b3e8bb17ea7989f36.png" width="450px" alt="image from gyazo"/>

## 3. Tips: RAGの限界と応用

- RAGは、外部の知識をLLMに与えて回答の質を上げる手法です
- RAGは「事前に登録した情報」が中心ですが、リアルタイム性が高い情報や更新性が高い情報を扱うためにはそういったデータを提供している外部サービス（API）と連携する必要があります。   
「Webhookを利用して外部サービスと連携する」というものもあります。  
  - 例：[お天気API](https://weather.tsukumijima.net/)   
  - JSONという書き方が少し難しいですが、チャレンジすると応用の幅が広がると思います！

## 4. チャレンジ課題

時間が余っている人はこちら。
プロンプトを書き換えてみたり、自分の大学のHPを読みこんでみるなど、オリジナル会話型AIを作ってみよう！

1. LINE Botで動かせるようにして、周りの人との共有してみよう
2. ナレッジデータにない情報は回答しないよう、プロンプトを調整してみよう
3. 盛岡ではなく「自分の大学/職場/施設」の情報でナレッジを追加してみよう

## 5. まとめ

生成AIだけだと、ローカル情報は学習されていないことが多く、もっともらしい誤回答（ハルシネーション）が起きやすいため、このパートでは「資料を検索して、その内容を根拠に回答する」RAGという仕組みで、回答の精度と再現性を上げました。

DIfyには、エクセルファイルやNotionの内部ページなど、扱えるデータが多く搭載されているので、 大学の案内・学内ルール・サークル情報などにも応用して、様々なAIチャットボットを作成することができます。

---

このページの内容は以上です。  

[◀ 目次ページ](./readme.md)
