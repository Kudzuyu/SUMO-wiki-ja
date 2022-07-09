
<!-- 
emitted into : 挿入する
write : 書き込む
invalid : 無効な
 -->

# VehRoutes

参考原文バージョン: 2022/3/14, 509d321714ca5a1a9fb9759aed4e0d22715c3d23

この出力にはvehicleの選択したrouteが含まれ、そのrouteが新たなrouteで置換された場合は、置換時点でのedgeとともにそれ以前のrouteがレポートされます。
さらに、vehicleがネットワークに出入りした時刻も格納されます。

通常の条件、つまり、全てのvehicleがあらかじめ決められたrouteを使う場合、出力にrouteやtripinfoから得られない情報は含まれません。
しかし、シミュレーション中にvehicleをrerouterなどで再ルーティングすると同時に、出力に新たな情報が含まれます。

## シミュレーション内でのインスタンス化

この出力は**--vehroute-output** {{DT_FILE}}か**--vehroutes** {{DT_FILE}}オプションを使うことで有効になります。
この出力に影響する他のオプションは[SUMO\#Output](../../sumo.md#output)にリスト化されています。

## 生成される出力

生成されたファイルは次のようになっています。

```xml
<routes>
    <vehicle id="<VEHICLE_ID>" [type="<TYPE_ID>"] depart="<INSERTION_TIME>" arrival="<ARRIVAL_TIME>" [routeLength="<LENGTH>"]>
        <routeDistribution>
            <route replacedOnEdge="<EDGE_ID>" replacedAtTime="<TIME>" probability="0" edges="<PREVIOUS_ROUTE>"/>

            ... 他の置換されたroute ...

            <route edges="<LAST_ROUTE>" [exitTimes="<EXIT_TIMES>"]/>
        <routeDistribution>
    </vehicle>

    <person id="<PERSON_ID>" depart="<INSERTION_TIME>" arrival="<ARRIVAL_TIME>">
        <ride from="..." to="..." lines="..." [started="<START_TIME>" ended="<END_TIME>"]/>
        <walk edges="..." speed="..." [exitTimes="<EXIT_TIMES>" started="<START_TIME>" ended="<END_TIME>"]/>
    </person>

    ... 他のvehicleやpersonに関する情報 ...

</routes>
```

| Name              | Type            | Description                                                                                 |
| ----------------- | --------------- | ------------------------------------------------------------------------------------------- |
| id                | (vehicle) id    | エントリが記述しているvehicle id |
| type              | vehicle type id | デフォルトと異なる場合、vehicle typeのid |
| depart            | s               | vehicleがネットワーク上に挿入された時刻 |
| arrival           | s               | routeの終端に到達したことで、vehicleがシミュレーションから削除された時刻 |
| routeLength       | m               | vehicleのrouteの合計長さ（vehroutes.route-lengthオプションが有効化されていた場合）|
| replacedOnEdge    | (edge) id       | routeが置き換えられたときvehicleがいたedge |
| replacedAtTime    | s               | 置換が起きたタイムステップ |
| <PREVIOUS_ROUTE\> | \[(edge) id\]+  | 置き換えられたroute|
| <LAST_ROUTE\>     | \[(edge) id\]+  | 最終的なvehicleのroute |
| <EXIT_TIMES\>     | \[time in s\]+  | **--vehroute-output.exit-times**オプションが有効化されている場合、routeまたはwalk内の各edgeの出発時刻 |
| <END_TIME\>       | s               | **--vehroute-output.exit-times**が有効化されている場合、walkやride（もしくはcontainerのtranship/transport）の到着時刻 |
| <START_TIME\>     | s               | **--vehroute-output.exit-times**オプションが有効化されている場合、walkの出発時刻か、vehicleに乗り込み再度運転を開始する時刻（containerのtranship/transportも含む）|

!!! note "注"
    vehicleに追加属性が設定されていた場合はそれも含まれます。

前と最後のrouteの両方が完了しているとは、routeが置換されない限り、vehicleが通らなければならない全てのedgeをrouteに含むことを意味します。
replacedOnEdgeとreplacedAtTime情報は置換されたrouteでのみ使用できます。
確率フィールドは、vehicleがそのrouteの最後まで移動するシミュレーションの入力にファイルが使えるようにするためだけに与えられます。
シミュレーションへの適切な入力になるよう、ファイルも出発時間で並べ替えられる必要があります。
この並べ替えは、**--vehroute-output.sorted**オプションを設定することで達成されます。

## 選択されたvehicleかvehicle typeのみ出力する
デフォルトでは全てのvehicleがvehroute出力を生成します。
選択したvehicleやvehicle typeに対して[vehrouteデバイスを割当て](../../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#assignment_by_generic_parameters)ることで、この設定は変更できます。
例えば、次の定義はvehicle type **t1**のデバイスを有効にします。

```xml
<vType id="t1">
  <param key="has.vehroute.device" value="true"/>
</vType>
```

別の方法として、vehroute出力を生成するvehicleの確率を設定するのに、SUMOの**--device.vehroute.probability*オプションを使うことができます。
例えば、オプションを**--device.vehroute.probability 0.25**と設定すると、1/4のvehicleにvehrouteデバイスが装備されます（各vehicleが25%の確率で装置の有無を決定します）。

## その他のオプション

- **--personroute-output FILE**: personやcontainerの出力を別のFILEに書き込み
- **--vehroute-output.exit-times**: 全てのedgeの終了時刻を書き込み。stopは'started'と'ended'属性、rideは'ended'を含みます
- **--vehroute-output.last-route**: シミュレーション中にvehicleが再ルーティングされた場合は、最後のrouteのみを書き込み
- **--vehroute-output.sorted**: 出発時間で書き出されるvehicleを並べ替え
- **--vehroute-output.dua**: duarouter-alternatives形式で出力を書き込み
- **--vehroute-output.cost**: 全てのrouteについて'cost'属性を書き込み
- **--vehroute-output.intended-depart**: 出発遅れが生じた場合でも、実際の出発時刻ではなく、決められていた出発時間を使用
- **--vehroute-output.route-length**: routeの合計長さを'length'属性として書き込み
- **--vehroute-output.write-unfinished**: シミュレーション終了時、目的地に到達していないvehicleのvehroute出力を書き込み
- **--vehroute-output.skip-ptlines**:  'line'属性をもつ公共交通vehicleのvehroute出力をスキップ
- **--vehroute-output.incomplete**:   
vehroute出力に無効なrouteとrouteのスタブ（from-to）を含む
- **--vehroute-output.stop-edges**:   stop間のedgeに関する情報を含む
- **--vehroute-output.speedfactor**:   出力にvehicle固有のspeedFactorの情報を含む（departSpeedを設定されたvehicleの場合、デフォルトはtrue）
