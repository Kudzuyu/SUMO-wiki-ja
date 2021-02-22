# SUMO早分かり

[原文ページ](https://sumo.dlr.de/wiki/Sumo_at_a_Glance)

## SUMOについて

"**S**imulation of **U**rban **MO**bility" または"SUMO"は、オープンソースで微視的かつマルチモーダルな道路交通シミュレーションです。
SUMOは与えられた道路ネットワークにおいて車一台ごとの動きから構成された交通流がどのようなものかシミュレーションすることができます。
シミュレーションでは交通整理に関する広範なトピックを扱うことができます。
SUMOは純粋に微視的です。
自動車は一台ごとに陽にモデル化され、自身の経路を持ち個別にネットワーク内を移動していきます。
シミュレーションは標準で決定的ですが、[ランダム性導入]()のための様々なオプションがあります。

SUMOパッケージをダウンロードしたら、SUMOの他のアプリケーションも含まれていることに注意してください。
これらのアプリケーションはSUMOで使う道路ネットワークや交通需要のデータをインポート/準備するのに使われます。
詳細は[#含まれるアプリケーション](#含まれるアプリケーション)を参照してください。

## 特徴

* 交通シミュレーションを構築し実行するのに必要な全てのアプリケーションが含まれています(ネットワークと経路のインポート、DUA、シミュレーション)
* シミュレーション
    - 連続空間かつ離散時間での車の動き
    - 複数の自動車の種類
    - 車線変更のある複数車線道路
    - 異なった右側通行ルールや信号
    - 高速なopenGL GUI
    - 数万単位の枝(道路)を含むネットワークの制御
    - 高速起動(1GHzマシンにおいて10万台までの車を1秒以内に更新)
    - 起動中の他のアプリケーションとの相互利用性
    - ネットワーク範囲での道路、車、検知器基準の出力\
    - 人基準のマルチモーダル移動のサポート
* ネットワークインポート
    - VISUM, Vissm, Shapefiles, OSM, RoboCup, MATsim, OpenDRIVE, XML-Descriptionsのインポート
    - ヒューリスティクスによる欠損値の決定
* ルーティング
    - 微視的経路 - 車一台ごとの経路設定
    - 様々な動的ユーザー割り当て
* 高い可搬性
    - C++の標準とポータブルなライブラリのみを使用
    - Windowsと主要なLinuxディストリビューション用のパッケージ
* XMLデータのみを扱うことによる高い相互運用性
* オープンソース([EPL](https://eclipse.org/legal/epl-v20.html))

## 使用例

2001年からSUMOは国家的、国際的な研究[プロジェクト]() で使われてきました。
アプリケーションには以下に示すものが含まれています。

* 交通信号評価
* 経路選択と再選択
* 交通監視手法の評価
* [車間通信シミュレーション(英語)](https://sumo.dlr.de/wiki/Topics/V2X)
* 交通予測

## 含まれるアプリケーション

パッケージには以下のアプリケーションが含まれています。

名前|説明
---|---
SUMO|可視化のない微視的シミュレーション(コマンドラインアプリケーション)
SUMO-GUI|可視化のある微視的シミュレーション
NETCONVERT|ネットワークインポート/生成器: 異なるフォーマットから道路ネットワークを読みこみ、SUMOフォーマットに変換する
NETEDIT|グラフィカルネットワークエディタ
NETGENERATE|SUMO用の抽象ネットワークを生成する
DUAROUTER|ネットワーク中で最速の経路を計算する
JTRROUTER|交差点での右左折の確率を元にした経路計算
DFROUTER|検知器基準の経路計算
MAROUTER|微視的割り当ての実行
OD2TRIPS|O/D行列を単一の車の移動に分解
POLYCONVERT|"points of interest"とそのポリゴンをインポートし、[SUMO-GUI]()での可視化用に変換
ACTIVITYGEN|モデル化された人口の交通利用希望から需要を生成
EMISSIONSMAP|排気ガスマップの作成
EMISSIONSDRIVINGCYCLE|与えられた走行サイクルでの排気ガス量の計算
Additional Tools|大きなアプリケーションを作る必要のないタスクがいくつかあります。そうした問題に関するいくつかの解法がこれらのツールでカバーされています。

いくつかのグループが彼らの仕事の一環としてSUMOパッケージを拡張しコードを申請しています。
これらのリリースの一部ではない場合、こうした貢献はしばしばあまりテストされておらず、古くなっているでしょう。
以下の貢献が含まれます。

## 歴史

SUMOの開発は2000年にスタートしました。
オープンソースの微視的道路交通シミュレーションを開発した主な理由は、交通研究コミュニティを自分たちのアルゴリズムを実装して評価できる道具でサポートするためです。
ツールは道路ネットワークや交通需要、交通制御の実装を追加で必要とせず、それだけで完全な交通シミュレーションが可能です。
こうしたツールを提供することで、DLRは (i)共通する基盤とモデルベースを用いて、実装されたアルゴリズムが比較しやすいように (ii)ほかのコントリビュータへの追加的な助けられる という二つがなされることを願っています。

## ソフトウェアデザイン原則

二つの主なデザインゴールが目標でした: ソフトウェアは高速でかつポータブルである。
この目的のため、最初期のソフトはコマンドラインからのみ動くように開発されていました。グラフィカルインターフェースはなく、全てのパラメータは手作業で設定する必要がありました。

また、これらのゴールのためにソフトウェアはいくつかの部分に分割されました。
それぞれの部分に明確な目的があり、独立に実行できなければなりません。
このことはSUMOを他のシミュレーションパッケージと異なったものにしており、例えば動的ユーザー割り当ては外部のアプリケーションではなくSUMO自身によって行なわれています。
分割によってパッケージ内の個々のアプリケーションが全てを行なうモノリシックなアプリケーションに比べて小さくなったことにより拡張が簡単になりました。



## 関係者

<table>
<thead>
<tr class="header">
<th><p>組織</p></th>
<th><p>氏名</p></th>
<th><p>項目/貢献</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><figure>
<img src="../images/Zaik_small.gif" alt="Zaik_small.gif" />
</figure></td>
<td><p>Christian Rössel</p></td>
<td><p>初期の微視的シミュレーションのコア、初期の検知器の実装</p></td>
</tr>
<tr class="even">
<td rowspan="11"><figure>
<img src="../images/Dlr_small.gif" title="dlr_small.gif" alt="" />
</figure></td>
<td><p>Peter Wagner</p></td>
<td><p>モデル、組織、精神的リーダー</p></td>
</tr>
<tr class="odd">
<td><p>Daniel Krajzewicz</p></td>
<td><p>全般</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Julia Ringel</p></td>
<td><p>交通信号信号 &amp; WAUT のアルゴリズム</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Eric Nicolay</p></td>
<td><p>全般</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Michael Behrisch</p></td>
<td><p>全般</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Yun-Pang Wang</p></td>
<td><p>ユーザー割り当て</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Danilot Teta Boyom</p></td>
<td><p>車両通信モデル (ソースからは削除済み)</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Sascha Krieg</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Lena Kalleske</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Laura Bieker</p></td>
<td><p>テスト、Pythonスクリプト</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Jakob Erdmann</p></td>
<td><p>ネットワークインポート、<a href="netedit.html" title="wikilink">netedit</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Andreas Gaubatz</p></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><p>Maik Drozdzynski</p></td>
<td></td>
</tr>
<tr class="odd">
<td rowspan="3"><p>Uni Lübeck</p></td>
<td><p>Axel Wegener</p></td>
<td><p>TraCI初期化器</p></td>
</tr>
<tr class="even">
<td><p>Thimor Bohn</p></td>
<td><p>TraCI</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Friedemann Wesner</p></td>
<td><p>TraCI</p></td>
<td></td>
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
<td rowspan="4"><p><img src="../images/Uni_erlangen.png" title="fig:uni_erlangen.png" width="149" alt="uni_erlangen.png" /><br />
<br />
<img src="../images/Uibk-small.png" title="fig:uibk-small.png" width="64" alt="uibk-small.png" /><br />
<br />
<img src="../images/Logo_cmu.png" title="fig:logo_cmu.png" width="100" alt="logo_cmu.png" /><br />
<br />
<img src="../images/Logo_ucla.png" title="fig:logo_ucla.png" width="100" alt="logo_ucla.png" /></p></td>
<td><p>Christoph Sommer</p></td>
<td><p><a href="http://veins.car2x.org/">Veins</a>とのTraCIマージ, Subscriptionインターフェース、その他</p></td>
</tr>
<tr class="odd">
<td><p>David Eckhoff</p></td>
<td><p>TraCI、決定的シミュレーションの振舞い</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Falko Dressler</p></td>
<td><p>TraCI</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Tobias Mayer</p></td>
<td><p>交通モデル抽象化, IDM model port</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>HU Berlin</p></td>
<td><p>Matthias Heppner</p></td>
<td><p>ユニットテスト</p></td>
</tr>
<tr class="odd">
<td rowspan="3"><figure>
<img src="../images/Tum-logo.png" title="tum-logo.png" alt="" />
</figure></td>
<td><p>Piotr Woznica</p></td>
<td><p><a href="activitygen.html" title="wikilink">activitygen</a></p></td>
</tr>
<tr class="even">
<td><p>Walter Bamberger</p></td>
<td><p>Development of <a href="activitygen.html" title="wikilink">activitygen</a> as a base for the evaluation of trust scenarios in VANETs. The work is part of the project <a href="http://www.ldv.ei.tum.de/fidens/">Fidens: Trust between Cooperative Systems</a> featuring trusted probabilistic knowledge processing in vehicular networks.</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Matthew Fullerton</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>IIT Bombay, India</p></td>
<td><p>Ashutosh Bajpai</p></td>
<td><p>randomDepart.py, a python script to generate the real traffic pattern by exponential Distribution.</p></td>
</tr>
<tr class="odd">
<td><figure>
<img src="../images/Torino_small.gif" title="torino_small.gif" alt="" />
</figure></td>
<td><p>Enrico Gueli</p></td>
<td><p><a href="http://sourceforge.net/projects/traci4j/">TraCI4J</a></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Leontios Papaleontiou</p></td>
<td><p><a href="Contributed/SUMO_Traffic_Modeler.html" title="wikilink">Contributed/SUMO Traffic Modeler</a></p></td>
</tr>
<tr class="odd">
<td><figure>
<img src="../images/Wroclaw_university_small.jpg" title="Wroclaw_university_small.jpg" alt="" />
</figure></td>
<td><p>Karol Stosiek</p></td>
<td><p>ドキュメント、ネットワーク生成</p></td>
</tr>
</tbody>
</table>
