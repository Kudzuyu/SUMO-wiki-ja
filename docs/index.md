
# SUMO ユーザードキュメント

このページは交通流シミュレータ[SUMO](https://sumo.dlr.de/index.html)の日本語Wikiです。本家[英語版Wiki](https://sumo.dlr.de/docs/index.html)の内容を翻訳しています。

!!! Warning "注意"
    このドキュメントは現在翻訳中であり、リンクが繋がっていなかったり、記事が不完全な場所を多く含んでいます。
    正確な情報は原文ページを参照してください。

    このドキュメントは[本家Wiki](https://sumo.dlr.de/wiki/Simulation_of_Urban_MObility_-_Wiki)に対応するように継続的にアップデートされています。
    ソースコードは[GitHub](https://github.com/Kudzuyu/SUMO-wiki-ja)で管理されています。
    読んでいて問題がありましたら、issueに挙げていただけると助かります。

    このWikiは、本家Wikiを継承し[CC-BY-SA](https://creativecommons.org/licenses/by-sa/3.0/deed.ja)ライセンスです。

"**S**imulation of **U**rban **MO**bility" (SUMO)は、巨大な道路ネットワークを制御するようにデザインされた、オープンソースかつポータブルで、微視的(Microscopic)な道路交通流シミュレーションパッケージです。
SUMO は主に[ドイツ航空宇宙局(German Aerospace Center)](http://www.dlr.de/)にある[交通システム研究所(Institute of Transportation Systems)](http://www.dlr.de/ts)の職員によって開発されています。
SUMO は[EPL](https://eclipse.org/legal/epl-v20.html)の下でライセンスされています。

"Eclipse SUMO"は Eclipse Foundation のトレードマークです。
SUMO を使う場合には、出版物を私達に知らせることで開発をサポートしてください。

質問の結果を共有するために[メーリングリスト(英語)](https://sumo.dlr.de/wiki/Contact)をつかってください。
一般的な質問の答えは[FAQ]でも見つかるかもしれません。

!!! Note
    一般に SUMO について引用するときは、現在のレファレンス刊行物を使ってください。["Microscopic Traffic Simulation using SUMO"](https://elib.dlr.de/124092/); Pablo Alvarez Lopez, Michael Behrisch, Laura Bieker-Walz, Jakob Erdmann, Yun-Pang Flötteröd, Robert Hilbrich, Leonhard Lücken, Johannes Rummel, Peter Wagner, and Evamarie Wießner. IEEE Intelligent Transportation Systems Conference (ITSC), 2018.

ドキュメントの執筆や訂正、コードの登録や他の結果を含めどんな助力でも高く評価します。

!!! info "訳注"
    日本語版の翻訳を手伝ってくれる人は[この Wiki の github ページ](https://github.com/Kudzuyu/SUMO-wiki-ja)、英語版の本家を手伝いたい人は[本家 Wiki の執筆者になる方法]を参照してください

## はじめに

- [SUMO 交通流シミュレータ](./SUMO_at_a_Glance.md)

## 基本的な使いかた

- [ドキュメントでの記法](./Basics/Notation.md)
- [必要な基本的コンピュータスキル](./Basics/Basic_Computer_Skills.md)
- [SUMO のインストール](./Installing/index.md)
- [コマンドラインアプリケーション](./Basics/Using_the_Command_Line_Applications.md)
- [チュートリアル](./Tutorials/index.md)

## ネットワーク構築

* [SUMO 道路ネットワーク](./Networks/SUMO_Road_Networks.md)の紹介
* [抽象的ネットワーク構築](./Networks/Abstract_Network_Generation.md)
* [NETCONVERT]からのネットワークインポート
    - [XML を用いたネットワーク定義]
    - [SUMO 以外のネットワークのインポート]
        * [OpenStreetMap]
            - [3 クリックシナリオ生成]
        * [VISUM]
        * [Vissim]
        * [OpenDRIVE]
        * [MATsim]
        * [ArcView(シェープファイル)]
        * [DlrNavTeq]
        * [Robocup Simulation League]
    - [SUMO ネットワークのインポート]
    - [車道シミュレーション用のネットワーク構築]
    - [歩行者シミュレーション用のネットワーク構築]
    - [より高度な NETCONVERT オプション]
    - [追加出力]
* [NETEDIT を用いたネットワークの生成と編集]
* [標高](./Networks/Elevation.md)
* [地理情報](./Geo-Coordinates.md)

## 交通需要のモデリング

* [SUMO 交通需要モデリングの紹介]
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

**交通需要生成のためのデータソース**

* [O/D 行列のインポート]
    - [その他の VISUM 需要のインポート]
    - [その他の Vissim 需要のインポート]
* [目的地からの経路]
* [右左折確率による経路選択]
* [行動ベースの需要生成]
* [ランダムトリップ]
* [マルチモーダルランダム交通]

## シミュレーション

* [基本的な定義](./Simulation/Basic_Definition.md)
* [シミュレーション状態の保存と読み込み]

### 出力

* [シミュレーション出力]

### TraCI (オンライン操作)

* [TraCI 概要](./TraCI.md)

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

* [排気ガス](./Models/Emissions.md)
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
* [ランダム性](./Simulation/Randomness.md)
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

[メインアプリケーション(SUMO,SUMO-GUI,NETCONVERT ほか)]に加えて、150 以上の補助ツールがあります。
ツールは交通ネットワークの解析から、需要の生成、出力のための需要の整形までのトピックをカバーしています。
これらのほとんどは[python](https://www.python.org/)で書かれています。
全てのツールが SUMO ディストリビューション中の`<SUMO_HOME>`/tools ディレクトリにあります。

以下はいくつかの特に重要なツールへのリンクです。

* [osmWebWizard]
* [TraCI/python から TraCI を使う]
* [Python での SUMO ネットワーク読みこみと出力(sumolib)]
* [モビリティトレースのエクスポート(traceExporter)]
* [二つのネットワークの違いの検知]
* [ツール/可視化]

## 理論

* [一般的な交通シミュレーション](./Theory/Traffic_Simulations.md)

## アプリケーションマニュアル

* [SUMO](./sumo.md)
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
