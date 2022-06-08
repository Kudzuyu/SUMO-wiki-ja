
# ParkingArea

<!-- 翻訳対応
* parkingArea : 固有名のためそのまま
* Maneuvering Times : 操縦時間
* Parking Areas/Area : 駐車場 -->

## 駐車場

道路ネットワークの外側に駐車するためのエリアは，'<parkingArea>'要素を使って定義できます．
この機能で次の目標が達成できます．

- fishboneもしくはparallelな駐車場を可視化する任意の駐車位置とアングルの設定ができる
- 道路ネットワーク外の駐車スペースを，設定した容量に限定できる
- 駐車場が満車になったときに[代替可能な駐車エリアへの自動再ルーティング](Rerouter.md#rerouting_to_an_alternative_parking_area)をトリガーできる

## 定義

道路脇のparkingAreaは次ように定義される

```
<parkingArea id="ParkAreaA" lane="a_0" startPos="200" endPos="250" roadsideCapacity="5" angle="45" length="30"/>
```

加えて，個々の駐車スペースを定義できる．

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

一つの駐車場の総容量は，*roadsideCapacity*と`<space>`要素の数の和で与えられる．

parkingAreaは次の変数をサポートしている．

| Attribute Name   | Value Type     | Value Range                                                                                  | Default                                | Description                                                                                                                |
| ---------------- | -------------- | ---------------------------------------- | -------------------------------------- | --------------------------------------------------- |
| **id**           | string         | id                                                                                           |                                        | （重複しない）駐車場の名前                                                                               |
| **lane**         | string         | valid lane id                                                                                |                                        | 駐車場のあるlaneの名前                                                                  |
| **startPos**     | float          | \-lane.length < x < lane.length (負の値のとき，laneの終わりからカウントされる) | 0                                      | lane上での開始点 (laneのlowerな位置，メートル単位)                                                  |
| endPos           | float          | \-lane.length < x < lane.length (負の値のとき，laneの終わりからカウントされる) | lane.length                            | lane上での終了てん (laneのhigherな位置，メートル単位，*startPos*より0.1 m以上大きい値である必要) |
| friendlyPos      | bool           | *true,false*                                                                                 | *false*                                | 無効な停止位置を自動的に修正するか (デフォルト値 *false*)                                         |
| name             | string         | simple String                                                                                |                                        | 駐車場を説明する任意のテキスト．可視化にのみ使われる．                                 |
| roadsideCapacity | int            | non-negative                                                                                 | 0                                      | 道路脇の駐車場の数                                                                         |
| onRoad           | bool           |                                                                                              | false                                  | 駐車中，車両が道路に残っているか．<br>**note:**<br>もし*true*を設定した場合，roadsideCapacityのみが使用され，`<space>`は定義できない．|
| width            | float          | positive                                                                                     | 3.2                                    | 道路脇の駐車スペース幅                                                                                  |
| length           | float          | positive                                                                                     | (endPos - startPos) / roadsideCapacity | 道路脇の駐車スペース長さ                                                                                 |
| angle            | float (degree) |                                                                                              | 0                                      | laneに対する道路脇駐車場の角度．正は時計回り方向                             |

### 駐車場スペースのカスタム
space要素は次の変数をサポートしている．

| Attribute Name | Value Type     | Value Range | Default                                                                  | Description                                     |
| -------------- | -------------- | ----------- | ------------------------------------------------------------------------ | ----------------------------------------------- |
| **x**          | float          |             |                                                                          | 駐車する車両のx座標，メートル単位 |
| **y**          | float          |             |                                                                          | 駐車する車両のy座標，メートル単位 |
| z              | float          |             | 0                                                                        | 駐車する車両のz座標，メートル単位 |
| width          | float          |             | width value of the parent parking area                                   | 駐車スペースの幅                  |
| length         | float          |             | length value of the parent parking area                                  | 駐車スペースの長さ                 |
| angle          | float (degree) |             | absolute angle of the parent parking area (lane angle + angle attribute) | 駐車スペースのAbsolute angle             |
| slope          | float (degree) |             | 0                                                                        | 駐車スペースのSlope angle                |

!!!注意
駐車場エリアは--additional-filesパラメータを介して設定に加える必要があります．（参考 {{AdditionalFile}}）

## 車両を駐車場に停止させる

parkingPlaceに停まるvehicleを宣言するには，`<stop>`定義をvehicleかそのrouteに含めなければいけない．

```
<vehicle id="0" depart="0">
    <route edges="e1 e2 e3"/>
    <stop parkingArea="pa0" duration="20"/>
</vehicle>
```

この定義は，"0"と名付けたvehicleがparkingArea"0"に停まることを表す．
ただし，vehicleのrouteのedge"e1,e2,e3"のいずれか一つに駐車場のあるlaneが含まれなければならない．

vehicleの"stop"要素の変数リストは下記を参照
[Definition_of_Vehicles,_Vehicle_Types,_and_Routes\#Stops](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#stops)

### 駐車場へ出入りするときの操作時間（Maneuvering Times）のモデリング

booleanオプションの**--parking.maneuver**をセットした場合，
parkingAreaを出入りするとき，vehicleは道路上で追加の時間を使う．
この時間は道路レーンに対する駐車ロットの角度に依存し，vTypeの変数である*maneuverAngleTimes*で設定できる．
この設定は，*ANGLE ENTERINGTIME LEAVINGTIME*と表される3値の組のリスト（コンマ区切り）で表す．

```
<vType id="example" maneuverAngleTimes="10 3.0 4.0,80 1.6 11.0,110 11.0 2.0,170 8.1 3.0,181 3.0 4.0"/>
```

値は最も近い角度が使われる．
*maneuverAngleTimes*の値はvClass固有の値で初期化され，その値は，

- デフォルト：`maneuverAngleTimes="10 3 4,80 1 11,110 11 2,170 8 3,181 3 4"`
- truck, trailer, coach, delivery: いずれもデフォルトと比較して2倍の時間
- bicycle, moped: `maneuverAngleTimes="181 1 1"`

## 満車時の再ルーティング
もし，満車のparkingAreaにvehicleが到達したとき
空車ができるまでまつか，[新しい駐車場へ再ルーティングする](../Simulation/Rerouter.md#rerouting_to_an_alternative_parking_area)．

## TraCI

幾つかの，駐車場に関する情報は，[traci.simulation.getParameter()のコール](../TraCI/Simulation_Value_Retrieval.md#generic_parameter_retrieval_0x7e)で直接アクセスできる．

- **parkingArea.capacity**: 駐車スペースの総数（roadsideCapacity + <space>要素の数）
- **parkingArea.occupancy**: その駐車場に駐車中のvehicle数
