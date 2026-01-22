# Difyで「盛岡の観光アドバイザーAIチャット」を作ろう

このパートでは、Difyでチャットアプリを作成し、授業で使うLLMとしてGeminiを接続します。  

---

## 1. このパートで作るもの「盛岡の観光アドバイザーAIチャット」

### 1-1. 作成するものの概要

- Dify上で動く「盛岡観光の相談に答えるチャットアプリ」を作ります。
- 次のパート（RAG）で「資料参照型」に拡張します。

参考リンク
- [Dify チャットフロー入門（ベース記事）](https://zenn.dev/protoout/articles/81-start-dify-chatflow)

---

## 2. Difyでチャットアプリを作るハンズオン

### 2-1. STEP1：Difyでチャットアプリを作成
- [Dify](https://cloud.dify.ai/)を開き、`始める`をクリックします。
- アカウントの作成後、ログインして下記のような画面になればOKです。
 <img src="https://i.gyazo.com/631c8c23eaca11c6e44bad392d3bbafa.jpg" width="450px" alt="image from gyazo"/>
 
- [ベース記事](https://zenn.dev/protoout/articles/81-start-dify-chatflow)に沿って、まずは、**チャットが動くところまで**作ります。  

- STEP1では、公開までやればOK
  - Difyでアプリを新規作成できている
  - チャットのプレビュー（試し会話）で1往復以上できている
  - 公開設定になっている

---

### 2-2. STEP2：モデルプロバイダーをGeminiへ接続（APIキー設定）

授業では、無料枠があり試作が進めやすいGeminiを利用します。
Difyは「モデルプロバイダー」画面から、使用するLLMを追加できます。

#### 1. GeminiのAPIキーについて

**事前に荻原先生に発行＆共有していただいたAPIキーを使いましょう！**
- 注意: APIキーは外部に公開しないでください（GitHubへ貼らない）
- [Google AI Studio](https://aistudio.google.com/apikey) を使用することで、自分でもAPIキーを発行することができます。

---

#### 2. Difyのモデルプロバイダー設定（Gemini）

- Dify管理画面を開く
<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/ec511155-8374-433c-a275-3295daaf9111.png" width="450px" alt="image from gyazo"/>

- 「モデルプロバイダー」からGeminiを選び、`セットアップ`へ
<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/4f4ab1f6-9d74-421d-917e-60e5c9b2b349.png" width="450px" alt="image from gyazo"/>

- APIキーを貼り付けて保存
<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/672eb24d-f237-433a-adf5-198e9fd459bc.png" width="450px" alt="image from gyazo"/>

- 接続が成功していることを確認
<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/c16bba01-bce4-4cd1-a98b-5e5f5c65b170.png" width="450px" alt="image from gyazo"/>

補足
- OpenAIのAPIキーがある人はOpenAIでもOKです
- もしGeminiで制限が来た場合は、予備としてGroqを接続するのがおすすめです  
  - [Groq コンソール](https://console.groq.com/home)

---

### 2-3. STEP3：プロンプトの変更（盛岡版にする）

[ベース記事](https://zenn.dev/protoout/articles/81-start-dify-chatflow)の手順に沿って、最後にプロンプトの調整をします。

- 設定のポイント
  - システムプロンプトを 盛岡の観光アドバイザー に変更する

プロンプト例（コピペ用）
```
## 役割
- あなたは盛岡の観光アドバイザーです。
- ユーザーからの質問に対して盛岡観光に役立つ情報を提供してください。

## 制約事項
- ユーザーが不快に思う返信は禁止です。
```

---

### 2-4. STEP4：動かしてみよう（動作確認）

プレビュー画面で、以下のような質問を投げて動作確認します。

- テスト例
  - 日帰りで盛岡を楽しみたい。おすすめの回り方は？
  - 盛岡冷麺を食べたい。アクセスしやすいエリアも教えて
  - 予算3,000円、駅近、夕方から行ける観光スポットある？

うまくいかないときの調整
- 返答がふわっとする → プロンプトに「最初に条件を質問してから提案する」など明記
- 店名やイベントなどが怪しい → RAGパートで「資料参照」に拡張して精度を上げる

---

## 3. Tips：デバッグのやり方（最小限）

### 3-1. プレビューでデバッグ

- まずは短いやり取りを複数回試す
- うまくいかないときの見直し順
  1. プロンプト（役割 / 制約 / 出力の形）が具体的か
  2. 質問が曖昧すぎないか（条件が足りないなら追加質問させる）
  3. モデルが想定どおりに選べているか

---

## 4. チャレンジ課題（余裕がある人向け）

- `課題1.` 会話スターターを3つ追加して、質問しやすい導線を作る
- `課題2.` 観光の前提質問テンプレを作る（予算 / 滞在時間 / 移動手段 / 興味）
- `課題3.` Groqもモデルプロバイダーに追加して、切り替えて試す

---

## 5. まとめ

- Difyでチャットアプリを作成し、Geminiを接続して動作確認まで完了しました。

---

このページの内容は以上です。  

[◀ 目次ページ](./readme.md)
