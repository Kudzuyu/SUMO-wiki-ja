# TraCI

## TraCI の紹介

TraCI は "**Tra**ffic **C**ontrol **I**nterface"の略です。
実行中の道路シミュレーションへのアクセスのために、オブジェクトからの値の取得と振るまいの操作を「オンラインで」行なうことができます。

## 使いかた

### SUMO スタートアップ

TraCI は[SUMO](document/SUMO.md)へのアクセスのために、TCP ベースのクライアント/サーバー構造を使用します。
これによって[SUMO](document/SUMO.md)はサーバーとして振舞い、コマンドラインオプション **`--repote-port`[`<INT>`](datatype-link)**をうけとってリスニングポートの番号とします。


**--remote-port [`<INT>`][datatype-link]**オプションとともに開始すると、[SUMO][SUMO-link]はシミュレーションのみを用意し、外部アプリケーションが接続してコントロールを引き受けるまで待機します。
**--end [`<TIME>`][datatype-link]***オプションは[SUMO][SUMO-link]が TraCI サーバーとして動いている場合無視され、クライアントがシミュレーション終了を通知するまで動きつづけることに注意してください。

[SUMO-GUI]をサーバーとして使う場合、シミュレーションは[開始ボタン**を押して始めるか、**--start**オプションで TraCI コマンド実行前に開始しておく必要があります。

### 複数クライアント

シミュレーションに接続できるクライアントの数はオプション**--num-clients**[`<INT>`](datatype-link)**で設定できます(デフォルト: 1)。
複数のクライアントを用いる場合には、クライアントの起動順序を[SetOrder コマンド]で明示する必要があることに注意してください。

個々のクライアントにはユニークな(もしそうでなければ任意の)整数値が指定され、クライアントのコマンド各シミュレーションステップごと、指定された整数値の昇順に実行されます。

クライアントは各シミュレーションステップ後に自動で同期されます。
このことは、全てのクライアントから`simulationStep`コマンドが呼ばれない限り、シミュレーションが進まないことを示します。
また、`simulationStep`コマンドはシミュレーションが進んだ後にクライアントに制御を返します。

!!! caution "警告"
    シミュレーションは全てのクライアントと接続された時に一度だけ開始されます。


### プロトコル仕様

[TraCI プロトコル仕様]を参照してください([Basic Flow]、[Messages]、[データタイプ]を含む)。


### TraCI コマンド

* [制御関係のコマンド]: シミュレーションのステップや

以下の API において、ID は[SUMO]の入力ファイルにおいて定義された ID と同じものです。
詳細は[general structure]で確認できます。

* 値の取得
    - [検知器]
    - [車線検知器]
    - [複数車線検知器]
    - [交差点]
    - [車線](TraCI/Lane_Value_Retrieval.md)
    - [車両]
    - [歩行者]
    - [車両タイプ]
    - [経路]
    - [PoI]
    - [ポリゴン]
    - [バス停](TraCI/BusStop.md)
    - [交差点]
    - [節点]
    - [シミュレーション一般]
    - [GUI](TraCI/GUI_Value_Retrieval.md)
* 状態の変化
    - [車線]
    - [交通信号]
    - [車両]
    - [歩行者]
    - [車両タイプ]
    - [経路]
    - [PoI]
    - [ポリゴン]
    - [節点]
    - [シミュレーション一般]
* サブスクリプション
    - [オブジェクトの値]
    - [オブジェクトのコンテキスト]

* [ジェネリックパラメータ]へのアクセス

### シャットダウン

TraCI を使うと、[SUMO][SUMO-link]の**--end**オプションは無視されます。
代わりに、[close コマンド]で終了します。
全経路ファイルおよび全車両がシミュレートされたかどうかを確認するには，[getMinExpectedNumber]が 0 を返すかどうかを確認してください。
シミュレーションは全てのクライアントから`close`コマンドを受けとると直ちに終了します。

## SUMO をライブラリとして使う

一般に TraCI は複数のプロセスを組合せて使われます。
SUMO サーバーのプロセスと一つ以上の TraCI クライアントプロセスです。
代替案として、[Libsumo]は SUMO をクライアント処理に埋め込んで使うことができます。
これによって同じメソッドを用いながら，ソケット通信のオーバーヘッドを避けることができます。
Libsumo は[SWIG]を用いたクライアント生成をサポートしており、これによって多くのプログラミング言語から使用することができます。
ビルド済み SUMO には C++、Java、Python のバインディングが含まれています。

## 使用例

* [TraCI を用いた適応的交通信号のチュートリアル] (Python)。
* [チュートリアル/CityMobil] : TraCI を車両への経路設定に使用 (Python)。
* [チュートリアル/TraCIPedCrossing] : TraCI を押しボタン式信号の構築に利用。

## リソース

### プログラミング言語ごとのインターフェース

* Python: [tools/traci パッケージ] によって，Python と SUMO を連携させることができます(このライブラリは全ての TraCI コマンドをサポートし、日々テストされています)。
* C++: [C++ TraCIAPI] はクライアントライブラリであり、[SUMO]のソースツリーの一部になっています(ほぼ全ての API をカバーしています)。
* C++: [Veins project](http://veins.car2x.org/) は[SUMO]と[OMNET++](https://omnetpp.org/)のミドルウェアを提供します。インフラの一部として TraCI API 用の C++クライアントライブラリが提供されています(API の完全性は Python クライアントに比べてわずかに劣ります)。
* .NET: [TraCI.NET](https://github.com/CodingConnected/CodingConnected.Traci) はほとんどの API をカバーするクライアントライブラリです。
* Matlab: [TraCI4Matlab](http://www.mathworks.com/matlabcentral/fileexchange/44805-traci4matlab** クライアントは SUMO のリリース内 ***<SUMO_HOME>***/tools/contributed/traci4matlab に入っています。全てのコマンドが実装されてはいません。
* Java: [Traas] は [SUMO]のソースツリーの一部としてクライアントライブラリを提供します(ほぼ全ての API をカバーしています)。
* その他: [SOAP]を使って Web サービスにアクセスできる言語であれば、[Traas Web サービス]を使って SUMO にアクセスできます。[Java web サービスクライアント] も TraaS に含まれます。API は Python クライアントに比べて遅延があります。

### V2X シミュレーション

TraCI を用いることで、[SUMO] を通信ネットワークシミュレーションと組みあわせ、[車車間通信] のシミュレーションを実現できます。
詳細は [トピック/V2X] で確認できます。

### その他

* [SUMO] の TraCI サーバーは基本ディストリビューションの一部です。ソースコードは`src/traci-server`フォルダにあります。

## リファレンス

* Axel Wegener, Michal Piorkowski, Maxim Raya, Horst Hellbrück, Stefan Fischer and Jean-Pierre Hubaux. TraCI: An Interface for Coupling Road Traffic and Network Simulators. Proceedings of the 11th Communications and Networking Simulation Symposium, April 2008. [ACM デジタルライブラリ](https://dl.acm.org/citation.cfm?doid=1400713.1400740)
* Axel Wegener, Horst Hellbrück, Christian Wewetzer and Andreas Lübke: VANET Simulation Environment with Feedback Loop and its Application to Traffic Light Assistance. Proceedings of the 3rd IEEE Workshop on Automotive Networking and Applications, New Orleans, LA, USA, 2008. [IEEEXplore](https://doi.org/10.1109/GLOCOMW.2008.ECP.67)

## パフォーマンス

TraCI の使用はシミュレーション速度を低下させます。
速度の低下は様々な因子に依存します。

* 各ステップごとの TraCI 関数呼びだし数
* 呼ばれる TraCI 関数の種類(いくつかの関数は他のものより高価)
* TraCI スクリプト中の計算
* クライアントの言語

### 例
 
使用例として車両ごとの x,y 座標をシミュレーション中のステップごとに取得してみます(python クライアントを使用します)。

```python
    while traci.simulation.getMinExpectedNumber() > 0: 
        for veh_id in traci.vehicle.getIDList():
             position = traci.vehicle.getSpeed(veh_id)
        traci.simulationStep()
```

* このスクリプトは毎秒 25000 台の車両を処理することができます。
* [組みこみ python]を使用すると 50000 台まで速度が上昇します。
* [サブスクリプション]を使用することで同じプログラムを 50000 台まで高速化できます。

```python
    while traci.simulation.getMinExpectedNumber() > 0: 
        for veh_id in traci.simulation.getDepartedIDList():
            traci.vehicle.subscribe(veh_id, [traci.constants.VAR_POSITION])
        positions = traci.vehicle.getAllSubscriptionResults()
        traci.simulationStep()
```

このスクリプトを[Bolongna シナリオ] (車両数 9000、5000 ステップ**のもとで動かして、以下の記録が得られました。

* TraCI なしで 8 秒
* 平易な位置取得で 90 秒
* サブスクリプションを使用した取得: 42 秒
* 組みこみ python 使用の取得: 46 秒
* サブスクリプションと組みこみ python の併用: 34 秒
  
C++クライアントはより高速です。

* 平易な位置取得: 80 秒
* サブスクリプション使用: 28 秒

## 現在および今後の開発

**執筆中**

## トラブルシューティング

### 出力ファイルが閉じられていない

この問題は、シミュレーションが終了していないのにクライアントが出力にアクセスしようとした時に生じます。
シミュレーションが終了するまでクライアントを待機させることで解決できます。
バグレポートは[ticket524 (削除済み) ](http://sourceforge.net/apps/trac/sumo/ticket/524)にあります。

### 古い API

**TraCI**コマンドには二つの「世代」が存在します。
第一世代は主に[SUMO]で使われている string ベースの ID と外部への表現として使われる int ベースの表現をマッピングします。
このマッピングは内部的に行なわれます(**TraCI**内で)。

現在の第二世代は[SUMO]が読みこむものと同じ文字列 ID を使用します。
もし第一世代の API を使うことを余儀なくされる場合 (例えば TraNS を使いたい場合)、バージョン 0.12.23 までの[SUMO]だけが使えます。
古いバージョンを手に入れることについては[FAQ]を参照してください。


[datatype-link]: basics_notation.md#データタイプ
[SUMO-link]: SUMO.md
