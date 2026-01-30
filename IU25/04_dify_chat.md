# Difyに触れてAIチャットアプリを作ろう

ここからは「Difyで何ができるのか」を掴むために、実際にDifyに触れてみましょう。  
このパートでは、LLMとしてGeminiを接続し、DifyでAIチャットアプリを作っていきます。  

## 1. 作るアプリケーション

### 1-1. 盛岡観光の質問をすると回答してくれるAIチャットアプリ

  <img src="https://i.gyazo.com/9968c20b8a6395091fc264e3a8e95a84.png" width="250px" alt="image from gyazo"/>

### 1-2. 全体のDifyフロー図

  <img src="https://i.gyazo.com/b2c0d6c458f5c309f29c5ba43cc9621a.png" width="450px" alt="image from gyazo"/>

## 2. ハンズオン：AIチャットアプリを作ろう

### 2-1. DifyでAIチャットアプリを作成する
1. [Dify](https://cloud.dify.ai/)を開き、ログインして下記のような画面になればOKです。

    <img src="https://i.gyazo.com/7b6715b8a0b7da4e31a694601caa4475.png" width="450px" alt="image from gyazo"/>

2. DifyのVersionが`1.11.4`になっているか、画面右上の丸いアイコンから確認しましょう。

    <img src="https://i.gyazo.com/7244bf7eb6f60446bf080717b36d5fd1.png" width="250px" alt="image from gyazo"/>

3. [Difyチャットアプリ作成ページ](https://zenn.dev/protoout/articles/81-start-dify-chatflow)に沿って、まずは、[「アプリケーションを作成しよう」](https://zenn.dev/protoout/articles/81-start-dify-chatflow#%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%92%E4%BD%9C%E6%88%90%E3%81%97%E3%82%88%E3%81%86)まで作っていきます。

  > [!CAUTION]
  > ワークフローではなく、**チャットフロー**を選んで作りましょう。
  >
  > <img src="https://i.gyazo.com/1c75f8a2e952742fcae766d4044a024e.png" width="300px" alt="image from gyazo"/>

### 2-2. LLMをGeminiのモデルに設定する

授業では、無料枠があり試作が進めやすいGeminiを利用します。  
Difyは「モデルプロバイダー」画面から、使用するLLMを追加できます。

1. [Difyモデルプロバイダー設定ページ](https://zenn.dev/protoout/books/15_dify-manual/viewer/model-setup-gemini#2-dify%E3%81%AE%E3%83%A2%E3%83%87%E3%83%AB%E3%83%97%E3%83%AD%E3%83%90%E3%82%A4%E3%83%80%E3%83%BC%E8%A8%AD%E5%AE%9A)に沿って、`セット成功`まで進めましょう。

- 事前にwordやメモ帳に控えておいたGeminiのAPIキーを使いましょう！

  <img src="https://i.gyazo.com/8709badf2c4cabba428ad6f4f03ff33c.png" width="450px" alt="image from gyazo"/>

> [!CAUTION]
> APIキーは外部に公開しないでください。

2. 下記のように、Geminiの右上のインジケーター（小さい丸）が緑なら接続OKです。

  <img src="https://i.gyazo.com/e225289892a099455d2f47d3730d85c1.png" width="450px" alt="image from gyazo"/>

3. プレビューで試す

- `プレビュー`ボタンを押すと、チャットウィンドウが開くので、「こんにちは」など何か挨拶してみましょう。
- 下記画像のように回答が返ってきたらOKです！

  <img src="https://i.gyazo.com/88bf6b20783ea0d37811226f31e08158.png" width="450px" alt="image from gyazo"/>

### 2-3. プロンプトを変更して、盛岡版にする

現時点では、AIチャットアプリは「汎用的なAI」で、質問しても回答の方向性がブレやすい状態です。  
**プロンプト（AIへの指示書）** に
- どのような役割で答えるのか（例：盛岡の旅行プランナー）
- どのような形で回答してもらいたいのか（例：旅程 → 予算 → 雨の日代替）
を入れて、 **盛岡観光の相談に寄った回答が返ってくるように設定していきます。**

1. LLMノードのSYSTEMに下記プロンプトを入れて`盛岡の観光アドバイザーAIチャットアプリ`を作成しましょう

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
- 提案スポットは2~3つ
```

<img src="https://i.gyazo.com/de4fcc0bab3a21a888fbcf42341df396.png" width="450px" alt="image from gyazo"/>

### 2-4. 動かしてみよう

1. プレビュー画面で、以下のようなメッセージを送ってみましょう。

  - 質問例
    - 日帰りで盛岡を楽しみたい。おすすめの回り方は？
    - 盛岡冷麺を食べたい。アクセスしやすいエリアも教えて
    - 予算3,000円、駅近、夕方から行ける観光スポットある？

2.下記画像のように、プロンプト通りの内容で盛岡について詳しく教えてもらえたら成功です。  
プロンプトを調整することで、自分が望む回答を得ることができます。

    <img src="https://i.gyazo.com/f822b0228e75f2dca8db520f41287cf5.png" width="300px" alt="image from gyazo"/>

  > SYSTEMにプロンプトを入れないで同じ質問をすると、下記画像のように質問返しをされるなど安定しない回答になります。
  > 
  > <img src="https://i.gyazo.com/17176606fdf0e03313954007d6d51ba0.png" width="300px" alt="image from gyazo"/>

### 2-5. 公開しよう

1. 画面右上の`公開`するをクリックし、`更新を公開`ボタンを押します

    <img src="https://i.gyazo.com/b66569ab623f4d957cd11406afea8a0d.png" width="300px" alt="image from gyazo"/>

2. `アクションが成功しました`が表示されたらOKです

    <img src="https://i.gyazo.com/5d21f62b70494405d4e139b4df38856a.png" width="300px" alt="image from gyazo"/>

3. `アプリを実行`ボタンをクリックします

    <img src="https://i.gyazo.com/bb95bb664ffadbdebbfd236a580748ea.png" width="300px" alt="image from gyazo"/>

4. 本番環境で早速試してみましょう！

    <img src="https://i.gyazo.com/ee9d791bead1cfead5dcd80dbc6f4757.png" width="300px" alt="image from gyazo"/>

## 3. Tips

3-1.  プレビューでデバッグする 
> [!TIP] 
> ※デバッグ：プログラムやシステムの中にある不具合（バグ）を見つけて、原因を特定し、直す作業のこと

- まずは短いやり取りを複数回試しましょう。

- うまくいかない時は以下を見直してみてください。
1. プロンプト（役割 / 制約 / 出力の形）が具体的か
2. 質問が曖昧すぎないか（条件が足りないなら追加質問させる）
3. モデルが想定どおりに選べているか
      <details>
      <summary>参考：モデルの違いについて</summary>
      
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

3-2. モデルプロバイダーについて

Geminiで制限が来た場合、  
OpenAIのAPIキーがある人はOpenAIでもOKです  
予備として[Groq コンソール](https://console.groq.com/home)を接続するのがおすすめです 


## 4. チャレンジ課題

### 4-1. 周りの人と共有してみよう

- どのような質問や回答を試してみたか共有してみましょう

### 4-2. プロンプトを改善して答えの質を上げてみよう

- プロンプトを変更して、回答に違いがあるか試してみましょう
  - 例：予算、滞在時間、移動手段、興味など

### 4-3. モデルを変えてみよう

[3-2. モデルプロバイダーについて](https://github.com/protoout/iu/edit/main/IU25/04_dify_chat.md#3-tips)を見ながら、モデルによって回答が変わるか確認してみましょう

### 4-4. 自分が作りたいBotの素材集めをする

- 作りたいBotのテーマを、AIチャットアプリと相談しながらイメージしてみましょう
  - 例：大学の施設案内/サークルFAQ/バイト手順/制作のチェックリストなど

## 5. まとめ

ここではDifyに触れて手軽にAIと会話ができるチャットアプリを作成しました。  
プロンプトを変更することで、自分のオリジナルチャットボットができるので、疑問の回答、雑談、作業の壁打ちなど、身近なテーマでいろいろ試してみましょう。

---

このページの内容は以上です。  

[◀ 目次ページ](./readme.md)
