# TraCI/GUI 変数の取得

[原文](https://sumo.dlr.de/docs/TraCI/GUI_Value_Retrieval.html)

## コマンド 0xac: GUI 変数の取得

|ubyte|string|
-|-
|変数|View ID|

GUI の変数の値を取得します。
View ID は"View #0"のような形をとり、最後の桁が GUI シミュレーションとして開かれている(サブ)ウィンドウの数をカウントします。
id はビューのサブウィンドウが非最大化されたときにビューのタイトルバーに表示されます(これは[新規ビューを開く]()ときにも自動的に行なわれます)。

<div style="text-align: center; font-weight: bold">
GUI 変数取得の概要
</div>
|変数|型|説明|[Python メソッド]|
-|-|-|-
|zoom (0xa0) |double| 現在のズームレベル(%)|[getZoom](https://sumo.dlr.de/pydoc/traci._gui.html#GuiDomain-getZoom)|
|offset (id 0xa1)|2D-position|現在見える範囲の中心座標のネットワーク中の位置|[getOffset](https://sumo.dlr.de/pydoc/traci._gui.html#GuiDomain-getOffset)|
|schema (id 0xa2)|string|使用中の可視化方法(例: "standard"や"real world")|[getSchema](https://sumo.dlr.de/pydoc/traci._gui.html#GuiDomain-getSchema)|
|boundary (id 0xa3)|2D-polygon|見えているネットワークの左下および右上|[getBoundary](https://sumo.dlr.de/pydoc/traci._gui.html#GuiDomain-getBoundary)|
|has view (id 0xa7)|bool|与えられた ID が見えるか|[hasView](https://sumo.dlr.de/pydoc/traci._gui.html#GuiDomain-hasView**|

## レスポンス 0xbc: GUI の値

|ubyte|string|ubyte|<return_type>|
-|-|-|-
|変数|ビューの ID|変数の型|<VARIABLE_VALUE>|

**"GUI 変数取得コマンド"**への対応になります。
