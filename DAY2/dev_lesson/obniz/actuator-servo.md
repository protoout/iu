---
title: "アクチュエーター: サーボモーター（SG90）"
---

サーボモーターは角度を指定して回転させるモーターです。

**★ 極性(+ -)があるため、ピンの接続に間違えがないか注意**してください。

![](https://akizukidenshi.com/img/goods/L/108761.jpg =200x)

> 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g108761/)

## 1. obnizでの配線

ピンのアサインと実際の配線は、みなさんがやりたいことに合わせて適宜変更をしてください。
ジャンパワイヤーの色は何色でも大丈夫です。

**`obniz Board`と`obniz Board 1Y`とでピンの配列が異なるためご注意ください。**

:::details obniz Board 1Yの配線の仕方をクリックで開く
| サーボモーター         | ジャンパワイヤー         | obnizピン|
|--------------|---------------|-------|
| 茶  |   白   |  マイナス-    |
| 橙   |  赤    |  プラス+     |
| 黄   |  青    |  obniz2番     |

写真上では以下の配線にしてあります。

- サーボモーター茶 - ジャンパワイヤ白
- サーボモーター橙 - ジャンパワイヤ赤
- サーボモーター黄 - ジャンパワイヤ青

真似して配線してみてください。

![](https://i.gyazo.com/7569445e6968343962bec179da49a56c.jpg =300x)

![](https://i.gyazo.com/fe68ac7ea4bd5bd203b84ffd06ec8461.png =500x)

![](https://i.gyazo.com/78e42de894f9c2714afc006e27a0f521.png =500x)
:::

:::details obniz Board（+/-/3.3vのソケットがない方）の配線の仕方をクリックで開く
| サーボモーター         | ジャンパワイヤー         | obnizピン|
|--------------|---------------|-------|
| 茶  |   白   |  obniz0番   |
| 橙   |  橙    |  obniz1番    |
| 黄   |  緑    |  obniz2番     |

写真上では以下の配線にしてあります。

- サーボモーター茶 - ジャンパワイヤ白
- サーボモーター橙 - ジャンパワイヤ橙
- サーボモーター黄 - ジャンパワイヤ緑

真似して配線してみてください。

![](https://i.gyazo.com/3d8108c40d25a72f0ad229092217f4dc.jpg =500x)
:::

## 2. 使うノードとつなぎ方

[Node-REDのobnizノードでどちらのノードを選ぶか - 使い方概要](https://qiita.com/n0bisuke/items/072a8a1bf77525fef835)を参考に、使うobnizノードを決めます。今回はアクチュエーターになるので`obniz-functionノード`が適しています。

:::details ノードの繋ぎ方をクリックで開く
### 2-1. obniz-functionノードの基本

まずは、以下の3つのノードを使います。

- `injectノード`
- `obniz-functionノード`
- `debugノード`

以下のように設置して線で繋ぎましょう。

![](https://i.gyazo.com/2eb9c633060a8af0e92642a3e30d0be3.gif =400x)

`obniz-functionノード`を追加したら**obniz IDの設定**を忘れずに行って下さい。この設定も[参考記事](https://qiita.com/n0bisuke/items/072a8a1bf77525fef835)を読んでおきましょう。

### 2-2. changeノードを追加

次に`changeノード`を追加して`20`などの数字を代入します。
代入する値の項目を`数値`に変更しましょう。

![](https://i.gyazo.com/27f6c8330de4b466778b7ee5d6b3d800.gif =400x)
:::

## 3. 初期化処理コードの編集

`obnizノード`の初期化処理の項目に以下を記述します。

パーツ単体で動かす時は上書きし、他のパーツとセットで動かす時は上書きではなく追記しましょう。

`obniz Board 1Y`の場合:

```js
obnizParts.servo = obniz.wired("ServoMotor",{ signal:2 }); //サーボモーターをどのくらい回すかの信号を2番に設定
```

:::details obniz Board（+/-/3.3vのソケットがない方）の場合

```js
obnizParts.servo = obniz.wired("ServoMotor", {gnd:0,vcc:1,signal:2}); //GNDに0番, 電源供給に1番,サーボモーターをどのくらい回すかの信号を2番に設定
```

:::

## 4. 各ノードの設定方法

- `obniz-functionノード`

```js
obnizParts.servo.angle(msg.payload); //msg.payloadの角度にサーボモーターを動かす

return msg //msgを出力
```

## 5. 結果

デプロイして実行し、`injectノード`のボタンを押すとサーボが1回だけ動きます。

### 5-1. 補足

サーボモータは角度を指定して動くので、次に動かす時は`changeノード`の数値を変えて実行してみましょう。

今回利用しているSG90というサーボモータは仕様上0~180度までしか動作しないです。そのため0~180の値を指定して試してみましょう。

## ■ 参考資料

[obnizの公式ドキュメント: サーボモーター](https://docs.obniz.com/ja/sdk/parts/ServoMotor/README.md)
