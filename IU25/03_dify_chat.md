# DifyでAIチャットを作ろう

このパートでは、Difyでチャットアプリを作成し、授業で使うLLMとしてGeminiを接続します。  

## 1. このパートで作るもの「盛岡の観光アドバイザーAIチャット」

### 1-1. 作成するものの概要

- Dify上で動く「盛岡観光の相談に答えるチャットアプリ」を作ります。
- 次のパート（RAG）で「資料参照型」に拡張します。

参考リンク
- [Dify チャットフロー入門（ベース記事）](https://zenn.dev/protoout/articles/81-start-dify-chatflow)

## 2. Difyでチャットアプリを作るハンズオン

### 2-1. Difyでチャットアプリを作成
- [Dify](https://cloud.dify.ai/)を開き、ログインして下記のような画面になればOKです。

  <img src="https://i.gyazo.com/7b6715b8a0b7da4e31a694601caa4475.png" width="450px" alt="image from gyazo"/>

- [ベース記事](https://zenn.dev/protoout/articles/81-start-dify-chatflow)に沿って、まずは、**チャットが動くところまで**作ります。  

- ここでは、公開までやればOK
  - Difyでアプリを新規作成できている
  - チャットのプレビュー（試し会話）で1往復以上できている
  
    <img src="https://i.gyazo.com/23057cb0680f982ec7932cb7f1705ef3.png" width="450px" alt="image from gyazo"/>

  - 公開設定になっている
  
    <img src="https://i.gyazo.com/b66569ab623f4d957cd11406afea8a0d.png" width="450px" alt="image from gyazo"/>

### 2-2. モデルプロバイダーをGeminiへ接続（APIキー設定）

授業では、無料枠があり試作が進めやすいGeminiを利用します。
Difyは「モデルプロバイダー」画面から、使用するLLMを追加できます。

#### 1. GeminiのAPIキーについて

**事前に荻原先生に発行＆共有していただいたAPIキーを使いましょう！**
- 注意: APIキーは外部に公開しないでください。
- [Google AI Studio](https://aistudio.google.com/apikey) を使用することで、自分でもAPIキーを発行することができます。

#### 2. Difyのモデルプロバイダー設定（Gemini）

- Dify管理画面を開く
<img src="https://i.gyazo.com/5c0132aef5fa8cda491563a587505550.png" width="450px" alt="image from gyazo"/>

- 「モデルプロバイダー」からGeminiを選び、`セットアップ`へ
<img src="https://i.gyazo.com/0ddcc0b9e7614b70e2515cf595a13a8f.png" width="450px" alt="image from gyazo"/>

- 荻原先生に共有していただいたAPIキーを貼り付けて保存
<img src="https://i.gyazo.com/fcb1ab3faa25556937e07945dc805d53.png" width="450px" alt="image from gyazo"/>

- 接続が成功していることを確認
<img src="https://i.gyazo.com/e225289892a099455d2f47d3730d85c1.png" width="450px" alt="image from gyazo"/>

補足
- OpenAIのAPIキーがある人はOpenAIでもOKです
- もしGeminiで制限が来た場合は、予備としてGroqを接続するのがおすすめです  
  - [Groq コンソール](https://console.groq.com/home)

### 2-3. プロンプトの変更して、盛岡版にする）

[ベース記事](https://zenn.dev/protoout/articles/81-start-dify-chatflow)の手順に沿って、最後にプロンプトの調整をします。
- SYSTEMプロンプトを 盛岡の観光アドバイザーAIチャット を作成しましょう

プロンプト例（コピペ用）
```
## 役割
- あなたは盛岡の日帰り旅行プランナー
- 回答は必ず以下の順で出す
1) 旅程：時刻→場所→やること→移動
2) 予算合計を1行
3) 雨の日代替を2個

## 制約事項
- 前置きや質問返しは禁止
- 提案スポットは最大5つ
```
<img src="https://i.gyazo.com/e7d0a803108b67b06cf3878231a2fe89.png" width="450px" alt="image from gyazo"/>

### 2-4. 動かしてみよう（動作確認）

プレビュー画面で、以下のような質問を投げて動作確認します。

- テスト例
  - 日帰りで盛岡を楽しみたい。おすすめの回り方は？
  - 盛岡冷麺を食べたい。アクセスしやすいエリアも教えて
  - 予算3,000円、駅近、夕方から行ける観光スポットある？
- 下記画像のように、プロンプト通りの内容で盛岡について詳しく教えてもらえたら成功です。
<img src="https://i.gyazo.com/f822b0228e75f2dca8db520f41287cf5.png" width="450px" alt="image from gyazo"/>

- プロンプトを調整することで、自分が望む回答を得ることができます。
- SYSTEMにプロンプトを入れないで同じ質問をすると、下記画像のように質問返しをされるなど安定しない回答になります。
<img src="https://i.gyazo.com/17176606fdf0e03313954007d6d51ba0.png" width="450px" alt="image from gyazo"/>

## 3. Tips：プレビューでデバッグ

- まずは短いやり取りを複数回試しましょう。
- うまくいかないときの見直し順
  1. プロンプト（役割 / 制約 / 出力の形）が具体的か
  2. 質問が曖昧すぎないか（条件が足りないなら追加質問させる）
  3. モデルが想定どおりに選べているか
      <details>
      <summary>モデルの違いについて</summary>
      - たくさんのモデルがありますが、目安としては**Pro > Flash > Flash-Lite**の順に精度が高いです。

      ### 一覧（上から順番に高精度）
      - Gemini 2.5 Pro（最上位のthinkingモデル）
      - Gemini Flash Latest（最新Flashへ自動追従）
      - Gemini 2.5 Flash（推論もできる高速モデル）
      - Gemini 2.0 Flash Exp（実験版、当たり外れあり）
      - Gemini 2.0 Flash 001（固定の安定版）
      - Gemini 2.0 Flash（latest扱いになり得る）
      - Gemini Flash-Lite Latest（Flash-Lite系の最新へ自動追従）
      - Gemini 2.5 Flash-Lite（軽量・コスパ）
      - Gemini 2.0 Flash-Lite 001（軽量の固定版）
      - Gemini 2.0 Flash-Lite（※2026/03/31で終了予定）

      ### 画像生成系（文章用途とは別枠）
      - Nano Banana（画像生成寄り）
      - Gemini 2.0 Flash Preview Image Generation（画像生成用)
      </details>

## 4. チャレンジ課題（余裕がある人向け）

- `課題1.` 観光の前提質問テンプレを作ってプロンプトを改善する（予算 / 滞在時間 / 移動手段 / 興味など）
- `課題2.` 自分の興味があるテーマでチャットbotを作ろう
- `課題3.` Groqもモデルプロバイダーに追加して、切り替えて試す

## 5. まとめ

- Difyでチャットアプリを作成し、Geminiを接続して動作確認まで完了しました。

---

このページの内容は以上です。  

[◀ 目次ページ](./readme.md)
