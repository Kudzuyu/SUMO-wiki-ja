# TraCI

## TraCIの紹介

TraCIは "**Tra**ffic **C**ontrol **I**nterface"の略です。
実行中の道路シミュレーションへのアクセスのために、オブジェクトからの値の取得と振るまいの操作を「オンラインで」行なうことができます。

## 使いかた

### SUMO スタートアップ

TraCIは[SUMO](document/SUMO.md)へのアクセスのために、TCPベースのクライアント/サーバー構造を使用します。

**--remote-port [`<INT>`][datatype-link]**オプションとともに開始すると、[SUMO][SUMO-link]はシミュレーションのみを用意し、外部アプリケーションが接続してコントロールを引き受けるまで待機します。
**--end [`<TIME>`][datatype-link]**オプションは[SUMO][SUMO-link]がTraCIサーバーとして動いている場合無視され、クライアントがシミュレーション終了を通知するまで動きつづけることに注意してください。

[SUMO-GUI]をサーバーとして使う場合、シミュレーションは

### 複数クライアント

[datatype-link]: basics_notation.md#データタイプ
[SUMO-link]: SUMO.md

### TraCIコマンド

* [制御関係のコマンド]: シミュレーションのステップや

* 値の取得
  - [検知器]
  - [車線検知器]
  - [複数車線検知器]
  - [交差点]
  - [車線]
  - [車両]
  - [歩行者]
  - [車両タイプ]
  - [経路]
  - [PoI]
  - [ポリゴン]
  - [交差点]
  - [節点]
  - [シミュレーション一般]
  - [GUI]

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

TraCIを使うと、[SUMO][SUMO-link]の**--end**オプションは無視されます。

## SUMOをライブラリとして使う

一般的に、TraCIは

## リソース

### Pythonによるインターフェース

* Python 

## リファレンス

## パフォーマンス

TraCIの使用はシミュレーション速度を低下させます。
速度の低下は様々な因子に依存します。

* 各ステップごとのTraCI関数呼びだし数
* 呼ばれるTraCI関数の種類(いくつかの関数は他のものより高価)
* TraCIスクリプト中の計算
* クライアントの言語

### 例
 
使用例として車両ごとのx,y座標をシミュレーション中のステップごとに取得してみます(pythonクライアントを使用します)。

```python
    while traci.simulation.getMinExpectedNumber() > 0: 
        for veh_id in traci.vehicle.getIDList():
             position = traci.vehicle.getSpeed(veh_id)
        traci.simulationStep()
```

* このスクリプトは毎秒25000台の車両を処理することができます。
* [組みこみpython]を使用すると50000台まで速度が上昇します。
* [サブスクリプション]を使用することで同じプログラムを50000台まで高速化できます。

```python
    while traci.simulation.getMinExpectedNumber() > 0: 
        for veh_id in traci.simulation.getDepartedIDList():
            traci.vehicle.subscribe(veh_id, [traci.constants.VAR_POSITION])
        positions = traci.vehicle.getAllSubscriptionResults()
        traci.simulationStep()
```

このスクリプトを[Bolongnaシナリオ] (車両数9000、5000ステップ)のもとで動かして、以下の記録が得られました。

* TraCIなしで8秒
* 平易な位置取得で90秒
* サブスクリプションを使用した取得: 42秒
* 組みこみpython使用の取得: 46秒
* サブスクリプションと組みこみpythonの併用: 34秒
  
C++クライアントはより高速です。

* 平易な位置取得: 80秒
* サブスクリプション使用: 28秒

## 更なる開発

## トラブルシューティング

### 出力ファイルが閉じられていない

この問題は、シミュレーションが終了していないのにクライアントが出力にアクセスしようとした時に生じます。
シミュレーションが終了するまでクライアントを待機させることで解決できます。
バグレポートは[ticket524(削除済み)](http://sourceforge.net/apps/trac/sumo/ticket/524)にあります。

### 古いAPI

**TraCI**コマンドには二つの「世代」が存在します。
第一世代は主に[SUMO]で使われているstringベースのIDと外部への表現として使われるintベースの表現をマッピングします。
このマッピングは内部的に行なわれます(**TraCI**内で)。

現在の世代である第二世代は[SUMO]が読みこむものと同じ文字列IDを使用します。
もし第一世代のAPIを使うことを余儀なくされる場合(例えばTraNSを使いたい場合)、バージョン0.12.23までの[SUMO]だけが使えます。
古いバージョンを手に入れることについては[FAQ]を参照してください。

