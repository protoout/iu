# インジケーター: LED

<img src="https://akizukidenshi.com/img/goods/L/112519.jpg" width="40%" />

> 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g112519/)

ピンのアサインと実際の配線は、みなさんがやりたいことに合わせて適宜変更をしてください。

## 1. obnizでの配線

**★ 極性(+ -)があるため、接続に間違いがないか注意**

<details>

<summary>配線の仕方をクリックで開く</summary>


<img src="https://i.gyazo.com/72603bdeeae78020b1a3625f06044b6d.png" width="40%" />

| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| LEDの長い脚（アノード +）  | obnizの0番    |
| LEDの短い脚（カソード -）  | obnizの1番    |

</details>

## 2. 使うノードとつなぎ方

<details>

<summary>ノードの繋ぎ方をクリックで開く</summary>

- `injectノード`
- `obniz-functionノード`

<img src="https://i.gyazo.com/590a12c00834a74480a8e79cdf270b7e.png" width="40%" />

</details>

## 3. 初期化処理コードの編集

```js
obnizParts.led = obniz.wired('LED', { anode:0, cathode:1 }); //脚の長い方（アノード, +）を0, 脚の短い方（カソード,-）を1に割り当てる
```

## 4. 各ノードの設定方法


### 4-1. 単純な点灯

- `obniz-functionノード`のコード

```js
obnizParts.led.on(); //ledをONにする

return msg;
```

### 4-2. 消灯

- `obniz-functionノード`のコード

```js
obnizParts.led.off(); //ledをONにする

return msg;
```

### 4-3. 単純な点滅

- `obniz-functionノード`のコード

```js
obnizParts.led.on(); //ledをONにする
obniz.wait(1000); //1秒(1000ミリ秒)待つ
obnizParts.led.off(); //ledをONにする

return msg;
```

## 5. 結果

点灯、消灯、点滅などができます。

## ■ 参考資料
[obnizの公式ドキュメント: LED](https://docs.obniz.com/ja/sdk/parts/LED/README.md)


----

# インジケーター: フルカラーLED（WS2811）

![](https://akizukidenshi.com/img/goods/L/108412.jpg =200x)

> 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g108412/)

RGBの値を指定することで、フルカラーで光るLEDです。

## 1. obnizでの配線

**★ 極性(+ -)があるため、接続に間違いがないか注意**

:::details 配線の仕方をクリックで開く

フルカラーLEDのピンは4本あり、この写真のように置きましょう。このスタートが重要です。

![](https://i.gyazo.com/5e4ff0d2a567250f2f8761b2c8a9f2f1.jpg =500x)

- LEDのピンを上方向にしたとき、脚の長さが「短・長・中・短」の順となる角度にLEDをまず置きます。
- その状態で、1番左のピンを軽く曲げてしまいます。（使用しないピンです）
    - 1番左のピンは利用しないため、目印に曲げておきます。

![](https://i.gyazo.com/0253a0e95e62455c88f0f60194dcdf75.jpg =500x)

| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| 折り曲げた脚  | (利用しない)   |
| 一番長い脚  | obnizの0番    |
| 中ぐらいの脚  | obnizの1番    |
| 一番短い足  | obnizの2番    |

:::

## 2. 使うノードとつなぎ方

:::details ノードの繋ぎ方をクリックで開く

- `injectノード`
- `obniz-functionノード` 

![](https://i.gyazo.com/590a12c00834a74480a8e79cdf270b7e.png =600x)

:::

## 3. 初期化処理コードの編集

```js
obnizParts.rgbled = obniz.wired('WS2811', {gnd:0, vcc: 1, din: 2});
```

## 4. 各ノードの設定方法

- `obniz-functionノード`のコード例 赤

```js
obnizParts.rgbled.rgb(255, 0, 0); //赤く光らせる
```

- `obniz-functionノード`のコード例 緑

```js
obnizParts.rgbled.rgb(0, 255, 0); //緑に光らせる
```


- `obniz-functionノード`のコード例 黒（消灯）
    - 0,0,0に指定するとLEDを消せます。

```js
obnizParts.rgbled.rgb(0, 0, 0);
```

## 5. 結果

`injectノード`のボタンを押すと指定した色に光ります。

## ■ 参考資料

[obnizの公式ドキュメント: WS2811](https://docs.obniz.com/ja/sdk/parts/WS2811/README.md)

