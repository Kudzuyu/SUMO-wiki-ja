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
**-c {{DT_FILE}}** <br/> **--configuration-file {{DT_FILE}}**|指定された設定を起動時に読みこむ
**-C {{DT_FILE}}** <br/> **--save-configuration {{DT_FILE}}**|現在の設定をファイルに保存する
**--save-templace {{DT_FILE}}**|設定のテンプレート(空)をファイルに保存する
**--save-schema {{DT_FILE}}**|設定のスキーマをファイルに保存
**--save-commented {{DT_BOOL}}**|保存されるテンプレート、設定、スキーマにコメントを追加する。デフォルト: ***false***

#### 入力

オプション|説明
---|---
**-n {{DT_FILE}}**<br/>**--net-files {{DT_FILE}}**|ファイルから道路ネットワークを読みこむ
**-r {{DT_FILE}}**<br/>**--route-files {{DT_FILE}}**|ファイルから経路ファイルを読みこむ
**-a {{DT_FILE}}**<br/>**--additional-files {{DT_FILE}}**|さらにファイルを読みこむ
**-w {{DT_FILE}}**<br/>**--weight-files {{DT_FILE}}**|オンラインでの再経路設定用の枝(道路)/車線の重みをファイルから読みこむ
**-x {{DT_STRING}}** <br/> **--weight-attribute {{DT_STRING}}**|枝(道路)の重みを与えるxmlの属性の名前。デフォルト: ***traveltime***
**--load-state {{DT_FILE}}**|ネットワークの状態をファイルから読みこむ
**--load-state.offset {{DT_TIME}}**|保存された状態から時間をずらす。デフォルト: ***0***
**--load-state.remove-vehicles {{DT_STRING}}**|読みこまれた状態について与えられたIDの車両を削除する

#### 出力

オプション|説明
---|---
**--write-license {{DT_BOOL}}**|全ての出力ファイルにライセンス情報を付加する。デフォルト: ***false***
**--output-prefix {{DT_STRING}}**|全ての出力ファイルに付加する接頭語を指定する。特別な文字列'TIME'は現在の時刻で置き換えられる
**--precision {{DT_INT}}**|小数の出力に対し、小数点以下何桁までの出力を行なうかを指定。デフォルト: ***2***
**--precision {{DT_INT}}**|緯度経度の出力に対し、小数点以下何桁までの出力を行なうかを指定。デフォルト: ***6***
**-H {{DT_BOOL}}** <br> **--human-readable-time {{DT_BOOL}}**|時間の値を秒のみのかわりに 時間:分:秒 あるいは 日:時間:分:秒の形式で書きこむ。デフォルト: ***false***
**--netstate-dump {{DT_FILE}}**|完全なネットワークの状態をファイルに保存する
**--netstate-dump.empty-edges {{DT_BOOL}}**|ダンプ時に空の枝についても完全に出力する。デフォルト: ***false***
**--netstate-dump.precision {{DT_INT}}**|位置と速度を指定した精度で出力する。デフォルト: ***2***
**emission-output {{DT_FILE}}**|個々の車両の排気ガスを保存する
**emission-output.precision {{DT_INT}}**|排気ガスの値を指定した精度で出力。デフォルト: ***2***
**battery-output {{DT_FILE}}**|個々の車両のバッテリーの値を保存する
**battery-output.precision {{DT_INT}}**|バッテリーの値を指定した精度で出力。デフォルト: ***2***
**--fcd-output {{DT_FILE}}**|[フローティングカーデータ(FCD)][fcd-wikipedia]を保存する
**--fcd-output.geo {{DT_BOOL}}**|FCDを緯度経度を用いて保存する。デフォルト: ***false***
**--fcd-output.signals {{DT_BOOL}}**|FCD出力に車両のライトの情報(ブレーキランプ等)を含める。デフォルト: ***false***
**--fcd-output.filter-edges.input-file {{DT_FILE}}**|FCD出力を指定されたファイルで定義された枝(道路)のみに制限する
**--full-output {{DT_FILE}}**|タイムステップごとに多くの情報を保存する(かなり冗長)
**--queue-output {{DT_FILE}}**|交差点での待ち車両列を保存する(実験的)
**--vtk-output {{DT_FILE}}**|速度を含めた完全な車両位置をVTKフォーマットで保存する(使い方: /path/out は/path/out_$TIMESTEP$.vtpファイルを出力)
**--amitran-output {{DT_FILE}}**|車両の軌跡をAmitranフォーマットで保存する
**--summary-output {{DT_FILE}}**|
**--tripinfo-output {{DT_FILE}}**|
**--tripinf o-output.write-unfinished {{DT_BOOL}}**|
**--vehroute-output {{DT_FILE}}**|
**--vehroute-output.exit-times {{DT_BOOL}}**|
**--vehroute-output.last-route {{DT_BOOL}}**|
**--vehroute-output.sorted {{DT_BOOL}}**|
**--vehroute-output.dua {{DT_BOOL}}**|
**--vehroute-output.cost {{DT_BOOL}}**|全経路のコストを出力。デフォルト: ***false***
**--vehroute-output.intended-depart {{DT_BOOL}}**|
**--vehroute-output.route-length {{DT_BOOL}}**|
**--vehroute-output.write-unfinished {{DT_BOOL}}**|
**--vehroute-output.skip-ptlines {{DT_BOOL}}**|
**--link-output {{DT_FILE}}**|
**--railsignal-block-output {{DT_FILE}}**|
**--bt-output {{DT_FILE}}**|
**--lanechange-output {{DT_FILE}}**|
**--lanechange-output.started {{DT_BOOL}}**|
**--lanechange-output.ended {{DT_BOOL}}**|
**--stop-output {{DT_FILE}}**|
**--save-state.times {{DT_INT}}**|
**--save-state.period {{DT_TIME}}**|
**--save-state.prefix {{DT_FILE}}**|
**--save-state.suffix {{DT_STRING}}**|
**--save-state.files {{DT_FILE}}**|

#### 時間

オプション|説明
---|---
**-b {{DT_TIME}}** <br/> **--begin {{DT_TIME}}**|開始時刻を秒単位で指定する。シミュレーションは指定された時刻から始まる。デフォルト: ***0***
**-e {{DT_TIME}}** <br/> **--end {{DT_TIME}}**|終了時刻を秒単位で指定する。シミュレーションはこの時刻で終了する。デフォルト: ***-1***
**--step-length {{DT_TIME}}**|各ステップの長さを秒単位で指定する。デフォルト: ***1***

#### 処理工程

オプション|説明
---|---
**--step-method.ballistic {{DT_BOOL}}**|車両の位置更新に弾道型手法を使うか(デフォルト半暗黙のオイラー手法)。デフォルト: ***false***
**--threads {{DT_INT}}**|並列シミュレーションに用いるスレッド数。デフォルト: ***1***
**--lateral-resolution {{DT_FLOAT}}**|
**-s {{DT_TIME}}** <br/> **--route-steps {{DT_TIME}}**|
**--no-internal-links {{DT_BOOL}}**|
**--ignore-junction-blocker {{DT_TIME}}**|
**--ignore-route-errors {{DT_BOOL}}**|
**--ignore-accidents {{DT_BOOL}}**|
**--collision.action {{DT_STRING}}**|
**--collision.stoptime {{DT_TIME}}**|
**--collision.check-junctions {{DT_BOOL}}**|
**--collision.mingap-factor {{DT_FLOAT}}**|
**--max-num-vehicles {{DT_INT}}**|
**--max-num-teleports {{DT_INT}}**|
**--scale {{DT_FLOAT}}**|
**--time-to-teleport {{DT_TIME}}**|
**--time-to-teleport.highways {{DT_TIME}}**|
**--waiting-time-memory {{DT_TIME}}**|
**--max-depart-delay {{DT_TIME}}**|
**--sloppy-insert {{DT_BOOL}}**|
**--eager-insert {{DT_BOOL}}**|
**--random-depart-offset {{DT_TIME}}**|
**--lanechange.duration {{DT_TIME}}**|
**--lanechange.overtake-right {{DT_BOOL}}**|
**--tls.all-off {{DT_BOOL}}**|
**--tls.acutuated.show-detectors {{DT_BOOL}}**|
**--time-to-impatience {{DT_TIME}}**|
**--default.action-step-length {{DT_FLOAT}}**|
**--default.carfollowmodel {{DT_STRING}}**|
**--default.speeddev {{DT_FLOAT}}**|
**--default.emergencydecel {{DT_STRING}}**|
**--emergencydecel.warning-threshold {{DT_FLOAT}}**|
**--pedestrian.model {{DT_STRING}}**|歩行者のモデルを指定する['noninteracting', 'striping', 'remote']。デフォルト: ***striping***
**--pedestrian.striping.stripe-width {{DT_FLOAT}}**|
**--pedestrian.striping.dawdling {{DT_FLOAT}}**|'striping'モデルに仕様するランダムな減速[0, 1]の因子を決める。デフォルト: ***0.2***
**--pedestrian.striping.jamtime {{DT_TIME}}**|
**--pedestrian.remote.address {{DT_STRING}}**|外部シミュレーション用のアドレス(ホスト:ポート)を指定する。デフォルト: ***localhost:9000***

#### 経路設定

オプション|説明
---|---
**--routing-algorithm {{DT_STRING}}**|経路設定のアルゴリズムを指定する['dijkstra', 'astar', 'CH', 'CHWrapper']。デフォルト: ***dijkstra***
**--weights.random-factor {{DT_FLOAT}}**|
**--weights.minor-penalty {{DT_FLOAT}}**|
**--astar.all-distances {{DT_FILE}}**|
**--astar.landmark-distances {{DT_FILE}}**|
**--pesontrip.walkfactor {{DT_FLOAT}}**|
**--pesontrip.transfer.car-walk {{DT_STRING}}**|
**--device.rerouting.probability {{DT_FLOAT}}**|
**--device.rerouting.explicit {{DT_STRING}}**|
**--device.rerouting.deterministic {{DT_BOOL}}**|
**--device.rerouting.period {{DT_TIME}}**|
**--device.rerouting.pre-period {{DT_TIME}}**|
**--device.rerouting.adaptation-weight {{DT_FLOAT}}**|
**--device.rerouting.adaptation-steps {{DT_INT}}**|
**--device.rerouting.adaptation-interval {{DT_TIME}}**|
**--device.rerouting.with-taz {{DT_BOOL}}**|
**--device.rerouting.init-with-loaded-weights {{DT_BOOL}}**|
**--device.rerouting.threads {{DT_INT}}**|
**--device.rerouting.synchronize {{DT_BOOL}}**|
**--device.rerouting.output {{DT_FILE}}**|
**--person-device.rerouting.probability {{DT_FLOAT}}**|
**--person-device.rerouting.explicit {{DT_STRING}}**|
**--person-device.rerouting.deterministic {{DT_BOOL}}**|
**--person-device.rerouting.period {{DT_TIME}}**|

#### レポート

オプション|説明
---|---
**-v {{DT_BOOL}}** <br/> **--verbose {{DT_BOOL}}**|
**--print-options {{DT_BOOL}}**|処理前にオプションの値を出力する。デフォルト: ***false***
**-? {{DT_BOOL}}** <br/> **--help {{DT_BOOL}}**|
**-V {{DT_BOOL}}** <br/> **--version {{DT_BOOL}}**|
**-X {{DT_STRING}}** <br> **--xml-validation {{DT_STRING}}**|
**--xml-validation.net {{DT_STRING}}**|
**-W {{DT_BOOL}}** <br/> **--no-warnings {{DT_BOOL}}**|
**-l {{DT_FILE}}** <br/> **--log {{DT_FILE}}**|
**--message-log {{DT_FILE}}**|
**--error-log {{DT_FILE}}**|
**--duration-log.disable {{DT_BOOL}}**|各ステップのパフォーマンスレポートを無効化する。デフォルト: ***false***
**--duration-log.statistics {{DT_BOOL}}**|車両の移動に関する統計を有効化する。デフォルト: ***false***
**--no-step-log {{DT_BOOL}}**|現在のシミュレーションステップでのコンソール出力を無効化する。デフォルト: ***false***

#### 排気ガス

オプション|説明
---|---
**--phemlight-path {{DT_FILE}}**|
**--device.emissions.probability {{DT_FLOAT}}**|
**--device.emissions.explicit {{DT_STRING}}**|
**--device.emissions.deterministic {{DT_BOOL}}**|

#### 通信

オプション|説明
---|---
**--device.btreceiver.probability {{DT_FLOAT}}**|
**--device.btreceiver.explicit {{DT_STRING}}**|
**--device.btreceiver.deterministic {{DT_BOOL}}**|
**--device.btreceiver.range {{DT_FLOAT}}**|
**--device.btreceiver.all-recognitions {{DT_BOOL}}**|
**--device.btreceiver.offtime {{DT_FLOAT}}**|
**--device.btsender.probability {{DT_FLOAT}}**|
**--device.btsender.explicit {{DT_STRING}}**|
**--device.btsender.deterministic {{DT_BOOL}}**|

#### バッテリー

オプション|説明
---|---
**--device.battery.probability {{DT_FLOAT}}**|車両がバッテリーデバイスを持っている確率。デフォルト: ***-1***
**--device.battery.explicit {{DT_STRING}}**|
**--device.battery.deterministic {{DT_BOOL}}**|
 
#### Example Device

オプション|説明
---|---
**--device.example.probability {{DT_FLOAT}}**|
**--device.example.explicit {{DT_STRING}}**|
**--device.example.deterministic {{DT_BOOL}}**|
**--device.example.parameter {{DT_FLOAT}}**|

#### Ssmデバイス

オプション|説明
---|---
**--device.ssm.probability {{DT_FLOAT}}**|
**--device.ssm.explicit {{DT_STRING}}**|
**--device.ssm.deterministic {{DT_BOOL}}**|
**--device.ssm.measures {{DT_STRING}}**|
**--device.ssm.thresholds {{DT_STRING}}**|
**--device.ssm.trajectories {{DT_BOOL}}**|
**--device.ssm.range {{DT_FLOAT}}**|
**--device.ssm.extratime {{DT_FLOAT}}**|
**--device.ssm.file {{DT_STRING}}**|
**--device.ssm.geo {{DT_BOOL}}**|

#### Tocデバイス

オプション|説明
---|---
**--device.toc.probability {{DT_FLOAT}}**|
**--device.toc.explicit {{DT_STRING}}**|
**--device.toc.deterministic {{DT_BOOL}}**|
**--device.toc.manualType {{DT_STRING}}**|
**--device.toc.automatedType {{DT_STRING}}**|
**--device.toc.responseTime {{DT_FLOAT}}**|
**--device.toc.recoveryRate {{DT_FLOAT}}**|
**--device.toc.lcAbstinence {{DT_FLOAT}}**|
**--device.toc.initialAwareness {{DT_FLOAT}}**|
**--device.toc.mrmDecel {{DT_FLOAT}}**|
**--device.toc.ogNewTimeHeadway {{DT_FLOAT}}**|
**--device.toc.ogNewSpaceHeadway {{DT_FLOAT}}**|
**--device.toc.ogMaxDecel {{DT_FLOAT}}**|
**--device.toc.ogChangeRate {{DT_FLOAT}}**|
**--device.toc.useColorScheme {{DT_BOOL}}**|
**--device.toc.file {{DT_STRING}}**|

#### Driver State Device

オプション|説明
---|---
**--device.driverstate.probability {{DT_FLOAT}}**|
**--device.driverstate.explicit {{DT_STRING}}**|
**--device.driverstate.deterministic {{DT_BOOL}}**|
**--device.driverstate.initialAwareness {{DT_FLOAT}}**|
**--device.driverstate.errorTimeScaleCoefficient {{DT_FLOAT}}**|
**--device.driverstate.errorNoiseIntensityCoefficient {{DT_FLOAT}}**|
**--device.driverstate.speedDifferenceErrorCoefficient {{DT_FLOAT}}**|
**--device.driverstate.headwayErrorCoefficient {{DT_FLOAT}}**|
**--device.driverstate.speedDifferenceChangePerceptionThreshold {{DT_FLOAT}}**|
**--device.driverstate.headwayChangePerceptionThreshold {{DT_FLOAT}}**|
**--device.driverstate.minAwareness {{DT_FLOAT}}**|
**--device.driverstate.maximalReactionTime {{DT_FLOAT}}**|

#### Bluelight Device

オプション|説明
---|---
**--device.bluelight.probability {{DT_FLOAT}}**|
**--device.bluelight.explicit {{DT_STRING}}**|
**--device.bluelight.deterministic {{DT_BOOL}}**|
**--device.bluelight.parameter {{DT_FLOAT}}**|

#### Fcd Device

オプション|説明
---|---
**--device.fcd.probability {{DT_FLOAT}}**|
**--device.fcd.explicit {{DT_STRING}}**|
**--device.fcd.deterministic {{DT_BOOL}}**|
**--device.fcd.period {{DT_STRING}}**|
**--person-device.fcd.probability {{DT_FLOAT}}**|
**--person-device.fcd.explicit {{DT_STRING}}**|
**--person-device.fcd.deterministic {{DT_BOOL}}**|
**--person-device.fcd.period {{DT_STRING}}**|

#### Traci Server

オプション|説明
---|---
**--remote-port {{DT_INT}}**|
**--num-clients {{DT_INT}}**|

#### Mesoscopic

オプション|説明
---|---
**--mesosim {{DT_BOOL}}**|
**--meso-edgelength {{DT_FLOAT}}**|
**--meso-tauff {{DT_TIME}}**|
**--meso-taufj {{DT_TIME}}**|
**--meso-taujf {{DT_TIME}}**|
**--meso-taujj {{DT_TIME}}**|
**--meso-jam-threshold {{DT_FLOAT}}**|
**--meso-multi-queue {{DT_BOOL}}**|
**--meso-junction-control {{DT_BOOL}}**|
**--meso-junction-control.limited {{DT_BOOL}}**|
**--meso-tls-penalty {{DT_FLOAT}}**|
**--meso-minor-penalty {{DT_TIME}}**|
**--meso-overtaking {{DT_BOOL}}**|
**--meso-recheck {{DT_TIME}}**|

#### Random Number

オプション|説明
---|---
**--random {{DT_BOOL}}**|
**--seed {{DT_INT}}**|
**--thread-rngs {{DT_INT}}**|

#### Gui Only

オプション|説明
---|---
**-g {{DT_FILE}}** <br/> **--gui-settings-file {{DT_FILE}}**|
**-Q {{DT_BOOL}}** <br/> **--quit-on-end {{DT_BOOL}}**|
**-G {{DT_BOOL}}** <br/> **--game {{DT_BOOL}}**|
**--game.mode {{DT_STRING}}**|
**-S {{DT_BOOL}}** <br/> **--start {{DT_BOOL}}**|
**--breakpoints {{DT_STRING}}**|
**--edgedata-files {{DT_FILE}}**|
**-D {{DT_BOOL}}** <br/> **--demo {{DT_BOOL}}**|
**-T {{DT_BOOL}}** <br/> **--disable-textures {{DT_BOOL}}**|
**--registry-viewport {{DT_BOOL}}**|
**--window-size {{DT_STRING}}**|
**--window-pos {{DT_STRING}}**|
**--tracker-interval {{DT_FLOAT}}**|
**--osg-view {{DT_BOOL}}**|
**--gui-testing {{DT_BOOL}}**|
**--gui-testing-debug {{DT_BOOL}}**|


## 入力ファイルの読みこみ順序

入力ファイル中で定義されたシミュレーションオブジェクトA(例: 車)が他のシミュレーションオブジェクトB(例: 車両タイプ)を参照している場合、オブジェクトBは必ずAより前に読みこまれるファイルか、Aと同じ入力ファイルのAより前の行に書かれていなければなりません。


## 追加ファイルのフォーマット

**--additional-files {{DT_FILE}}**オプションで追加されるファイルは、[交通信号]()、[検知器]()、[種々の速度標識]()、[バス停]()など幅広いネットワーク要素を含んでいます。
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


[fcd-wikipedia]: https://ja.wikipedia.org/wiki/%E3%83%95%E3%83%AD%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%AB%E3%83%BC%E3%83%87%E3%83%BC%E3%82%BF
