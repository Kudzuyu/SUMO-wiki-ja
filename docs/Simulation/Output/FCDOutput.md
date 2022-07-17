
# FCDOutput

参考原文バージョン: 2022/7/1, c3d6ddcaca6785b6880ad9d82115341778f39fbb

FCD（フローティングカーデータ）出力は、ネットワーク上の各vehicleについて、各タイムステップにおける位置や速度、その他の情報を含みます。
この出力は各vehicleに搭載された高精度・高頻度なGPS装置のように振舞います。
頻度や取得レート、精度、データ形式を調整する[TraceExporter tool](../../Tools/TraceExporter.md)を使い、出力をさらに加工できます。

## シミュレーション内でのインスタンス化

**--fcd-output** {{DT_FILE}}オプションが設定されたとき、シミュレーションはこの出力を生成します。
{{DT_FILE}}は書き出される出力のファイル名です。
同じ名前の他のファイルは上書きされます。また、書き出し先のフォルダが存在している必要があります。

デフォルトでは、シミュレーション内の全てのvehicleとpersonについてfcd出力が有効化され、各ステップで出力されます。
[オプションかパラメータによるデバイスの割当て](../../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#devices)を使う（すなわち**--device.fcd.probability 0.25**）ことで、fcd出力を生成するvehicleの集合を減らすことができます。
**--device.fcd.period** {{DT_TIME}}オプションを使い出力期間を設定できます。
出力を遅らせる（すなわちwarm-up時間が経過するのを待つ）には、**--device.fcd.begin** {{DT_TIME}}オプションを使います。

## 生成される出力

生成されるXMLファイルは次のようになります。

```
<fcd-export>
  <timestep time="<TIME_STEP>">
      <vehicle id="<VEHICLE_ID>" x="<VEHICLE_POS_X>" y="<VEHICLE_POS_Y>" angle="<VEHICLE_ANGLE>" type="<VEHICLE_TYPE>"
      speed="<VEHICLE_SPEED>"/>
      ... 他のvehicle ...
  </timestep>
  ... 次のタイムステップ ...
</fcd-export>
```

| Name     | Type                 | Description                                                                                                             |
| -------- | -------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| timestep | (simulation) seconds | このtimestep要素内の値のタイムステップ |
| id       | id                   | vehicleのid |
| type     | id                   | vehicle typeの名前 |
| speed    | m/s                  | vehicleの速度 |
| angle    | degree               | navigational standardにおけるvehicleの角度（0-360度、時計回りで12時の位置が0） |
| x        | m or longitude       | vehicleのx軸の絶対座標（フロントバンパー中央）。値は指定された地理投影に依存します。|
| y        | m or latitude        | vehicleのy軸の絶対座標（フロントバンパー中央）。値は指定された地理投影に依存します。|
| z        | m                    | vehicleのz軸の絶対座標（フロントバンパー中央）。<br><br>**Note:**  この値が存在するのはネットワークが標高データを含む場合のみです。 |
| pos      | m                    | 現在laneの開始位置からのvehicleの走行位置 |
| lane     | id                   | 現在laneのid |
| slope    | degree               | vehicleの傾き（度、現在位置における道路の傾きに等しい）|
| signals  | bitset               | [シグナル状態の情報](../../TraCI/Vehicle_Signalling.md)（blinkersなど）。**--fcd-output.signals**オプションが設定されたときのみ現れます。 |

**--fcd-output.geo**オプションが設定されたとき、書き込まれる(x,y)座標は緯度経度の地理座標となります。

### 精度

デフォルトのfcd出力では、1cm精度の位置の値（メートル単位）を出力します（**--precision**オプションで変更可能です）。
**--fcd-output.geo**オプションを設定した場合、値は小数点以下6桁の精度をもつ経緯度になります（**--precision.geo**オプションで変更可能です）。

## personとcontainer出力

シミュレーションにおけるpersonやcontainerは次のように出力されます。

```
<fcd-export>
  <timestep time="<TIME_STEP>">
      <vehicle .../>
      ...
      <person id="..." x="..." y="..." angle="..." type="..." speed="..." edge="..." slope="..."/>
      ...
      <container id="..." x="..." y="..." angle="..." type="..." speed="..." edge="..." slope="..."/>
      ...
  </timestep>
  ... next timestep ...
</fcd-export>
```

personやcontainerがvehicleで輸送されている場合は、そのvehicleの子要素として`<person>`要素と`<container>`要素が書き出されます。

## 出力のフィルタリング／制限

!!! caution "警告"
    生成された出力ファイルは非常に巨大になる可能性があります。[gzipped](https://en.wikipedia.org/wiki/Gzip)の出力ファイルを書き出すには拡張子`.gz`を出力ファイル名に付けてください。

### 出力を生成するvehicle集合の制限

**fcd**デバイスを搭載する[vehicleの集合を制御](../../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#devices)することで、出力を特定のvehicle typeやidに制限することができます。

次の例は*ego*と呼ばれる単一のvehicleに出力を限定しています。
```
--device.fcd.explicit ego
```

次の例は、fcd出力をシミュレーション全体から単一flowに制限しています。

```
--device.fcd.probability 0 ...
```

```
<flow ...>
   <param key="has.fcd.device" value="true"/>
</flow>
```

### ロケーションの制限

**--fcd-output.filter-edges.input-file** {{DT_FILE}}オプションのファイルからedge一覧を読み込むことで、出力をそのedge集合に制限できます。
このファイル形式は、[netedit](../../Netedit/index.md)でselectionsを保存するときと同一のものです。
```
edge:id1
edge:id2
...
```

### shapeによるロケーションの制限

**--fcd-output.filter-shapes**オプションで`<poly>`のidリストを設定することで、出力を特定エリア内のvehicleに限定できます。
[polygon shapes](../Shapes.md)はadditionalファイルから読み込まれている必要があります。

### センサー範囲による出力の制限

全てのvehicleが**fcd**装置を搭載していないとき、**--device.fcd.radius**オプションで所望の半径（メートル単位）を設定することで、搭載しているvehicleの範囲内にある他vehicleやpersonを出力に含めることができます。

## その他のオプション

- **--fcd-output.geo** 地理参照ネットワーク向けに出力する座標をWGS84に切り替えます。
- **--fcd-output.signals** 出力に[signal state information](../../TraCI/Vehicle_Signalling.md)を加えます。
- **--fcd-output.distance** 出力に[kilometrage](../Railways.md#kilometrage-mileage-chainage)情報を加えます。
- **--fcd-output.acceleration** 出力に加速度データを加えます。（[sublane model](../SublaneModel.md)を使う場合は横加速度も出力します。）
- **--fcd-output.max-leader-distance FLOAT** 与えられた距離内にリーダーのvehicleがいる場合にleaderGap、leaderSpeed、leaderID属性を出力に加えます。そうでない場合、leaderIDは""、leaderGap、leaderSpeedは-1とします。
- **--fcd-output.params KEY1,KEY2,...** [generic parameters](../GenericParameters.md)を出力に加えます。（deviceとcarfollowmodelのパラメータ、および任意のユーザー定義値をサポートします。）
- **--fcd-output.attributes ATTR1,ATTR2,...** 出力を削減するために、書き出す属性を与えられたリストに制限します。次の属性は特殊なものです。
  - **all**: 全ての属性を書き出します。
  - **vehicle**: 各personにvehicle属性を追加する。（personが走行中か歩行中かを見分けます。）
  - **odometer**: 各vehicleのodometer値（出発地からの走行距離）を書き出します。
  - **posLat**: 各vehicleのlane上における横位置を書き出します。
  
## 注釈

vehicle形状の図形と組み合わせることで、例えば、[NASA WorldWind](http://worldwind.arc.nasa.gov/java/)や[Google Earth](http://earth.google.com)のような素晴らしい動画を作ることができます。
