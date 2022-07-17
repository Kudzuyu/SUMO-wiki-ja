<!-- read: 読み出し、load: 読み込み -->

# Shapes

参考原文バージョン: 2022/2/2, 60aea55fd807421a02e3e5b30fb7fa4d4632ab39

## シミュレーション内でのポリゴンとPOIの使用

* ポリゴンとPOIの使用例（from Traffic Online, area#1）*
![tol1_with_polys.gif](../images/Tol1_with_polys.gif "ポリゴンとPOIの使用例（from Traffic Online, area#1")

色のあるポリゴンとPOI（points of interest）の定義は[*additional-file*](../sumo.md#format_of_additional_files)で読み込むことできます。
現在、これらの形状は、シミュレーションの見た目を改善し、デバッグを容易にすることを目的としています。
それらとの特別な相互作用はまだ実装されていません。

ポリゴンとPOIの両方は"layer"に配置される場合があります。
レイヤーの値が最も低い形状は、よりレイヤーの値が高い形状の後ろになります。
ネットワーク自身はlayer 0として描写されます。
additionalファイルはPOIとポリゴンの両方の定義を含む場合があります。

幾何学的なオブジェクトは、手動で定義するか、[polyconvert](../polyconvert.md)を使ってインポートできます。
適切なgeometry-fileはadditionalファイルの1つとして[sumo](../sumo.md)に与えることができます（**--additional-files <FILE\>**オプションを使用）。
[sumo-gui](../sumo-gui.md)で利用するには、使用する[configurationfile](../Basics/Using_the_Command_Line_Applications.md#configuration_files)内でadditionalファイルのリストに加えるか、[GUI](../sumo-gui.md#loading_shapes_and_pois)でインタラクティブにadditionalファイルを読み込む必要があります。

## 定義

幾何学的オブジェクト（POIやpolygon）は"additional file"に1つずつ保存されます。
現在、root要素は任意です。

### Polygonの定義

polygonは次のように定義されます。
`<poly id="<POLYGON_ID>" type="<TYPENAME>" color="<COLOR>" fill="<FILL_OPTION>" layer="<LAYER_NO>" shape="<2D-POSITION>[ <2D-POSITION>]*"/>`

各属性は次のような意味があります。

| Attribute Name | Value Type       | Description                                                                         |
| -------------- | ---------------- | ----------------------------------------------------------------------------------- |
| **id**         | id (string)      | polygonのuniqueなid |
| **shape**      | 2D position list | polygonの形状                                                            |
| color          | color            | polygonを表示するRBGAカラー、詳しくは{{DT_Color}}を参照してください。|
| geo            | bool             | 形状を地理座標として解釈して変換するか否か |
| fill           | bool             | polygonを塗りつぶすか否か。boolオプションでデフォルトは*false*|
| lineWidth      | double           | 塗りつぶされていないpolygonを描写する幅（m単位、デフォルトは*1*）|
| layer          | float            | polygonラインのあるレイヤー。設定は任意（optional）|
| type           | string           | polygonのtype名|
| imgFile        | string           | このpolygonをレンダリングするのに使うビットマップ |
| angle          | float            | レンダリングされる画像角度（度単位） |

### POI（Point of interest）定義

POI(point-of-interest)は次のように定義されます。
`<poi id="<POLYGON_ID>" type="<TYPENAME>" color="<RED>,<GREEN>,<BLUE>" layer="<LAYER_NO>" [(x="<X_POS>" y="<Y_POS>") | (lane="<LANE_ID>" pos="<LANE_POS>")]/>`

poiの位置する場所は、x/y座標か、laneの名前とそのlaneにおける位置のいずれかを使って与えることができることを意味しています。
各属性は次のような意味があります。

| Attribute Name        | Value Type  | Description|
| --------------------- | ----------- | ---------------------------------------------------------------------------------- |
| **id**                | id (string) | polygonのuniqueなid |
| **color**             | color       | poiを表示する色。*<RED\>*、*<GREEN\>*、*<BLUE\>*は0から1の間の値である必要があります。この値は','を使って区切られます。設定は任意でデフォルトは*1,0,0*です。|
| x<sup>(\*)</sup>      | float       | x軸上のpoiの位置（m単位）|
| y<sup>(\*)</sup>      | float       | y軸上のpoiの位置（m単位）|
| lane<sup>(\*)</sup>   | id (string) | poiが位置するlaneの名前。laneは読み込まれたネットワーク上に存在する必要があります。|
| pos<sup>(\*)</sup>    | float       | poiが位置するlaneの位置|
| posLat<sup>(\*)</sup> | float       | poiが位置するlaneにおける横方向のoffset（負の値は、走行方向の車線中心線の右側になります）|
| lon<sup>(\*)</sup>    | float       | 東西軸上のpoiの地理座標（度単位）|
| lat<sup>(\*)</sup>    | float       | 南北軸上のpoiの地理座標（度単位）|
| type                  | string      | poiのtype名|
| layer                 | float       | 描写や選択のためのpoiのレイヤー|
| imgFile               | string      | このpoiをれだリングするのに使われるbitmap。何も与えられない場合は、代わりに円形が描写されます。ビットマップは白色（*1,1,1*）でない限りは指定された色で着色されます。|
| width                 | float       | レンダリングされる画像の幅（m単位）|
| height                | float       | レンダリングされる画像の高さ（m単位）|
| angle                 | float       | レンダリングされる画像角度（度単位） |


<sup>(\*)</sup> `x/y`、`lane/pos`、`lon/lat`のいずれか1つを与える必要があります。

!!! note "注"
    *lane*、*pos*、*posLat*属性を指定する場合、その属性はTraCIからアクセスできる[generic parameters](../Simulation/GenericParameters.md)として自動的に追加されます。

## 関連情報

- 他のソースからpolygonやPOIをインポートする方法を知るには、[polyconvert](../polyconvert.md)の説明を確認してください。
- （開発者向け）[Developer/Implementation Notes/Drawing in sumo-gui](../Developer/Implementation_Notes/Drawing_in_sumo-gui.md)では、[sumo-gui](../sumo-gui.md)が読み込んだstructureをレンダリングする方法を説明しています。
- [TraCI](../TraCI.md)を経由して、[読み込まれたPOI変数の読み出し](../TraCI/POI_Value_Retrieval.md)や[読み込まれたpolygon変数を読み出し](../TraCI/Polygon_Value_Retrieval.md)が可能です。
- [TraCI](../TraCI.md)を経由して、[POIを追加してそれらのプロパティを操作](../TraCI/Change_PoI_State.md)したり、[polygonでも同様のこと](../TraCI/Change_Polygon_State.md)ができます。

