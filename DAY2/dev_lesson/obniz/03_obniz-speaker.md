# アクチュエーター: スピーカー（ブザー）

 <img src="https://akizukidenshi.com/img/goods/L/104118.jpg" width="40%" />

> 出典：[秋月電子通商](http://akizukidenshi.com/catalog/g/gP-04118/)

## 1. obnizでの配線

<details>

<summary>配線の仕方をクリックで開く</summary>

<img src="https://i.gyazo.com/081b807593f7bf2ab4725e5d44952a99.jpg" width="40%" />

★ 極性(+ -)なし

| 電子パーツの脚         | 接続先         |
|--------------|---------------|
| スピーカーの脚 |   5   |
| スピーカーの脚  |   6   |

</details>

## 2. 使うノードとつなぎ方

<details>

<summary>使うノードとつなぎ方をクリックで開く</summary>

- `injectノード`
- `changeノード`
- `obniz-functionノード`
- `debugノード`


<img src="https://i.gyazo.com/86af5bb0ab066922e2c2ca830eb03244.gif" width="40%" />

</details>

## 3. 初期化処理コードの編集

5番と6番に接続する例です。

```js
obnizParts.speaker = obniz.wired("Speaker",{ signal:5, gnd:6 }); 
```

## 4. 各ノードの設定方法

- `changeノード`

msg.payloadを「数値」「500」（数字は任意で変更してください。単位はヘルツ。）

<img src="https://i.gyazo.com/cb0e5bf464ca48dd7ed5450fd7886c5e.gif" width="40%" />

- `obniz-functionノード`

```js
obnizParts.speaker.play(msg.payload); // msg.payloadで受け取った値（ヘルツ）の音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.speaker.stop(); //止める
```

## 5. 結果

1000Hzの音が鳴り、1秒すると止まる。

## ■ 参考資料
[obnizの公式ドキュメント: スピーカー](https://docs.obniz.com/ja/sdk/parts/Speaker/README.md)

- 音階の表

| 音階 | 周波数[Hz] |
| ---- | ---------- |
| ド   | 523        |
| レ   | 587        |
| ミ   | 659        |
| ファ | 698        |
| ソ   | 784        |
| ラ   | 880        |
| シ   | 988        |
| ド   | 1046       |

ドレミを1秒ずつ鳴らすサンプル

```js
obnizParts.speaker.play(523); // ドの音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.speaker.play(587); // レの音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.speaker.play(659); // ミの音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.speaker.stop(); 
```
