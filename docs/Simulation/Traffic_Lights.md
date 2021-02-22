# 交通信号

[原文ページ](https://sumo.dlr.de/wiki/Simulation/Traffic_Lights)

通常、[NETCONVERT]()と[NETGENERATE]()はネットワークの計算中に交通信号と交差点の信号制御プログラムを生成します。
現在もなお、こうして生成されたプログラムは頻繁に現実のものと異なっています。

!!! note "訳注"
    SUMOは主にドイツの人々によって開発が始められたため、道路の進行方向などで日本と異なるシステムが存在します。
    本文では
    「左折専用レーン」は「右折専用レーン」など適宜読みかえてください。

## 自動生成される信号(TLS)プログラム

* 全ての交通信号はデフォルト90秒の固定サイクルで生成されます。この設定は**--tls.cycle.time**で変更することができます。
* 全ての青信号時間の後に、黄色信号時間があります。黄色信号時間は交差点に繋がっている道路の最高速度から計算されますが、**--tls.yellow.time**によって変更できます。
* 交差点での速度が70km/hのしきい値(**tls.minor-left.max-speed**によって変更可))を下回っている場合、

* 青信号時間が部分的に衝突する交通流を許可している場合(直進と対向車線からの左折)

* 現実には全ての信号が赤になって交差点を整理する時間があります(全赤時間)。SUMOはデフォルトではこの時間を設けません。青信号の前に全赤時間を設ける場合は**--tls.allred.time**が使えます。
* 生成された信号の点灯レイアウトは 

### デフォルトの四方向交差点()

デフォルトでは、信号のプログラムは四つの青信号時間を持って生成されます。

1. 直進時間
1. 左折時間(左折専用レーンがあるとき)

### 交差点配置の

### その他の交差点

### 交通量の知識を用いた生成プログラムの改善

* 信号を交通量に動的に適応させるには、ネットワークを**--tls.default-type actuated**で

## 新しい信号プログラムの定義

信号の新しいプログラムは[追加ファイル]の一部として読みこむことができます。
読みこみ時には最後のプログラムが使われます。
プログラム同士の切りかえはWAUTまたはTraCIとその両方を使って行ないます。
また、GUIのコンテキストメニューから切りかえることも可能です。
[追加ファイル]の中の信号プログラムの定義は以下のようなものです。

```
<additional>
   <tlLogic id="0" programID="my_program" offset="0" type="static">
      <phase duration="31" state="GGggrrrrGGggrrrr"/>
      <phase duration="5"  state="yyggrrrryyggrrrr"/>
      <phase duration="6"  state="rrGGrrrrrrGGrrrr"/>
      <phase duration="5"  state="rryyrrrrrryyrrrr"/>
      <phase duration="31" state="rrrrGGggrrrrGGgg"/>
      <phase duration="5"  state="rrrryyggrrrryygg"/>
      <phase duration="6"  state="rrrrrrGGrrrrrrGG"/>
      <phase duration="5"  state="rrrrrryyrrrrrryy"/>
   </tlLogic>
</additional>
```

!!! note "注"
    はじめに

### `<tlLogic>` 属性

tlLogic要素の中では以下の属性/要素が使われます。

属性|型|説明
---|---|---
`id`|id(string)|信号のid。.net.xmlファイルに存在するidでなければならない。一般的に信号のidは交差点のidと同一。信号制御のある交差点で赤/緑の棒を右クリックすることで名前を取得できる。
`type`|enum (static, actuated, delay_based) | 信号のタイプ(固定周期、)

<span style="color:#FF0000; background:#FF0000">FOO</span>

### `<phase>`属性

フェーズには以下の属性を持ち定義されます。

属性|型|説明
---|---|---
`duration|時間(int)|フェーズの期間
`state`|現示状態のリスト|


## プログラム変更時間と手続きの定義

実際問題として、交通信号はしばしば一日の中でまた時には平日と週末とでも異なったプログラムを使います。

```
<WAUT refTime="0" id="myWAUT" startProg="weekday_night">
   <wautSwitch time="21600" to="weekday_day"/>    <!-- monday, 6.00 -->
   <wautSwitch time="79200" to="weekday_night"/>  <!-- monday, 22.00 -->
   <wautSwitch time="108000" to="weekday_day"/>   <!-- tuesday, 6.00 -->
... further weekdays ...
   <wautSwitch time="453600" to="weekend_day"/>   <!-- saturday, 6.00 -->
... the weekend days ...
</WAUT>
```

WAUTのフィールドはそれぞれ次のような意味を持ちます。

属性|型|説明
---|---|---
`id`|string id|定義されるWAUTの名前
`refTime`|int|
`startProg`|string id|シミュレーション開始時に使用されるプログラム

wautSwitchのフィールドでは以下のようになります。

属性|型|説明
---|---|---
`time`|int|切りかえる時間
`to`|string id|


```
<additional>

  <tlLogic id="X" type="static" programID="S1" offset="0">
    <phase duration="50" state="Gr"/>
    <phase duration="50" state="rG"/>
  </tlLogic>
  
  <tlLogic id="X" type="static" programID="S2" offset="0">
    <phase duration="30" state="Gr"/>
    <phase duration="80" state="rG"/>
  </tlLogic>


  <WAUT startProg="0" refTime="100" id="w1">
    <wautSwitch to="S1" time="300"></wautSwitch>
    <wautSwitch to="SS" time="800"></wautSwitch>
  </WAUT>

  <wautJunction junctionID="X" wautID="w1"></wautJunction>

<additional>
```

## 信号のパフォーマンス評価

### 検知器の自動生成ツール

信号評価のための検知器の定義生成を補助するツールがあります。

!!! note "注"
    感応式信号は自身の検知器を内部で使うため、検知器を改めて定義する必要はありません。

* **generateTLSE2DEtectors.py**は範囲内の検知器を含んだファイルを生成します。全ての交差点に通じる車線はこれらの検知器でカバーできます。交差点からのオフセット(距離)は**--distance-to-TLS{{DT_FLOAT}}**(または **-d{{DT_FLOAT}}**)で与えられ、標準は1mです。
* **generateTLSE3DEtectors.py**は


## TraCIを用いた信号制御

[TraCIは信号制御のための様々な関数を提供します。] 以下に基本的な流れを示します。

### フェーズの設定

TraCIを用いて適応的な制御を実装する一般的なパターンは(主に[追加ファイル]を用いて)、SUMOによって信号が切りかわるのを避けるために、全ての青信号時間が長期間(例: 1000秒)にわたるプログラムを読みこみ、信号が青から赤になってほしいときにいつでも、次のフェーズ(一般的には黄色フェーズ)に切りかえるために**setPhase**関数を使うことです。
この方法のいいところは、黄色と赤の時間がいまだSUMOによって自動でコントロールされており、スクリプトでは単純に現在の青信号の期間を決めればよいことです。

フェーズが分岐するコントローラを実装するには、青信号フェーズの後に複数の変更先を定義しておき、

### 期間の設定

**setPhaseDuration**関数を使うことで現在のフェーズの残り時間を変更することができます。
この変更は2回目以降の同じフェーズには影響を与えないことに注意してください。

### 状態設定

信号を切りかえるもう一つの手法は、**setRedYellowGreenState**を使って全てのリンクを直接書きかえることです。
この関数を使うと、SUMOはそれ以降状態を変更しなくなります(**setProgram**を使って他のプログラムに切りかえるまで)。
従って、スクリプトは全てのフェーズと状態変更を制御しなければなりません。

### 完全なプログラムの設定

**setCompleteRedYellowGreenDefinition**メソッドを使うことで、静的な信号プログラムを読みこむことができます。
このメソッドは引数に複雑なデータ構造を必要とするため、はじめに**getCompleteRedYellowGreendefinition**を使ってデータ構造を読みこみ、それを編集することが推奨されています。

### 定義済みプログラムとの切りかえ

SUMOは *.net.xml*ファイルと[追加ファイル]から複数の信号プログラムを読みこむことができます。
TraCIの関数**setProgram**を使うことで、スクリプト中でそれらを切りかえることができます。

