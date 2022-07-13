
# District

参考原文バージョン: 2022/3/9, 1a2b7091aba72bb4606ceccbcc31bbbd93158db9

## districts2poly.py

[districts](../Demand/Importing_O/D_Matrices.md#describing_the_taz)を[sumo-gui](../sumo-gui.md)における可視化のためのpolygonに変換します。
**--hue, --saturation, --brightness**オプションを使うことで色を制御できます。
各オプションは、\[0, 1\]の値だけでなく、特殊な値*random*をサポートしています。

```
python tools/districts2poly.py <net-file> <route-file>
```

!!! caution
    現在は'edges'属性を使ったdistrictsのみサポートされています。

## edgesInDistricts.py

ネットワークとpolygonのリストをパースして、各polygonの内部にある全てのedgeからなるtazファイルを書き出します。
taz-shapeファイルは[polyconvert](../polyconvert.md)で生成されるフォーマットである必要があります。

```
python tools/edgesInDistricts.py -n <net-file> -t <taz-files>
```

詳細は**--help**オプションを呼び出してください。

!!! caution
    提供されるtaz shapeはネットワークファイルと同じ座標投影を使っている必要があります。
    [polyconvert](../polyconvert.md)でshapeを読み込む時にこれを確認する最も良い方法は、**--net-file**オプションを設定することです。

## filterDistricts.py
与えられたvehicle classが許可されたedgeのみをtaz定義に含めるよう、ネットワークファイルとvehicle classを使ってtaz（district）ファイルをフィルタします。

```
python tools/district/filterDistricts.py -n <net-file> -t <taz-file> -o <output-file> --vclass passenger
```

詳細は**--help**オプションを呼び出してください。

## generateBidiDistricts.py

互いに逆向きのedgeを探し、それを共通のdistrict（TAZ）に配置します。
[fromTazとtoTaz属性のあるtrip](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#traffic_assignement_zones_taz)と組合せてルーティングを改善するのに使えます。

```
python tools/generateBidiDistricts.py <net-file>
```

詳細は**--help**オプションを呼び出してください。

### 使用例

一般的なOSMネットワークに適用するとき、edgeとnegetedなidをもつedgeは、同じ道路の異なる方向のedgeを表現します。
生成されたbidi-tazは、次のようになります。

```
<taz id="-123" edges="-123 123"/>
<taz id="123" edges="-123 123"/>
```

*from*と*to*属性を使う一般的な`<trip>`定義が、代わりに*fromTaz*と*toTaz*属性を使う場合は、

```
<trip id="someTrip" from="123" to="456" depart="0"/>
<trip id="someTripWithBidiTaz fromTaz="123" toTaz="456"/>
```

2番目の定義は、taz*123*の定義方法によって、edge*123*かedge*-123*のいずれかから出発ことを許します。
これは、望ましくないターンアラウンドを生成されたtripの最初と最後で防ぐことで、座標変換のマッピングから生成されたtripを簡略化します。

## gridDistricts.py

与えられたネットワークファイルに対して、与えられた幅（m単位）のdiscricts（taz）のグリッドを生成する。

```
python tools/district/gridDistricts.py -n <net-file> -o <output-file> -w 300
```