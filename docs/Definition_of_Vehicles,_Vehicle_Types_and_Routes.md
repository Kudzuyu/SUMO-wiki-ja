# 車両、車両タイプ、経路の定義

**車両、車両タイプ、経路の定義**

---|---
拡張子|.rou.xml
コンテンツタイプ|車両、車両タイプ、経路
オープンフォーマットか|Yes
SUMO特有か|Yes
XMLスキーマ|[routes_file.xsd]()

SUMOでの車両需要を定義するためには[様々なアプリケーション]()が使えます。
需要ファイルを手作業で定義したり、生成されたファイルをテキストエディタで編集することももちろん可能です。
こうしたことを始める前に、SUMOにおける車両は三つの部分からなっているということを知っておくことが重要です。

* 車両の物理的な性質を定義する車両タイプ
* 車両が通るであろう経路
* 車両それ自身

経路と車両タイプはどちらも複数の車両で共有することができます。
車両タイプを定義することは必須事項ではありません。
もし与えられなかった場合は、デフォルトタイプが使用されます。
運転手を陽に表現する必要はありません。
[歩行か運転を行なう人のシミュレーションには、追加のファイルが必要になります。]()

## 車両と経路

始めに、自身のみの経路を持つ車を定義してみましょう。

```
<routes>
   <vType id="type1" accel="0.8" decel="4.5" sigma="0.5" length="5" maxSpeed="70"/>

   <vehicle id="0" type="type1" depart="0" color="1,0,0">
      <route edges="beg middle end rend"/>
   </vehicle>

</routes>
```

[SUMO]() (または[SUMO-GUI]()) にこのような経路定義を与えると[SUMO]()は時刻0にスタートする車両タイプ"type1"で名前が"0"の赤い(color=1,0,0)車両を生成します。
この車両は道路"beg", "middle", "end"を通り、枝"rend"に着くと同時にシミュレーションから取り除かれます。

この車両は他の車両と共有されていないこの車両だけの経路を内包しています。
このケースでは経路は車両が参照する前に「表面化」つまり定義されていなければなりません。
また、経路はidによって名前が付いていなければなりません。

# デバイス

参考原文バージョン: 2022/9/1, a8217371322aa0915ac83d4deeb7d21b003364e5

vehicleデバイスは、出力（device.fcd）や振舞い（device.rerouting）など、複数のモデル化や設定に使われます。

次のデバイス名がサポートされており、以下の`<DEVICENAME>`プレイスホルダーに使うことができます。

- [emission](Models/Emissions.md)
- [battery](Models/Electric.md)
- [elechybrid](Models/ElectricHybrid.md)
- [btreiver](Simulation/Bluetooth.md)
- [btsender](Simulation/Bluetooth.md)
- [bluelight](Simulation/Emergency.md)
- [rerouting](Demand/Automatic_Routing.md)
- [ssm](Simulation/Output/SSM_Device.md)
- [toc](ToC_Device.md)
- [driverstate](Driver_State.md)
- [fcd](Simulation/Output/FCDOutput.md)
- [tripinfo](Simulation/Output/TripInfo.md)
- [vehroute](Simulation/Output/VehRoutes.md)
- [taxi](Simulation/Taxi.md)
- [glosa](Simulation/GLOSA.md)
- [example](Developer/How_To/Device.md)

## 自動割当て

いくつかのデバイスは自動的に割り当てられます。
シミュレーションに読み込まれる全ての`<trip>`には、最初のrouteを計算する*rerouting*デバイスが自動的に装備されます。

*fcd*など他のデバイスは、**--fcd-output**オプションを設定すると自動的に割り当てられます。

## グローバルオプションによる割当て

デバイスは、**--device.<DEVICENAME\>.probability**オプションを設定することで、シミュレーション内の全てのvehicleに設定できます。（例えば、`--device.fcd.probability 0.25`を設定すると、1/4のvehicleにfcdデバイスを装備させます。各vehicleはデバイスを装備するかを25%の確率でランダムに決定します。）
正確な割当てを実行するために、追加オプション**--device.<DEVICENAME\>.deterministic** を設定したり、他のオプションとして、**--device.<DEVICENAME\>.explicit <ID1,ID2,...IDk\>**オプションを使って、デバイスを装備させるvehicleのidリストを渡すことができます。

!!! note "注"
    これらのオプションは、出力オプションによる自動割当てより優先させる。

## ジェネリックパラメータによる割当て

vehicleのタイプや個々のvehicleにデバイスを割り当てる別のオプションとして、[ジェネリックパラメータ](Simulation/GenericParameters.md)を使う方法があります。
この場合、下記のように、vehicleのタイプやvehicleを定義します。

```xml
<routes>
    <vehicle id="v0" route="route0" depart="0">
        <param key="has.<DEVICENAME>.device" value="true"/>
    </vehicle>

    <vType id="t1">
        <param key="has.<DEVICENAME>.device" value="true"/>
    </vType>

    <vehicle id="v1" route="route0" depart="0" type="t1"/>
    
    <vType id="t2">
        <param key="device.<DEVICENAME>.probablity" value="0.5"/>
    </vType>

    <vehicle id="v2" route="route0" depart="0" type="t2"/>
</routes>
```

!!! note "注"
    vehicleの`<param>`は、vehicleのタイプの`<param>`より優先されます。
    いずれもオプションによる割当てより優先されます。
