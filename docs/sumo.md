# SUMO

## 俯瞰

**SUMO**はシミュレーション自身です。
微視的で連続空間かつ離散時間を持つ交通シミュレーションです。

* **目的**: 定義済みのシナリオのシミュレート
* **システム**: ポータブル(Linux/Windowsでテスト済み)で、コマンドラインから動作する 
* **入力(必須)**:
    * A) [NETCONVERT]または[NETGENERATE]により生成された道路ネットワーク、[ネットワーク構築]を参照
    * B) 経路の集合([DUAROUTER]、[JTTROUTER]、[DFROUTER]または[ACTIVITYGEN]により生成、[車両、車両タイプ及び経路の定義]も参照
* **入力(任意)**: 交通信号、様々な速度標識、検知器などその他の定義
* **出力**: SUMOでは様々な出力が可能であり、可視化は[SUMO-GUI]で行なわれる
* **プログラミング言語**: C++

## 使い方



### オプション

#### 設定

オプション|説明
---|---
**-c [`<FILE>`][datatype-link]** <br/> **--configuration-file [`<FILE>`][datatype-link]**|指定された設定を起動時に読みこむ
**-C [`<FILE>`][datatype-link]** <br/> **--save-configuration [`<FILE>`][datatype-link]**|現在の設定をファイルに保存する
**--save-templace [`<FILE>`][datatype-link]**|設定のテンプレート(空)をファイルに保存する
**--save-schema [`<FILE>`][datatype-link]**|設定のスキーマをファイルに保存
**--save-commented [`<BOOL>`][datatype-link]**|保存されるテンプレート、設定、スキーマにコメントを追加する。デフォルト: ***false***

#### 入力

オプション|説明
---|---
**-n [`<FILE>`][datatype-link]**<br/>**--net-files [`<FILE>`][datatype-link]**|ファイルから道路ネットワークを読みこむ
**-r [`<FILE>`][datatype-link]**<br/>**--route-files [`<FILE>`][datatype-link]**|ファイルから経路ファイルを読みこむ
**-a [`<FILE>`][datatype-link]**<br/>**--additional-files [`<FILE>`][datatype-link]**|さらにファイルを読みこむ
**-w [`<FILE>`][datatype-link]**<br/>**--weight-files [`<FILE>`][datatype-link]**|オンラインでの再経路設定用の枝(道路)/車線の重みをファイルから読みこむ
**-x [`<STRING>`][datatype-link]** <br/> **--weight-attribute [`<STRING>`][datatype-link]**|枝(道路)の重みを与えるxmlの属性の名前。デフォルト: ***traveltime***
**--load-state [`<FILE>`][datatype-link]**|ネットワークの状態をファイルから読みこむ
**--load-state.offset [`<TIME>`][datatype-link]**|保存された状態から時間をずらす。デフォルト: ***0***
**--load-state.remove-vehicles [`<STRING>`][datatype-link]**|読みこまれた状態について与えられたIDの車両を削除する

#### 出力

オプション|説明
---|---
**--write-license [`<BOOL>`][datatype-link]**|全ての出力ファイルにライセンス情報を付加する。デフォルト: ***false***
**--output-prefix [`<STRING>`][datatype-link]**|全ての出力ファイルに付加する接頭語を指定する。特別な文字列'TIME'は現在の時刻で置き換えられる
**--precision [`<INT>`][datatype-link]**|小数の出力に対し、小数点以下何桁までの出力を行なうかを指定。デフォルト: ***2***
**--precision [`<INT>`][datatype-link]**|緯度経度の出力に対し、小数点以下何桁までの出力を行なうかを指定。デフォルト: ***6***
**-H [`<BOOL>`][datatype-link]** <br> **--human-readable-time [`<BOOL>`][datatype-link]**|時間の値を秒のみのかわりに 時間:分:秒 あるいは 日:時間:分:秒の形式で書きこむ。デフォルト: ***false***
**--netstate-dump [`<FILE>`][datatype-link]**|完全なネットワークの状態をファイルに保存する
**--netstate-dump.empty-edges [`<BOOL>`][datatype-link]**|ダンプ時に空の枝についても完全に出力する。デフォルト: ***false***
**--netstate-dump.precision [`<INT>`][datatype-link]**|位置と速度を指定した精度で出力する。デフォルト: ***2***
**emission-output [`<FILE>`][datatype-link]**|個々の車両の排気ガスを保存する
**emission-output.precision [`<INT>`][datatype-link]**|排気ガスの値を指定した精度で出力。デフォルト: ***2***
**battery-output [`<FILE>`][datatype-link]**|個々の車両のバッテリーの値を保存する
**battery-output.precision [`<INT>`][datatype-link]**|バッテリーの値を指定した精度で出力。デフォルト: ***2***
**--fcd-output [`<FILE>`][datatype-link]**|[フローティングカーデータ(FCD)][fcd-wikipedia]を保存する
**--fcd-output.geo [`<BOOL>`][datatype-link]**|FCDを緯度経度を用いて保存する。デフォルト: ***false***
**--fcd-output.signals [`<BOOL>`][datatype-link]**|FCD出力に車両のライトの情報(ブレーキランプ等)を含める。デフォルト: ***false***
**--fcd-output.filter-edges.input-file [`<FILE>`][datatype-link]**|FCD出力を指定されたファイルで定義された枝(道路)のみに制限する
**--full-output [`<FILE>`][datatype-link]**|タイムステップごとに多くの情報を保存する(かなり冗長)
**--queue-output [`<FILE>`][datatype-link]**|交差点での待ち車両列を保存する(実験的)
**--vtk-output [`<FILE>`][datatype-link]**|速度を含めた完全な車両位置をVTKフォーマットで保存する(使い方: /path/out は/path/out_$TIMESTEP$.vtpファイルを出力)
**--amitran-output [`<FILE>`][datatype-link]**|車両の軌跡をAmitranフォーマットで保存する
**--summary-output [`<FILE>`][datatype-link]**|
**--tripinfo-output [`<FILE>`][datatype-link]**|
**--tripinf o-output.write-unfinished [`<BOOL>`][datatype-link]**|
**--vehroute-output [`<FILE>`][datatype-link]**|
**--vehroute-output.exit-times [`<BOOL>`][datatype-link]**|
**--vehroute-output.last-route [`<BOOL>`][datatype-link]**|
**--vehroute-output.sorted [`<BOOL>`][datatype-link]**|
**--vehroute-output.dua [`<BOOL>`][datatype-link]**|
**--vehroute-output.cost [`<BOOL>`][datatype-link]**|全経路のコストを出力。デフォルト: ***false***
**--vehroute-output.intended-depart [`<BOOL>`][datatype-link]**|
**--vehroute-output.route-length [`<BOOL>`][datatype-link]**|
**--vehroute-output.write-unfinished [`<BOOL>`][datatype-link]**|
**--vehroute-output.skip-ptlines [`<BOOL>`][datatype-link]**|
**--link-output [`<FILE>`][datatype-link]**|
**--railsignal-block-output [`<FILE>`][datatype-link]**|
**--bt-output [`<FILE>`][datatype-link]**|
**--lanechange-output [`<FILE>`][datatype-link]**|
**--lanechange-output.started [`<BOOL>`][datatype-link]**|
**--lanechange-output.ended [`<BOOL>`][datatype-link]**|
**--stop-output [`<FILE>`][datatype-link]**|
**--save-state.times [`<INT>`][datatype-link]**|
**--save-state.period [`<TIME>`][datatype-link]**|
**--save-state.prefix [`<FILE>`][datatype-link]**|
**--save-state.suffix [`<STRING>`][datatype-link]**|
**--save-state.files [`<FILE>`][datatype-link]**|

#### 時間

オプション|説明
---|---
**-b [`<TIME>`][datatype-link]** <br/> **--begin [`<TIME>`][datatype-link]**|開始時刻を秒単位で指定する。シミュレーションは指定された時刻から始まる。デフォルト: ***0***
**-e [`<TIME>`][datatype-link]** <br/> **--end [`<TIME>`][datatype-link]**|終了時刻を秒単位で指定する。シミュレーションはこの時刻で終了する。デフォルト: ***-1***
**--step-length [`<TIME>`][datatype-link]**|各ステップの長さを秒単位で指定する。デフォルト: ***1***

#### 処理工程

オプション|説明
---|---
**--step-method.ballistic [`<BOOL>`][datatype-link]**|車両の位置更新に弾道型手法を使うか(デフォルト半暗黙のオイラー手法)。デフォルト: ***false***
**--threads [`<INT>`][datatype-link]**|並列シミュレーションに用いるスレッド数。デフォルト: ***1***
**--lateral-resolution [`<FLOAT>`][datatype-link]**|
**-s [`<TIME>`][datatype-link]** <br/> **--route-steps [`<TIME>`][datatype-link]**|
**--no-internal-links [`<BOOL>`][datatype-link]**|
**--ignore-junction-blocker [`<TIME>`][datatype-link]**|
**--ignore-route-errors [`<BOOL>`][datatype-link]**|
**--ignore-accidents [`<BOOL>`][datatype-link]**|
**--collision.action [`<STRING>`][datatype-link]**|
**--collision.stoptime [`<TIME>`][datatype-link]**|
**--collision.check-junctions [`<BOOL>`][datatype-link]**|
**--collision.mingap-factor [`<FLOAT>`][datatype-link]**|
**--max-num-vehicles [`<INT>`][datatype-link]**|
**--max-num-teleports [`<INT>`][datatype-link]**|
**--scale [`<FLOAT>`][datatype-link]**|
**--time-to-teleport [`<TIME>`][datatype-link]**|
**--time-to-teleport.highways [`<TIME>`][datatype-link]**|
**--waiting-time-memory [`<TIME>`][datatype-link]**|
**--max-depart-delay [`<TIME>`][datatype-link]**|
**--sloppy-insert [`<BOOL>`][datatype-link]**|
**--eager-insert [`<BOOL>`][datatype-link]**|
**--random-depart-offset [`<TIME>`][datatype-link]**|
**--lanechange.duration [`<TIME>`][datatype-link]**|
**--lanechange.overtake-right [`<BOOL>`][datatype-link]**|
**--tls.all-off [`<BOOL>`][datatype-link]**|
**--tls.acutuated.show-detectors [`<BOOL>`][datatype-link]**|
**--time-to-impatience [`<TIME>]**|
**--default.action-step-length [`<FLOAT>`][datatype-link]**|
**--default.carfollowmodel [`<STRING>`][datatype-link]**|
**--default.speeddev [`<FLOAT>`][datatype-link]**|
**--default.emergencydecel [`<STRING>`][datatype-link]**|
**--emergencydecel.warning-threshold [`<FLOAT>`][datatype-link]**|
**--pedestrian.model [`<STRING>`][datatype-link]**|歩行者のモデルを指定する['noninteracting', 'striping', 'remote']。デフォルト: ***striping***
**--pedestrian.striping.stripe-width [`<FLOAT>`][datatype-link]**|
**--pedestrian.striping.dawdling [`<FLOAT>`][datatype-link]**|'striping'モデルに仕様するランダムな減速[0, 1]の因子を決める。デフォルト: ***0.2***
**--pedestrian.striping.jamtime [`<TIME>`][datatype-link]**|
**--pedestrian.remote.address [`<STRING>`][datatype-link]**|外部シミュレーション用のアドレス(ホスト:ポート)を指定する。デフォルト: ***localhost:9000***

#### 経路設定

オプション|説明
---|---
**--routing-algorithm [`<STRING>`][datatype-link]**|経路設定のアルゴリズムを指定する['dijkstra', 'astar', 'CH', 'CHWrapper']。デフォルト: ***dijkstra***
**--weights.random-factor [`<FLOAT>`][datatype-link]**|
**--weights.minor-penalty [`<FLOAT>`][datatype-link]**|
**--astar.all-distances [`<FILE>`][datatype-link]**|
**--astar.landmark-distances [`<FILE>`][datatype-link]**|
**--pesontrip.walkfactor [`<FLOAT>`][datatype-link]**|
**--pesontrip.transfer.car-walk [`<STRING>`][datatype-link]**|
**--device.rerouting.probability [`<FLOAT>`][datatype-link]**|
**--device.rerouting.explicit [`<STRING>`][datatype-link]**|
**--device.rerouting.deterministic [`<BOOL>`][datatype-link]**|
**--device.rerouting.period [`<TIME>`][datatype-link]**|
**--device.rerouting.pre-period [`<TIME>`][datatype-link]**|
**--device.rerouting.adaptation-weight [`<FLOAT>`][datatype-link]**|
**--device.rerouting.adaptation-steps [`<INT>`][datatype-link]**|
**--device.rerouting.adaptation-interval [`<TIME>`][datatype-link]**|
**--device.rerouting.with-taz [`<BOOL>`][datatype-link]**|
**--device.rerouting.init-with-loaded-weights [`<BOOL>`][datatype-link]**|
**--device.rerouting.threads [`<INT>`][datatype-link]**|
**--device.rerouting.synchronize [`<BOOL>`][datatype-link]**|
**--device.rerouting.output [`<FILE>`][datatype-link]**|
**--person-device.rerouting.probability [`<FLOAT>`][datatype-link]**|
**--person-device.rerouting.explicit [`<STRING>`][datatype-link]**|
**--person-device.rerouting.deterministic [`<BOOL>`][datatype-link]**|
**--person-device.rerouting.period [`<TIME>`][datatype-link]**|

#### レポート

オプション|説明
---|---
**-v [`<BOOL>`][datatype-link]** <br/> **--verbose [`<BOOL>`][datatype-link]**|
**--print-options [`<BOOL>`][datatype-link]**|処理前にオプションの値を出力する。デフォルト: ***false***
**-? [`<BOOL>`][datatype-link]** <br/> **--help [`<BOOL>`][datatype-link]**|
**-V [`<BOOL>`][datatype-link]** <br/> **--version [`<BOOL>`][datatype-link]**|
**-X [`<STRING>`][datatype-link]** <br> **--xml-validation [`<STRING>`][datatype-link]**|
**--xml-validation.net [`<STRING>`][datatype-link]**|
**-W [`<BOOL>`][datatype-link]** <br/> **--no-warnings [`<BOOL>`][datatype-link]**|
**-l [`<FILE>`][datatype-link]** <br/> **--log [`<FILE>`][datatype-link]**|
**--message-log [`<FILE>`][datatype-link]**|
**--error-log [`<FILE>`][datatype-link]**|
**--duration-log.disable [`<BOOL>`][datatype-link]**|各ステップのパフォーマンスレポートを無効化する。デフォルト: ***false***
**--duration-log.statistics [`<BOOL>`][datatype-link]**|車両の移動に関する統計を有効化する。デフォルト: ***false***
**--no-step-log [`<BOOL>`][datatype-link]**|現在のシミュレーションステップでのコンソール出力を無効化する。デフォルト: ***false***

#### 排気ガス

オプション|説明
---|---
**--phemlight-path [`<FILE>`][datatype-link]**|
**--device.emissions.probability [`<FLOAT>`][datatype-link]**|
**--device.emissions.explicit [`<STRING>`][datatype-link]**|
**--device.emissions.deterministic [`<BOOL>`][datatype-link]**|

#### 通信

オプション|説明
---|---
**--device.btreceiver.probability [`<FLOAT>`][datatype-link]**|
**--device.btreceiver.explicit [`<STRING>`][datatype-link]**|
**--device.btreceiver.deterministic [`<BOOL>`][datatype-link]**|
**--device.btreceiver.range [`<FLOAT>`][datatype-link]**|
**--device.btreceiver.all-recognitions [`<BOOL>`][datatype-link]**|
**--device.btreceiver.offtime [`<FLOAT>`][datatype-link]**|
**--device.btsender.probability [`<FLOAT>`][datatype-link]**|
**--device.btsender.explicit [`<STRING>`][datatype-link]**|
**--device.btsender.deterministic [`<BOOL>`][datatype-link]**|

#### バッテリー

オプション|説明
---|---
**--device.battery.probability [`<FLOAT>`][datatype-link]**|車両がバッテリーデバイスを持っている確率。デフォルト: ***-1***
**--device.battery.explicit [`<STRING>`][datatype-link]**|
**--device.battery.deterministic [`<BOOL>`][datatype-link]**|
 
#### Example Device

オプション|説明
---|---
**--device.example.probability [`<FLOAT>`][datatype-link]**|
**--device.example.explicit [`<STRING>`][datatype-link]**|
**--device.example.deterministic [`<BOOL>`][datatype-link]**|
**--device.example.parameter [`<FLOAT>`][datatype-link]**|

#### Ssmデバイス

オプション|説明
---|---
**--device.ssm.probability [`<FLOAT>`][datatype-link]**|
**--device.ssm.explicit [`<STRING>`][datatype-link]**|
**--device.ssm.deterministic [`<BOOL>`][datatype-link]**|
**--device.ssm.measures [`<STRING>`][datatype-link]**|
**--device.ssm.thresholds [`<STRING>`][datatype-link]**|
**--device.ssm.trajectories [`<BOOL>`][datatype-link]**|
**--device.ssm.range [`<FLOAT>`][datatype-link]**|
**--device.ssm.extratime [`<FLOAT>`][datatype-link]**|
**--device.ssm.file [`<STRING>`][datatype-link]**|
**--device.ssm.geo [`<BOOL>`][datatype-link]**|

#### Tocデバイス

オプション|説明
---|---
**--device.toc.probability [`<FLOAT>`][datatype-link]**|
**--device.toc.explicit [`<STRING>`][datatype-link]**|
**--device.toc.deterministic [`<BOOL>`][datatype-link]**|
**--device.toc.manualType [`<STRING>`][datatype-link]**|
**--device.toc.automatedType [`<STRING>`][datatype-link]**|
**--device.toc.responseTime [`<FLOAT>`][datatype-link]**|
**--device.toc.recoveryRate [`<FLOAT>`][datatype-link]**|
**--device.toc.lcAbstinence [`<FLOAT>`][datatype-link]**|
**--device.toc.initialAwareness [`<FLOAT>`][datatype-link]**|
**--device.toc.mrmDecel [`<FLOAT>`][datatype-link]**|
**--device.toc.ogNewTimeHeadway [`<FLOAT>`][datatype-link]**|
**--device.toc.ogNewSpaceHeadway [`<FLOAT>`][datatype-link]**|
**--device.toc.ogMaxDecel [`<FLOAT>`][datatype-link]**|
**--device.toc.ogChangeRate [`<FLOAT>`][datatype-link]**|
**--device.toc.useColorScheme [`<BOOL>`][datatype-link]**|
**--device.toc.file [`<STRING>`][datatype-link]**|

#### Driver State Device

オプション|説明
---|---
**--device.driverstate.probability [`<FLOAT>`][datatype-link]**|
**--device.driverstate.explicit [`<STRING>`][datatype-link]**|
**--device.driverstate.deterministic [`<BOOL>`][datatype-link]**|
**--device.driverstate.initialAwareness [`<FLOAT>`][datatype-link]**|
**--device.driverstate.errorTimeScaleCoefficient [`<FLOAT>`][datatype-link]**|
**--device.driverstate.errorNoiseIntensityCoefficient [`<FLOAT>`][datatype-link]**|
**--device.driverstate.speedDifferenceErrorCoefficient [`<FLOAT>`][datatype-link]**|
**--device.driverstate.headwayErrorCoefficient [`<FLOAT>`][datatype-link]**|
**--device.driverstate.speedDifferenceChangePerceptionThreshold [`<FLOAT>`][datatype-link]**|
**--device.driverstate.headwayChangePerceptionThreshold [`<FLOAT>`][datatype-link]**|
**--device.driverstate.minAwareness [`<FLOAT>`][datatype-link]**|
**--device.driverstate.maximalReactionTime [`<FLOAT>`][datatype-link]**|

#### Bluelight Device

オプション|説明
---|---
**--device.bluelight.probability [`<FLOAT>`][datatype-link]**|
**--device.bluelight.explicit [`<STRING>`][datatype-link]**|
**--device.bluelight.deterministic [`<BOOL>`][datatype-link]**|
**--device.bluelight.parameter [`<FLOAT>`][datatype-link]**|

#### Fcd Device

オプション|説明
---|---
**--device.fcd.probability [`<FLOAT>`][datatype-link]**|
**--device.fcd.explicit [`<STRING>`][datatype-link]**|
**--device.fcd.deterministic [`<BOOL>`][datatype-link]**|
**--device.fcd.period [`<STRING>`][datatype-link]**|
**--person-device.fcd.probability [`<FLOAT>`][datatype-link]**|
**--person-device.fcd.explicit [`<STRING>`][datatype-link]**|
**--person-device.fcd.deterministic [`<BOOL>`][datatype-link]**|
**--person-device.fcd.period [`<STRING>`][datatype-link]**|

#### Traci Server

オプション|説明
---|---
**--remote-port [`<INT>`][datatype-link]**|
**--num-clients [`<INT>`][datatype-link]**|

#### Mesoscopic

オプション|説明
---|---
**--mesosim [`<BOOL>`][datatype-link]**|
**--meso-edgelength [`<FLOAT>`][datatype-link]**|
**--meso-tauff [`<TIME>`][datatype-link]**|
**--meso-taufj [`<TIME>`][datatype-link]**|
**--meso-taujf [`<TIME>`][datatype-link]**|
**--meso-taujj [`<TIME>`][datatype-link]**|
**--meso-jam-threshold [`<FLOAT>`][datatype-link]**|
**--meso-multi-queue [`<BOOL>`][datatype-link]**|
**--meso-junction-control [`<BOOL>`][datatype-link]**|
**--meso-junction-control.limited [`<BOOL>`][datatype-link]**|
**--meso-tls-penalty [`<FLOAT>`][datatype-link]**|
**--meso-minor-penalty [`<TIME>`][datatype-link]**|
**--meso-overtaking [`<BOOL>`][datatype-link]**|
**--meso-recheck [`<TIME>`][datatype-link]**|

#### Random Number

オプション|説明
---|---
**--random [`<BOOL>`][datatype-link]**|
**--seed [`<INT>`][datatype-link]**|
**--thread-rngs [`<INT>`][datatype-link]**|

#### Gui Only

オプション|説明
---|---
**-g [`<FILE>`][datatype-link]** <br/> **--gui-settings-file [`<FILE>`][datatype-link]**|
**-Q [`<BOOL>`][datatype-link]** <br/> **--quit-on-end [`<BOOL>`][datatype-link]**|
**-G [`<BOOL>`][datatype-link]** <br/> **--game [`<BOOL>`][datatype-link]**|
**--game.mode [`<STRING>`][datatype-link]**|
**-S [`<BOOL>`][datatype-link]** <br/> **--start [`<BOOL>`][datatype-link]**|
**--breakpoints [`<STRING>`][datatype-link]**|
**--edgedata-files [`<FILE>`][datatype-link]**|
**-D [`<BOOL>`][datatype-link]** <br/> **--demo [`<BOOL>`][datatype-link]**|
**-T [`<BOOL>`][datatype-link]** <br/> **--disable-textures [`<BOOL>`][datatype-link]**|
**--registry-viewport [`<BOOL>`][datatype-link]**|
**--window-size [`<STRING>`][datatype-link]**|
**--window-pos [`<STRING>`][datatype-link]**|
**--tracker-interval [`<FLOAT>`][datatype-link]**|
**--osg-view [`<BOOL>`][datatype-link]**|
**--gui-testing [`<BOOL>`][datatype-link]**|
**--gui-testing-debug [`<BOOL>`][datatype-link]**|


## 入力ファイルの読みこみ順序

入力ファイル中で定義されたシミュレーションオブジェクトA(例: 車)が他のシミュレーションオブジェクトB(例: 車両タイプ)を参照している場合、オブジェクトBは必ずAより前に読みこまれるファイルか、Aと同じ入力ファイルのAより前の行に書かれていなければなりません。


## 追加ファイルのフォーマット

**--additional-files [`<FILE>`][datatype-link]**オプションで追加されるファイルは、[交通信号]()、[検知器]()、[種々の速度標識]()、[バス停]()など幅広いネットワーク要素を含んでいます。
こうしたファイルは

```xml
 <additional>
    <inductionLoop id="myLoop1" lane="foo_0" pos="42" freq="900" file="out.xml"/>
    <inductionLoop id="myLoop2" lane="foo_2" pos="42" freq="900" file="out.xml"/>
 
    <busStop id="station1" lane="foo_0" startPos="5" endPos="20"/>

    <vType id="bus" maxSpeed="20" length="12"/>
 </additional>
```
## 補助資料


[datatype-link]: basics_notation.md#データタイプ
[fcd-wikipedia]: https://ja.wikipedia.org/wiki/%E3%83%95%E3%83%AD%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%AB%E3%83%BC%E3%83%87%E3%83%BC%E3%82%BF