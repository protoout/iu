---
DifyでWebhookトリガーでLINE Botを作ってみた
---
Webhookトリガーが使えるようになったので外部のプラグインを使わずにLINE Botのリプライが作れそうですね。

こんな感じでトリガーと適当なノードを用意してまずはテストランをします。

> ![CleanShot 2025-12-25 at 12.36.11.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/79ceeee9-2dcb-4414-bb31-513f2a8fb39a.png)

ページ下部の`変数検査`に`_webhook_row`というキーが表示されているので、こちらをみてみます。

> ![CleanShot 2025-12-25 at 13.39.53.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/0d88e674-2454-4ba9-bb67-aeb165c406b3.png)


以下は省略版。

`body`の中を見ると良さそうですね。

```json 
{
//省略

  "body": {
    "destination": "U123e6ec1fe70658b2de7f8d1d1823006",
    "events": [
      {
        "type": "message",
        "message": {
          "type": "text",
          "id": "593588425774071895",
          "quoteToken": "LRkHUlHjkhgbk...",
          "markAsReadToken": "Xmr5b6J8kB1Yy1IHJhholXbJKESJLcDsvSNb...",
          "text": "aaa"
        },
        "webhookEventId": "01KD9WW8YQ8ZBGGE00H1XPE05D",
        "deliveryContext": {
          "isRedelivery": false
        },
        "timestamp": 1766637576666,
        "source": {
          "type": "user",
          "userId": "Ud267f...."
        },
        "replyToken": "740258f39e7e48a2b0199f3a8ef3927a",
        "mode": "active"
      }
    ]
  },
  "files": {}
}
```

## シンプルなリプライを作ってみる


https://qiita.com/n0bisuke/items/0ab7b3b38557384370ed

https://qiita.com/n0bisuke/items/80c0ba160869f982633c

### 環境変数にトークンを入れておく

今回の例だと署名検証してないのでアクセストークンだけでOKですがシークレットとアクセストークン両方セットしておきました。

> ![CleanShot 2025-12-25 at 12.55.54.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/c2f6dff0-f919-4d44-8156-9e6988a00e9a.png)

> ![CleanShot 2025-12-25 at 12.56.31.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/1555abe3-c8a5-458c-9ec6-073a2adbebcf.png)


### 変数の処理

コード実行でreplyTokenとユーザーから送られてきたメッセージを取得します。

```js
function main({webhook_row}) {
    const webhook_body = webhook_row.body;
    const event = webhook_body.events[0];

    return {
        webhook_body: webhook_body,
        replay_token: event.replyToken,
        userMessage: event.message.text
    }
}

```

設定はこんな感じ

> ![CleanShot 2025-12-25 at 13.42.54.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/5055ee40-ae3b-4fdc-a70e-3b5fd372268f.png)

### HTTPノードでリプライをする

- APIエンドポイント: `https://api.line.me/v2/bot/message/reply`
- ヘッダー
    - Authorization: Bearer <CH_ACCESS_TOKEN>
	- Content-Type: application/json

> ![CleanShot 2025-12-25 at 13.43.44.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/51c65a3e-27f6-435a-b0ee-d54ec07b71c3.png)

リクエスト本体はJSONを指定して以下のよう（画面スクショも参照）に書きます。

```json
{
"replyToken": "{{#1766636742410.replay_token#}}",
 "messages":  [{
        type: 'text',
        text: "{{#1766636742410.userMessage#}}"
  }]
}
```

### おうむ返し

これで無事におうむ返しができました。

> ![CleanShot 2025-12-25 at 13.47.32.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/cff1b7fe-34a8-4de1-8942-03d0b11e4bb9.png)

### 公開時とテスト時でWebhookのURLを変更

- 公開時のトリガーURL: `https://trigger.ai-plugin.io/triggers/webhook/~~~~~`
- テスト時のトリガーURL: `https://trigger.ai-plugin.io/triggers/webhook-debug/~~~~~`

> ![CleanShot 2025-12-25 at 14.07.14.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/d2377e34-77ba-4aef-8553-f8746514478d.png)

という形でURLが分かれてるので最後に公開する際には公開時のURLに切り替えましょう。

> ![CleanShot 2025-12-25 at 14.13.57.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/a1fb4c91-56bf-4203-ae0e-065696830edb.png)

## 所感

変数検証の機能が便利ですね...! 

> ![CleanShot 2025-12-25 at 14.06.36.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/cbbe363f-301e-407c-afb6-69256f16f60d.png)

HTTPリクエスト後んbodyの中身などもみれてデバッグがやりやすくなりました。

> ![CleanShot 2025-12-25 at 14.21.07.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/0d70e8db-01e6-45f6-acb9-3d0fb53db434.png)


DSLはこちらに置いておきます。

`https://gist.githubusercontent.com/n0bisuke/f401e969559b8e27034d0eb55efc95e1/raw/1dfe2bd83e8f703968e2171d6c3e038cb8c9b758/line-dify-reply.yml`


署名検証はトライしたけどちょっと厳しそうだったのでその話はまた別記事で。

とはいえWebhookトリガー便利！色々なサービスと繋げられそうな雰囲気です。

---
LINE Notifyを使わずDifyだけでLINEにメッセージを送信する
---
Dify単体でLINEにメッセージ送信をしたいと思います。
Difyのバージョンは0.15.3です。

## 完成イメージ

こんなワークフローです。

> ![CleanShot 2025-02-26 at 18.31.00.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/987471df-b273-4423-a431-28363e1bb0d4.png)

https://x.com/n0bisuke/status/1894682181903040610

## 準備

- Difyのワークフロー作成ができる環境
- LINE Botのアカウント
    - チャンネルアクセストークン
    - 自身へ送信する際のUserId

これらが必要です。



## 解説

大きく分けて

- 初期設定（開始ノードと環境変数）
- コードノード1
- コードノード2
- HTTPノード

の3つを利用しています。

> ![CleanShot 2025-02-26 at 18.38.13.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/23c91760-5ebc-4a6e-b261-18ff38ab5157.png)

### 0. 初期設定

- 開始ノード

開始ノードには、ユーザーに送信するメッセージを設定するための文字列変数を設定しておきます。sendMessageという名前にしました。

> ![CleanShot 2025-02-26 at 18.42.36.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/8a0f5369-0bc2-4235-a846-a3e41a1521a5.png)

- 環境変数

また、誰に送信するのか投稿先のIDを設定する必要がありますが、`to`という名前の環境変数を設定し、認証のLINE Botのチャンネルアクセストークンは`line_channel_access_token`という名前にしておきます。

> ![](https://i.gyazo.com/4a64899f87341e4ad15ceaa991e96aed.png)

投稿先のIDは自身のユーザーIDを設定すると試しやすいです。LINE DevelopsersのBOT管理画面内の`チャネル基本設定`にある`あなたのユーザーID`と書いてあるものが自身のユーザーIDです。

> ![CleanShot 2025-02-26 at 18.46.46.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/65b39a6d-f5a2-43cf-b3ae-45506531495d.png)
> チャンネルアクセストークンは`チャネル基本設定`の右隣のタブの`Messaging API設定`の中に記載があります。

### 1. コードノード1 - Message Objectの作成

[LINE Messaging APIのPushメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)のページなどを見るとMessaging APIに送信するメッセージオブジェクトという形式が分かります。

```json
[
        {
            "type":"text",
            "text":"Hello, world1"
        },
        {
            "type":"text",
            "text":"Hello, world2"
        }
]
```

こんな形式です。

- 入力変数: to（環境変数で指定したto）, sendMessage（開始ノードで設定したsendMessage）

> ![CleanShot 2025-02-26 at 18.40.16.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/cddd2cfd-ebf3-4f56-b859-cfc5c6d8c3b8.png)

```js
function main({to, sendMessage}) {
    const messageObj = {
        "to": to,
        "messages":[
            {
                "type":"text",
                "text": sendMessage
            }
        ]
    };

    return {result: JSON.stringify(messageObj)};
}
```

※わかる人向け

ちなみにここで`コードノード`を使わずに`HTTPノード`に設定するだけでもよかったのですが、[メッセージオブジェクトの検証](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-push-message)を応用的にしたいかもなと思ったので手前でメッセージオブジェクトの作成をしています。

### 2. コードノード2 - X-Line-Retry-Keyの生成（スキップしてもOK）

ここでは[リトライ用のリトライキー](https://developers.line.biz/ja/docs/messaging-api/retrying-api-request/)として、UUIDを生成しています。

なくても動くのでスキップしてもOKですが、その場合HTTPノードのヘッダーも削除します。
入力変数は特にないです。

※Claude 3.7に書いてもらいました。

```js
/**
 * 環境に応じて最適なUUID生成方法を使用
 * @returns {string} 生成されたUUID
 */
function generateUUID() {
    // 方法1: crypto.randomUUID()を試す（Node.js 14.17.0以降で使用可能）
    if (typeof crypto !== 'undefined' && typeof crypto.randomUUID === 'function') {
        return crypto.randomUUID();
    }
    
    // 方法2: Node.jsのcrypto moduleを使用
    try {
        const crypto = require('crypto');
        return crypto.randomUUID();
    } catch (e) {
        // crypto moduleが使用できない場合は次の方法を試す
    }
    
    // 方法3: crypto.getRandomValues()を試す
    if (typeof crypto !== 'undefined' && typeof crypto.getRandomValues === 'function') {
        const buffer = new Uint8Array(16);
        crypto.getRandomValues(buffer);
        
        // UUID v4標準に準拠するように特定のビットを調整
        buffer[6] = (buffer[6] & 0x0f) | 0x40;  // version 4
        buffer[8] = (buffer[8] & 0x3f) | 0x80;  // variant RFC4122

        // UUIDフォーマットに変換
        let uuid = '';
        for (let i = 0; i < 16; i++) {
            uuid += buffer[i].toString(16).padStart(2, '0');
            if (i === 3 || i === 5 || i === 7 || i === 9) {
                uuid += '-';
            }
        }
        return uuid;
    }
    
    // 方法4: Math.random()を使用（フォールバック）
    return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
        const r = Math.random() * 16 | 0;
        const v = c === 'x' ? r : (r & 0x3 | 0x8);
        return v.toString(16);
    });
}

function main() {
    // 環境に応じて最適なUUID生成方法を選択
    const uuid = generateUUID();
    
    return {
        result: uuid
    }
}
```

> ![CleanShot 2025-02-26 at 18.52.49.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/0628a3e0-b056-461b-8455-d1f5f96ef0fa.png)

### 3. HTTPノード - メッセージの送信本体

本体です。 ヘッダーの`Authorization`キーに対して値が`Bearer {チャンネルアクセストークン}`という形式にするところが注意ポイントな気がします。Bearerの後はスペースが必要です。

- メソット: POST
- URL: `https://api.line.me/v2/bot/message/push`
- ヘッダー: 
    - `Authorization`: `Bearer {環境変数に入れたチャンネルアクセストークン}`
    - `X-Line-Retry-Key`: `{コードノード2つ目の結果のUUID}`
- ボディ: JSON指定、{コードノード1つ目の結果のメッセージオブジェクト}
  
> ![CleanShot 2025-02-26 at 18.56.28.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/35387/4209193b-af11-4311-9be6-62bb21428c32.png)


## まとめ

LINE Notifyを使わずにPushメッセージでLINEに送信する仕組みを作りました

たぶん動く（試してない）DSLをおいておきます。

> https://gist.github.com/n0bisuke/50b06c279f5ce74e4162eea9c52f5c2c

これをワークフロー公開してツールとして使えるようにしておけば結構便利な気がしますね。




## 6. GPT5かgpt-ossも使ってみる（おまけ）
- Hugging FaceのAPIでgpt-oss使ってみましょう
- GPT5 APIキーあればいける

---

## 7. 自由時間
- 色々作ってみてね

---

## 8. まとめ
- DifyでAIチャットアプリ作れた
- RAG機能も使ってみた
- LINE Bot作れた

