# FullOutput

2021/2/11, 6f16726b811a2e7785fa7181cefc8de802c4d96c

このオプションの背後にあるアイデアは、既存のnetstate-dumpオプションの機能を改善することです。
生成されるXML構造体はedge、lane、vehicle、traffic lightに関する情報を含んでいます。
このオプションの意図は、全てのシミュレーションコマンド（例えば、traci）を記録する必要なしに、シミュレーション結果を確認することです。

## シミュレーション内でのインスタンス化

SUMOにfull-dumpを含むファイルをビルドさせるには、**--full-output** {{DT_FILE}}でコマンドラインのパラメータを拡張してください。
{{DT_FILE}}は書き出される出力ファイル名です。
同じ名前の他のファイルは上書きされます。また、書き出し先のフォルダが存在している必要があります。

## 生成される出力

full-dumpのxmlファイルは各時刻における各edge、lane、vehicle、traffic lightに関する情報を含みます。
full-dumpファイルは次ようになります。

```
<full-export>
    <data timestep="<TIME_STEP>">
    <vehicles>
        <vehicle id="<VEHICLE_ID>" eclass="<VEHICLE_ECLASS>" co2="<VEHICLE_CO2>" co="<VEHICLE_CO>" hc="<VEHICLE_HC>"
        nox="<VEHICLE_NOX>" pmx="<VEHICLE_PMX>" fuel="<VEHICLE_FUEL>" electricity="<VEHICLE_ELECTRICITY>" noise="<VEHICLE_NOISE>" route="<VEHICLE_ROUTE>" type="<VEHICLE_TYPE>"
        waiting="<VEHICLE_WAITING>" lane="<VEHICLE_LANE>" pos_lane="<VEHICLE_POS_LANE>" speed="<VEHICLE_SPEED>"
        angle="<VEHICLE_ANGLE>" x="<VEHICLE_POS_X>" y="<VEHICLE_POS_Y>"/>
        ... 他のvehicle ...
    </vehicles>
    <edges>
        <edge id="<EDGE_ID>" traveltime="<EDGE_TRAVELTIME>">
        <lane id="<LANE_ID>" co="<LANE_CO>" co2="<LANE_CO2>" nox="<LANE_NOX>" pmx="<LANE_CO>"
        hc="<LANE_HC>" noise="<LANE_NOISE>" fuel="<LANE_FUEL>" electricity="<LANE_ELECTRICITY>" maxspeed="<LANE_MAXSPEED>" meanspeed="<LANE_MEANSPEED>"
        occupancy="<LANE_OCCUPANCY>" vehicle_count="<LANE_VEHICLES_COUNT>"/>
            ... 存在する他のedgeのlane
        </edge>
            ... 他のネットワーク上のedge
    </edges>
    <tls>
        <trafficlight id="0/0" state="GgGr"/>
        ... 他のtraffic light
    </tls>
</data>
... 次のタイムステップ ...
</full-export>
```

書き出される値の意味は次の表の通りです。

| Name                | Type                 | Description                                                                                                             |
| ------------------- | -------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| time_step          | (simulation) seconds | このtimestep要素内の値のタイムステップ |
| id                  | id                   | vehicle/lane/edge/trafficlightのid |
| eclass              | id                   | vehicleの特定のemission classのid |
| co2\@vehicle         | mg/s                 | time_stepでvehicleが排出するCO2の量 |
| co2\@lane            | mg/s                 | time_stepにlane上のvehicleが排出するCO2の総量 |
| co\@vehicle          | mg/s                 | time_stepでvehicleが排出するCOの量 |
| co\@lane             | mg/s                 | time_stepにlane上のvehicleが排出するCOの総量 |
| hc\@vehicle          | mg/s                 | time_stepでvehicleが排出するHCの量 |
| hc\@lane             | mg/s                 | time_stepにlane上のvehicleが排出するHCの総量 |
| nox\@vehicle         | mg/s                 | time_stepでvehicleが排出するNOXの量 |
| nox\@lane            | mg/s                 | time_stepにlane上のvehicleが排出するNOXの総量|
| pmx\@vehicle         | mg/s                 | time_stepでvehicleが排出するPMXの量|
| pmx\@lane            | mg/s                 | time_stepにlane上のvehicleが排出するPMXの総量 |
| noise\@vehicle       | dB                   | time_stepでvehicleが出すノイズの量 |
| noise\@lane          | dB                   | lane上のvehicleが排出するノイズの量 |
| fuel\@vehicle        | ml/s                 | time_stepでvehicleが消費する燃料 |
| fuel\@lane           | ml/s                 | lane上のvehicleが消費する燃料 |
| electricity\@vehicle | Wh/s                 | time_stepでvehicleが消費する電力 |
| electricity\@lane    | Wh/s                 | lane上のvehicleが消費する電力 |
| route               | id                   | routeの名前 |
| type                | id                   | vehicle typeの名前 |
| waiting             | seconds              | vehicleが待機している総時間 |
| lane                | id                   | laneの名前 |
| pos                 | meters               | lane上のvehicleの位置（laneの開始位置からフロントバンパーまでの距離） |
| speed               | m/s                  | vehicleの走行速度 |
| angle               | degree               | vehicleの角度 |
| pos_x              | \---                 | vehicleのx軸の絶対座標（フロントバンパー中央）。値は、指定された地理投影に依存します。 |
| pos_y              | \---                 | vehicleのy軸の絶対座標（フロントバンパー中央）。値は、指定された地理投影に依存します。  |
| traveltime          | seconds              | laneの平均旅行時間 |
| fuel\@lane           | l/km/h               | laneの燃料消費量 |
| maxspeed            | m/s                  | laneのvehicleの最大速度 |
| meanspeed           | m/s                  | laneのvehicleの平均速度 |
| occupancy           | %                    | laneの占有率（パーセント）　|
| vehicles_count     | \#veh                | lane上のvehicle数 |
| state               | string               | 現在の[traffic lightの状態](../../Simulation/Traffic_Lights.md) |

## 注釈

生成されるファイルサイズが非常に大きいので、bzip2などの圧縮ツールにファイルを直接パイプしたほうがよいです。
この巨大なファイルの利点は、例えば、traffic lightの状態とlaneの旅行時間など、あなたにとって重要なものを出力するためのXMLスタイルシートを書くことができる点です。
