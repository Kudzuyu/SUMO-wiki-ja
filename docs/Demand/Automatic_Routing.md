<!-- 
dynamic user equilibrium : 動的利用者均衡
period : 間隔
interval : 間隔
district : 地区
Adapting by X : Xによる更新
apadt : 適用，更新
insertion : 挿入時, 挿入
the multiple of X and Y : XとYの倍数
route : （固有名と思われる個所以外は）経路
 -->

# 自動ルーティング

参考原文バージョン: 2021/2/11, 6f16726b811a2e7785fa7181cefc8de802c4d96c

## 導入


次の場面では、シミュレーション実行中の動的ルーティングが適切な場合があります。
- 動的利用者均衡を得るための時間や計算量が不十分な場合
- シミュレーション実行中にネットワークの変更が生じる場合
- 実行中にvehicleの経路を更新する必要がある場合

この場合、routeファイルかtripファイル、もしくはその組合せを入力として、[sumo](../sumo.md)をルーティングに直接用いることができます。

このルーティング方法を機能させるには、ルートを周期的に再計算する能力を、一部、もしくは全てのvehicleに与えます。
このルーティングは、ネットワーク内の現在と直近の交通状況を考慮しているため、ネットワーク内の混雑やその他の変化に適応できます。
下記オプションによって、どのvehicleに装備させるか、どの頻度で再ルーティングをするか、どうやって現状や直近の知識から推定旅行時間を計算するかを設定できます。

## オプション

ルーティングに関連するオプションは次の通りです。

| Option                                          | default        | Description                                                                               |
|-------------------------------------------------|----------------|-------------------------------------------------------------------------------------------|
| **--device.rerouting.probability** {{DT_FLOAT}} | -1             | ルーティングデバイスを持つvehicleの確率（-1は0と等価） |
| **--device.rerouting.explicit** {{DT_STR}}      |                | 指定されたvehicleにデバイスを割り当てる |
| **--device.rerouting.deterministic**            | false          | The devices are set deterministic using a fraction of 1000 (with the defined **probability**) |
| **--device.rerouting.period** {{DT_STR}}        | 0              | vehicleのルートが変更される間隔 |
| **--device.rerouting.pre-period** {{DT_STR}}    | 60             | 挿入や出発の前のルート変更間隔 |
| **--device.rerouting.adaptation-interval** {{DT_INT}} | 1              | edgeの重みを更新する間隔 |
| **--device.rerouting.adaptation-weight** {{DT_FLOAT}} | 0.0 (disabled) | 指数平均のための初期のedge重み。[0,1]|
| **--device.rerouting.adaptation-steps** {{DT_INT}}    | 180            | 平均化のためのadaptation stepの数（>0）|
| **--device.rerouting.with-taz**                  | false          | [traffic assignment zones (TAZ/districts)](../Demand/Importing_O/D_Matrices.md#describing_the_taz)をルーティングのエンドポイントとして使う|
| **--device.rerouting.init-with-loaded-weights**  | false          | オプション**--weight-files**をシミュレーション開始時のedge重みの初期値に使用するか|

vehicleがルーティングデバイスを持つとき、*挿入前*のみ、再ルーティングはデフォルトで有効になります。
周期的な再ルーティングを有効にするには**--device.rerouting.period**を設定します。

## Edgeの重み

いずれかのvehicleでルーティングが有効になっている場合、すべてのedgeについてネットワークにおける平均旅行時間を収集します。
もし、".period"オプションによる定期的な経路選択時か挿入時のいずれかでvehicleを経路を決める場合、現在のedgeの重み（旅行速度、つまり旅行時間）に従いvehicleは目的のedge（もしくは地区）への最短経路を選択します。
edge重みの更新は、単に過去の値を書き換えるのではなく、次の重み付き平均化で計算されます。
各シミュレーションステップにおける全edgeの重み更新は、シミュレーションの実行速度低下の主な原因であり、この間隔は".adaptation-interval"オプションで変更可能です。

!!! note "訳注"
    これらの重みは、*vehicle.setRoutingMode*を使ってルーティングモードが*ROUTING_MODE_AGGREGATED*に設定されている場合に、[TraCI](../TraCI.md)の関数*vehicle.rerouteTraveltime*と*vehicle.changeTarget*を使ったときに参照されます。
    同様に、*simulation.findRoute*関数は、引数（routingMode=*ROUTING_MODE_AGGREGATED*）を設定することで、これらの重みを使うように切り替えられます。

### 指数平均による更新

**--device.rerouting.adaptation-weight** {{DT_FLOAT}} オプションを設定することで、各edgeの旅行速度は次のように計算されます。

```
FLOAT * priorValue + (1 - FLOAT) * currentMeanSpeed
```

この平均化は**--device.rerouting.adaptation-interval**で設定された間隔に従って実行されます。

### 移動平均による更新

**--device.rerouting.adaptation-steps** {{DT_INT}}オプションを設定することで、各edgeの旅行速度は、INTの最新のmeanSpeedの平均値で計算されます。
この平均化は**--device.rerouting.adaptation-interval**で設定された間隔に従って実行されます。

!!! note "訳注"
    平均化には**adaptation-interval**と**adaptation-steps**の倍数にまで遡った速度の値が使われます。

### edgeの重みを調べる

シミュレーション中のedgeの重みの変化を理解するのに、次の詳細値を確認することが役立ちます。

- [sumo-gui](../sumo-gui.md#changing_the_appearance.2Fvisualisation_of_the_simulation)で道路を*by routing device assumed speed*で色付け
- **--device.rerouting.output** {{DT_FILE}}オプションを使ってrawな値を出力
- [TraCI function''vehicle.getParameter("device.rerouting.edge:EDGEID")](../TraCI/Vehicle_Value_Retrieval.md#supported_device_parameters)を使って、各edgeの平均旅行時間を取得

## 不完全なtripとflow

明示的にデバイスを設定していなくても、tripか"from"と"to"属性のあるflowを使って生成された全てのvehicleは、挿入時に自動的にルーティングされます。
ルーティングでエラーが生じる、つまり、全ての必須のedge（"from"、"to"、stopのedge）と接続性（走行可能なvehicle classも考慮される）を満たす経路が見つからないときはいつでも、致命的エラーとしてシミュレーションが止まります。
これは、 **--ignore-route-errors**を使い、エラーが起きた場合にrouteを変更しないようにすることで無効化できます。
（tripを使って定義されていることで）vehicleがrouteを持たず、経路が見つからないうえ、**--ignore-route-errors**が使われている場合は、そのvehicleは挿入されません。
もし、[地区ファイル](../Demand/Importing_O/D_Matrices.md#describing_the_taz)が読み込まれている場合、"from"と"to"属性の代わりに"fromTaz"と"toTaz"を使うことができます。


## パラメーターを使った別の宣言方法

再ルーティングデバイスのあるvehicle集合を定義する別の方法として、[generic parameters](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#devices)を使う方法があります。

## TraCI

TraCI関数の*vehicle.getParameter*と*vehicle.setParameter*を使うことで、ルーティングデバイスにアクセスできます。

**getParameter**

- device.rerouting.period（秒単位の個々の再ルーティング間隔を返します。）
- device.rerouting.edge:EDGE_ID（再ルーティングのためのEDGE_ID（ネットワークedgeのid）の推定旅行時間を返します。）
- has.rerouting.device（デバイスの有無を"true"か"false"で返します。）

**setParameter**

- device.rerouting.period（doubleリテラル。秒単位の再ルーティングの間隔を設定します。）
- device.rerouting.edge:EDGE_ID（doubleリテラル。全車両の再ルーティングのための推定旅行時間を設定します。EDGE_IDはネットワークのedgeのid。この値は次の更新インターバル（--device.rerouting.adaptation-interval）で上書きされます。）
- has.rerouting.device（"true": 自動的・動的な再ルーティングを有効化します。）

## ランダム性

**--weights.random-factor** {{DT_FLOAT}}オプションを設定したとき、ルーティングのためのedgeの重みは、ランダムな係数（1から{{DT_FLOAT}}の一様分布から選ばれた値）によって動的に歪められます。
このランダム化はedgeの重みが使われるたび実行されるため、同一のvehicleが、異なるタイムステップで、異なる経路を選びます。
この方法で生成される経路は、指定された係数により、最悪時には、最短経路より長くなる可能性があります。
このランダム性は、グリッド型のネットワークなど、複数の似通った経路が利用できる状況において、合理的な経路分布を達成するのによい方法です。

## 並列化

シミュレーションにおけるルーティングは並列化可能です。
この機能は、周期的な再ルーティングが有効で、多くの処理時間を要する状況で有効です。
ルーティングを並列実行するには、**--device.rerouting.threads** {{DT_INT}}オプションで並列化するスレッド数を設定します。
**--device.rerouting.synchronize**オプションを設定すると、全てのvehicleが同時に再ルーティングされることを保証します。（デフォルトでは、vehicleの挿入時間に沿って再ルーティングされます。）
