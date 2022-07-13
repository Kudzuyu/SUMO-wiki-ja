
# Sumolib

参考原文バージョン: 2022/3/30, c60e6e70bb3dfa2bf77ff4a4ebd8886d959b41c2

**sumolib**は、sumoネットワークやシミュレーションの出力、その他の生成物を扱うpythonモジュールです。
使用可能な関数のリストは、[pydoc generated documentation](http://sumo.dlr.de/pydoc/sumolib.html)を参照してください。
コードは[こちら](https://github.com/eclipse/sumo/tree/main/tools/sumolib)で確認できます。

## スクリプト内での**sumolib**のインポート

ライブラリを使うには、pythonの読込パスに{{SUMO}}/toolsディレクトリを含める必要があります。
これは通常、次のように記述されます。

```
import os, sys
if 'SUMO_HOME' in os.environ:
    tools = os.path.join(os.environ['SUMO_HOME'], 'tools')
    sys.path.append(tools)
else:   
    sys.exit("please declare environment variable 'SUMO_HOME'")
```

## ネットワークファイルの読込

```
# import the library
import sumolib
# parse the net
net = sumolib.net.readNet('myNet.net.xml')
```

次の属性を'readNet'関数に与えることができます（i.e. `readNet('myNet.net.xml', withInternal=True)`）

- withPrograms (bool): 全ての信号機プログラムを読み込む（デフォルトはFalse）
- withLatestPrograms (bool) : 各信号機について最後のプログラムだけ読み込みます。これは、sumoではデフォルトで有効になるプログラムです（デフォルトはFalse）
- withConnections (bool) : 全ての接続を読み込む（デフォルトはTrue）
- withFoes (bool) : 通行権情報を読み込む（デフォルトはTrue）
- withInternal (bool) : 内部のedgeとlaneを読み込む（デフォルトはFalse）
- withPedestrianConnections (bool) : sidewalkとcrossingの間の接続を読み込む（デフォルトはFalse）

## 使用例

### ネットワークを読み込んでnodeとedgeを取り出す

```
# import the library
import sumolib
# parse the net
net = sumolib.net.readNet('myNet.net.xml')
# retrieve the coordinate of a node based on its ID
print net.getNode('myNodeID').getCoord()
# retrieve the successor node ID of an edge
nextNodeID = net.getEdge('myEdgeID').getToNode().getID()
```

### edgeファイルの*plain xml*から平均edge速度を計算する

```
speedSum = 0.0
edgeCount = 0
for edge in sumolib.xml.parse('myNet.edg.xml', ['edge']):
    speedSum += float(edge.speed)
    edgeCount += 1
avgSpeed = speedSum / edgeCount
```

!!! note "注"
    これはあくまで加工例です。ネットワークにおける平均旅行速度を計算するときは、[edgeData](../Simulation/Output/Lane-_or_Edge-based_Traffic_Measures.md)や[tripinfos](../Simulation/Output/TripInfo.md)、[summary-output](../Simulation/Output/Summary.md)を処理しましょう。

### [Statistics](http://sumo.dlr.de/pydoc/sumolib.miscutils.html#Statistics) モジュールを使って速度の中央値を計算する

```
edgeStats = sumolib.miscutils.Statistics("edge speeds")
for edge in sumolib.xml.parse('myNet.edg.xml', ['edge']):
    edgeStats.add(float(edge.speed))
avgSpeed = edgeStats.median()
```

!!! note "注"
    *speed*属性は、ユーザー作成の*.edg.xml*では任意ですが、[netconvert](../netconvert.md) や[netedit](../Netedit/index.md)でファイルが書き出された場合はいつでも含まれます。

### 地理座標に基づき近傍のedgeを探す
実行には[pyproj](https://github.com/pyproj4/pyproj)モジュールがインストールされている必要があります。
巨大なネットワークについては[rtree](https://pypi.org/project/Rtree/)を強く推奨します。

```
net = sumolib.net.readNet('myNet.net.xml')
radius = 0.1
x, y = net.convertLonLat2XY(lon, lat)
edges = net.getNeighboringEdges(x, y, radius)
# pick the closest edge
if len(edges) > 0:
    distancesAndEdges = sorted([(dist, edge) for edge, dist in edges])
    dist, closestEdge = distancesAndEdges[0]
```

### routeファイルの全edgeをパース

```
for route in sumolib.xml.parse_fast("myRoutes.rou.xml", 'route', ['edges']):
    edge_ids = route.edges.split()
    # do something with the vector of edge ids
```

### routeファイルのvehicleとそのroute edgeをパース

```
for vehicle in sumolib.xml.parse("myRoutes.rou.xml", "vehicle"):
    route = vehicle.route[0] # access the first (and only) child element with name 'route'
    edges = route.edges.split()
```

自動的にデータ変換をかける場合（出発時間の"HH:MM:SS"を含む）

```
from sumolib.miscutils import parseTime
for vehicle in sumolib.xml.parse("myRoutes.rou.xml", "vehicle", attr_conversions={
            'depart' : parseTime,
            'edges' : (lambda x : x.split())}):
    edges = vehicle.route[0].edges
    if vehicle.depart > 42:
       ...
```


### edgeデータファイル（meanData）から全edgeをパース

```
for interval in sumolib.xml.parse("edgedata.xml", "interval"):
    for edge in interval.edge:    
        # do something with the edge attributes i.e. edge.entered
```

### 座標変換

```
net = sumolib.net.readNet('myNet.net.xml')
# network coordinates (lower left network corner is at x=0, y=0)
x, y = net.convertLonLat2XY(lon, lat)
lon, lat = net.convertXY2LonLat(x, y)
# raw UTM coordinates
x, y = net.convertLonLat2XY(lon, lat, True)
lon, lat = net.convertXY2LonLat(x, y, True)
# lane/offset coordinates
# from lane position to network coordinates
x,y = sumolib.geomhelper.positionAtShapeOffset(net.getLane(laneID).getShape(), lanePos)
# from network coordinates to lane position
lane, d = net.getNeighboringLanes(x, y, radius)[0] (see "locate nearby edges based on the geo-coordinate" above)
lanePos, dist = sumolib.geomhelper.polygonOffsetAndDistanceToPoint((x,y), lane.getShape())
```
[TraCI/Interfacing_TraCI_from_Python\#coordinate_transformations](../TraCI/Interfacing_TraCI_from_Python.md#coordinate_transformations)も参照してください。

### xmlの操作と書き込み

```
with open("patched.nod.xml", 'w') as outf:
    # setting attrs is optional, it results in a cleaner patch file
    attrs = {'node': ['id', 'x', 'y']}  # other attrs are not needed for patching
    # parse always returns a generator but there is only one root element
    nodes = list(sumolib.xml.parse('plain.nod.xml', 'nodes', attrs))[0]
    for node in nodes.node:
        node.addChild("param", { "key": "origPos", "value" : "%s %s" % (node.x, node.y) } )
        node.x = float(node.x) + random.randint(-20, 20)
        node.y = float(node.y) + random.randint(-20, 20)
    outf.write(nodes.toXML())
```

## その他の例

[{{SUMO}}/tests/tools/sumolib]({{Source}}tests/tools/sumolib)のtestサブフォルダにある*runner.py*に、更なる別のsumolibの使用例があります。

