# ダウンロード

## SUMO 最新版リリース(Version 1.8.0)

**リリース日: 2020/2/12**

## Windowsバイナリ

32bit/64bitのバイナリ、必要な全てのdll、使用例、ツール、HTML形式のドキュメントが含まれます。
特に"extra"ビルドのコンテンツとライセンスに関しては、[ノートの下部](#ライセンスについて)を参照してください。

* 64bit インストーラ [sum-win64-1.8.0.msi](https://sumo.dlr.de/releases/1.8.0/sumo-win64-1.8.0.msi)
* 64bit zip[sumo-win64-1.8.0.zip](https://sumo.dlr.de/releases/1.8.0/sumo-win64-1.8.0.zip)
* 64bit zip(extra)[sumo-win64extra-1.8.0.zip](https://sumo.dlr.de/releases/1.8.0/sumo-win64extra-1.8.0.zip)
* 32bit インストーラ[sumo-win32.1.8.0.msi](https://sumo.dlr.de/releases/1.8.0/sumo-win32-1.8.0.msi)
* 32bit zip[sumo-win32-1.8.0.zip](https://sumo.dlr.de/releases/1.8.0/sumo-win32-1.8.0.zip)

## SUMO-Game

* Windowsバイナリ [sumo-game-1.8.0.zip](https://sumo.dlr.de/releases/1.8.0/sumo-game-1.8.0.zip)

## ソースコード

ソースコード、使用例、Visual StudioやLinux Makefile作成用のCMakeファイルを含みます。
テストは含みません。

* [sumo-src-1.8.0.tar.gz](https://sumo.dlr.de/releases/1.8.0/sumo-src-1.8.0.tar.gz)
* [sumo-src-1.8.0.zip](https://sumo.dlr.de/releases/1.8.0/sumo-src-1.8.0.zip)

## 全部のせtarball

上記に加えて、テストとドキュメントを含み、バイナリを含まないセットです。

* [sumo-all-1.8.0.tar.gz](https://sumo.dlr.de/releases/1.8.0/sumo-all-1.8.0.tar.gz)

## Linuxバイナリ

コミュニティは特に[open buildサービス](https://build.opensuse.org/project/show/home:behrisch)でいくつかのリポジトリを管理しています。
詳細なリストは下記を参照してください。

更に、debianとubuntuとlaunchpadプロジェクトとarchlinuxパッケージもあります。

* [https://salsa.debian.org/science-team/sumo.git](https://salsa.debian.org/science-team/sumo.git)
* [https://launchpad.net/~sumo](https://launchpad.net/~sumo)
* [https://aur.archlinux.org/packages/sumo/](https://aur.archlinux.org/packages/sumo/)

最新のsumoをubuntuに入れる場合、以下のようにしてください。

```
sudo add-apt-repository ppa:sumo/stable
sumo apt update
sumo apt install sumo sumo-tools sumo-doc
```

### リポジトリ

リポジトリにライブラリが含まれない場合(projやgdal)、ディストリビューションの一部として提供れているか、他のリポジトリが必要になります(buildサービスリポジトリの一つを試す必要があります。例えば[アプリケーション:Geo](https://download.opensuse.org/repositories/Application:/Geo/))
今のところ、パッケージにはドキュメントが含まれていません。
リポジトリにはnightlyビルドも含まれます(sumo_nightly)。

* [openSUSE Leap 42.2](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Leap_42.2/)
* [openSUSE Leap 42.3](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Leap_42.3/)
* [openSUSE Leap 15.0](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Leap_15.0/)
* [openSUSE Leap 15.1](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Leap_15.1/)
* [openSUSE Leap 15.2](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Leap_15.2/)
* [openSUSE Tumbleweed](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Tumbleweed/)
* [Fedra 29](http://download.opensuse.org/repositories/home:/behrisch/Fedora_29/)
* [Fedra 30](http://download.opensuse.org/repositories/home:/behrisch/Fedora_30/)
* [Fedra 31](http://download.opensuse.org/repositories/home:/behrisch/Fedora_31/)
* [Fedra 32](http://download.opensuse.org/repositories/home:/behrisch/Fedora_32/)
* [Fedra Rawhide](http://download.opensuse.org/repositories/home:/behrisch/Fedora_Rawhide/)
* [CentOS 7](http://download.opensuse.org/repositories/home:/behrisch/CentOS_7/)
* [CentOS 8](http://download.opensuse.org/repositories/home:/behrisch/CentOS_8/)


Ubuntu、 Debian、 Archのユーザーは、上記のコミュニティリポジトリを参照してください。

## macOS

[Homebrewを用いたインストールガイド]()か、[ビルド手順]()を参照してください。

"Bottles"は[Homebrew]をインストールするために使えます。
最新の2つのメジャーバージョン用にビルドされており(現在はMojaveとCatalina)、ソースから最小限の要件(fox、proj、xerces-c)でビルドされています。
オプションのライブラリが必要ならば、それらをbrewで指定すれば、brewがSUMOをソースからコンパイルします。
詳しくは、[Formula's README](https://github.com/DLR-TS/homebrew-sumo/blob/master/README.md)を参照してください。

### アプリランチャー

macOSでより自然に扱うために、アプリランチャーも提供されています(アイコンとショートカット)。
ランチャーは**全てのバージョンのSUMOで動き、アップデートの必要はありません**。

* [SUMOランチャーダウンロード](https://sumo.dlr.de/daily/SUMO_launchers.dmg)

## Pythonパッケージ

SUMO1.8.0から、pip([Python packaging index](https://pypi.org/project/eclipse-sumo/))を用いたインストールも可能になりました。
`pip install eclipse-sumo`でアプリケーションをインストールするか、`pip install libsumo`のようにして、traci、libsumo、sumolibのどれかだけを入れることができます。
この方法は2014年以降のWindowsとLinuxで動作しますが、現在のところmacOSでは動作しません。
アプリケーションはPython 2とPython 3の両方で動作し、libsumoはPython 3.5以上でのみ動作します。

## パッケージ

SUMOは複数のパッケージとして提供されています。
以下の表にそれぞれのコンテンツを示します。

||bin|build|ソースコード|ユーザードキュメント|開発者ドキュメント(doxygen)|データ|例|チュートリアル|テスト|ツール(jarを除く)|jar|
|-|-|-|-|-|-|-|-|-|-|-|-|
|sumo-src-XXX.tar.gz sumo-src-XXX.zip||✔|✔|||✔|✔|✔||✔||
|sumo-win??-XXX.zip sumo-win??-XXX.msi|✔|||✔||✔|✔|✔||✔|✔|
|sumo-all-XXX.tar.gz sumo-all-XXX.zip||✔|✔|✔||✔|✔|✔|✔|✔|✔|
|rpm|(✔)|||✔||✔|✔|✔||✔||

## 依存関係(開発者向け)

Windows向けにVisual Studioで開発する場合、[このリポジトリ](https://github.com/DLR-TS/SUMOLibraries)をcloneすることで全ての依存関係を見つけることができます。SUMOを実行することだけが目的の場合は、上に挙げた依存ランタイムの含まれたバイナリーをダウンロードしてください。


## シナリオと他のデータ

* [完全シナリオ]()
* [ネットワーク]()
* [交通量データ]()

## ライセンスについて

SUMOはオープンソースライブラリのみを使い、GPL v2以降を二次ライセンスオプションとする[EPL-2.0](https://www.eclipse.org/legal/epl-v20.html)でライセンスされています。

基本ビルドはEclipseの認めたライセンス(特にGPLとLGPLでないコード)のコードとwindowsバイナリのみを含んでいます。shapeファイルのインポートやOpenSceneGraph 3D GUIのような機能を使いたい場合は、"extra"ビルトをダウンロードしてください。
