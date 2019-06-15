# SUMO ユーザードキュメント

[原文ページ](https://sumo.dlr.de/wiki/SUMO_User_Documentation)

"**S**imulation of **U**rban **MO**bility" (Eclipse SUMO)は大規模な道路ネットワークを制御するためにつくられた、オープンソースでポータブルであり、微視的かつ連続的な道路交通シミュレーションパッケージです。
SUMOは主に[German Aerospace Center(ドイツ航空宇宙局)](http://www.dlr.de/)にある[Institute of Transportation Systems(交通システム研究所)](http://www.dlr.de/ts)の職員によって開発されています。
SUMOは[Eclipse Public License](https://eclipse.org/legal/epl-v20.html)の下でライセンスされています。
"Eclipse SUMO"はEclipse Foundationのトレードマークです。
SUMOを使う場合には、出版物を私達に知らせることで開発をサポートしてください。

質問の結果を共有するために[メーリングリスト(英語)](https://sumo.dlr.de/wiki/Contact)をつかってください。
一般的な質問の答えは[FAQ]でも見つかるかもしれません。

!!! Note
    一般にSUMOについて引用するときは、現在のレファレンス刊行物を使ってください。["Microscopic Traffic Simulation using SUMO"](https://elib.dlr.de/124092/); Pablo Alvarez Lopez, Michael Behrisch, Laura Bieker-Walz, Jakob Erdmann, Yun-Pang Flötteröd, Robert Hilbrich, Leonhard Lücken, Johannes Rummel, Peter Wagner, and Evamarie Wießner. IEEE Intelligent Transportation Systems Conference (ITSC), 2018.

ドキュメントの執筆や訂正、コードの登録や他の結果を含めどんな助力でも高く評価します。

!!! info "訳注"
    日本語版の翻訳を手伝ってくれる人は[このWikiのgithubページ](https://github.com/Kudzuyu/SUMO-wiki-ja)、英語版の本家を手伝いたい人は[本家Wikiの執筆者になる方法]を参照してください

## はじめに

- [SUMO交通流シミュレータ](document/sumo_at_a_glance.md)

## 基本的な使いかた

- [ドキュメントでの記法](document/basics_notation.md)
- [必要な基本的コンピュータスキル](document/basics_basic_computer_skills.md)
- [SUMOのインストール](document/install.md)
- [コマンドラインアプリケーション](document\basics_using_the_command_line_applications.md)
- [チュートリアル](document/tutrials.md)

## ネットワーク構築

* [SUMO道路ネットワーク]の紹介
* [抽象的ネットワーク構築](document/networks_abstract_network_generation.md)
* [NETCONVERT]からのネットワークインポート
    - [XMLを用いたネットワーク定義]
    - [SUMO以外のネットワークのインポート]
        * [OpenStreetMap]
            - [3クリックシナリオ生成]
        * [VISUM]
        * [Vissim]
        * [OpenDRIVE]
        * [MATsim]
        * [ArcView(シェープファイル)]
        * [DlrNavTeq]
        * [Robocup Simulation League]
    - [SUMOネットワークのインポート]
    - [車道シミュレーション用のネットワーク構築]
    - [歩行者シミュレーション用のネットワーク構築]
    - [より高度な NETCONVERT オプション]
    - [追加出力]
* [NETEDITを用いたネットワークの生成と編集]
* [標高](document/networks_elevation.md)
* [地理情報](document/geo-coordinates.md)

## 需要のモデリング

* [SUMO需要モデリングの紹介]
* [車両、車両タイプ、経路の定義]
* [公共交通のシミュレーション]
* [個人のシミュレーションと]
* [物流のシミュレーション]
* [最短または最適な経路設定]
* [複数交通を用いる経路設定]
* [シミュレーション中の経路設定]
* [動的ユーザー割り当ての計算]
* [歩行者による交通需要の生成]
* [車列生成のための車両タイプ作成]

**需要生成のためのデータソース**

* [O/D行列のインポート]
    - [その他のVISUM需要のインポート]
    - [その他のVissim需要のインポート]
* [目的地からの経路]
* [右左折確率による経路選択]
* [行動ベースの需要生成]
* [ランダムトリップ]
* [マルチモーダルランダム交通]

## シミュレーション

* [基本的な定義](document/simulation_basic_definition.md)
* [シミュレーション出力]
* [TraCI (オンライン)]
* [シミュレーション状態の保存と読みこみ]

### 交通管理とその他の構造

* [交通信号]
* [公共交通]
* [様々な速度標識]
* [経路変更器/代替経路表示]
* [蒸発器] (非推奨、かわりに測定器を使ってください)
* [交通流と速度の動的測定]
* [駐車場]

### 交通の種類

* [歩行者]
* [自転車]
* [鉄道]
* [水路]

### 追加的な特徴

* [排気ガス]
* [電気自動車]
* [物流]
* [一般的なパラメータ]
* [シェープの可視化]
* [無線検知]
* [緊急車両]
* [単純な隊列(Simpla)]

### モデル詳細

* [車両の速度]
* [車両の挿入]
* [車両の権限]
* [交差点のダイナミクス]
* [ランダム性]
* [(再)経路設定]
* [サブレーンモデル]
* [逆走]
* [安全性]
* [中視的モデル]

### よくある問題

* [車両のテレポート]
* [予期しない妨害]
* [予期しない車線変更戦略]
* [高密度交通流を得るには]

## [補助ツール]

全てのツールの索引は以下を参照してください。

* [ツール索引]

[メインアプリケーション(SUMO,SUMO-GUI,NETCONVERT ほか)]に加えて、150以上の補助ツールがあります。
ツールは交通ネットワークの解析から、需要の生成、出力のための需要の整形までのトピックをカバーしています。
これらのほとんどは[python](https://www.python.org/)で書かれています。
全てのツールがSUMOディストリビューション中の`<SUMO_HOME>`/toolsディレクトリにあります。

以下はいくつかの特に重要なツールへのリンクです。

* [osmWebWizard]
* [TraCI/pythonからTraCIを使う]
* [PythonでのSUMOネットワーク読みこみと出力(sumolib)]
* [モビリティトレースのエクスポート(traceExporter)]
* [二つのネットワークの違いの検知]
* [ツール/可視化]

## 理論

* [一般的な交通シミュレーション](document/theory_traffic_simulations.md)

## アプリケーションマニュアル

* [SUMO]
* [SUMO-GUI]
* [NETCONVERT]
* [NETEDIT]
* [NETGENERATE]
* [OD2TRIPS]
* [DUAROUTER]
* [JTRROUTER]
* [DFROUTER]
* [MAROUTER]
* [POLYCONVERT]
* [ACTIVITYGEN]
* [EMISSIONSMAP]
* [EMISSIONSDRIVINGCYCLE]

## 付録

* [更新履歴]
* [単語の説明]
* [FAQ]
* [補助ツール]
* [ファイル拡張子]
