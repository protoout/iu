# Difyに触れてAIチャットアプリを作ろう

ここからは「Difyで何ができるのか」を掴むために、実際にDifyに触れてみましょう。
このパートでは、LLMとしてGeminiを接続し、DifyでAIチャットアプリを作っていきます。  

## 1. 作るアプリケーション

### 1-1. 作るアプリケーション

- Dify上で、ユーザーが盛岡観光の質問をすると回答してくれるAIチャットアプリ

  <img src="https://i.gyazo.com/9968c20b8a6395091fc264e3a8e95a84.png" width="250px" alt="image from gyazo"/>

### 1-2. 全体のDifyフロー図

<img src="https://i.gyazo.com/b2c0d6c458f5c309f29c5ba43cc9621a.png" width="450px" alt="image from gyazo"/>

## 2. ハンズオン：汎用的なチャットアプリを作ろう

### 2-1. DifyでAIチャットアプリを作成
1. [Dify](https://cloud.dify.ai/)を開き、ログインして下記のような画面になればOKです。

  <img src="https://i.gyazo.com/7b6715b8a0b7da4e31a694601caa4475.png" width="450px" alt="image from gyazo"/>

2. DifyのVersionが`1.11.4`になっているか確認しましょう。

  <img src="https://i.gyazo.com/3c214ed1059fe525450ebb8641138b43.png" width="250px" alt="image from gyazo"/>

3. [Difyチャットアプリ作成ページ](https://zenn.dev/protoout/articles/81-start-dify-chatflow)に沿って、まずは、[「アプリケーションを作成しよう」](https://zenn.dev/protoout/articles/81-start-dify-chatflow)まで作っていきます。
  
  > [!CAUTION]
  > ワークフローを選ぶのではなく、チャットフローで選んで作ること！
  >
  > <img src="https://i.gyazo.com/1c75f8a2e952742fcae766d4044a024e.png" width="450px" alt="image from gyazo"/>

### 2-2. LLMをGeminiのモデルに設定しよう

授業では、無料枠があり試作が進めやすいGeminiを利用します。
Difyは「モデルプロバイダー」画面から、使用するLLMを追加できます。

1. GeminiのAPIキーについて

事前にwordやメモ帳に控えておいたGeminiのAPIキーを使いましょう！

<img src="https://i.gyazo.com/8709badf2c4cabba428ad6f4f03ff33c.png" width="450px" alt="image from gyazo"/>

  > [!CAUTION]
  > APIキーは外部に公開しないでください。

2. Difyのモデルプロバイダー設定（Gemini）

- [Difyモデルプロバイダー設定ページ](https://zenn.dev/protoout/books/15_dify-manual/viewer/model-setup-gemini#2-dify%E3%81%AE%E3%83%A2%E3%83%87%E3%83%AB%E3%83%97%E3%83%AD%E3%83%90%E3%82%A4%E3%83%80%E3%83%BC%E8%A8%AD%E5%AE%9A)に沿って、`セット成功`まで進めましょう。
- 下記のように、Geminiの右上のインジケーター（小さい丸）が緑なら接続OKです。

<img src="https://i.gyazo.com/e225289892a099455d2f47d3730d85c1.png" width="450px" alt="image from gyazo"/>

補足：もしGeminiで制限が来た場合
- OpenAIのAPIキーがある人はOpenAIでもOKです
- 予備として[Groq コンソール](https://console.groq.com/home)を接続するのがおすすめです 

3. プレビューで試す

- `プレビュー`ボタンを押すと、チャットウィンドウが開くので、「こんにちは」など何か挨拶してみましょう。
- 下記画像のように回答が返ってきたらOKです！

<img src="https://i.gyazo.com/88bf6b20783ea0d37811226f31e08158.png" width="300px" alt="image from gyazo"/>

### 2-3. プロンプトの変更して、盛岡版にする）

[ベース記事](https://zenn.dev/protoout/articles/81-start-dify-chatflow)の手順に沿って、最後にプロンプトの調整をします。
- SYSTEMプロンプトを 盛岡の観光アドバイザーAIチャットアプリ を作成しましょう

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

- ここでは、公開までやればOK
  - Difyでアプリを新規作成できている
  - チャットのプレビュー（試し会話）で1往復以上できている
  
    <img src="https://i.gyazo.com/23057cb0680f982ec7932cb7f1705ef3.png" width="450px" alt="image from gyazo"/>

  - 公開設定になっている
  
    <img src="https://i.gyazo.com/b66569ab623f4d957cd11406afea8a0d.png" width="450px" alt="image from gyazo"/>

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
      - たくさんのモデルがありますが、目安としては Pro > Flash > Flash-Lite の順に精度が高いです。

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

- DifyでAIチャットアプリを作成し、Geminiを接続して動作確認まで完了しました。
  <img src="https://i.gyazo.com/5dff5672c3a73f6332d0efb8ae885c61.png" width="450px" alt="image from gyazo"/>

---

このページの内容は以上です。  

[◀ 目次ページ](./readme.md)
