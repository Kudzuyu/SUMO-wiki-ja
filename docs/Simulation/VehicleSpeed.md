<!-- 
    desired speed : 希望速度
    right-of-way : 通行優先権
    minor road : 下級道路
    visibility : 視認性
    car-following : 後続車
-->

# VehicleSpeed

参考原文バージョン: 2022/8/30, 18fe56b7d8e4458e21cda47050f0bc801a014f7a

vehicleの速度に対する影響要因は多岐にわたります。
以下ではそれら要因について説明します。
各要因はvehicleの速度の上限を設定します。
任意の状況における実際の速度は、全ての要因の最小速度になります。

## 最大速度（maxSpeed）

[`<vType>-attribute maxSpeed`](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#vehicle_typesは、vehicleが走行する最大速度をモデル化します。
この速度は、エンジンの最大速度とみなせます。

## 最大希望速度（desiredMaxSpeed）

[`<vType>-attribute desiredMaxSpeed`](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#vehicle_types)は、vehicleのドライバーのタイプが使いたい平均的な最大希望速度をモデル化します。
各vehicleの実際の最大希望速度は、そのタイプの`maxDesiredSpeed`にvehicleの[individual speedFactor](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#speed_distributions)を乗じて計算されます。
個々の最大希望速度は、`maxSpeed`と道路の制限速度の次の上限として与えられます。

このプロパティの主な用途は、道路の法廷速度で制限できないvehicle（つまり歩行者や自転車）について、その速度分布をモデル化することです。
一方で、通常のvehicleは制限速度に制限され、個々のspeedFactorとspeedLimitを掛け合わせて速度分布がモデル化されます。
そのため、`desiredMaxSpeed`のデフォルト値は、[vClasses](../Definition_of_Vehicles%2C_Vehicle_Types%2C_and_Routes.md#abstract_vehicle_class)によって異なる値を持ちます。

- `pedestrian`: 1.39 (5km/h)
- `bicycle`: 5.56 (20km/h) 
-  その他、全てのクラス: 2778 (10000km/h)

!!! caution "注意"
    バージョン1.14.1までは、このプロパティは存在せず、`maxSpeed`が希望速度のモデル化に用いられていました。
    そのため、全ての自転車について、デフォルトの最大速度が一定値になっていました。

## edge/laneの速度と速度要因

通常、`speed`属性が[edgesに対して定義](../Networks/PlainXML.md#edge_descriptions)されています。
しかし、同一のedgeでも[laneの間で異なる](../Networks/PlainXML.md#lane-specific_definitions)場合もあります。
これは法定速度による制限をモデル化しています。

現在の制限速度より低いedgeに移動するとき、vehicleは、新たなedgeに到達する時点で新たな制限速度に収まるよう減速します。

各vehicleに[個々の速度係数（speedFactor）を割り当てて](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#speed_distributions)、vehicleにその制限を超えさせることができます。
バージョン1.0.0以降、vehicleは、分散0.1、平均1.0のランダムなspeedFactorを持っており、デフォルトでvehicleの集団内で希望速度が異なるようになっています。

vehicleが（他vehicleに制限されず）自由走行しているとき、次のスピードまで加速します。
```
min(maxSpeed, speedFactor * desiredMaxSpeed,  speedFactor * speedLimit)
```

!!! note "注"
    **--default.speeddev 0**オプションを設定することでレガシーな振舞いが得られます。

バージョン0.24.0以降は[edgeごとのvClass固有の速度制限](../Networks/PlainXML.md#vehicle-class_specific_speed_limits)を定義することもできます。


## 車両追従モデル

vehicleの[車両追従モデル](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#car-following_models)は、vehicleの前方方向の速度を決定します。
デフォルトモデルは、衝突を回避するために停止できる*安全な*最大速度を常に選択します。

### 加速と減速

全てのモデルは[acceleration an deceleration](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#car-following_models)に制約があり、その制約に左右されます。
デフォルトでは、vehicleは*accel*値より強く加速しません。
デフォルトモデルは（秒あたりの）*decel*値に収まるように操作を計画しますが、他のモデルはこの値について異なる解釈することがあります。
全てのモデルは*emergencyDecel*値より強くブレーキをかけることはありません。
この値は、デフォルトでは*deceL*と同じ値ですが、個別に設定することもできます。

!!! note "注"
    これは、利用可能なモデルが準ずる慣習であり、カスタムモデルで無視される可能性があります。

### Dawdling

いくつかの車両追従モデルは、ドライバーの不完全性（imperfection）をモデル化する`sigma`属性をサポートしています。
**0**以上の値では、デフォルトの車両追従モデルに従うドバイバーは、\[0, `accel`\]の間のランダムな量だけ安全な状態よりも遅く移動します。

## 交差点

通行優先権のないvehicleは、交差点に近づくとき減速しなければいけません。
もし、交差点が通行優先権をもつ他のvehicleに使用されている場合、安全な時間窓が見つかるまで停止する必要があります。
その時間窓は車両追従モデルと同じ安全性の仮定に基づきます。
この仮定は、デフォルトの*Krauss*モデルでは、先行車が急ブレーキで完全停止したとしても各vehicleは安全に停止できる必要があることを意味します。

vehicleが通行優先権を持っていても、[せっかちな（impatient）](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#impatience)ドライバーが交差点を渡ったことが原因で、vehicleは減速する必要があるかもしれません。
交差点における[通行優先権のルール](../Networks/PlainXML.md#right-of-way)は[nodeのtype属性](../Networks/PlainXML.md#node_descriptions)や[traffic lights](../Simulation/Traffic_Lights.md)で定義されます。

もしvehicleがまだ交差点に侵入していない場合、移動可能な[交差点内の待機場所](Intersections.md#waiting_within_the_intersection)が塞がれていない限りは、交差点に既に侵入している他vehicleに応じて、多くの場合は減速します。
もし、2つのvehicleが交差点内で同時に競合した場合、侵入した時刻や速度、通行優先権のルール、信号機の状態に基づいて優先順が決められます。
この優先順は減速すべきvehicleと通行可能なvehicleを決定します。

デフォルトでは、下級道路から近づくvehicleは、近くに優先的なvehicleがいない場合でも、交差点から4.5m離れた場所までに減速します。
減速後、安全距離が確保された場合に再加速できます。
この距離モデルは視認性をモデル化したもので、個々の[connectionの`visibility`属性](../Networks/PlainXML.md#connection_descriptions)で設定できます。

'zipper'タイプの交差点に近づくvehicleは、vehicleの順番を位置と速度に基づいて自動的に決定します。
先行車に滑らかに追従するために減速する必要があるかもしれません。
デフォルトでは、zipperの合流行動は交差点の100m手前で開始されます。
この距離は'visibility'属性を使って設定することもできます。

交差点を通過するvehicleは、[曲がり角に応じた減速制限](Intersections.md#speed_while_passing_the_intersection)にも左右される可能性があります。

## レーン変更

vehicleは、レーン変更操作の実行のために減速することがあります。
レーン変更する他vehicleを支援するために減速することもあります。
もし、vehicleのいるlaneがvehicleのrouteにおける次のedgeに接続していなかった場合、vehicleは減速したのち停止します。

## Stops

[`stop`-definition](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#stops)の位置へ近づくとvehicleは減速します。

## 加減速制約

vehicleは、時間ステップごとに特定の量だけ速度を変更できます。
この量は[`<vType>`の属性の`accel`と`decel`](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#vehicle_types)で定義されます。

## departSpeed / arrivalSpeed

vehicleは、個々に設定された[`departSpeed`](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#vehicles_and_routes)でネットワークに挿入されます。
routeの終端に近づく場合、vehicleは、設定された[`arrivalSpeed`](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#vehicles_and_routes)に一致するよう速度を調整します。

## 速度可変標識（Variable Speed Signs）

[Variable speed signs](../Simulation/Variable_Speed_Signs.md)は、設定された時間インターバルでedgeの速度制限を変更するのに使われます。

## キャリブレータ―

[Calibrators](../Simulation/Calibrator.md)は、設定された時間インターバルでedge上のflowを合わせるのに用いられますが、edgeの制限速度の修正にも用いることができます。

## デバイス

[Vehicle devices](../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#devices)は、vehicleの振舞いをカスタマイズしたり、追加の出力を生成する方法です。
次のデバイスはvehicleの速度に影響を与えることができます。

- [glosa](../Simulation/GLOSA.md) : 信号機付近でスムーズな速度に加減速
- [driverstate](../Driver_State.md) : 後続車とのギャップと速度差に関する認識エラーに基づき、速度をランダムに変化

## TraCI
[TraCIコマンド](../TraCI/Change_Vehicle_State.md)を使うことでvechileに速度を強制できます。
*slow down*コマンドを使う場合、速度に対する確率的な影響は適用されません。
[*speed mode*コマンドを使うことで、種々のsafetyに関する影響を選択的に無効化できます。](../TraCI/Change_Vehicle_State.md#speed_mode_0xb3)

