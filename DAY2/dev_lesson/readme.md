## IoTの世界に飛び込もう！obnizとNode-REDで手を動かして学ぶIoT

### 事前準備 

<details><summary>事前準備確認</summary>

#### 1. Node-REDのおさらいと予習
  Day1 で触れた Node-RED の内容を学んでください。リンクは[こちら](../..//DAY1/dev_lesson/node-red)
  
  ![image](https://github.com/user-attachments/assets/00139787-1a36-456f-8423-ecae8688c26b)
  
#### 2. obnizの Wi-Fi 接続
  既に実施しているかもしれないので、設定が必要な方のみ。リンクは[こちら](./obniz/00_wifiset_obniz.md)

#### 3. 使うツール
  今回必要なものを記載しているので、念のため確認をお願いします。リンクは[こちら](./tools.md)

</details>

----
  
### 今日はハードウェアにチャレンジします【13:15〜13:20】  

0. [自己紹介](https://www.canva.com/design/DAGegVdPr2U/fbcdfSy6tN4Fwq-TduD3Xw/edit?utm_content=DAGegVdPr2U&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)
    
2. この授業でやること・ゴール  
     
   **やること:** IoTデバイスを簡単に開発・制御できるデバイス( obniz )を使って、プロトタイピングを企画・制作・発表する
     
   **ゴール:** アイデアをカタチにする楽しさを感じつつ、つくる感覚を身に着ける
     
3. タイムテーブル  
  
    | 時間        | 内容                                       |
    |-------------|--------------------------------------------|
    | 13:20-14:20 | Lesson01 obnizをはじめよう |
    | 14:30-14:40 | Lesson02 横井さんからTips紹介 | 
    | 14:40-15:15 | Lesson03 これまで学んだことを使ってIoTプロトタイプを作ってみよう | 
    | 15:15-15:45 | Lesson04 成果物を発表しよう！ | 
  
----  
    
### Lesson01 obnizをはじめよう 【13:20〜14:20】

**やること:** obnizの基本的な使い方を学びいくつかの電子パーツを動かす

**ゴール:** 授業のペースに乗って、手を動かして実働させる体験をする  

1. [obnizをはじめよう](./obniz/01_start_obniz.md)
   
2. [LEDを光らせてみよう](./obniz/02_obniz-LED.md)
     
     早く終わった方はこちらの課題にも挑戦してみてください  
     👨‍💻 応用課題: ほぼ同じ流れ！スピーカーを鳴らしてみよう  [参考](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/actuator-speaker)  
     
3. [サーボモーターを動かしてみよう](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/actuator-servo)
       
     **`obniz-close` で停止を確認して次へ！**
       
     早く終わった方はこちらの課題にも挑戦してみてください  
     👨‍💻 応用課題: 連続でサーボモーターを動かしてみよう  [参考](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/turorial-servo-keep-moving)  
      
4. [超音波測距センサーで距離を取得しよう](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/sensor-distance-hcsr04)  
       

     早く終わった方はこちらの課題にも挑戦してみてください  
     👨‍💻 応用課題: 手を近づけたら好きな言葉が出力されるようにする (ヒント無し！🥶)
     
     **`obniz-close` で停止を確認して次へ！**
     `obniz-repeat`を停止するノードは下図の通り  
     <img width="50%" alt="image" src="https://github.com/user-attachments/assets/d0b9eb11-774f-4e43-8b99-96ca2c4d0d1c" />  

       
6. 自由につくってみよう！  
    例題を用意しました！挑戦してみたいことがあればこの例以外のものでも構いません！
     - スピーカーで曲を作ってみよう
     - ものが近づいたらLEDを光らせてみよう

> [!TIP]
> 他のセンサーの動かし方はこちらにまとまっています

#### [obniz x Node-REDマニュアル](https://zenn.dev/protoout/books/07_node-red-obniz)

この資料の中にある「インジケーター: LED」「アクチュエーター: サーボモーター（SG90）」「センサー: 超音波距離センサー（HC-SR04）」をやりました！

これらのセンサーの使い方も載っています！
  - スピーカー（ブザー）
  - 照度センサー
  - 温湿度センサー
  - LEDの応用
  - サーボモーターの応用

> [!NOTE]
> もしobnizで複数のパーツを同時に使いたい時は[こちら](./obniz/obniz-tips.md)を参考にしてください

----

  
### 休憩タイム🍵  

  
----
### Lesson02 【14:30〜14:40】

#### ～横井さんからTips紹介～

----

### Lesson03 これまで学んだことを使ってIoTプロトタイプを作ってみよう【14:40〜15:15】

**やること:** 今日学んだことをフル活用して、アイデアを形にしてみましょう  
  
**ゴール:** 企画と技術の両面を見て簡単なプロダクトに落とし込む

**フォーマット:**  
- 制作物
> [!CAUTION]
> パワーポイントなどの資料を作成する必要はありません

他のセンサーも紹介します！  
  - 温湿度センサー
  - 照度センサー

制作に移る前に、[こちら](https://docs.google.com/spreadsheets/d/1yLajd9JEMNv0urU73ieXg5O-b04ziGM9nMxa_579_3A/edit?pli=1&gid=1573507651#gid=1573507651)のスプレッドシートに制作案を記載してください！   
  
![image](https://github.com/user-attachments/assets/d6c482fc-82a2-4d39-83ba-8ec815cce5bb)


#### 2つのセンサを使う初期化コード例
１．超音波センサとスピーカー
```
obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:0, echo:1, trigger:2, vcc:3 }); //超音波センサ　0,1,2,3番にピンを割り当てる
obnizParts.Speaker = obniz.wired("Speaker",{ signal:9, gnd:11 }); //スピーカー　9,11番にピンを割り当てる
```
2. 温湿度センサとLED
```
obnizParts.led = obniz.wired('LED', { anode:0, cathode:1 }); //LED 脚の長い方（アノード, +）を0, 脚の短い方（カソード,-）を1に割り当てる
obnizParts.dht20 = obniz.wired("DHT20",{vcc:4, sda:5, gnd:6,  scl:7 ,voltage: "5v"}); //温湿度 4,5,6,7番にピンをアサインし、電圧を5Vに設定
```  
----

### Lesson4 成果物を発表しよう！【15:15〜15:45】  

**やること:** どのような意図で何を制作したのかを発表してみましょう

**ゴール:** 自身の取り組みが周りの人に伝わる

**ルール:**  
- 1人3分で発表します

----

[ハンズオン終了お疲れさまでした](./greetings.md)
