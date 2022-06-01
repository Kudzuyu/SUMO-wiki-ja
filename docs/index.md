# Simulation of Urban MObility(SUMO)日本語Wiki

[原文ページ(English Documantation)](https://sumo.dlr.de/docs/index.html)

参考原文バージョン: 2022-01-04 (56f9f69ce04ad4fb1bd031ed1b9e49d2b742ff94)

このページは交通流シミュレータ[SUMO](https://sumo.dlr.de/index.html)の日本語Wikiです。本家[英語版ドキュメント](https://sumo.dlr.de/docs/index.html)の内容を翻訳しています。

"**S**imulation of **U**rban **MO**bility" (SUMO) は、オープンソースで移植性の高い、大規模ネットワークを扱うために設計された微視的かつ連続的な交通シミュレーション・パッケージです。
歩行者を含むインターモーダルなシミュレーションが可能で、シナリオ作成用のツールも豊富に用意されています。
SUMOはドイツ航空宇宙センター(https://www.dlr.de)の交通システム研究所(https://www.dlr.de/ts)の職員が中心となって開発しています。
SUMOは、[EPL 2.0](https://eclipse.org/legal/epl-v20.html)に基づいてライセンスされています。
ソースコードは、以下の二次ライセンスのもとで利用できるようにすることもできます。
EPL 2.0に規定された利用可能条件が満たされている場合、ソースコードは以下の二次ライセンスでも利用可能です。[GPL2以降](https://www.gnu.org/licenses/old-licenses/gpl-2.0-standalone.html).

!!! Warning "注意"
    一般的にSUMOを引用する場合は、最新の出版物を使用してください。
    ["Microscopic Traffic Simulation using SUMO"](https://elib.dlr.de/127994/); Pablo Alvarez Lopez, Michael Behrisch, Laura Bieker-Walz, Jakob Erdmann, Yun-Pang Flötteröd, Robert Hilbrich, Leonhard Lücken, Johannes Rummel, Peter Wagner, and Evamarie Wießner. IEEE Intelligent Transportation Systems Conference (ITSC), 2018.

本ドキュメントの内容は自由に編集可能です。
ページを編集するためには、右上の「Edit on GitHub」ボタンをクリックし、Pull Requestを送信してください。

[記事の編集](Editing_Articles.md)についての簡単なヘルプはこちらです。
ローカルでドキュメントを[ビルド](Developer/Documentation_Build.md)することや、コピーを[ダウンロード](https://sumo.dlr.de/sumo_documentation.zip)することも可能です。

英語版のドキュメントは継続的に更新され、常に最新の開発バージョンを参照しています。
SUMOの特定のリリースバージョンのドキュメントは、そのバージョンのダウンロードに含まれており、{{SUMO}}/docs/userdoc/index.htmlを開くことで閲覧することができます。

!!! Warning "注意"
    このドキュメントは現在翻訳中であり、リンクが繋がっていなかったり、記事が不完全な場所を多く含んでいます。
    できる限り原文ページも参照して正確な情報を得てください。

このドキュメントは[本家英語版ドキュメント](https://sumo.dlr.de/docs/index.html)に対応するように継続的にアップデートされています。
ソースコードは[GitHub](https://github.com/Kudzuyu/SUMO-wiki-ja)で管理されています。
問題を発見したら、issueに挙げていただけると助かります。

日本語ドキュメントは、本家ドキュメントを継承し[CC-BY-SA](https://creativecommons.org/licenses/by-sa/3.0/deed.ja)ライセンスです。

# はじめに

- [SUMO概要](SUMO_at_a_Glance.md)

# 基本的な使用方法

- [このドキュメントでの表記](Basics/Notation.md)
- [必要な基本的なコンピュータスキル](Basics/Basic_Computer_Skills.md)
- [SUMOのインストール](Installing/index.md)
- [SUMOのコマンドラインアプリケーション使用](Basics/Using_Command_Line_Application.md)
- [チュートリアル](Tutorials/index.md)
- [アプリケーション入力の検証](XMLValidation.md)

# ネットワーク構築

- [SUMOロードネットワーク](Networks/SUMO_Road_Networks.md)への導入
- [抽象的なネットワークの生成](Networks/Abstract_Network_Generation.md)
- [netconvertでネットワークを取り込む](netconvert.md)
  - [XMLを使って独自のネットワークを定義する](Networks/PlainXML.md)
  - [SUMO以外のネットワークをインポートする](Networks/Import.md)
    - [OpenStreetMapからのインポート](Networks/Import/OpenStreetMap.md)
      - [3クリックシナリオジェネレータ](Networks/Import/OpenStreetMap.md#3-click_scenario_generation)
    - [VISUM](Networks/Import/VISUM.md)
    - [Vissim](Networks/Import/Vissim.md)
    - [OpenDRIVE](Networks/Import/OpenDRIVE.md)
    - [MATsim](Networks/Import/MATsim.md)
    - [ArcView(シェープファイル)](Networks/Import/ArcView.md)
    - [DlrNavTeq](Networks/Import/DlrNavteq.md)
    - [ロボカップシミュレーションリーグから](Networks/Import/RoboCup.md)
  - [SUMO ネットワークのインポート](Networks/Import/SUMO_Road_Networks.md)
  - [高速道路シミュレーションのためのネットワーク構築](Simulation/Motorways.md#building_a_network_for_motorway_simulation)
  - [歩行者シミュレーションのためのネットワーク構築](Simulation/Pedestrians.md#building_a_network_for_pedestrian_simulation)
  - [その他のnetconvertオプション](Networks/Further_Options.md)
  - [追加の出力](Networks/Further_Outputs.md)
- [neteditによるネットワークの作成と修正](netedit/index.md)
- [標高データを含む](Networks/Elevation.md)
- [地理座標](Geo-Coordinates.md)

# 需要モデリング

- [SUMO需要モデル入門](Demand/Introduction_to_demand_modelling_in_SUMO.md)
- [車両、車両タイプ、ルートの定義](Definition_of_Vehicles,_Vehicle_Types,_and_Routes.md)
- [neteditによる交通需要の定義](netedit/elementsDemand.md)
- [公共交通のシミュレーション](Simulation/Public_Transport.md)
- [個人とトリップチェーンのシミュレーション](Specification/Persons.md)
- [物流のシミュレーション](Specification/Logistics.md)
- [最短または最適経路のルーティング](Demand/Shortest_or_Optimal_Path_Routing.md)
- [インターモーダルルーチング](IntermodalRouting.md)
- [シミュレーションでのルーティング](Demand/Automatic_Routing.md)
- [動的なユーザ割り当ての計算](Demand/Dynamic_User_Assignment.md)
- [歩行者交通需要の生成](Simulation/Pedestrians.md#generating_pedestrian_demand)
- [車両をモデル化するための車種分布の生成](Tools/Misc.md#createvehtypedistributionspy)

### 交通需要生成のためのデータソース

- [O/Dマトリックスのインポート](Demand/Importing_O/D_Matrices.md)
  - [VISUMデマンドのインポート](Demand/Further_Ways_to_import_VISUM_Demand_Definitions.md)
  - [他のVissimデマンドのインポート](Demand/Further_Ways_to_import_Vissim_Demand_Definitions.md)
- [カウントデータ（ロードカウント、ターンカウント）からのルート](Demand/Routes_from_Observation_Points.md)
- [旋回確率によるルート](Demand/Routing_by_Turn_Probabilities.md)
- [活動ベースの需要生成](Demand/Activity-based_Demand_Generation.md)
- [ランダムトリップ](Tools/Trip.md#randomtripspy)
- [マルチモーダルランダムトラフィック](Tools/Import/OSM.md#osmwebwizardpy)
- [GTFSデータ](Tools/Import/GTFS.md)

#シミュレーション

- [基本定義](Simulation/Basic_Definition.md)
- [シミュレーションの状態の保存と読み込み](Simulation/SaveAndLoad.md)

## 出力
- [Simulationの出力概要](Simulation/Output/index.md)

## TraCI (オンラインインタラクション)
- [TraCI overview](TraCI.md) - The **Tra**ffic **C**ontrol **I**nterface
- [Libsumo](Libsumo.md) - ライブラリとしてsumoを使用する

## 交通管理およびその他の構造物

- [信号機](Simulation/Traffic_Lights.md)
- [公共交通](Simulation/Public_Transport.md)
- [速度可変標識](Simulation/Variable_Speed_Signs.md)
- [リルーター/代替ルート標識](Simulation/Rerouter.md)
- [Vaporizer](Simulation/Vaporizer.md) (非推奨、代わりにキャリブレータを使用)
- [流量と速度と種類の動的なキャリブレーション](Simulation/キャリブレータ.md)
- [パーキングエリア](Simulation/ParkingArea.md)
- [ターンアラウンド](シミュレーション/Turnarounds.md)

## Traffic Modes

- [歩行者シミュレーション](シミュレーション/Pedestrians.md)
- [自転車シミュレーション](Simulation/Bicycles.md)
- [鉄道シミュレーション](Simulation/Railways.md)
- [水路シミュレーション](Simulation/Waterways.md)

## その他の機能

- [排気ガス](Models/Emissions.md)
- [電気自動車](Models/Electric.md)
- [電気ハイブリッド車、架線、変電所](Models/ElectricHybrid.md)
- [物流](仕様/Logistics.md)
- [一般的なパラメータ](Simulation/GenericParameters.md)
- [形状の可視化](Simulation/Shapes.md)
- [無線デバイスの検出](Simulation/Bluetooth.md)
- [緊急車両](Simulation/Emergency.md)
- [簡易プラトーニング(Simpla)](Simpla.md)
- [需要応答型輸送（DRT）／タクシー](Simulation/Taxi.md)
- [グリーンライト最適速度勧告(GLOSA)](Simulation/GLOSA.md)

## モデル詳細

- [車両速度](シミュレーション/VehicleSpeed.md)
- [車両挿入](Simulation/VehicleInsertion.md)
- [車両パーミッション(アクセス制限)](Simulation/VehiclePermissions.md)
- 道路容量](Simulation/RoadCapacity.md)
- [交差点ダイナミクス](Simulation/Intersections.md)
- [ランダムネス](Simulation/Randomness.md)
- [経路変更と再経路変更](シミュレーション/経路変更.md)
- [サブレーンモデル](シミュレーション/SublaneModel.md)
- [逆走](シミュレーション/OppositeDirectionDriving.md)
- [安全](シミュレーション/Safety.md)
- [メゾスコピックモデル](シミュレーション/Meso.md)
- [長さと距離](Simulation/Distances.md)

## FAQ

- [車両のテレポート](Simulation/Why_Vehicles_are_teleporting.md)
- [予期せぬ妨害](FAQ.md#the_simulation_has_lots_of_jamsdeadlocks_what_can_i_do)
- [折り返しが多すぎる](Simulation/Turnarounds.md)
- [予想外の車線変更操作は？](FAQ.md#why_do_the_vehicles_perform_unexpected_lane-changing_maneuvers)
- [高い流量を得るにはどうしたらいいですか](FAQ.md#how_do_i_get_high_flowsvehicle_densities)

# その他のツール

主なアプリケーション[(sumo, sumo-gui, netedit, netconvertなど)](SUMO_at_a_Glance.md#included_applications)に加え、150以上の追加ツールが存在します。
これらのツールは、トラフィックネットワーク分析、需要生成、需要修正から出力分析までのトピックをカバーしています。
そのほとんどは[python](https://www.python.org/)で記述されています。すべてのツールは、SUMO-distributionの{{SUMO}}/toolsの下に見つけることができます。
すべてのツールの索引は、以下を参照してください。

- [ツールインデックス](Tools/index.md)

以下は、最も重要で使用されているツールへのリンクです。

- [osmWebWizard](Tools/Import/OSM.md#osmwebwizardpy) - ウェブブラウザを使って、数クリックで、簡単なシナリオを作成することができます。
- [Interfacing TraCI from Python](TraCI/Interfacing_TraCI_from_Python.md) - Pythonを使用して実行中のSUMOシミュレーションにアクセスします。
- [sumolib](Tools/Sumolib.md) - SUMOネットワークとSUMO xmlファイル全般を扱うPythonモジュール
- [Xml Tools](Tools/Xml.md) - SUMOの出力をCSV/Spreadsheetに、またはその逆に変換するためのツールです。
- [traceExporter.py](Tools/TraceExporter.md) - モビリティートレース(FCD出力)を異なる "トレースファイル "形式にエクスポートする。
- [netdiff.py](Tools/Net.md#netdiffpy) - 2つのネットワーク間の差異を測定します。
- [Visualization Tools](Tools/Visualization.md) - シミュレーションの様々な出力をグラフィカルで分かりやすく表示します。

#理論

- [トラフィックシミュレーション全般](Theory/Traffic_Simulations.md)

# 応用マニュアル

- [sumo](sumo.md)
- [sumo-gui](sumo-gui.md)
- [netconvert](netconvert.md)
- [netedit](netedit/index.md)
- [netgenerate](netgenerate.md)
- [od2trips](od2trips.md)
- [デュアルータ](duarouter.md)
- [jtrouter](jtrouter.md)
- [dfrouter](dfrouter.md)
- [marouter](marouter.md)
- [ポリコンバート](polyconvert.md)
- [activitygen](activitygen.md)
- [emissionsMap](Tools/Emissions.md#emissionsmap)
- [emissionsDrivingCycle](Tools/Emissions.md#emissionsdrivingcycle)。

# ソフトウェアの貢献
SUMOを拡張したり、より使いやすくするためにツールを作ったりした人がいます。これらの拡張のすべてが "SUMOコア"の一部であるわけではありません。

- [配布物に含まれるもの](Contributed/index.md#included_in_the_distribution)
- [外部](Contributed/index.md#external_extensions)

# Appendices

- [変更履歴](ChangeLog.md)
- [用語集](Other/Glossary.md)
- [よくある質問](FAQ.md)
- [既知のファイル拡張子](その他/File_Extensions.md)

