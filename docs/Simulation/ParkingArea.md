# ParkingArea

参考原文バージョン: 2022/3/17, e478a225c9ccd81efa6c4edcf8eb5a109ef620c6

<!-- 
訳語対応
* parkingArea: 固有名のためそのまま
* maneuvering times: 操縦時間
* parking areas/area: 駐車場
* road-side parking: 路上駐車場
* car parks: 路外駐車場
-->

## 駐車場

道路ネットワーク外に駐車するためのエリア（路上駐車場もしくは路外駐車場）は、'<parkingArea>'要素を使って定義できます。
この機能で次の目標が達成できます。

- 任意の駐車位置と角度を定義することで、fishbone型もしくはparallel型の駐車場を可視化できます。
- 道路ネットワーク外の駐車スペースを設定した容量に限定できます。
- 駐車場が満車になったとき[代替可能な駐車エリアへの自動再ルーティング](Rerouter.md#rerouting_to_an_alternative_parking_area)をトリガーできます。

## 定義

路上駐車場であるparkingAreaは次のように定義されます。

```
<parkingArea id="ParkAreaA" lane="a_0" startPos="200" endPos="250" roadsideCapacity="5" angle="45" length="30"/>
```

加えて、個々の駐車スペースを定義できます。

```
<parkingArea id="ParkAreaB" lane="b_0" startPos="240" endPos="260" roadsideCapacity="0" width="5" length="10" angle="30">
    <space x="853" y="623"/>
    <space x="863" y="618"/>
    <space x="873" y="613"/>
    <space x="883" y="608"/>
    <space x="893" y="603"/>
    <space x="848" y="611" width="4" length="8" angle="120"/>
    <space x="858" y="606" width="4" length="8" angle="120"/>
    <space x="868" y="601" width="4" length="8" angle="120"/>
    <space x="878" y="596" width="4" length="8" angle="120"/>
    <space x="888" y="591" width="4" length="8" angle="120"/>
</parkingArea>
```

1つの駐車場の総容量は、*roadsideCapacity*と`<space>`要素の数の和で与えられます。

parkingAreaは次の変数をサポートしています。

| Attribute Name   | Value Type     | Value Range                                                                                  | Default                                | Description                                         |
| ---------------- | -------------- | -------------------------------------------------------------------------------------------- | -------------------------------------- | --------------------------------------------------- |
| **id**           | string         | id                                                                                           |                                        | （重複しない）駐車場の名前                             |
| **lane**         | string         | valid lane id                                                                                |                                        | 駐車場のあるlaneの名前                                |
| **startPos**     | float          | \-lane.length < x < lane.length （負の値のとき、laneの終わりからカウントされます）                 | 0                                      | lane上での開始点（laneのlowerな位置、メートル単位）     |
| endPos           | float          | \-lane.length < x < lane.length （負の値のとき、laneの終わりからカウントされます）                 | lane.length                            | lane上での終了点（laneのhigherな位置、メートル単位、*startPos*より0.1メートル以上大きい値である必要があります） |
| friendlyPos      | bool           | *true,false*                                                                                 | *false*                                | 無効な停止位置を自動的に修正するか（デフォルト値 *false*）|
| name             | string         | simple String                                                                                |                                        | 駐車場を説明する任意のテキスト。可視化にのみ使われます。    |
| roadsideCapacity | int            | non-negative                                                                                 | 0                                      | 道路脇の駐車場の数                                     |
| onRoad           | bool           |                                                                                              | false                                  | 駐車中、車両が道路に残っているか。<br>**note:**<br>もし*true*を設定した場合、roadsideCapacityのみが使用され、`<space>`は定義できません。|
| width            | float          | positive                                                                                     | 3.2                                    | 道路脇の駐車スペース幅                                 |
| length           | float          | positive                                                                                     | (endPos - startPos) / roadsideCapacity | 道路脇の駐車スペース長さ                               |
| angle            | float (degree) |                                                                                              | 0                                      | laneに対する道路脇駐車場の角度。正は時計回り方向。         |

### 駐車場スペースのカスタム
space要素は次の変数をサポートしています。

| Attribute Name | Value Type     | Value Range | Default                                                                  | Description                    |
| -------------- | -------------- | ----------- | ------------------------------------------------------------------------ | ------------------------------ |
| **x**          | float          |             |                                                                          | 駐車する車両のx座標、メートル単位 |
| **y**          | float          |             |                                                                          | 駐車する車両のy座標、メートル単位 |
| z              | float          |             | 0                                                                        | 駐車する車両のz座標、メートル単位 |
| width          | float          |             | width value of the parent parking area                                   | 駐車スペースの幅                 |
| length         | float          |             | length value of the parent parking area                                  | 駐車スペースの長さ               |
| angle          | float (degree) |             | absolute angle of the parent parking area (lane angle + angle attribute) | 駐車スペースのAbsolute angle     |
| slope          | float (degree) |             | 0                                                                        | 駐車スペースのSlope angle        |

!!! caution "警告"
    駐車場エリアは--additional-filesパラメータを介して設定に加える必要があります。（参考 {{AdditionalFile}}）

## 車両を駐車場に停止させる

parkingPlaceに停まるvehicleを宣言するには、`<stop>`定義をvehicleか、もしくはそのrouteに含めなければいけません。

```
<vehicle id="0" depart="0">
    <route edges="e1 e2 e3"/>
    <stop parkingArea="pa0" duration="20"/>
</vehicle>
```

この定義は"0"と名付けたvehicleがparkingArea"0"に停まることを表します。
ただし、vehicleのrouteのedge"e1,e2,e3"のいずれか1つに、駐車場のあるlaneが含まれなければなりません。

vehicleの"stop"要素の変数リストは下記を参照してください。
[Definition_of_Vehicles,_Vehicle_Types,_and_Routes\#Stops](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#stops)

### 駐車場へ出入りするときの操作時間のモデリング

booleanオプションの**--parking.maneuver**をセットした場合、parkingAreaを出入りするとき、vehicleは道路上で追加の時間を使います。
この時間は道路レーンに対する駐車ロットの角度に依存し、vTypeの変数*maneuverAngleTimes*で設定できます。
この設定は、*ANGLE ENTERINGTIME LEAVINGTIME*で表される3値の組のリスト（コンマ区切り）で表します。

```
<vType id="example" maneuverAngleTimes="10 3.0 4.0,80 1.6 11.0,110 11.0 2.0,170 8.1 3.0,181 3.0 4.0"/>
```

値はもっとも近い角度が使われます。
*maneuverAngleTimes*の値はvClass固有の値で初期化され、その値は、

- デフォルト：`maneuverAngleTimes="10 3 4,80 1 11,110 11 2,170 8 3,181 3 4"`
- truck, trailer, coach, delivery: いずれもデフォルトと比較して2倍の時間
- bicycle, moped: `maneuverAngleTimes="181 1 1"`

## 満車時の再ルーティング
もし、満車のparkingAreaにvehicleが到達したとき、空車になるまで待つか、[新しい駐車場へ再ルーティングされます](../Simulation/Rerouter.md#rerouting_to_an_alternative_parking_area)。

## TraCI

駐車場に関する情報は[traci.simulation.getParameter()のコール](../TraCI/Simulation_Value_Retrieval.md#generic_parameter_retrieval_0x7e)で直接アクセスできます。

- **parkingArea.capacity**: 駐車スペースの総数（roadsideCapacity + <space>要素の数）
- **parkingArea.occupancy**: その駐車場に駐車中のvehicle数
