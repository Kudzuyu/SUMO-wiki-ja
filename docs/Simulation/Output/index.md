<!-- headway : 車頭間隔 -->
<!-- induction loops : 誘導ループ -->
<!-- unaggregated induction loops : 非集積誘導ループ -->
<!-- clock hanging on the wall : 物理的な時計 -->
<!-- measures (device) : 計測（器） -->

# 出力

参考原文バージョン: 2021/10/28, a3700ac1fe61aab241d74f5afd347e78aa551703

## はじめに

[sumo](../../sumo.md)は多数の異なる計測値を生成できます。
全ての計測結果は、[writing files](../../Basics/Using_the_Command_Line_Applications.md#writing_files)の共通のルールに従い、収集された値をファイルやソケット接続に書き出します。
デフォルトではすべて無効化されているので、個別にトリガーする必要があります。
一部の出力([raw vehicle positions dump](RawDump.md)、[trip information](TripInfo.md)、[vehicle routes information](VehRoutes.md)、[simulation state statistics](Summary.md))は、コマンドラインのオプションでトリガーできます。
その他は{{AdditionalFiles}}で定義する必要があります。

### 出力の変換

全てのSUMOの出力ファイルは、デフォルトで、XML形式で書き出されます。
pythonツールの[xml2csv.py](../../Tools/Xml.md#xml2csvpy)を使うと、多くのスプレッドシートソフトで開くことができるフラットファイル（CSV）形式に出力ファイルを変換できます。
もし容量を圧縮した"標準的な"バイナリが必要な場合は[xml2protobuf.py](../../Tools/Xml.md#xml2protobufpy)が使えます。
また、全てのファイルは、ファイル拡張性.gzをトリガーに圧縮形式（gzip）で読み書きできます。

### 繰返し実行結果の分割

複数のシミュレーションの実行結果を分割しておきたい場合、**--output-prefix** {{DT_STR}}オプションで**全ての**出力ファイル名に接頭辞をつけることができます。
**--output-prefix TIME**を設定したとき、全ての出力は、シミュレーションを開始した時刻を接頭辞として使い、出力を自動分割します。

## 利用可能な出力ファイル

以下では、利用可能な出力をトピックや集計タイプごとのグループにまとめて列挙しています。
各出力の詳細はそれぞれのリンクで確認できます。

### vehicleの非集計情報

- [raw vehicle positions dump](RawDump.md):
  時間経過に伴うすべてのvehicleの位置
  *含まれる情報*: すべてのシミュレーション時間ステップにおける、すべてのvehicleの位置と速度
  *用途*: ノードの移動量入手（ns-2向けのV2V）
- [emission output](EmissionOutput.md):
  シミュレーションステップごとの全ての車両の排出量
- [full output](FullOutput.md): various
  全てのedge、lane、vehicleの情報（可視化に有効）
- [vtk output](VTKOutput.md): generates
  [VTK](http://www.vtk.org/)（Visualization Toolkit）フォーマットで知られるファイルで、vehicleごとの速度と位置を表します。
- [fcd output](FCDOutput.md):
  各vehicleの名前、位置、角度、タイプが含まれるフローティングカーデータ
- [trajectories output](AmitranOutput.md):
  Amitran規格に従う各vehicleの名前、位置、速度、加速度を含む軌跡データ
- [lanechange output](Lanechange.md):
レーン変更イベントと、各vehicleごとの変更に伴う動機
- [surrogate safety measures(SSM)](SSM_Device.md): 
車頭間隔、ブレーキ割合など、安全性に関連する指標の出力
- [vehicle type probe](VTypeProbe.md):
特定のvehicle typeに対する時間経過によるvehicleの位置（非推奨。代わりに、FCD出力をvTypeでフィルターして下さい）

### シミュレーションされた検出器

- [Inductive loop detectors (E1)](Induction_Loops_Detectors_(E1).md):
  シミュレーションされた誘導ループ
- [Instant induction loops](Instantaneous_Induction_Loops_Detectors.md):
　シミュレーションされた非集積誘導ループ
- [Lane area detectors (E2)](Lanearea_Detectors_(E2).md):
  laneセグメントの検出器（すなわち、シミュレーションされた車両トラッキングカメラ）
- [Multi-Entry-Exit detectors (E3)](Multi-Entry-Exit_Detectors_(E3).md):
  定義された場所の入退場イベントを検出してエリア内の交通を追跡するシミュレータ
- [Route Detectors](RouteProbe.md): 
  route分布のサンプリングを検出します。

### edgeやlaneの値

- [edgelane traffic](Lane-_or_Edge-based_Traffic_Measures.md):
edgeやlaneにおけるネットワーク性能指標
- [aggregated Amitran measures](Amitran_Traffic_Measures.md):
Amitran規格のedgeやlaneにおけるネットワーク性能指標
- [edgelane emissions](Lane-_or_Edge-based_Emissions_Measures.md):
edgeやlaneにおけるvehicleによる汚染物質排出量
- [edgelane noise](Lane-_or_Edge-based_Noise_Measures.md):
（Harmonoiseに基づく）edgeやlaneにおけるvehicleによるノイズ量
- [queue output](QueueOutput.md): 
レーンごとの交差点からの車列長さ

### 交差点に関する値

交差点の交通に関する特定の出力フォーマットはありません。
代わりに、交差点の交通を測る計測器を配置することで、交差点に関連する交通を測ることができます。

- [Tools/Output\#generateTLSE1Detectors.py](../../Tools/Output.md#generatetlse1detectorspy)
全てのTLS制御の交差点の周辺に誘導ループ検出器を生成するスクリプト（各レーンの特定地点を観測）
- [Tools/Output\#generateTLSE2Detectors.py](../../Tools/Output.md#generatetlse2detectorspy)
全てのTLS制御の交差点の周辺にlane-area検出器を生成するスクリプト（各レーンの特定エリアを観測）
- [Tools/Output\#generateTLSE3Detectors.py](../../Tools/Output.md#generatetlse3detectorspy)
TLS制御の交差点か、交差点の任意のリストの周辺に、multi-entry-exit検出器を静止絵するスクリプト。
検出器には、交差点に進入するedgeを集約するか分離するか、交差点内部を含むか否かを設定できます。（edgeにおけるエリアに基づく検出）

別の方法として、[edgeまたはlaneの値](#values_for_edges_or_lanes)の手動集計により、交差点内のフローを求めることができます。

### vehicleの情報

- [trip information](TripInfo.md):
各vehicleの旅程に関する集計情報（排出データを含むか選択可能）
- [vehicle routes information](VehRoutes.md): 
シミュレーション実行中の各vehicleのroute情報
- [stop output](StopOutput.md): 
  vehicleの[stops](../../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#stops)と、personやcontainerの積み込み／積み降ろしに関する情報
- [battery usage](../../Models/Electric.md#battery-output):
電動化vehicleのバッテリー状態の情報
- [collision output](Collisions.md):
vehicle同士や、vehicleと歩行者の間の衝突情報

### シミュレーション（ネットワーク）の情報

- [simulation state statistics](Summary.md):
（vehicleのカウントなど）シミュレーション状態に関する情報
- [simulation state person statistics](PersonSummary.md):
（personのカウントなど）personのシミュレーション状態に関する情報
- [statistic output](StatisticOutput.md):
シミュレーション全体の統計（vehicleやteleport、安全性、person、vehicleTripStatistics、rideStatisticsなど）

### [信号機](Traffic_Lights.md)の情報

- [traffic light states](Traffic_Lights.md#tls_states):
  信号機の現示状態の情報
- [stream-based traffic light switches](Traffic_Lights.md#tls_switches):
特定linkの信号の現示切り替えについての情報
- [traffic light states, by switch](Traffic_Lights.md#tls_switch_states):
変化のある場合に限定した信号機シグナルの現示状態の情報
- [areal detectors coupled to tls](Traffic_Lights.md#coupled_areal_detectors):
tlsでトリガーされるシミュレーションされたvehicle追跡カメラ

### デバッグ情報

- **--link-output** {{DT_FILE}}オプションは、交差点モデルに関するデバッグ向けデータを保存します。このデータは、各vehicleが直近で交差点を占有しようとしている長さを明らかにします。
- **--movereminder-output** {{DT_FILE}}オプションは、vechileの装置やlane、出力設備の間の相互作用のデバッグ向けデータを保存します。これは、デバッグフラグつきで[sumo](../../sumo.md)をコンパイルしたときのみ利用可能です。
- **--railsignal-block-output** {{DT_FILE}}オプションは、鉄道信号機のブロックに関する情報を保存します。制御されたrailSignalリンクごとに、次の情報が生成されます。
  - **forwardBlock**: 信号機のあるリンクから前方向にある次の鉄道信号機までの全てのlane
  - **bidiBlock**: 前方ブロック内で遭遇し、通行を許可する鉄道スイッチの先にある次のrailSignalまで続く、逆方向のトラックを構成する全てのlane
  - **backwardBlock**: 進入鉄道シグナルまで上流に続く、外側からのforwardBlockかbidiBlockに進入する全てのlane
  - **conflictLinks**: *<SIGNALID\>_<LINKINDEX\>*でエンコードされた、外側から衝突エリア（forwardBlock, bidiBlock, backwardBlock）へ進入するすべての制御されたリンク

## コマンドライン出力（step-log）

デフォルトでは、sumoが実行中であることを示す"heartbet"情報を表示します。
次の情報は100シミュレーションステップごとに表示されます。

- Step #: 現在のシミュレーション時刻
- 最新ステップの存続時間（**ms**）
- リアルタイム要因（ステップ長さと存続時間、**RT**）
- 1秒あたりのvehicleの更新数（**UPS**）
- **TraCI**: 現在ステップでTraCI処理にかかった時間（外部スクリプトを含む）
- **vehicles TOT**: それまでに出発したvehicle数
- **ACT**: 走行中のvehicle数
- **BUF**: 遅延挿入されたvehicle数

この出力は**--no-step-log**オプションで無効化できます。
その間隔は**--step-log.period TIME**オプションで設定できます。

## コマンドライン出力（verbose）

**--verbose**オプション（もしくは**-v**）でシミュレーションを実行したとき、（**--duration-log false**オプションで明示的に無効化されていない限り）次のデータが表示されます。

### vehicleのカウント

- Inserted: 道路ネットワークに挿入されたvehicle数
- Loaded: routeファイルから読み込まれたvehicle数
これは、二つの理由から放出されたものと異なる可能性があります。
  - 1.0以下の値の**--scale**オプションで実行している場合
  - ネットワークが混雑していて、シミュレーション時間が終わるまで全てのvehicleを挿入できなかった場合
- Running: シミュレーション終了時、ネットワーク上でアクティブなvehicle数
- Waiting: 混雑によりまだ挿入できていないvehicle数
- Teleports: 次のうちいずれかの理由で、vehicleがテレポートした回数（テレポート警告が出される度にこれらの理由が表示されます）
  - [Collision](../Why_Vehicles_are_teleporting.md#collisions):
    先行vehicleに関するminGap要件に違反したvehicle
  - [Timeout](../Why_Vehicles_are_teleporting.md#waiting_too_long_aka_grid-locks):
    vehicleが--time-to-teleport（デフォルトは300）秒移動できなかった。
    - wrong lane: 現在のlaneではrouteが維持できないず、lane変更もできなかったために、vehicleが移動できなくなった
    - yield: 優先権がないため、vehicleが交差点を通過できなかった。
    - jam: 次のlaneに空きがなかったため、vehicleが移動できなかった。

もし、シミュレーションにpersonが含まれている場合、次のデータが出力に追加されます。

- Inserted: routeファイルから読み込まれたperson数
- Running: シミュレーション終了時にネットワーク上でアクティブなperson数
- Jammed: personが詰まった回数

### タイミングデータ

- Duration: シミュレーション実行の（物理的な時計で測れらた）経過時間
- TraCI-Duration: TraCIコマンドの処理にかかった（物理的な時計で測れらた）経過時間。traciクライアントスクリプトで費やされた時間を含みます。
- "Real time factor": *simulated time* / *computation time*の商。1時間シミュレーションするのに360秒かかった場合は10になります。
- UPS (updates per second): 計算機時間1秒あたりのvehicleの更新数の平均。1つのvehicle更新に平均1ミリ秒かかる場合は1000になります。

もし、シミュレーションにおける経路生成に時間がかかった場合、各経路生成アルゴリズムのインスタンスは以下をレポートします。

- ルーティングクエリの数
- 最良経路を見つけるために確認されたedge数
- ルーティングにかかった総時間と、ルーティング呼び出しごとの平均時間

### 集計された交通計測

**--duration-log.statistics**オプション（もしくは**-t**）が設定されたとき、詳細出力が（*false*が明示的に設定されていない限り）自動的に有効化され、以下の項目について、全てのvehicle tripの平均が表示されます。

- RouteLength: 平均route長さ
- Speed: 平均trip速度
- Duration: 平均trip期間
- WaitingTime: （不本意な）待ち時間の平均
- TimeLoss: 希望より遅く移動したためにロスした平均時間（WaitingTimeを含む）。希望速度は、vehicleの[speedFactor](../../Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md#speed_distributions)を考慮します。
- DepartDelay: vehicleの出発が[道路のスペース不足によって遅延](../VehicleInsertion.md)した時間の平均

  !!! note
      デフォルトでは、すでに到着したvehicleだけがこれらの統計に含まれます。**--tripinfo-output.write-unfinished**オプションが設定された場合、走行中のvehicleも統計に含まれます。

- DepartDelayWaiting: シミュレーション終了までに道路のスペース不足で挿入できなかったvehicleの平均待ち時間（**--tripinfo-output.write-unfinished**オプションが設定された場合にのみ表示されます）

もし、シミュレーションに歩行者（歩行するperson）が含まれていた場合、以下の出力が追加されます。

- walks: 入力に含まれる`<walk>`要素数
- RouteLength: 平均歩行距離
- Duration: 平均歩行期間
- TimeLoss: 最大速度以下での歩行、もしくは、停止によりロスした平均時間

もし、シミュレーションにpassengers（vehicleに乗車しているperson）が含まれている場合、以下の出力が追加されます。

- Rides: 入力に含まれる`<ride>`要素数
- WaitingTime: 乗車待ちの平均時間
- RouteLength: 平均乗車長さ
- Duration: 平均乗車期間
- Bus rides: 道路上を走行する公共交通vehicleへの乗車回数（公共交通は*line*要素を持つかで識別されます）
- Train rides: 線路上 を走行する公共交通vehicleへの乗車回数
- Bike rides: *bicycle*クラスのvehicleへの乗車回数
- Aborted rides: 適切なvehicleが利用できなかったために、完了できなかった乗車

また、[統計出力](StatisticOutput.md)には上記の統計や、安全（safety）や乗車（ride）、輸送（transport）に関する統計を含むシミュレーション全体の統計を見ることができます。

このオプションを設定して[sumo-gui](../../sumo-gui.md)を使ったとき、ネットワークパラメータのダイアログに、これらの交通指標の走行平均も表示されます。（ダイアログは、ネットワーク背景を右クリックすることでアクセスできます。）

