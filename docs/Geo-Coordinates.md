<!-- 
Geo-Coordinates : 地理座標
Geo-Referenced : 地理参照
 -->

# 地理座標

参考原文バージョン: 2022/3/13, d7982a5f34cb4b2ed3a98784f5aba01fa5d5864b
[原文ページ](https://sumo.dlr.de/wiki/Geo-Coordinates)

## 地理関係ネットワーク

SUMOネットワークは常に直行座標系（メートル単位）でエンコードされ、緯度経度への変換を可能とするために地理情報を含んでいることがあります。
デフォルトでは直行座標系はネットワークの左下が0,0になるようにシフトしたUTM-projectionを使います。

!!! note "注"
    投影に関する情報は*.net.xml*ファイルの先頭にある`<location>`要素にエンコードされています。

* [OSM]()からネットワークをインポートすると、地理参照は生成された*.net.xml*ファイルに自動的に含まれます
* [平易なxmlファイル]()からネットワークをインポートすると、座標は緯度と経度で与えられ、**--proj.utm**のような投影オプションを使ってインポートされます
* シェープファイルからネットワークを読みこんだ場合は、地理参照は元となったデータのフォーマットに依存します

## 地理座標のチェック

[SUMO-GUI]()や[netedit]()において地理参照ネットワークではどこでも、右クリックすることでオプション*copy*から*geo-position to clipboard*が可能です。
*緯度*、*経度*座標の結果は[maps.google.com]や[map.bing.com]のようなマップエンジンにペーストするのに適しています。
また、地理座標と同じようにマウスカーソルの位置のネットワーク座標もウィンドウ右下に表示されています。

## 座標変換

* [TraCI]()を使うことで、地理座標をネットワーク座標（m,m）と地理座標（経度、緯度）の間で相互に変換できます。
* [sumolib]()でも同じことが可能です。

## XML入力における地理座標の使用

[duarouter]アプリケーションは、与えられた座標に最も近いedgeやjunctionへtripを直接マッピングする
[fromLonLat, toLonLat, viaLonLat](Demand/Shortest_or_Optimal_Path_Routing.md#trip_definitions)属性をサポートしています。


## 地理座標付き出力の取得

* netconvertコマンドを使うことでネットワークを地理座標付き*プレーンxml*でエクスポートすることができます。

```
netconvert --sumo-net-file myNet.net.xml --plain-output-prefix plain --proj.plain-geo
```

* [FCD出力]()では**--fcd-output.geo**オプションを付けることで、地理座標付きの出力を得ることができます。
* [duarouter]()は地理座標を用いてtrip定義を生成する**--write-trips.geo**オプションをサポートしています。（前節を参照してください）

## 地理座標のマッピング

地理座標（経度、緯度）と道路座標（laneID, offset）との間の変換が望ましい場合があります。
この変換は通常、経度、緯度からx,y座標（メートル単位のネットワーク座標）へ変換し、その座標を最も近いlaneに対応させる2ステップで実現されます。
このタスクには次の情報源が有用です。

- [軌跡をマッチングさせる方法](FAQ.md#how_do_i_generate_sumo_routes_from_gps_traces)
- [traci.moveToXY](TraCI/Change_Vehicle_State.md#move_to_xy_0xb4) はvehicleを適切なネットワーク上の位置に移動させます
- [subolibを使い地理座標をedgeに変換](Tools/Sumolib.md#locate_nearby_edges_based_on_the_geo-coordinate)
- [TraCI](TraCI/Simulation_Value_Retrieval.md#command_0x82_position_conversion) は座標（x,yもしくは経度、緯度）とedgeを変換します
