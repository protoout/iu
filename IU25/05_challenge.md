# 05. 応用課題

リッチメニューという機能を使うとLINE Botの見栄えが格段に上がります。  
特にプログラムが必要とかでもなく設定からいけるので、やれる人はチャレンジしてアプリケーションとしての使い勝手を上げましょう。

- LINE公式アカウント（LINE Official Account Manager）リッチメニューを作成するマニュアル｜LINEヤフー for Business  
  https://www.lycbiz.com/jp/manual/OfficialAccountManager/rich-menus/

プログラム的に制御もできます

- リッチメニューを使う（LINE Developers）  
  https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/

![LINEリッチメニュー](https://i.gyazo.com/669a86b1940aa84ba5da6098e37057b0.png)

---

## まとめ

この資料では、Difyで作成したAIをLINE Botとして利用できるようにする手順を学びました。ポイントを整理すると以下の通りです。

- DifyのAIをLINE Bot化できる  
  Difyで公開したチャットアプリを、LINEの公式アカウントと接続することで、身近なLINE上で利用可能になります。

- プラグインを活用した連携  
  Difyのプラグイン機能を使うと、LINEをはじめとした外部サービスと簡単に連携可能です。  
  今回はLINEプラグインを導入し、設定を行うことでAIをLINE Botとして動かせました。  
  ※安定稼働のため、LINEプラグインはバージョン0.0.4を利用するのが推奨です。

- Webhookの設定でLINEと接続完了  
  LINE Developersに発行されたWebhook URLを設定し、検証で成功が表示されれば、実際にLINE Botとして利用可能になります。

- 応用と拡張性  
  リッチメニューを設定することでUIを改善したり、他のノーコードツールやプログラムを組み合わせて拡張することもできます。  
  Difyを中核に据えれば、SlackやNotionなど他サービスとの連携も広がります。

今回のハンズオンで、DifyとLINE Botの連携の基本的な流れを体験できました。  
今後はリッチメニューや追加機能を試しながら、より使いやすいBotを作っていきましょう。

- [前の資料へ](/IU25/04_liinebot.md)
