
<!-- 
authority
permission : パーミッション（なにこれ？）
reversible lane : リバーシブル‐レーン
交通量に応じてセンターラインの位置を移動できる道路。可逆車線。
https://www.weblio.jp/content/Reversible+lane
line-of-sight : 視線
 -->
 
# Rerouter

参考原文バージョン: 2022/3/17, 133f8e99cb69330cff7537132cefe02555695b95

Rerouterは、vehicleが指定されたedgeに移動すると同時に、vehicleのrouteを変更します。

下記の宣言を{{AdditionalFile}}に追加することで、rerouteを道路ネットワークに設定します。
`<rerouter id="<REROUTER_ID>" edges="<EDGE_ID>[;<EDGE_ID>]*" file="<DEFINITION_FILE>" [probability="<PROBABILITY>"]/>`
Rerouterは1つ以上のedgeに設定できます。
さらに、定義の中にvehicleを再ルーティングする確率を0（なし）から1（全て）の間で定義できます。
宣言できる値は次の表の通りです。

| Attribute Name | Value Type  | Description                                                                                            |
| -------------- | ----------- | ------------------------------------------------------------------------------------------------------ |
| **id**         | id (string) | rerouterのid                                                                              |
| **edges**      | float       | vehicleを再ルーティングする1つのedge id、もしくは複数のedge idリスト|
| file           | float       | 定義ファイルへのパス（rerouterの子要素としてintervalsを定義することもできます。） |
| probability    | float       | vehicleを再ルーティングする確率（0から1の間の値、デフォルト値は1）      |
| timeThreshold  | time (s)    | rerouterが有効になるまでの最小累計待ち時間（デフォルト値は0で常に適用されます。）|
| vTypes         | stringList  | rerouterが適用されるvType idのリスト（スペース区切り、デフォルトは""で全てのvTypeに適用されます。）|
| off            | bool        | rerouterを初期状態から非アクティブにするか（アクティブにするのはGUI上で操作する。デフォルトは*false*）|

rerouterはいくつか異なる方法で動作する可能性があります。
一定期間内に、edgeを閉じるか、新たな目的地や事前定義されたルートを車両に割り当てることができます。
次のセクションで動作の詳細を記します。

## 定義スタイル

rerouterの宣言には2つのスタイルがあります。

### 1ファイルですべて定義する場合

{{AdditionalFile}}は次のようになります。

```
<additional>
   <rerouter id="<REROUTER_ID>" edges="<EDGE_ID>[;<EDGE_ID>]*" [probability="<PROBABILITY>"]>
      <interval begin="<BEGIN_TIME>" end="<END_TIME>">
         ... action description ...
      </interval>
      ... further intervals ...
   </rerouter>
   ... further rerouters ...
</additional>
```

### 分割されたファイルで定義する場合

{{AdditionalFile}}は次のようになります。

```
<additional>   
   <rerouter id="<REROUTER_ID>" edges="<EDGE_ID>[;<EDGE_ID>]*" [probability="<PROBABILITY>"]>
     <include href="definitions.xml"/>      
   </rerouter>
   ... further rerouters ...
</additional>
```

時間経過に対するアクションを記述する`definitions.xml`は次のようになります。

```
   <interval begin="<BEGIN_TIME>" end="<END_TIME>">
      ... action description ...
   </interval>
   ... further intervals ...
```

注釈：定義ファイルにはroot-level要素がありません。

以降の例では[everything-in-one-file](#everything_in_one_file)シンタックスが使われています。

!!! caution "警告"
      rerouterのfile変数にadditional定義を含めるサポートは、バージョン1.13.0で削除されました。

## Streetの閉鎖

"closingReroute"は、<EDGE_ID\>のedgeの閉鎖をrerouterに強制します。
このedgeを通過しようとしていたvehicleは、rerouterで定義されたedge変数のうちどれか1つに到達すると同時に、新たなrouteを得ます、
新たなrouteを設定するアルゴリズムは、閉鎖されたedgeを割ける条件のもとで、[\#Assigning_a_new_Destination](#assigning_a_new_destination)に記されたものと同じになります。
closingRerouteの定義は次のようになります。

```
<rerouter>
   <interval begin="<BEGIN_TIME>" end="<END_TIME>">
      <closingReroute id="<EDGE_ID>"/>
   </interval>
   ... further intervals ...
</rerouter>
```

定義できる変数は次の通りです。

| Attribute Name | Value Type              | Description |
| -------------- | ----------------------- | --------------------------------------------------------------- |
| **id**         | id (string)             | 閉鎖するedgeのid。idはネットワークないのedgeのidです。|
| allow          | list of vehicle classes | オプションである[vehicle classes](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#abstract_vehicle_class)のスペース区切りのリストは、閉鎖されたedgeでの走行が許可されます。それ以外の走行は禁止されます。|
| disallow       | list of vehicle classes | オプションである[vehicle classes](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#abstract_vehicle_class)のスペース区切りのリストは、閉鎖されたedgeでの走行が禁止されます。それ以外の走行は許可されます。|

`allow`と`disallow`属性のない`<closingReroute>`を使ったとき、代わりのrouteで目的地の到達できないvehicleは古いrouteを維持し、事実上edgeの閉鎖を無視します。
`allow`と`disallow`属性を使ったとき（同一定義に1つのみ使える）、routeを替えられないvehicleは、定義されたintervalまで、閉鎖されたedgeの前で停止します。
この機能は、自然発生的な道路閉鎖による交通渋滞の模擬に使うことができます。

!!! caution "警告"
      修正されたパーミッションを使うとき、オプションの**--ignore-route-errors**が必要になる可能性があります。使わない場合、閉鎖がactiveなときに挿入される車両がrouteエラーを生じる可能性があるからです。また、パーミッションは緊急ブレーキの原因になる可能性もあります。この緩和方法として、閉鎖する前に[VariableSpeedSigns](../Simulation/Variable_Speed_Signs.md)を設置し、一時的に交通を減速させる方法があります。

## Laneの閉鎖

"closingLaneReroute"は、パーミッションを*authority*に設定することで、rerouterに<LANE_ID\>のレーン閉鎖を強制します。
そのrouteを通過し[rerouting device](../Demand/Automatic_Routing.md)が備えられたvehicleは、rerouteの定義のedge変数に含まれるいずれか1つに到達したと同時に、新たなrouteが計算されます。


closingLaneRerouteの定義は次の通りです。

```
<rerouter>
   <interval begin="<BEGIN_TIME>" end="<END_TIME>">
      <closingLaneReroute id="<LANE_ID>"/>
   </interval>
   ... further intervals ...
</rerouter>
```

この定義で使われる属性は次の通りです。

| Attribute Name | Value Type              | Description |
| -------------- | ----------------------- | --------------------------- |
| **id**         | id (string)             |  閉鎖するlaneのid。idはネットワークに含まれている必要があります。|
| allow          | list of vehicle classes | オプションである[vehicle classes](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#abstract_vehicle_class)のスペース区切りのリストは、閉鎖されたedgeでの走行が許可されます。それ以外の走行は禁止されます。デフォルトは*authority*。|
| disallow       | list of vehicle classes | オプションである[vehicle classes](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#abstract_vehicle_class)のスペース区切りのリストは、閉鎖されたedgeでの走行が禁止されます。それ以外の走行は許可されます。この属性は禁止するクラスを少数で簡潔に記述するために、**allow**の代わりに使うことができます。|

!!! note "注"
      パーミッションの修正は、緊急ブレーキの原因になる可能性もあります。この緩和方法として、閉鎖する前に[VariableSpeedSigns](../Simulation/Variable_Speed_Signs.md)を設置し、一時的に交通を減速させる方法があります。

### リバーシブルレーン

次の方法に従い、2つの`closingLaneReroute`の定義を用いることで、リバーシブルレーンを模擬できます。

- 反対方向を向く2つのedgeを定義する。各edgeは少なくとも2つのレーンをもつ。
- [中央のレーンのうちの一つを通行禁止にする](../Netedit/editModesCommon.md#inspecting_lanes)。（disallow="all"）
- 中央レーンが同じ空間を占めるように、edgeの形状を修正する。
   - [各edgeのsidewaysを調整する。 (lane幅のデフォルト値は-1.6)](../Netedit/editModesCommon.md#frame_operation)
   - もしくは、[直接形状を調整する](../Netedit/neteditUsageExamples.md#specifying_the_complete_geometry_of_an_edge_including_endpoints)。

特定の期間に、リバーシブルレーンの方向を変更するには、次のようにrerouterを使うことができます。

```
<rerouter id="example" edges="E1 -E1">
      <interval begin="7:0:0" end="8:30:0">
            <closingLaneReroute id="E1_1" allow="all"/>
            <closingLaneReroute id="-E1_1" disallow="all"/>
      </interval>
   </rerouter>
```

rerouterでlaneのpermissionを変更する代わりに、traci関数の[`traci.lane.setAllowed` と `setDisallowed`](../TraCI/Change_Lane_State.md)を使うことができます。

## 新たな目的地の割当て

"dest_prob_reroute"は、rerouter定義のedge属性のうちの1つのedgeを通過するvehicleに対し、新たなrouteをrerouteに割り当てさせることができます。
新たなrouteの目的地は次のelementのように新たな目的地名によって定義されます。

```
<rerouter>
   <interval begin="<BEGIN_TIME>" end="<END_TIME>">
      <destProbReroute id="<EDGE_ID1>" probability="<PROBABILITY1>"/>
      <destProbReroute id="<EDGE_ID2>" probability="<PROBABILITY2>"/>
   </interval>
   ... further intervals ...
</rerouter>
```

最速routeはダイクストラアルゴリズムを使って自動的に計算され、vehicleの位置するedgeからはじまり、新たな目的地で終わります。
次の旅行時間がroutingでは考慮されます（最初に適用された値が使われます）。

- もしvehicleに[rerouting device](../Demand/Automatic_Routing.md)が搭載されている場合は、ネットワークにおける現在の（スムーズ化された）旅行時間
- もし、[TraCIコマンド*change edge travel time information*](../TraCI/Change_Vehicle_State.md#change_edge_travel_time_information_0x58)が設定された場合、現在の車両からみた主観的なedgeコスト
- [sumo](../sumo.md)の**--weight-files**オープションで読み込まれたedgeの重み
- 空のネットワークにおける旅行時間

dest_prob_rerouteで使われる属性は以下の通りです。

| Attribute Name  | Value Type                        | Description |
| --------------- | --------------------------------- | ------------------------------ |
| **id**          | id (string)                       | 新たな目的地のid。idは、ネット―枠内に含まれているか、特別な値である*keepDestination*, *terminateRoute*のいずれかである必要があります。|
| **probability** | float (should be between 0 and 1) | vehicleがedgeを目的地として使う確率。確率は合計が1になるよう自動的に正規化されます。|

!!! note "注釈"
      同じintervalで**closingReroute**と**destProbReroute**を組み合わせることができます。この場合、元の目的地に到達できないvehicleのみ、確率分布から新たな目的地を得ます。

### 特殊な定義値

- *keepDestination*: 現状のrouteを維持するvehicle
- *terminateRoute*: vehicleをシミュレーションから除き、rerouterのあるedgeに到着したとみなしカウントする。

## 新たなRouteの割当て
rerouter定義のedge属性で定義されたedgeの1つを通過したvehicleに対し、"route_prob_reroute"はrerouterに新たなrouteを割り当てることを強制します。
このケースでは、新たな目的地の代わりに、完全なrouteのidを与える必要があります。

```
<rerouter>
   <interval begin="<BEGIN_TIME>" end="<END_TIME>">
      <routeProbReroute id="<ROUTE_ID1>" probability="<PROBABILITY1>"/>
      <routeProbReroute id="<ROUTE_ID2>" probability="<PROBABILITY2>"/>
   </interval>
   ... further intervals ...
</rerouter>
```

この定義で使える属性は次の通りです。

| Attribute Name | Value Type  | Description            |
| -------------- | ----------- | ---------------------------------------------------------------------------------------------- |
| **id**         | id (string) | 割り当てる新たなrouteのid。idはあらかじめ読み込まれたrouteのidである必要があります。|
| probability    | float       | 目的地として与えられたedgeをvehicleが使う確率。デフォルトは1。確率は全てのエントリについて自動的に正規化されます。|

### 繰返しのある（Repeated）公共交通のroute

stopを含むrerouterで新たなrouteを割り当てる場合、vehicleはそのstopを使います。
もし、stopが'until'属性を使うとき、routeは['cycleTime'](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#repeated_routes)属性を使い、
各繰返しで設定した量だけuntill-timesをシフトする必要があります。

## 代替駐車場への再ルーティング

駐車場に止まった車両には、駐車場が満車のため、駐車できない状況が生じる可能性があります。

このような場合、vehicleは、駐車場が空くまで道路上で待つか、異なる駐車場へ再ルーティングできます。
後者の振舞いには`parkingAreaReroute`を定義する必要があります。
この再ルーティング定義では、代わりに使用できる駐車場集合を定義します。
異なる駐車場への再ルーティングが生じるのは、次の2つの場合です。

- vehicleがparkingAreaに到達したとき満車で駐車できない場合
- vehicleがrerouter-gedgeの1つに入り次の条件を全て満たす場合
    - 現在の目的地であるparkingAreaがparkingAreaRerouteの集合に含まれ、なおかつ、`visible="true"`という属性をもつ
    - 現在の目的地であるparkingAreaが満車

定義は次のようになります。

```
   <rerouter id="myRerouter" edges="a b">
      <interval begin="0" end="2000">
         <parkingAreaReroute id="ParkAreaA"/>
         <parkingAreaReroute id="ParkAreaB"/>
      </interval>
   </rerouter>
```

この定義で使える変数は次の表の通りです。

| Attribute Name | Value Type  | Description              |
| -------------- | ----------- | ----------------------------------------------------------------------------------------- |
| **id**         | id (string) | 存在する駐車場のid |
| probability    | float       | 各代替が選ばれる確率（デフォルトは1） |
| visible        | bool        | このparkingAreaの駐車量がparkingAreaのあるedgeに到達する前に分かるか否か。（これは視線や駐車情報システムをモデル化しています。）|

### 駐車場検索のメモリ

駐車場検索とは、vehicleが満車のparkingAreaに出くわし、利用率の状態のないもとで代わりの目的地リストから1つを選ばなければいけない状況を指します。
vehicleは空きのある駐車場を見つけるまで、代わりの目的地への移動を繰り返さなければなりません。

以前に訪れたparkingAreaは、最後の訪問以降に空きが出たと期待し、再び訪問されるのが合理的かもしれません。
デフォルトでは、満車だったparkingAreaには600秒の間は訪問しません。
これは、下記のように、vehicle-paramかvType-paramで修正できます。

```
   <vehicle ...>
      <param key="parking.memory" value="300"/>
   </vehicle
```

!!! caution "警告"
      バージョン1.10.0まで駐車記憶は0のため、vehicleが一部のエリアのみを繰返し訪問する可能性があります。

### 代わりの駐車エリアの決定

代わりのparkingAreaは、複数の属性の重み付き和の最小化に従い、visible、かつ、1つ以上空きのある全ての駐車エリアから選ばれます。
不可視のparkingArea（属性が`visible="false"`）は、満車時であっても代わりの駐車場集合に含まれ、利用率は\[0,capacity\[から選ばれたランダムな値をとります。
各属性（すなわち、利用率、時間、距離）は、空きのあるparkingArea候補の最大値で[0-1]に正規化され、必要に応じて反転（invert）します。
デフォルトでは、vehicleの現在地から新たな駐車場までの距離のみが考慮されます。
次の表には重み図けられる要因を示しており、これは[vehicleのgenericパラメータかそのvType](../Simulation/GenericParameters.md)で調整できます。

| Parameter Name              | Default value | Description                                                              | Inverse (Bigger is better) |
| --------------------------- | ------------- | ------------------------------------------------------------------------ | -------------------------- |
| parking.probability.weight  | 0             | `parkingAreaReroute`の*probability*属性の影響| yes                        |
| parking.capacity.weight     | 0             | 駐車場の容量の和 | yes                        |
| parking.absfreespace.weight | 0             | 空きスペースの絶対的な数                                       | yes                        |
| parking.relfreespace.weight | 0             | 空きスペースの相対的な数                                       | yes                        |
| parking.distanceto.weight   | 1             | 駐車場への道路距離                                    | no                         |
| parking.timeto.weight       | 0             | 駐車エリアまでの推定旅行時間                              | no                         |
| parking.distancefrom.weight | 0             | 駐車エリアから目的地までの道路距離      | no                         |
| parking.timefrom.weight     | 0             | 駐車エリアから目的地までの推定旅行時間 | no                         |

'parking.probability.weight'に正の値が設定されたとき、0から'probability'属性の値の間の乱数が各parkingArea候補に振られます。
この値は、全てのparkingAreaReroute要素の最大の確率の値で、[0,1]に正規化されます。
負に正規化された値は、parking.probability.weightをかけて候補スコアに入力されます。

### 駐車の振舞いに影響する他のパラメータ

Parameter Name         | Default value | Description                                                              | 
| -------------------- | ------------- | ------------------------------------------------------------------------ |
| parking.anywhere     | -1            | x回parkingAreaRerouteの実行に失敗したあと、途中で任意のfreeなparkingAreaを利用することを許可します。（-1で無効化される） |
| parking.frustration  | 100           | 時間がたつにつれ、visiblyでfreeなparkingAreasを選好しやすくします。（parkingAreaReroutesにx回失敗したあと、駐車率が分からない目標は*ほぼ*満車であると仮定する）| 
| parking.knowledge    | 0             | 確率xで、ドライバーに、不可視のparkingAreasの正確な混雑率を*推測*させます。 |

### 再ルーティング後の目的地

一般的に、新たな駐車場に再ルーティングされたvehicleは、stopが終了したあとも、元の目的地を維持します。
次のような特殊なケースの場合、

1. 元のrouteが、元のparkingAreaのあるedgeで終わっていて、
2. 元のparkingAreaの\[startPos, endPos\]内にarrivalPosがある

新たなrouteが新たなparkingAreaで終わり、新たなparkingAreaのendPosが新しいarrivalPosとして設定されます。

# streetが閉鎖されたときのvehicleの振舞い

rerouteのあるvehicle同士の相互作用は複雑で、多数の異なる要因に依存します。
以下では、各要因と要因の組み合わせごとの振舞いを説明します。
以下では、routeを辿る間に`<closingReroute .../>`が影響するedgeをもつvehicleを仮定します（他のvehicleは直接影響されません）。

1. closing style
   - a) hard closing: `<closingReroute>`は'allow'か'disallow'属性を使用してvehicleを禁止します。
   - b) soft closing: 属性は使われません。（edgeの使用は推奨されないが、禁止もされません）
2. alternatives
   - a) 代替ルートが存在する
   - b) 代替ルートが存在しない
3. detour signage
   - a) 代替ルートが分岐する前にrerouter edgeが検出された
   - b) 代替ルートが分岐する前にrerouter edgeが検出されていない
4. vehicle style
   - a) 影響を受けるedgeが優先されるrouteにあって、出発地・目的地でvehicleが定義されている（i.e. `<trip from="..." to="...">`）
   - b) 固定されたrouteでvehicleが定義されている
5. closing time versus departure time
   - a) 閉塞がactiveになっあと、vehicleが出発
   vehicle departs after closing becomes active
   - b) 閉塞がactiveになる前、vehicleが出発（閉塞がrouteの途中で発生）

以下は起こりうるvehicleの振舞いです。

- **R**: rerouteのあるedgeに到達したら代替ルートを使用します。
- **D**: 出発時に代替ルートを使用します。
- **I**: 閉塞edgeを無視して運転を続けます。
- **W**: edgeが再び開くか、テレポートまでの時間に達するまで、閉じたedgeの前で待機します。（テレポート時間に到達した場合は、閉じたedgeを越えてテレポートします。）
- **E**: エラーを生成します。

次の効果が発生します。

## Hard closing

- 1a-2a-3a-4a-5a: **D** 
- 1a-2a-3a-4a-5b: **R** 
- 1a-2a-3a-4b-5a: **R** 
- 1a-2a-3a-4b-5b: **R** 
                       
- 1a-2a-3b-4a-5a: **D**
- 1a-2a-3b-4a-5b: **W**
- 1a-2a-3b-4b-5a: **W**
- 1a-2a-3b-4b-5b: **W**
                       
- 1a-2b-3a-4a-5a: **E** (becomes **W** with **--ignore-route-errors**)
- 1a-2b-3a-4a-5b: **W**
- 1a-2b-3a-4b-5a: **W**
- 1a-2b-3a-4b-5b: **W**
                       
- 1a-2b-3b-4a-5a: **E** (becomes **W** with **--ignore-route-errors**)
- 1a-2b-3b-4a-5b: **W**
- 1a-2b-3b-4b-5a: **W**
- 1a-2b-3b-4b-5b: **W**
                       
## Soft closing        
                       
- 1b-2a-3a-4a-5a: **R**
- 1b-2a-3a-4a-5b: **R**
- 1b-2a-3a-4b-5a: **R**
- 1b-2a-3a-4b-5b: **R**
                       
- 1b-2a-3b-4a-5a: **I**
- 1b-2a-3b-4a-5b: **I**
- 1b-2a-3b-4b-5a: **I**
- 1b-2a-3b-4b-5b: **I**
                       
- 1b-2b-3a-4a-5a: **I**
- 1b-2b-3a-4a-5b: **I**
- 1b-2b-3a-4b-5a: **I**
- 1b-2b-3a-4b-5b: **I**
                       
- 1b-2b-3b-4a-5a: **I**
- 1b-2b-3b-4a-5b: **I**
- 1b-2b-3b-4b-5a: **I**
- 1b-2b-3b-4b-5b: **I**

## 閉鎖されたedgeからの出発

vehicleの主発edgeが閉鎖されているとき、vehicleはこれを無視して'soft'閉鎖をします。
'hard'閉鎖については、シミュレーションはエラーを発生させます。
もし、**--ignore-route-errors**がセットされている場合、vehicleは警告と共に破棄されます。
