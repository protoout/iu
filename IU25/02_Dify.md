# Dify
---
## Difyとは？
- 生成AI（LLM）を使って、ノーコードでアプリを作って運用まで持っていくための開発プラットフォームです。  
  ワークフロー、RAG、連携（インテグレーション）、モニタリングなどをまとめて扱えます。
- 読み方は公式で「ディフィー」になってる

## Difyのメリット
- ノーコード / ローコードで作りやすい  
  画面操作中心でチャットボットや業務用AIアプリを組み立てられ、まず動くものを最短で作れます。
- ワークフローとエージェントで複雑な処理も組める  
  条件分岐やツール呼び出しなどをワークフロー化でき、エージェント的に自律判断させる構成も作れます。
- RAGで自社ナレッジや資料を活用できる  
  ナレッジベースを使った検索 + 生成（RAG）で、社内FAQやドキュメント参照型のAIを構築できます。
- 外部のナレッジ基盤とも連携できる  
  Dify外にあるナレッジベースをAPI経由で接続し、情報ソースを広げることも可能です。
- 目的に合わせてさまざまなLLMを選べる  
  用途に応じてLLMを切り替えながら開発できます。
- 作ったAIをいろいろな場所で使える  
  作成したアプリをデプロイして、外部システムから呼べる形（運用前提）にしやすいです。
- 運用・改善がしやすい（観測・モニタリング）  
  利用状況を見ながら改善を回しやすく、試作から本番運用への移行を意識した設計になっています。

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

- [次の資料へ](/IU25/03_rag.md)
- [前の資料へ](01_Orientation.md/)
