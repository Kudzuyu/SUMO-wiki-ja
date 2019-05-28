# チュートリアル

[原文ページ](https://sumo.dlr.de/wiki/Tutorials)

!!! note "注"
    チュートリアルでは一般的でないコンピュータスキルを持っていることを仮定しています。
    なにか疑問が生じた場合は、[]()を参照してください。
    
## 初心者向けチュートリアル

- [OSMWebWizard]() - osmWebWizard.pyを用いて、ほんの数クリックで最初のシナリオを設定しましょう。
- [クイックスタート]() - NETEDITを用いたより複雑なチュートリアル。SUMOの最初のステップです。
- [SUMOオリンピック]() - neteditで特別な車線と単純な信号を作ります。
- [アウトバーン]() - 高速道路を構築し、混成高速道路交通流を作成、自動車の速度の可視化、可視化設定の保存
- [マンハッタン]() - [マンハッタン交通モデル]()を構築します。
- [シミュレーション出力の評価]() - Pythonを使ってシミュレーション結果を評価します。

## 高度なチュートリアル

- [こんにちは、SUMO]() - 最も単純なネットワークと一台の車を「手作業で」セットアップします
- [シナリオガイド]() - シミュレーションのシナリオ構築のための段階ごとの高レベルなアウトラインです
- [高速道路検知器]() - インダクションループデータから高速道路のシナリオを作成します
- [交通流ダイアグラム]() - SUMOで交通流ダイアグラムを計算します
- [OpenStreetMapのPT]() - [OpenStreetMap]http://www.openstreetmap.org/)から、実行可能な公共交通を構築します

## TraCIチュートリアル

これらのチュートリアルは[Python-TraCIライブラリ]()を使ってSUMOシミュレーションとpythonスクリプトを接続します。

- [交通信号のためのTraci]() SUMOと外部プログラムを接続する例としてTraciを使った交通信号制御を取り上げます。
- [Traciによる歩行者の横断]() - TraCIを使った歩行者によって交通信号を動かす例です。

## その他

### Curso de Simulação em Mobilidade

Ednardo Ferreiraによるポルトガル語の[Udemyチュートリアル](https://www.udemy.com/ferramenta-de-microssimulacao-de-trafego-sumo/learn/v4/overview)です。

### SUMOユーザーカンファレンス

- [SUMO2015](http://sumo.dlr.de/daily/sumo2015_tutorial.zip)
- [SUMO2016](http://sumo.dlr.de/daily/sumo2016_tutorial.zip), [New Features 2016 (スライド)](http://sumo.dlr.de/daily/SUMO2016_new_features.pdf)
- [SUMO2017](http://sumo.dlr.de/daily/sumo2017_tutorial.zip)
- [SUMO2018](http://sumo.dlr.de/daily/sumo2018_tutorial.zip)
- [SUMO2019](http://sumo.dlr.de/daily/sumo2019_tutorial.zip)

### ITSC 2015

チュートリアルの準備:

- python2.7をインストール [https://www.python.org/ftp/python/2.7.7/python-2.7.7.msi](https://www.python.org/ftp/python/2.7.7/python-2.7.7.msi) 
- シンタックスハイライト付きテキストエディタのインストール (例: [http://download.tuxfamily.org/notepadplus/archive/6.7.5/npp.6.7.5.Installer.exe])
- [http://sumo.dlr.de/daily/sumo-msvc10Win32-svn.zip](http://sumo.dlr.de/daily/sumo-msvc10Win32-svn.zip)をダウンロードし、**半角空白(' ')を含まないディレクトリ**に展開する。
0.24.0は[NETEDIT]()を含んでいないので、最新の開発版を使います。
- [http://sumo.dlr.de/daily/ITSC2015_tutorial.zip](http://sumo.dlr.de/daily/ITSC2015_tutorial.zip)からチュートリアルファイルをダウンロード

### インポートとエクスポート

- [ファイル生成のトレース]() - 乗り物に関するトレースファイルを取得する方法を示します。
乗り物同士のコミュニケーションに有用です。

### 照準補正

[サンパブロダム]() - NEARCTISサマースクールで用いられた、観測地点を車が通過する時間を用いた自動車の追従パラメータの補正

## もっと進んだ例

### テストスイートから例題を使う

SUMOは大量のテスト群を備えています。
それらは環境のテストとして走らせるように設定されていますが、抽出して[SUMO]()とパッケージの他のツールとともに使うことも可能です。

テストをダウンロードして抽出している場合、そのフォルダにアクセスして、"extractTest.py"を起動してくださいまる 
例えば、リルーターを使う例は以下のようにして動かせます。

```
<SUMO>/tools/extractTest.py -o d:\tmp\test \
 sumo\extended\rerouter\use_routing_device
```

を実行すると[自動車の経路再設定]()の例を展開します。

## 未完成のチュートリアル

以下のチュートリアルは完成していません。

- [出力のパース]() - リルーターを使った円環道路の運転とシミュレーション出力の解析を含む複雑なチュートリアルです。

## 過去のチュートリアル

ここに示したチュートリアルは完全性を保っていますが、他のチュートリアル/ドキュメントにとってかわりました。

- [OpenStreetMapからのインポート]() - 交通シミュレーションのために[OpenStreetMap]()から地図を準備する方法を示しています。
- [クイックスタート(旧式)]() - [NETEDIT]()のかわりにテキストエディタを用いてエッジ/ノードファイルを編集しシナリオを構築します。
- [シティモービル(CityMobil)]() - 自動生成されるバスを用いて停車場のシミュレーションをします。
このチュートリアルは歩行者と駐車エリアの実装前に書かれました。