# ダウンロード

[原文ページ](https://sumo.dlr.de/wiki/Basics/Notation)

参考原文バージョン: 2022.3.30(c60e6e70bb3dfa2bf77ff4a4ebd8886d959b41c2)

## SUMO 最新リリース(Version {{ Version }})

**リリース日: {{ReleaseDate}}**

## Windows

64bitのバイナリ、必要な全てのdll、使用例、ツール、HTML形式のドキュメントが含まれます。
コンテンツとライセンスの説明(特に、GeoTiff、shapefileと3DモデルのGPLコードを含む"extra"ビルドについて)に関しては、[ノートの下部](#ライセンスについて)を参照してください。

* 64bit インストーラ [sum-win64-{{Version}}.msi](https://sumo.dlr.de/releases/{{Version}}/sumo-win64-{{Version}}.msi)
* 64bit zip[sumo-win64-{{Version}}.zip](https://sumo.dlr.de/releases/{{Version}}/sumo-win64-{{Version}}.zip)
* 64bit extra付きインストーラ (GPUコードを含む)[sumo-win64extra-{{Version}}.msi](https://sumo.dlr.de/releases/{{Version}}/sumo-win64extra-{{Version}}.msi)
* 64bit extra付きzip (GPUコードを含む)[sumo-win64extra-{{Version}}.zip](https://sumo.dlr.de/releases/{{Version}}/sumo-win64extra-{{Version}}.zip)

## SUMO-Game

* Windowsバイナリ [sumo-game-{{Version}}.zip](https://sumo.dlr.de/releases/{{Version}}/sumo-game-{{Version}}.zip)

## Linuxバイナリ

コミュニティは特に[open buildサービス](https://build.opensuse.org/project/show/home:behrisch)でいくつかのリポジトリを管理しています。
詳細なリストは下記を参照してください。

更に、debianとubuntuとlaunchpadプロジェクトとarchlinuxパッケージもあります。

* [https://salsa.debian.org/science-team/sumo.git](https://salsa.debian.org/science-team/sumo.git)
* [https://launchpad.net/~sumo](https://launchpad.net/~sumo)
* [https://aur.archlinux.org/packages/sumo/](https://aur.archlinux.org/packages/sumo/)

また、SUMOの[flatpak](https://flathub.org/apps/details/org.eclipse.sumo)もあります。

最新のsumoをubuntuに入れる場合、以下のようにしてください。

```
sudo add-apt-repository ppa:sumo/stable
sumo apt update
sumo apt install sumo sumo-tools sumo-doc
```

### リポジトリ

リポジトリにライブラリ(projやgdalなど)が含まれない場合、ディストリビューションの一部として提供れているか、他のリポジトリが必要になります(buildサービスリポジトリの一つを試す必要があります。例えば[アプリケーション:Geo](https://download.opensuse.org/repositories/Application:/Geo/))
今のところ、パッケージにはドキュメントが含まれていません。
リポジトリにはnightlyビルドも含まれます(***sumo-git***)。

* [openSUSE Leap 42.3](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Leap_42.3/)
* [openSUSE Leap 15.0](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Leap_15.0/)
* [openSUSE Leap 15.1](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Leap_15.1/)
* [openSUSE Leap 15.2](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Leap_15.2/)
* [openSUSE Leap 15.3](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Leap_15.3/)
* [openSUSE Leap 15.4](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Leap_15.4/)
* [openSUSE Tumbleweed](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Tumbleweed/)
* [Fedra 30](http://download.opensuse.org/repositories/home:/behrisch/Fedora_30/)
* [Fedra 31](http://download.opensuse.org/repositories/home:/behrisch/Fedora_31/)
* [Fedra 32](http://download.opensuse.org/repositories/home:/behrisch/Fedora_32/)
* [Fedra 33](http://download.opensuse.org/repositories/home:/behrisch/Fedora_33/)
* [Fedra 34](http://download.opensuse.org/repositories/home:/behrisch/Fedora_34/)
* [Fedra 35](http://download.opensuse.org/repositories/home:/behrisch/Fedora_35/)
* [Fedra Rawhide](http://download.opensuse.org/repositories/home:/behrisch/Fedora_Rawhide/)
* [CentOS 7](http://download.opensuse.org/repositories/home:/behrisch/CentOS_7/)
* [CentOS 8](http://download.opensuse.org/repositories/home:/behrisch/CentOS_8/)


リポジトリの追加とインストール（GPGキーのチェックをしない、手っ取り早い方法！）は、CentOS 7のyumの場合、以下のようになります。

```
yum-config-manager --add-repo=https://download.opensuse.org/repositories/science:/dlr/CentOS_7/
yum install -y --nogpgcheck epel-release
yum install -y --nogpgcheck sumo-{{Version}}.
```

また、openSUSE Leap 15.3のzypperでは以下のようになります。
```
zypper ar http://download.opensuse.org/repositories/science:/dlr/15.3/ science:dlr
sumo={{Version}} で zypper を実行します。
```
バージョン番号を省略すると、最新のNightly Buildがインストールされます。
Ubuntu、 Debian、 Archのユーザーは、上記のコミュニティリポジトリを参照してください。

## MacOS

[Homebrewを用いたインストールガイド](Installing/index.md#MacOS)か、[ビルド手順](Installing/MacOS_Build.md)を参照してください。

"Bottles"は[Homebrew]をインストールするために使えます。
最新の2つのメジャーバージョン用にビルドされており(現在はMojaveとCatalina)、ソースから最小限の要件(fox、proj、xerces-c)でビルドされています。
オプションのライブラリが必要ならば、それらをbrewで指定すれば、brewがSUMOをソースからコンパイルします。
詳しくは、[Formula's README](https://github.com/DLR-TS/homebrew-sumo/blob/master/README.md)を参照してください。

### アプリランチャー

MacOSでより自然に扱うために、アプリランチャーも提供されています(アイコンとショートカット)。
ランチャーは**全てのバージョンのSUMOで動き、アップデートの必要はありません**。

* [SUMOランチャーダウンロード](https://sumo.dlr.de/daily/SUMO_launchers.dmg)

これらのランチャーは、MacOS上で`.sumocfg`ファイルを開くためのデフォルトアプリケーションとして**sumo-gui**を選択し、さらに**sumo-gui**、**netedit**、**OSM Web Wizard**をDockに追加できるようにするものです。

!!! warning "重要なお知らせ"
    ランチャーを使用するためには、事前にSUMOをインストールし、[SUMO_HOME](Basics/Basic_Computer_Skills.md#sumo_home) 環境変数を設定していることを確認する必要があります(バージョンは問いません)。

## ソースコード

以下のリンクから、ソースコード、使用例、Visual StudioやLinux Makefile作成用のCMakeファイルをダウンロードできます。
このファイルはテストを含みません。

* [sumo-src-{{Version}}.tar.gz](https://sumo.dlr.de/releases/{{Version}}/sumo-src-{{Version}}.tar.gz)
* [sumo-src-{{Version}}.zip](https://sumo.dlr.de/releases/{{Version}}/sumo-src-{{Version}}.zip)

## Pythonパッケージ/仮想環境

SUMO 1.8.0から(MacOSは1.12.0から)、pip([Python packaging index](https://pypi.org/project/eclipse-sumo/))を用いたインストールも可能になりました。
`pip install eclipse-sumo`でアプリケーションをインストールするか、traciのみ(`pip install traci`)、libsumoのみ(`pip install libsumo`)、sumolibのみ(`pip install sumolib`)のインストールも可能です。

この方法は2014年以降のWindows、MacOSおよび全てのLinuxで動作します。
アプリケーションはPython 2とPython 3の両方で動作し、libsumoはPython 3.6以上でのみ動作します。
これにより、最新のSUMOを[仮想環境](https://docs.python.org/3/library/venv.html) またはNightly Buildを使って以下のコマンド (Linuxの場合)簡単にテストできます。

```
python -m venv sumo_test
cd sumo_test
.bin/activate
pip install eclipse-sumo
```
!!! warning "MacOSの依存関係"
    MacOSでPython wheel を使うには、一度[標準インストール](Installing/index.md#macos)に従って、例えばbrew経由ですべての依存関係をインストールし最新版にしておく必要があります。

# SUMO - 最新開発版

SUMOは現在活発に開発されています。継続的に更新されるバグ修正と機能強化のリストがあります。
バグフィックスと機能強化のリストは、[ChangeLog](ChangeLog.md)をご覧ください。

最新の機能を利用するために
(およびリリース前のフィードバック)](Contact.md) を参照してください。
私たちの [コードリポジトリ](https://github.com/eclipse/sumo/) から最新版を使用することをお勧めします。

メインブランチにプッシュするたびに、Windows、Linux、macOS用のビルドが開始されます。
その結果は、[関連するコミットはこちら](https://github.com/eclipse/sumo/actions) をクリックし、あなたのプラットフォームに適したファイルをダウンロードすることで確認できます。
をクリックし、お使いのプラットフォームに適したファイルをダウンロードしてください (GitHub にサインインする必要がある場合があります)。

## Nightly Snapshot

<div><span class="badge badge-pill badge-dark"><?php getNightlyFreshness("sumo-win64-git.zip");?></span></div><span class="badge badge-pill badge-dark"><?php getNightlyFreshness("sumo-win64-git.zip");?

リポジトリ内のコードは、[毎晩コンパイルされます](Developer/Nightly_Build.md)。
Windows のビルドはすべて 64bit プラットフォーム用です。
内容やライセンスの説明については
ライセンス（特にGeoTIFF、シェイプファイル、3DモデルをサポートするGPLコードを含む「追加」ビルドに関して）。
以下のノート](Downloads.md#note_on_licensing)を参照してください。以下のパッケージが入手可能です。


* [ソース (zip)](https://sumo.dlr.de/daily/sumo-src-git.tar.gz)
* [ソース (tar.gz)](https://sumo.dlr.de/daily/sumo-src-git.zip)
* [ソースと静的なHTMLドキュメント (tar.gz)](https://sumo.dlr.de/daily/sumo_git.orig.tar.gz)
* [Windowsインストーラー(msi)](https://sumo.dlr.de/daily/sumo-win64-git.msi)
* [Windows zip](https://sumo.dlr.de/daily/sumo-win64-git.zip)
* [全てのエクストラファイル(GPL コードを含む)を含む Windows インストーラー (msi)](https://sumo.dlr.de/daily/sumo-win64extra-git.msi)
* [全てのエクストラファイル(GPL コードを含む)を含む Windows zip (msi)](https://sumo.dlr.de/daily/sumo-win64extra-git.zip)

* [SUMO GameのWindows 64bitバイナリ](https://sumo.dlr.de/daily/sumo-game-win64-git.zip)
* [Windows 64bit デバッグ版](https://sumo.dlr.de/daily/sumo-win64Debug-git.zip)

ナイトリービルドは [Python packaging index test instance](https://test.pypi.org/project/eclipse-sumo/) からも入手可能です。
最新のナイトリーバージョン(仮想環境で行うことを強く推奨します)をインストールするには、[上記の説明](#pythonパッケージ仮想環境)のインストール行を以下のように置き換えてください。
```
pip install -i https://test.pypi.org/simple/ eclipse-sumo
```
これはpythonパッケージですが、コンパイルされたSUMOバイナリがすべて含まれており、完全に機能するはずです([上記のセクション](#pythonパッケージ仮想環境)の要件を参照してください)。

オープン・ビルド・サービスのLinux [リポジトリ](#リポジトリ)には、ナイトリービルドも含まれています。
残念ながら Debian, Ubuntu, Arch のバージョンにはありません。

[対応するドキュメント](https://sumo.dlr.de/daily/userdoc)は[Doxygen](https://sumo.dlr.de/daily/doxygen)でもライブで見ることができます。
また、[テスト結果](https://sumo.dlr.de/daily) や [コードカバレッジ解析](https://sumo.dlr.de/daily) などの成果物も毎晩生成されます。

!!! caution "注意"
    Windows 用のバイナリパッケージは、1 日に 1 回（ベルリン時間の深夜）だけコンパイルされるため、[最新の Git リビジョン](https://github.com/eclipse/sumo/commits/main) から遅れることがあります。

# 過去のリリースと代替ダウンロード

[リリースディレクトリ](https://sumo.dlr.de/releases/) には、1.2.0 以降のすべてのリリースファイルが含まれています。
これらの古いリリースは、[sourceforge download portal](https://sourceforge.net/projects/sumo/files/sumo/) からも入手可能です。
古いバージョンを試したい場合、仮想環境を使うこともでき、 ([上記の説明](#python_packages_virtual_environments))を固定バージョンで使用することもできます(例: ` pip install eclipse-sumo=1.9.0` (1.8.0以降で動作))。

もし、古いバージョンのリポジトリの完全なzip(テストを含む)が必要なら、ローカルリポジトリのタグをご覧ください(https://github.com/eclipse/sumo/tags)。

# その他

## リポジトリへの直接アクセス

最新のソースを Git リポジトリから直接取得することができます。
[リポジトリへのアクセスに関する FAQ](FAQ.md#how_do_i_access_the_code_repository) をご覧ください。
通常、これらのソースはコンパイルされ、私たちのテストスイートを正常に完了するはずです。
ビルドの現在の状態を評価するために、次のページを見てください。
[夜間テストの統計](https://sumo.dlr.de/daily/) を見てください。

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
