# TraCI/BusStop

名前の着いたバス停(BusStop)から変数の値を取得します。
返り値は直前のシミュレーションステップにおける指定された変数の値になります。
バス停から変数の値を取得するためには，[追加ファイル]内で[バス停を定義]し，シミュレーション開始前に読み込んでおく必要があることに注意してください。
`freq`と`file`の二つの属性は TraCI に影響しません。

以下の変数の値を取得することができます。
返り値の型も表内に示されています。

|変数|型|説明|[Python メソッド](https://sumo.dlr.de/docs/TraCI/Interfacing_TraCI_from_Python.html)|
-|-|-|-
|end pos|double|車線内におけるバス停の終端座標(単位: [m])|[getEndPos](https://sumo.dlr.de/pydoc/traci._busstop.html#BusStopDomain-getEndPos)|
|lane ID|string|バス停の設置されている車線の名前|[getLaneID](https://sumo.dlr.de/pydoc/traci._busstop.html#BusStopDomain-getLaneID)|
|name|string|バス停の名前|[getName](https://sumo.dlr.de/pydoc/traci._busstop.html#BusStopDomain-getName)|
|person count|integer|総待ち人数の合計|[getPersonCount](https://sumo.dlr.de/pydoc/traci._busstop.html#BusStopDomain-getPersonCount)|
|person ID|stringList|バス待ちの人の ID|[getPersonIDs](https://sumo.dlr.de/pydoc/traci._busstop.html#BusStopDomain-getPersonIDs)|
|start pos|double|車線内におけるバス停の始端座標(単位: [m])|[getStartPos](https://sumo.dlr.de/pydoc/traci._busstop.html#BusStopDomain-getStartPos)|
|vehicle count|integer|バス停に止まった車両の総台数|[getVehicleCount](https://sumo.dlr.de/pydoc/traci._busstop.html#BusStopDomain-getVehicleCount)|
|vehicle ID|stringList|バス停に止まっている車両の ID|[getVehicleIDs](https://sumo.dlr.de/pydoc/traci._busstop.html#BusStopDomain-getVehicleIDs)|


