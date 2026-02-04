# RAGを使った「盛岡の観光アドバイザーAIチャットボット」を作ろう

- 現状作成したAIは事前に学習している盛岡観光のアドバイスができます。  
  ですが、リアルタイムな情報や地域特有のローカルな情報などについては把握していません。
- ここではAIに“外部データを検索する仕組み”を連携させて、特定の知識に強いAIを作っていきましょう。

## RAGに触れてみよう

生成AIは、特定の分野の情報に関して知らないことがあった場合に、存在しない情報を生成して“それっぽいウソ”をつくことがあります。 （=ハルシネーション）  
そのようなハルシネーションを防ぐために今回はRAGという手法を扱っていきます。

### RAG（Retrieval-Augmented Generation）って何?

RAG（Retrieval-Augmented Generation）は、AIが回答を作る前に**関連する資料を検索して**、見つけた情報を**根拠**として使いながら回答する方法です。  

| 略 | 意味 | やること |
|---|---|---|
| R | Retrieval（検索） | 必要な情報を Web / 資料 / DB / ファイル から探す |
| A | Augmented（補強） | 見つけた情報を根拠として LLM に渡す |
| G | Generation（生成） | 根拠をもとに、読みやすい文章で答える |

参考：[漫画で理解するRAGの説明](https://note.com/preview/nbcd4a100e8c7?prev_access_key=a430d90f75599f57e6ee9654730312d2)

### LLMだけ vs RAGあり

生成AIの話で紹介した「LLMだけではあと一歩足りないところ」をRAGありだと以下のように解決できます。

| やりたいこと | LLM単体 | RAGあり |
|---|---|---|
| 「今朝のドル円レートを教えて」 | "昨日は…"と言い出す | **為替API** で最新値を取って即回答 |
| 「学内/ゼミのルールを確認したい」 | 一般論でそれっぽく答えがち（根拠が弱い） | **配布資料や規約の該当箇所**を探して、それを根拠に答えられる |

## 1. 作るアプリケーション

### 1-1. 盛岡のローカル観光情報について回答するAIチャットボット

  <img src="https://i.gyazo.com/e2870f25bbac039cd72f2b7f53c80d80.jpg" width="450px" alt="image from gyazo"/>

## 2. ハンズオン：RAGを使った盛岡の観光アドバイザーAIチャットボットを作ろう

### 2-0. Difyのチャットフローを開く
1. [Dify](https://dify.ai/jp)の画面で、先ほど作成した盛岡の観光アドバイザーチャットボットを開きましょう。

    <img src="https://i.gyazo.com/5dff5672c3a73f6332d0efb8ae885c61.png" width="450px" alt="image from gyazo"/>

盛岡のローカルな観光情報をAIに与える前に、質問を送ってみましょう。  
RAGを入れた後で回答にどのような変化が起きるかを試していきます。  

2. 今回は盛岡のローカルな観光情報の知識（ナレッジ）を扱っていきます。  
  [盛岡のローカル観光情報ナレッジ](https://gist.githubusercontent.com/n0bisuke/a6d77572f3b55e9755e0580ebea2414d/raw/c37cb9a96318eb9b1615b7276628230dbb5dd88e/morioka-oyako.md)を開いてみてください。

3. 下記をコピーして先ほど作成したチャットボットに貼り付けて聞いてみましょう。

   ```txt
   直利庵本店の大人料金と小学生料金も含めて旅程を出して
   ```

4. 現状は下記のようにローカルな観光情報が返ってこず、それっぽい嘘の情報が返ってきていてハルシネーションがおきています。  
  - 本来は、大人料金：3,300円・小学生料金：1,650円

    <img src="https://i.gyazo.com/053b6cbce159c107ad01a1c7eeb21986.jpg" width="450px" alt="image from gyazo"/>

### 2-1. ナレッジデータをファイル保存する

- 先ほど開いた[盛岡のローカル観光情報ナレッジ](https://gist.githubusercontent.com/n0bisuke/a6d77572f3b55e9755e0580ebea2414d/raw/c37cb9a96318eb9b1615b7276628230dbb5dd88e/morioka-oyako.md)をファイルとして保存します。  
`morioka-oyako.md`または`morioka-oyako.txt`という名前で自分のパソコンに保存してください。

    <img src="https://i.gyazo.com/5d03e8e9fa1725f0f27e2c9f9046283d.png" width="150px" alt="image from gyazo"/>

補足: zipでまとめてDLしたい人は[こちら](https://gist.github.com/n0bisuke/a6d77572f3b55e9755e0580ebea2414d)

### 2-2. ナレッジの登録をしよう

1. Dify画面の上部にある[ナレッジタブ](https://cloud.dify.ai/datasets)をクリックします。  

    <img src="https://i.gyazo.com/6d37cc15a7954a2bc22f1152e49af3c9.png" width="450px" alt="image from gyazo"/>

2. 画面左上の`+ナレッジベースを作成`をクリックします。

    <img src="https://i.gyazo.com/00293973083117c298714eb8c38e4236.png" width="300px" alt="image from gyazo"/>

3. 先ほど保存したファイル（`morioka-oyako.md` など）をドラッグアンドドロップでアップロードします。

    <img src="https://i.gyazo.com/44b34ca32a8699bbced5a4b206601d51.png" width="300px" alt="image from gyazo"/>

4. 実際にアップロードができたら「次へ」というボタンをクリックしましょう。

    <img src="https://i.gyazo.com/6b9699b09e8a5b17d964195335e7dc1c.png" width="300px" alt="image from gyazo"/>

### 2-3. ナレッジのチャンク設定をしよう
ここからは検索しやすい形でナレッジデータを保存する設定をしていきいます。  
ナレッジ設定の詳細については、3.Tipsを参照ください。  

1. 基本汎用設定で良いですが、今回は精度を優先して `親子分割モード` を選択します。

    <img src="https://i.gyazo.com/a7ed0fb494e320d45de9bf2873198bd3.png" width="450px" alt="image from gyazo"/>

2. チャンク識別子と検索用子チャンク識別子は以下に書き換えましょう。
  - チャンク識別子: `##`
  - 検索用子チャンク識別子: `=====`

    <img src="https://i.gyazo.com/609e339e1339dd94154e381a12c0d2a9.png" width="450px" alt="image from gyazo"/>

  - チャンク（chunk）とは？  
    - チャンクは、長い文章や資料を **検索しやすいサイズに小分けした「文章のかたまり」** のことです。  
    - RAGでは、ナレッジデータをそのまま丸ごと使うのではなく、**チャンク単位で保存しておき**、質問に近い部分だけを探して取り出します。

3. インデックス方法
  - 親子モードでは自動的に`高品質`が選択されます。

     <img src="https://i.gyazo.com/511dbc1c2450b65428bf76629fc73fa1.png" width="450px" alt="image from gyazo"/>

  - インデックスとは？
    - チャンクで分割したナレッジを、検索しやすいように整理して保存するための「索引の作り方」のことです。

4. 埋め込みモデル
  - 埋め込みモデルは「gemini-embedding-001」を選びましょう。

      <img src="https://i.gyazo.com/f39519002fae379e54e92b2e55046c71.png" width="450px" alt="image from gyazo"/>

### 2-4. ナレッジの検索設定と保存をしよう

本来は「ハイブリッド + リランカー」の方が精度が高いです。  
ただ、リランカーは別途APIキーが必要な場合があるので、今回はウェイト設定で進めます。

1. `ハイブリッド検索`をクリックして選びましょう。

    <img src="https://i.gyazo.com/8c43d475ce1b25f798b3d9cb24c416f7.png" width="450px" alt="image from gyazo"/>

2. `ウェイト設定` を選択します。

    <img src="https://i.gyazo.com/fc14ea2b1739476acf83fc96f5b71a97.png" width="450px" alt="image from gyazo"/>

3. `保存して処理`のボタンをクリックしましょう。

    <img src="https://i.gyazo.com/6782e5a33d0a533d1b7cc2fcb21952c1.png" width="450px" alt="image from gyazo"/>


> [!CAUTION]
> 4. 少々埋め込み処理時間が発生します。  
> 埋め込みが完了したことを確認しましょう。
>
> <img src="https://i.gyazo.com/bde4a5a225ba4c79c6a81380257cb3c4.png" width="450px" alt="image from gyazo"/>

5. `ドキュメントに移動`をクリック

    <img src="https://i.gyazo.com/e4311250b72841b277afd46062218626.png" width="450px" alt="image from gyazo"/>

6. 右側のステータスが `利用可能` という表示になっていることを確認しましょう。  
   無事にナレッジが追加できています。

    <img src="https://i.gyazo.com/b355dd66cc8543274e0359f40047342a.png" width="450px" alt="image from gyazo"/>

### 2-5. チャットフローに「知識検索ノード」を追加する

1. 画面上部の「スタジオ」タブをクリックし、自分のチャットアプリを開きましょう。

    <img src="https://i.gyazo.com/d346623b6c7942da8ca3a11226692bad.png" width="450px" alt="image from gyazo"/>

2. 知識検索ノードを追加する


    1.  `開始ノード` と `LLMノード` を繋ぐ線の上にカーソルを持っていくと、`「+」`ボタンがでます。

        <img src="https://i.gyazo.com/ce641441280e456578804d1c919a4675.png" width="450px" alt="image from gyazo"/>

    2. その`「+」`ボタンをクリックして、 `知識検索` ノードを追加します。

        <img src="https://i.gyazo.com/f1b31a4a0ce4a2294c650d1bdb5170cd.png" width="450px" alt="image from gyazo"/>

    3. 4つのノードが並びました。

        <img src="https://i.gyazo.com/c07911c0b224983db30572af072312fd.png" width="450px" alt="image from gyazo"/>

### 2-6. 知識検索ノードの設定でナレッジを紐づける

1. ここから知識検索ノードをクリックして、右側の画面で設定していきます。

    <img src="https://i.gyazo.com/5baf19bc878348331fad2d31824c33c8.png" width="300px" alt="image from gyazo"/>

2. ナレッジベース項目の右側にある`+`ボタンをクリックします。

    <img src="https://i.gyazo.com/0a5e05fc89e439ecbdee334c47c0b7ff.png" width="300px" alt="image from gyazo"/>

3. 先ほど作成したナレッジを選択して、`追加`ボタンをクリックします。

    <img src="https://i.gyazo.com/f88dc73902a2f7c7c202a581bb811b54.png" width="300px" alt="image from gyazo"/>

4. ナレッジベースが登録されました。

    <img src="https://gyazo.com/6e0fe598a6be8a8cd889a368e2a40e05.png" width="300px" alt="image from gyazo"/>

### 2-7. LLMの設定

1. 次にLLMノードをクリックして右側の画面で設定していきます。
  - 入れるモデルは`Gemini 2.0 Flash-Lite 001`を選びます。

> [!TIP]
> RAGが効いていることを分かりやすくするため、あえて少し古めのモデルを使います。  
> （賢すぎるモデルだと、RAGなしでも答えてしまうことがあります。）  
>
> <img src="https://i.gyazo.com/93a33031303a9e50de4d3d5a4e57142e.png" width="300px" alt="image from gyazo"/>

> [!CAUTION]
> ただし、制作タイムではgemini-2.5を使うようにしましょう。
> gemini-2.5の方がコストと性能とのバランスが良く、gemini-2.0は2026年3月末で使用できなくなるためです。
>
> <img src="https://i.gyazo.com/b55a38a9b80dc19cc726fb0f4762d427.png" width="300px" alt="image from gyazo"/>
>
> 参考；[Gemini APIリリースノート](https://ai.google.dev/gemini-api/docs/changelog?hl=ja)

2. コンテキストの「変数値を設定」の欄をクリックして、知識検索の中の`result`を選びましょう。 

    <img src="https://i.gyazo.com/7a2138ec292a26b29c610dc949c8bb5e.png" width="300px" alt="image from gyazo"/><br>

    <img src="https://i.gyazo.com/b1299412977579fcb86909c8b44ee624.png" width="300px" alt="image from gyazo"/>

3. LLMノードのSYSTEMの中に現在入っているプロンプトは削除し、以下のプロンプトをコピーして置き換えましょう。

  ```
  ## 役割
  - あなたは盛岡の観光アドバイザーです
  - ユーザーからの質問に対して盛岡観光に役立つ情報を提供してください
  - コンテキストに基づいて回答してください
  
  {{#context#}}

  ## 制約事項
  - ユーザーが不快に思う返信は禁止です
  ```

> [!TIP]
> コンテキストは、きちんと紫色で変数として入っているか確認しましょう。
> 
> <img src="https://i.gyazo.com/1868c1034865e2ffec19e8314a59bb3e.png" width="450px" alt="image from gyazo"/>

### 2-8. 動かしてみよう

**冒頭で聞いた質問**をチャットボットに聞いてみましょう。  
登録したナレッジの情報通りの回答が返ってきたら成功です。

<img src="https://i.gyazo.com/e2870f25bbac039cd72f2b7f53c80d80.jpg" width="450px" alt="image from gyazo"/>

※ うまくナレッジの情報をもとに回答していない場合は、プロンプトも調整してみましょう。

### 2-9. 公開して試そう

1. 画面右上の`公開する`をクリックし、`更新を公開`ボタンを押します

    <img src="https://i.gyazo.com/b66569ab623f4d957cd11406afea8a0d.png" width="300px" alt="image from gyazo"/>

2. `アクションが成功しました`が表示されたらOKです

    <img src="https://i.gyazo.com/5d21f62b70494405d4e139b4df38856a.png" width="300px" alt="image from gyazo"/>

3. `アプリを実行`ボタンをクリックします

    <img src="https://i.gyazo.com/bb95bb664ffadbdebbfd236a580748ea.png" width="300px" alt="image from gyazo"/>

4. 本番環境で早速試してみましょう！

    <img src="https://i.gyazo.com/2155a0d3c2672ad1fc76d1d74a42df75.png" width="300px" alt="image from gyazo"/>

## 3. Tips: RAGの限界と応用

### 3-1. 外部サービス（API）と連携
リアルタイム性が高い情報や更新性が高い情報を扱うためには外部サービス（API）と連携する必要があります。   
[お天気API](https://weather.tsukumijima.net/) のように「Webhookを利用して外部サービスと連携する」という仕組みもあります。  

### 3-2.ナレッジ設定の詳細について
[RAGの精度を高めるナレッジ設計ガイド](https://github.com/protoout/iu/blob/main/IU25/rag_guide.md)を見ながら、ナレッジを改善していきましょう。  
参考：[RAGの精度が上がらない？設定を見直してみよう！](https://protoout.studio/2296077e488780f081dace683bb63f86)

## 4. チャレンジ課題

時間が余っている人は、ナレッジを追加してみたり、プロンプトを書き換えるなど、オリジナル会話型AIを作ってみましょう！

### 4-1. 盛岡ではなく「自分の大学/職場/施設」の情報でナレッジを追加してみよう
[RAGの精度を高めるナレッジ設計ガイド](https://github.com/protoout/iu/blob/4c3344f43355f5660bc776128adfed358cd5024c/IU25/rag_guide.md#rag%E3%81%AE%E7%B2%BE%E5%BA%A6%E3%82%92%E9%AB%98%E3%82%81%E3%82%8B%E3%83%8A%E3%83%AC%E3%83%83%E3%82%B8%E8%A8%AD%E8%A8%88%E3%82%AC%E3%82%A4%E3%83%89)を参考に、自分の身近なテーマの資料（大学の案内や施設のFAQなど）を用意してナレッジに登録し、同じ手順でRAGが効くか試しましょう。

### 4-2. LINE Botでも動かしてみよう
作成したチャットボットをLINE Botとして連携し、LINE上で質問してちゃんと返答が返るか動作確認しましょう。

### 4-3. 周りの人と共有してみよう
自分のBotのQRコードを共有して他の人にも実際に使ってもらい、フィードバック（良かった点/分かりにくい点）を集めましょう。

### 4-4. ナレッジデータにない情報は回答しないよう、プロンプトを調整してみよう
ナレッジに根拠がない質問が来たときは推測で答えず「資料にないため分かりません」と返すように、LLMのプロンプトを追記して調整しましょう。

## 5. まとめ

このパートではRAGという手法を学び、特定の知識の情報に強いAIチャットボットを作成していきました。  
回答の精度を上げるためにはデータを入れる前の前処理が大切になりますので、他のナレッジ検索や保存方法も試してみてください。  
<br>
Difyには、様々なファイル形式やNotion連携など扱えるデータが多く搭載されています。  
大学の案内・学内ルール・サークル情報など自分が作りたいアイデアを形にする手段の1つとしてRAGを活用してみましょう。

---

このページの内容は以上です  

[◀ 目次ページ](./readme.md)
