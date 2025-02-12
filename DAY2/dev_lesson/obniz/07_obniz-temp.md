---
title: "センサー: 温度センサー（LM60）"
---

![](https://akizukidenshi.com/img/goods/L/102490.jpg =200x)

> 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g102490/)

温度センサLM60BIZ/LM60CIMです。センサで取得した温度を知ることができます。

## 1. obnizでの配線

:::details 配線の仕方をクリックで開く
![](https://docs.obniz.com/ja/sdk/parts/LM60/wired.png =400x)

**★ 極性(+ -)があるため、接続に間違えがないか注意**

| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
|  Gnd |  obnizの0番    |
|  output  |   obnizの1番   |
|  Vcc  |   obnizの2番   |
:::

## 2. 使うノードとつなぎ方

:::details ノードの繋ぎ方をクリックで開く

- `obniz-repeatノード`
- `debugノード`

![](https://i.gyazo.com/f12a5b25d4c360c7e545ededed17019e.png =520x)
:::

## 3. 初期化処理コードの編集

0番,1番,2番に接続する例です。

```js
obnizParts.lm60 = obniz.wired("LM60", { gnd:0 , output:1, vcc:2});
```

## 4. 各ノードの設定方法

### `obniz-repeatノード`

- コードを以下に書き換えます。
    - `getWait()`を利用して、温度センサの値を一度だけ取得します

```js
msg.payload = await obnizParts.lm60.getWait(); //温度センサの値を一度だけ取得します

return msg; //msgの値を次のノードに受け渡し
```

- `interval(ms)`の値を書き換えます。
    - 単位はms（1000ms = 1秒）です。
    - 1秒に1回取得する場合の設定です。

> ![](https://i.gyazo.com/1dc5aa3fb71c0eebb810a1e19f929b7b.png =600x)

## 5. 結果

コンソールに温度の数値がでてくれば成功です！

## ■ 参考資料

[obnizの公式ドキュメント: 温度センサー LM60](https://docs.obniz.com/ja/sdk/parts/LM60/README.md)

https://zenn.dev/protoout/articles/70-obniz-nodejs-lm60biz
