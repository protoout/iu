# 3.miiboとLINEを連携する

### LINEdevelopersにログインする
https://developers.line.biz/ja/

### コンソールから事前に作ったプロバイダーの中のチャネルを開く
<img src="https://i.gyazo.com/6ab44ffa9a4744ccbed2a54094ad6af6.png" width="450px" alt="image from gyazo"/>

## 1.LINEの情報を取得する
1. 「チャンネル基本設定」のタブから「チャンネルシークレット」を取得する
    発行されていなければ、「発行」ボタンをクリックして文字列をコピーします。
    コピーしたら、パソコンに搭載されているメモ帳、付箋、Wordなどに貼り付けて控えておきましょう。
<img src="https://i.gyazo.com/4d45ad3a58b8abb7770fa1af718ab784.png" width="450px" alt="image from gyazo"/>
<img src="https://i.gyazo.com/8aa805cce8792c525f2ac1e04a151ca0.png" width="450px" alt="image from gyazo"/>

1. 「messageing API設定」のタブから「チャンネルアクセストークン」を取得する
    発行されていなければ、「発行」ボタンをクリックして文字列をコピーします。
    こちらもコピーしたら、メモ帳、付箋、Wordなどに貼り付けて控えておきましょう。
<img src="https://i.gyazo.com/7f302b0956c1aad41c0bc2a4de975328.png" width="450px" alt="image from gyazo"/>
<img src="https://i.gyazo.com/5f707875217adfc29bf322a485029573.png" width="450px" alt="image from gyazo"/>
   
    応答メッセージとあいさつメッセージが無効になっていることを確認してください。  
<img src="https://i.gyazo.com/f8a24c530b76d92b20e898a1229188b6.png" width="450px" alt="image from gyazo"/>
   
    挨拶メッセージは有効になっている方がおススメとのことで、右端の編集ボタンからオンにしておきましょう。
<img src="https://i.gyazo.com/f4ad4a98705b79ec5e7ddf9a3231e286.png" width="450px" alt="image from gyazo"/>  
<img src="https://i.gyazo.com/a49afca099e1f8030ed3ecc8daf838b9.png" width="450px" alt="image from gyazo"/>

## 2.miiboにLINEの情報を登録する
1. miiboのエージェントページに移動する
1. 左のメニューバーから「外部サービス連携」をクリックする
<img src="https://i.gyazo.com/87a6864e9fb3985633eb5157cf319229.png" width="450px" alt="image from gyazo"/>

1. 「LINE上で会話する」ボタンをクリックする
<img src="https://i.gyazo.com/76f66b6b4d40add359ad2345dfbc55d6.png" width="450px" alt="image from gyazo"/>

1. 先ほど取得した「チャンネルシークレット」と「チャンネルアクセストークン」を貼り付け、「LINEと連携する」ボタンをクリックする
<img src="https://i.gyazo.com/b7dc30f134392ab6176097f27a4e8fb7.png" width="450px" alt="image from gyazo"/>


## 3.LINEにWebhook URLを登録する
1. miiboで発行された「Webhook URL」をコピーする
    Webhookとは、サービス（アプリケーション）の何らかのアクションを他のアプリケーションへリアルタイムに通知する仕組みのことです。

1. LINEのチャネルページへ移動する
1. 「messageing API設定」のタブからWebhook設定をする
<img src="https://i.gyazo.com/7f302b0956c1aad41c0bc2a4de975328.png" width="450px" alt="image from gyazo"/>

1. 「編集」ボタンをクリックする
<img src="https://i.gyazo.com/2dc501d6a7c30fe75ce8d6572657ecf0.png" width="450px" alt="image from gyazo"/>

1. 先ほどコピーしたWebhook URLを貼り付け、「更新」ボタンをクリックする
<img src="https://i.gyazo.com/e7ee66e8691b50ce00405eda49deee39.png" width="450px" alt="image from gyazo"/>

1. Webhookの利用ボタンをクリックし、オンにする
<img src="https://i.gyazo.com/88de95e073afa7218f78e883e8fa3d4d.png" width="450px" alt="image from gyazo"/>

1. 「検証」ボタンをクリックし、「成功」の表示から連携完了を確認する
<img src="https://i.gyazo.com/2699f7e4370f7140e2b8ff2e12e9a805.png" width="450px" alt="image from gyazo"/>

# いったん完成
### LINEから会話する
スマートフォンで、友達になったLINE Botへ何かを送信し、返答がくるのを確認しましょう。
<img src="https://i.gyazo.com/7b3929bf5dd796a84f81600102e18709.png" width="450px" alt="image from gyazo"/>

miiboとLINE Botが連携され、会話型AIが完成しました。
ここからオリジナリティを出していきましょう。


