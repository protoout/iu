---
title: "センサー: 照度センサー(CdS)"
---

![](https://akizukidenshi.com/img/goods/L/100110.jpg =200x)

> 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g100110/)

## 1. obnizでの配線

★極性なし

:::details 配線の仕方をクリックで開く
| 電子パーツの脚         | 接続先         |
|--------------|---------------|
|  ジャンパワイヤ赤 |   obnizの0番   |
|   ジャンパワイヤ白 |  obnizの1番    |
|   ジャンパワイヤ黒 |  obnizの2番    |


以下のように配線しましょう。

![](https://i.gyazo.com/833479cfa8c24055be4f7739560e6763.png =400x)

![](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/cbd3510a-9c8f-47eb-84c8-b99edb9c8336.jpg =400x)

![](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/1b53f227-13cb-4f93-86bc-26d7673c834c.jpg =400x)
:::

## 2. 使うノードとつなぎ方

:::details ノードの繋ぎ方をクリックで開く
- `obniz-repeatノード`
- `debugノード`

![](https://i.gyazo.com/d324617577c3c0af6a86362a49f3509b.png =500x)
:::

## 3. 初期化処理コードの編集

```js
obniz.io0.output(true); //io0番を5vに
obniz.io2.output(false); //io2番をGNDに
```

:::details 別のピンの書き換え例

赤い線を5番に、白い線を7番につなぐ場合の書き方

```js
obniz.io5.output(true); //io5番を5vに
obniz.io7.output(false); //io7番をGNDに
```

:::

## 4. 各ノードの設定方法

- `obniz-repeatノード`
    - `ad1`: Analogデータ（光の強さ）をDigital信号に変換して取得する1番、の意味

```js
const voltage = await obniz.ad1.getWait(); //ピン1からアナログ（光の強さ）をデジタル信号に変換した値を取得

msg.payload = voltage;

return msg;
```

:::details 別のピンの書き換え例

例えば、6番のピンから分圧の値を取得する場合は、`ad6`と書き換えます。 

```js
const voltage = await obniz.ad6.getWait(); //ピン6からアナログ（光の強さ）をデジタル信号に変換した値を取得
```

:::

## 5. 結果

明るさに応じてコンソールに表示されている数値が変動すれば成功です。

## ■ 参考資料
[obnizの公式ドキュメント: obniz AD](https://docs.obniz.com/ja/reference/common/ad)
