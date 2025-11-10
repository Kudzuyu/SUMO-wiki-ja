# SUMO概要

[原文ページ](https://sumo.dlr.de/wiki/Sumo_at_a_Glance)

## About

"**S**imulation of **U**rban **MO**bility" (SUMO) は、オープンソースで微視的かつマルチモーダルな道路交通シミュレーションです。
SUMOは与えられた道路ネットワークにおいて車一台ごとの動きから構成された交通流がどのようなものかシミュレーションすることができます。
シミュレーションでは交通整理に関する広範なトピックを扱うことができます。
SUMOは純粋に微視的です。
自動車は一台ごとに陽にモデル化され、自身の経路を持ち個別にネットワーク内を移動していきます。
シミュレーションは標準で決定的ですが、[ランダム性導入]()のための様々なオプションがあります。

SUMOパッケージをダウンロードしたら、SUMOの他のアプリケーションも含まれていることに注意してください。
これらのアプリケーションはSUMOで使う道路ネットワークや交通需要のデータをインポート/準備するのに使われます。
詳細は[#含まれるアプリケーション](#含まれるアプリケーション)を参照してください。


「**S**imulation of **U**rban **MO**bility」（略称「SUMO」）は、オープンソースの微視的マルチモーダル交通シミュレーションです。
車両一台ずつから成る交通需要が、与えられた道路ネットワーク上をどのように移動するかをシミュレートできます。
このシミュレーションは、広範な交通管理課題の検討を可能にします。
純粋に微視的アプローチを採用しており、各車両が明示的にモデル化され、独自の経路を持ち、ネットワーク内を個別に移動します。
シミュレーションはデフォルトで決定論的ですが[ランダム性の導入](Simulation/Randomness.md)に関する様々なオプションが用意されています。

SUMOパッケージには、SUMO以外にも追加のアプリケーションが含まれています。
これらのアプリケーションは、SUMOで使用するための道路ネットワークや需要データのインポート/準備に使用されます。
より詳細なリストについては[付属アプリケーション](#included_applications)を参照してください。

## 機能

- 交通シミュレーションの準備と実行に必要な全アプリケーションを包含 （ネットワーク・経路インポート、DUA、シミュレーション）
- シミュレーション
  - 連続空間・離散時間の車両移動
  - 多様な車両タイプ
  - 車線変更可能な複数車線道路
  - 様々な優先通行権ルール、信号機
  - 高速なOpenGL GUI
  - 数万のエッジ（道路）からなるネットワークを管理
  - 高速実行（1GHzマシンで最大100,000車両更新/秒）
  - 実行時の他アプリケーションとの相互運用性
  - 実行時における他アプリケーションとの相互運用性
  - ネットワーク全体、エッジベース、車両ベース、検知器ベースの出力
  - 人ベースのインターモーダル移動をサポート
- ネットワークインポート
  - VISUM、Vissim、シェープファイル、OSM、RoboCup、MATsim、 OpenDRIVE、XML記述のインポート
  - 欠損値はヒューリスティックにより決定
- ルート設定
  - 微視的ルート - 各車両が独自のルートを持つ
  - 様々な動的ユーザー割り当てアルゴリズム
- 高い移植性
  - 標準C++と移植性のあるライブラリのみを使用
  - Windowsおよび主要Linuxディストリビューション向けパッケージが存在
- XMLデータのみの使用による高い相互運用性
- オープンソース（[EPL 2.0](https://www.eclipse.org/legal/epl-2.0/)）

## 使用例

2001年以降、SUMOパッケージは複数の国内および国際的な[研究プロジェクト](Other/Projects.md)で利用されてきました。
主な応用例は以下の通りです：

- 交通信号機の評価
- 経路選択と再設定
- 交通監視手法の評価
- [車載通信のシミュレーション](Topics/V2X.md)
- 交通予測

## 含まれるアプリケーション

本パッケージには以下が含まれます：

| アプリケーション名 | 概要 |
| --------------------------------------------------- | ---------------------------------------------------- ----- |
| [sumo](sumo.md) | 可視化なしの微視的シミュレーション；コマンドラインアプリケーション |
| [sumo-gui](sumo-gui.md) | グラフィカルユーザーインターフェース付き微視的シミュレーション |
| [netconvert](netconvert.md) | ネットワークインポーターおよびジェネレーター；様々な形式の道路ネットワークを読み込みSUMO形式に変換 |
| [netedit](Netedit/index.md) | グラフィカルネットワークエディタ |
| [netgenerate](netgenerate.md) | SUMOシミュレーション用の抽象ネットワークを生成 |
| [duarouter](duarouter.md) | 様々な需要記述形式をインポートし、ネットワーク上の最速経路を計算。DUA（二項分布モデル）を実行 |
| [jtrrouter](jtrrouter.md) | 交差点方向転換率を用いた経路計算 |
| [dfrouter](dfrouter.md) | 誘導ループ計測値からの経路計算 |
| [marouter](marouter.md) | マクロ的割当を実施 |
| [od2trips](od2trips.md) | 出入地マトリクスを単一車両の移動に分解 |
| [polyconvert](polyconvert.md) | 各種フォーマットの関心地点・ポリゴンをインポートし、[sumo-gui](sumo-gui.md) で可視化可能な記述に変換 |
| [activitygen](activitygen.md) | モデル化された人口の移動意向に基づく需要を生成 |
| [emissionsMap](Tools/Emissions.md#emissionsmap) | 排出量マップを生成 |
| [emissionsDrivingCycle](Tools/Emissions.md#emissionsdrivingcycle) | 指定された走行サイクルに基づく排出量を計算 |
| [追加ツール](Tools/index.md) | 大規模なアプリケーションを記述する必要がないタスクが存在します。これらのツールは様々な問題に対する複数の解決策をカバーしています。 |

複数の関係者が作業中にSUMOパッケージを拡張し
コードを提出しています。これらの貢献は通常テストされておらず、古くなっている可能性があります。全ての貢献のリストは[こちら](Contributed/index.md)で確認できます。

## 歴史

SUMOの開発は2000年に始まりました。
オープンソースの微視的道路交通シミュレーションを開発した主な理由は、交通研究コミュニティに対し独自のアルゴリズムを実装・評価できるツールを提供するためでした。
このツールは、完全な交通シミュレーションを実現するために必要な全ての要素、例えば道路ネットワーク、需要、交通制御を扱う手法の実装や設定などについては考慮する必要がありません。
このようなツールを提供することでDLRはi)共通のアーキテクチャとモデル基盤を使用することで実装されたアルゴリズムの比較可能性を高め、ii)他の貢献者からの追加的な支援を得ることを目指しました。

## ソフトウェア設計基準

主要な設計目標は二つありました：高速であること、移植性を持つこと。
このため、最初のバージョンはコマンドラインからのみ実行されるように開発されました——当初はグラフィカルインターフェースは提供されず、全てのパラメータを手動で入力する必要がありました．
これにより遅延を招く可視化処理を省略し、実行速度を向上させることが目的でした。
また、これらの目標に基づき、ソフトウェアは複数の部分に分割されあました。
各コンポーネントは特定の目的を持ち、個別に実行する必要があります．
この点がSUMOを他のシミュレーションパッケージと異なる点であり、 例えば動的なユーザー割り当てはシミュレーション本体内で実行され、 本ソフトのように外部アプリケーション経由ではない。
この分割によりパッケージ内の各アプリケーションを拡張しやすくなる。
なぜなら各コンポーネントは全てを処理する単一アプリケーションよりも規模が小さいためである。
また、複雑で重荷となるデータ構造を使用する代わりに、現在の目的に合わせて調整された高速なデータ構造を各 で使用することが可能になります。
それでも、このことは他のシミュレーションパッケージと比較して、SUMOの使用を少し不便なものにしています。
まだやるべきことが残っているため、現時点では統合されたアプローチに向けた再設計は考えていません。

## 貢献者と参加者

<table>
<thead>
<tr class="header">
<th><p>所属機関</p></th>
<th><p>氏名</p></th>
<th><p>担当分野 / 貢献内容</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><figure>
<img src="images/Zaik_small.gif" alt="Zaik_small.gif" />
</figure></td>
<td><p>Christian Rössel</p></td>
<td><p>初期微視的シミュレーションコア; 初期検出器実装</p></td>
</tr>
<tr class="even">
<td rowspan="11"><figure>
<img src="images/Dlr_small.gif" title="dlr_small.gif" alt="" />
</figure></td>
<td><p>Peter Wagner</p></td>
<td><p>モデル、組織、精神的指導</p></td>
</tr>
<tr class="odd">
<td><p>Daniel Krajzewicz</p></td>
<td><p>全般</p></td>
</tr>
<tr class="even">
<td><p>Julia Ringel</p></td>
<td><p>信号機 &amp; WAUT アルゴリズム</p></td>
</tr>
<tr class="odd">
<td><p>Eric Nicolay</p></td>
<td><p>全般</p></td>
</tr>
<tr class="even">
<td><p>Michael Behrisch</p></td>
<td><p>全般</p></td>
</tr>
<tr class="odd">
<td><p>Yun-Pang Wang</p></td>
<td><p>利用者割り当て</p></td>
</tr>
<tr class="even">
<td><p>Danilot Teta Boyom</p></td>
<td><p>車両間通信モデル（ソースから削除済み）</p></td>
</tr>
<tr class="odd">
<td><p>Sascha Krieg</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Lena Kalleske</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Laura Bieker</p></td>
<td><p>テスト、Pythonスクリプト</p></td>
</tr>
<tr class="even">
<td><p>Jakob Erdmann</p></td>
<td><p>ネットワークインポート、<a href="netedit.md">netedit</a></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Andreas Gaubatz</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Maik Drozdzynski</p></td>
<td></td>
</tr>
<tr class="odd">
<td rowspan="3"><p>リューベック大学 (Uni Lübeck)</p></td>
<td><p>Axel Wegener</p></td>
<td><p>TraCI 発起人</p></td>
</tr>
<tr class="even">
<td><p>Thimor Bohn</p></td>
<td><p>TraCI</p></td>
</tr>
<tr class="odd">
<td><p>Friedemann Wesner</p></td>
<td><p>TraCI</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Felix Brack</p></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Tino Morenz</p></td>
<td></td>
</tr>
<tr class="even">
<td rowspan="4"><p><img src="images/Uni_erlangen.png" title="fig:uni_erlangen.png" width="149" alt="uni_erlangen.png" /><br />
<br />
<img src="images/Uibk-small.png" title="fig:uibk-small.png" width="64" alt="uibk-small.png" /><br />
<br />
<img src="images/Logo_cmu.png" title="fig:logo_cmu.png" width="100" alt="logo_cmu.png" /><br />
<br />
<img src="images/Logo_ucla.png" title="fig:logo_ucla.png" width="100" alt="logo_ucla.png" /></p></td>
<td><p>Christoph Sommer</p></td>
<td><p>TraCIと<a href="https://veins.car2x.org/">Veins</a>の統合、サブスクリプションインターフェース、その他</p></td>
</tr>
<tr class="odd">
<td><p>David Eckhoff</p></td>
<td><p>TraCI、決定論的シミュレーション動作</p></td>
</tr>
<tr class="even">
<td><p>Falko Dressler</p></td>
<td><p>TraCI</p></td>
</tr>
<tr class="odd">
<td><p>Tobias Mayer</p></td>
<td><p>交通モデル抽象化、IDMモデルポート</p></td>
</tr>
<tr class="even">
<td><p>ベルリン工科大学 (HU Berlin)</p></td>
<td><p>Matthias Heppner</p></td>
<td><p>ユニットテスト</p></td>
</tr>
<tr class="odd">
<td rowspan="3"><figure>
<img src="images/Tum-logo.png" title="tum-logo.png" alt="" />
</figure></td>
<td><p>Piotr Woznica</p></td>
<td><p><a href="activitygen.md">activitygen</a></p></td>
</tr>
<tr class="even">
<td><p>Walter Bamberger</p></td>
<td><p>VANET における信頼シナリオの評価基盤としての <a href="activitygen.md">activitygen</a> の開発。この作業は、自動車ネットワークにおける信頼性の高い確率的知識処理を特徴とするプロジェクト <a href="https://www.ldv.ei.tum.de/fidens/">Fidens: 協調システム間の信頼</a> の一部です。</p></td>
</tr>
<tr class="odd">
<td><p>Matthew Fullerton</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>インド工科大学ボンベイ校 (IIT Bombay, India)</p></td>
<td><p>Ashutosh Bajpai</p></td>
<td><p>randomDepart.py、指数分布によって実際の交通パターンを生成する Python スクリプト。</p></td>
</tr>
<tr class="odd">
<td><figure>
<img src="images/Torino_small.gif" title="torino_small.gif" alt="" />
</figure></td>
<td><p>Enrico Gueli</p></td>
<td><p><a href="https://sourceforge.net/projects/traci4j/">TraCI4J</a></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Leontios Papaleontiou</p></td>
<td><p><a href="Contributed/SUMO_Traffic_Modeler.md">Contributed/SUMO Traffic Modeler</a></p></td>
</tr>
<tr class="odd">
<td><figure>
<img src="images/Wroclaw_university_small.jpg" title="Wroclaw_university_small.jpg" alt="" />
</figure></td>
<td><p>Karol Stosiek</p></td>
<td><p>ドキュメント作成、ネットワーク構築</p></td>
</tr>
</tbody>
</table>

その他多くの[貢献者]({{Source}}AUTHORS)。
