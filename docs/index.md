# Simulation of Urban MObility(SUMO)日本語Wiki

"**S**imulation of **U**rban **MO**bility" (SUMO) は、オープンソースで移植性の高い、大規模ネットワークを扱うために設計された微視的かつ連続的な交通シミュレーション・パッケージです。
歩行者を含むインターモーダルなシミュレーションが可能で、シナリオ作成用のツールも豊富に用意されています。
SUMOはドイツ航空宇宙センター(https://www.dlr.de)の交通システム研究所(https://www.dlr.de/ts)の職員が中心となって開発しています。
SUMOは、[EPL 2.0](https://eclipse.org/legal/epl-v20.html)に基づいてライセンスされています。
ソースコードは、以下の二次ライセンスのもとで利用できるようにすることもできます。
EPL 2.0に規定された利用可能条件が満たされている場合、ソースコードは[GPL2以降](https://www.gnu.org/licenses/old-licenses/gpl-2.0-standalone.html)の二次ライセンスでも利用可能です。

成果報告や質問には[メーリングリスト](Contact.md)を使ってください．
いくつかのよくある質問は[FAQ](FAQ.md)にあるかもしれません．

SUMOを使った時には，私達(訳注: SUMO公式) にその[出版物](Publications.md)について連絡してください．

!!! note
    When citing SUMO in general please use our current reference publication: ["Microscopic Traffic Simulation using SUMO"](https://elib.dlr.de/127994/); Pablo Alvarez Lopez, Michael Behrisch, Laura Bieker-Walz, Jakob Erdmann, Yun-Pang Flötteröd, Robert Hilbrich, Leonhard Lücken, Johannes Rummel, Peter Wagner, and Evamarie Wießner. IEEE Intelligent Transportation Systems Conference (ITSC), 2018.

このドキュメントは自由に編集できます。
特定のページを編集するには、右上の「GitHubで編集」ボタンをクリックし、プルリクエストを送信してください。
[記事の編集](Editing_Articles.md)に関する簡単なヘルプはこちらです。
ドキュメントの[ローカルビルド](Developer/Documentation_Build.md)や，[ダウンロード](https://sumo.dlr.de/sumo_documentation.zip)もできます。

このドキュメントは継続的に更新され、常に最新の開発版を参照しています。
特定のリリース版のSUMO向けドキュメント (訳注: 英語版)はそのバージョンのダウンロードに含まれており、{{SUMO}}/docs/userdoc/index.htmlから閲覧できます。

## Introduction 

- [SUMOシミュレーション](SUMO_at_a_Glance.md)

## 基本的な使い方

- [ドキュメント中の記法](Basics/Notation.md)
- [必要なコンピュータスキル](Basics/Basic_Computer_Skills.md)
- [SUMOのインストール](Installing/index.md)
- [SUMO CLIの使い方](Basics/Using_the_Command_Line_Applications.md)
- [チュートリアル](Tutorials/index.md)
- [アプリケーション入力の検証](XMLValidation.md)
- [表形式出力](TabularOutputs.md)

## ネットワーク構築

- [SUMO Road Networks概要](Networks/SUMO_Road_Networks.md)
- [抽象ネットワーク生成](Networks/Abstract_Network_Generation.md)
- [netconvert](netconvert.md) によるネットワークインポート
- [XMLを使用した独自ネットワーク定義](Networks/PlainXML.md)
- [SUMO以外のネットワークのインポート](Networks/Import.md)
- [OpenStreetMapからのインポート](Networks/Import/OpenStreetMap.md)
- [3クリックシナリオ生成](Networks/Import/OpenStreetMap.md#3-click_scenario_generation)
- [VISUMからのインポート](Networks/Import/VISUM.md)
- [Vissimからのインポート](Networks/Import/Vissim.md)
- [OpenDRIVEからのインポート](Networks/Import/OpenDRIVE.md)
- [MATsimからのインポート](Networks/Import/MATsim.md)
- [ArcView (shapefiles)からのインポート](Networks/Import/ArcView.md)
- [DlrNavTeqからのインポート](Networks/Import/DlrNavteq.md)
- [Robocup Simulation Leagueからのインポート](Networks/Import/RoboCup.md)
- [SUMOネットワークのインポートとパッチ適用](Networks/Import/SUMO_Road_Networks.md)
- [高速道路シミュレーション用ネットワーク構築](Simulation/Motorways.md#building_a_network_for_motorway_simulation)
- [歩行者シミュレーション用ネットワーク構築](Simulation/Pedestrians.md#building_a_network_for_pedestrian_simulation)
- [追加のnetconvertオプション](Networks/Further_Options.md)
- [SUMO以外のネットワークのエクスポート](Networks/Export.md)
- [追加出力](Networks/Further_Outputs.md)
- [neteditによるネットワークの作成と修正](Netedit/index.md)
- [標高データの組み込み](Networks/Elevation.md)
- [地理座標](Geo-Coordinates.md)

## 交通需要モデリング

- [SUMO需要モデリング入門](Demand/Introduction_to_demand_modelling_in_SUMO.md)
- [車両、車両タイプ、ルートの定義](Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md)
- [neteditによる交通需要の定義](Netedit/elementsDemand.md)
- [公共交通機関のシミュレーション](Simulation/Public_Transport.md)
- [個人および移動連鎖のシミュレーション](Specification/Persons.md)
- [物流のシミュレーション](Specification/Logistics.md)
- [最短または最適経路ルーティング](Demand/Shortest_or_Optimal_Path_Routing.md)
- [インターモーダルルーティング](IntermodalRouting.md)
- [シミュレーション内でのルーティング](Demand/Automatic_Routing.md)
- [動的利用者割り当ての計算](Demand/Dynamic_User_Assignment.md)
- [歩行者交通需要の生成](Simulation/Pedestrians.md#generating_pedestrian_demand)
- [車両タイプ分布を生成して車両群をモデル化](Tools/Misc.md#createvehtypedistributionpy)

### 需要生成のためのデータソース

- [O/Dマトリックスのインポート](Demand/Importing_O/D_Matrices.md)
- [その他のVISUM需要インポーター](Demand/Further_Ways_to_import_VISUM_Demand_Definitions.md)
- [その他のVissim需要インポーター](Demand/Further_Ways_to_import_Vissim_Demand_Definitions.md)
- [計測データからの経路生成（道路計測、方向転換計測）](Demand/Routes_from_Observation_Points.md)
- [方向転換確率による経路生成](Demand/Routing_by_Turn_Probabilities.md)
- [活動ベースの需要生成](Demand/Activity-based_Demand_Generation.md)
- [ランダムな旅行](Tools/Trip.md#randomtripspy)
- [マルチモーダルなランダム交通](Tools/Import/OSM.md#osmwebwizardpy)
- [GTFSデータ](Tools/Import/GTFS.md)

## シミュレーション

- [基本定義](Simulation/Basic_Definition.md)
- [シミュレーション状態の保存と読み込み](Simulation/SaveAndLoad.md)
- [SUMO-JuPedSim連携](jupedsim.md)

### 出力
- [シミュレーション出力概要](Simulation/Output/index.md)

### TraCI (オンラインインタラクション)
- [TraCI概要](TraCI.md) - **Tra**ffic **C**ontrol **I**nterface
- [Libsumo](Libsumo.md) - sumoをライブラリとして使用

### 交通管理およびその他の構造

- [信号機](Simulation/Traffic_Lights.md)
- [公共交通](Simulation/Public_Transport.md)
- [可変速度標識](Simulation/Variable_Speed_Signs.md)
- [迂回路標識](Simulation/Rerouter.md)
- [蒸発器](Simulation/Vaporizer.md) (非推奨、代わりに[キャリブレーター](Simulation/Calibrator.md)を使用)
- [流量・速度・車種動的キャリブレーション](Simulation/Calibrator.md)
- [駐車エリア](Simulation/ParkingArea.md)
- [折り返し地点](Simulation/Turnarounds.md)

### 交通モード

- [歩行者シミュレーション](Simulation/Pedestrians.md)
- [自転車シミュレーション](Simulation/Bicycles.md)
- [鉄道シミュレーション](Simulation/Railways.md)
- [水路シミュレーション](Simulation/Waterways.md)

### 追加機能

- [排気ガス](Models/Emissions.md)
- [電気自動車](Models/Electric.md)
- [ハイブリッド電気自動車、架線、変電所](Models/ElectricHybrid.md)
- [物流](Specification/Logistics.md)
- [汎用パラメータ](Simulation/GenericParameters.md)
- [形状可視化](Simulation/Shapes.md)
- [無線機器検出](Simulation/Bluetooth.md)
- [緊急車両](Simulation/Emergency.md)
- [簡易プラトーニング (Simpla)](Simpla.md)
- [デマンド型交通 (DRT) / タクシー](Simulation/Taxi.md)
- [信号最適速度案内 (GLOSA)](Simulation/GLOSA.md)
- [ステーションファインダー（自律充電）](Simulation/Stationfinder.md)

### モデル詳細

- [車両速度](Simulation/VehicleSpeed.md)
- [車両挿入](Simulation/VehicleInsertion.md)
- [車両許可（アクセス制限）](Simulation/VehiclePermissions.md)
- [道路容量](Simulation/RoadCapacity.md)
- [交差点ダイナミクス](Simulation/Intersections.md)
- [ランダム性](Simulation/Randomness.md)
- [経路設定と経路変更](Simulation/Routing.md)
- [サブレーンモデル](Simulation/SublaneModel.md)
- [逆走](Simulation/OppositeDirectionDriving.md)
- [安全性](Simulation/Safety.md)
- [メゾスコピックモデル](Simulation/Meso.md)
- [長さおよび距離](Simulation/Distances.md)
- [摩擦](Simulation/Friction.md)

### よくある問題

- [車両がテレポートする理由](Simulation/Why_Vehicles_are_teleporting.md)
- [予期せぬ渋滞](FAQ.md#the_simulation_has_lots_of_jamsdeadlocks_what_can_i_do)
- [方向転換が多すぎる](Simulation/Turnarounds.md)
- [予期せぬ車線変更？](FAQ.md#why_do_the_vehicles_perform_unexpected_lane-changing_maneuvers)
- [高い流量を得るには？](FAQ.md#how_do_i_get_high_flowsvehicle_densities)

## 追加ツール

[主要アプリケーション（sumo、sumo-gui、netedit、netconvertなど）](SUMO_at_a_Glance.md#included_applications)に加え、250以上の追加ツールが用意されています。
これらは交通ネットワーク分析、交通需要の創出と修正から出力分析までをカバーしています。
ほとんどは[python](https://www.python.org/)で記述されています。
全てのツールはSUMOディストリビューションの{{SUMO}}/toolsディレクトリ内にあります。

全ツールのインデックスはこちら:

- [ツールインデックス](Tools/index.md)

以下は特に重要／使用頻度の高いツールへのリンクです：

- [osmWebWizard](Tools/Import/OSM.md#osmwebwizardpy) - ウェブブラウザで数クリックするだけで簡易シナリオを作成
- [PythonからのTraCI連携](TraCI/Interfacing_TraCI_from_Python.md) - Pythonで実行中のSUMOシミュレーションにアクセス
- [sumolib](Tools/Sumolib.md) - SUMOネットワークおよび一般的なsumo xmlファイルを扱うPythonモジュール
- [Xml Tools](Tools/Xml.md) - SUMO出力をCSV/スプレッドシートに変換、またはその逆変換を行うツール
- [traceExporter.py](Tools/TraceExporter.md) - モビリティトレース（FCD出力）を様々な「トレースファイル」形式にエクスポート
- [netdiff.py](Tools/Net.md#netdiffpy) - 二つのネットワーク間の差異を判定
- [可視化ツール](Tools/Visualization.md) - 幅広いシミュレーション出力をグラフィカルかつ分かりやすく可視化

## 理論

- [交通シミュレーション全般](Theory/Traffic_Simulations.md)

## アプリケーションマニュアル

- [sumo](sumo.md)
- [sumo-gui](sumo-gui.md)
- [netconvert](netconvert.md)
- [netedit](Netedit/index.md)
- [netgenerate](netgenerate.md)
- [od2trips](od2trips.md)
- [duarouter](duarouter.md)
- [jtrrouter](jtrrouter.md)
- [dfrouter](dfrouter.md)
- [marouter](marouter.md)
- [polyconvert](polyconvert.md)
- [activitygen](activitygen.md)
- [emissionsMap](Tools/Emissions.md#emissionsmap)
- [emissionsDrivingCycle](Tools/Emissions.md#emissionsdrivingcycle)

## ソフトウェアの貢献
一部の人々はSUMOを拡張したり、より使いやすくするためのツールを構築しました。
拡張機能のすべてがSUMOコアの一部であるわけではありません。

- [配布物に含まれるもの](Contributed/index.md#included_in_the_distribution)
- [外部](Contributed/index.md#external_extensions)

## 付録

- [変更履歴](ChangeLog.md)
- [用語集](Other/Glossary.md)
- [FAQ](FAQ.md)
- [既知のファイル拡張子](Other/File_Extensions.md)
- [netedit](Netedit/index.md) がサポートする[すべての XML 要素と属性のリスト](Netedit/attribute_help.md)

