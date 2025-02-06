---
title: "インジケーター: パトランプ"
---

**★ 極性(+ -)があるため、接続に間違いがないか注意**

![](https://ueeshop.ly200-cdn.com/u_file/UPAH/UPAH808/2108/products/14/69524b4790.jpg?x-oss-process=image/format,webp =200x)

> 出典：[Keyestudio](https://www.keyestudio.com/products/keyestudio-traffic-light-module-black-and-eco-friendly-for-arduino)

## 1. obnizでの配線

:::details 配線の仕方をクリックで開く
![](https://i.gyazo.com/8464f2e5de5bac0515ec7b4cea9d4b96.jpg =500x)

| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| GND  |  obnizの3番    |
|  G  |   obnizの4番   |
|  Y  |   obnizの5番   |
|  R  |   obnizの6番   |
:::

## 2. 使うノードとつなぎ方

:::details ノードの繋ぎ方をクリックで開く
- `injectノード`
- `changeノード`
- `obniz-functionノード`
- `debugノード`

![](https://i.gyazo.com/b234409ec7acc7448c55b56d91b21225.gif =600x)
:::

## 3. 初期化処理コードの編集

3番、4番、5番、6番に接続する例です。

```js
obnizParts.light = obniz.wired("Keyestudio_TrafficLight", {gnd:3, green:4, yellow:5, red:6});
```

## 4. 各ノードの設定方法

- `changeノード`
![](https://i.gyazo.com/e6079d428656a9f49c7dab4fa3b43343.gif =600x)

- `obniz-functionノード`

```js
obnizParts.light.single(msg.payload); //payloadの文字列がredなら赤、yellowなら黄色、greenなら緑で光らせる

return msg;
```

## 5. 結果

`injectノード`のボタンをクリックすると、赤いLEDが光ります。

`injectノード`でpayloadの設定を「green」「yellow」に変更すると、違う色のLEDが光ります。

## ■ 参考資料
[obnizの公式ドキュメント: Keyestudio TrafficLight](https://docs.obniz.com/ja/sdk/parts/Keyestudio_TrafficLight/README.md)
