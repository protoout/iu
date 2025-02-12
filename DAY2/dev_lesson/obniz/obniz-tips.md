# 複数のセンサーを使う方法  
  
## 1. 距離センサーが反応したら音を出す

### 1-1. 距離センサーとスピーカーの配線

`0,1,2,3ピン`に超音波距離センサー、`9,11ピン`にスピーカーを写真のように配線してみましょう。

> <img src="https://i.gyazo.com/53bb7be7ba1d99ed2934715654e4b1f3.png" width="400px" />
> 
  
### 1-2. 距離センサーの設定   

> [!NOTE]  
> **事前にやった超音波センサーの内容のおさらいも含まれています**  
> 条件分岐のノードが書いてあるので気になる方はやってみてください   

`obniz repeatノード`を使います。

> <img src="https://i.gyazo.com/d4fb9397dff4fbfcf93c7f26d5da1117.png" width="400px" />

次に、[超音波距離センサーのマニュアルページ](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/sensor-distance-hcsr04)を参考に`設定ノード`の初期化処理の箇所と`obniz repeatノード`に中に以下の内容をコピペします。
  
#### 1. `設定ノード`の初期化処理

```js
obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:0, echo:1, trigger:2, vcc:3 }); //0,1,2,3番にピンを割り当てる
```
  
#### 2. `obniz repeat ノード`にコードを記載

```js
msg.payload = await obnizParts.hcsr04.measureWait(); // センサーから取得した値をmsg.payloadに格納

return msg; //msg.payloadを出力
```
  
#### 3. デプロイ

距離センサーに手を近づけたりすると、デバッグノードで変化がわかります。

> <img src="https://i.gyazo.com/56b3c520396c384bbc241c2e9d05d9d4.gif" width="400px" />

これで距離センサーから値を取れました。
  
  
### 1-2. スピーカーから音を鳴らす

音を鳴らしてみます。

`obniz functionノード`を使います  

次に、[スピーカーのマニュアルページ](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/actuator-speaker)を参考に`設定ノード`と`obniz function ノード`を用意します。

`obniz function ノード`を同様に二つ用意して線で繋ぎます。

> <img src="https://i.gyazo.com/98af8e97befeb2e693aecf6ddc398ef7.png" width="400px" />
  
#### 1. `設定ノード`の初期化処理を**更新**

> [!WARNING]
> 今回は超音波センサーとスピーカーを両方使うので、初期化処理は以下のようになります。
> ピンアサインも気をつけましょう。

```js
obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:0, echo:1, trigger:2, vcc:3 }); //0,1,2,3番にピンを割り当てる
obnizParts.Speaker = obniz.wired("Speaker",{ signal:9, gnd:11 }); //←追加
```
  
#### 2. `obniz function ノード`1つ目

音を鳴らす処理です。

```js
obnizParts.Speaker.play(1000); // 1000Hz で音を鳴らす
await obniz.wait(1000); //1秒待つ
```
  
#### 3. `obniz function ノード`2つ目

音を止める処理です。

```js
obnizParts.Speaker.stop(); // 音を止める
```
  
### 3-3. 実際に動かしてみる

さて、デプロイしてみます。

問題なくいくと以下のように距離に応じて音が鳴ったり止まったりしてくれます。

> [<img src="https://i.gyazo.com/b8d54909da2960018e032e9b4df4e863.png" width="400px" />](https://twitter.com/n0bisuke/status/1789748155984052702)
> 手をかざすと音が鳴って、手を遠ざけると音が止まる
  
### 3-4. 最終系

こんな感じでステップを踏んでフローを変えてきました。

> <img src="https://i.gyazo.com/fbdcafe1eacd1e10bb644d620ab35a4a.png" width="400px" />


**[戻る](../)**
