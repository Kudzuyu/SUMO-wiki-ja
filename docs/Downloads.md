# ダウンロード

## SUMO - 最新リリース (バージョン {{Version}})

**リリース日:** {{ReleaseDate}}

### Windows

バイナリ（64ビット）、必要なすべてのDLL、サンプル、ツール、HTML形式のドキュメントが含まれます。
内容とライセンスの説明（特にGeoTIFF、シェープファイル、3DモデルをサポートするGPLコードを含む「追加」ビルドに関するもの）については、[下記の注記](Downloads.md#note_on_licensing)を参照してください。

<ul>
<li>64ビットインストーラー: <a class="no-arrow-link" href="https://sumo.dlr.de/releases/ {{Version}}/sumo-win64-{{Version}}.msi">sumo-win64-{{Version}}.msi</a></li>
<li>64ビット版zip: <a class="no-arrow-link" href="https://sumo.dlr.de/releases/{ {Version}}/sumo-win64-{{Version}}.zip「>sumo-win64-{{Version}}.zip</a></li>
<li>すべての追加機能を含む64ビットインストーラー（GPLコードを含む）：<a class="no-arrow-link" href="https://sumo.dlr.de/releases/ {{Version}}/sumo-win64extra-{{Version}}.msi">sumo-win64extra-{{Version}}.msi</a></li>
<li>すべての追加機能を含む64ビットZIP（GPLコードを含む）：<a class= "no-arrow-link" href="https://sumo.dlr.de/releases/{{Version}}/sumo-win64extra-{{Version}}.zip">sumo-win64extra-{{Version}}.zip</a></li>
</ul>

SUMOはwinget経由でも利用可能です。
`winget install --name sumo`で最新リリース版（ただし追加機能版ではない）を入手できます。

#### SUMO-Game

<ul><li>Windowsバイナリ: <a class="no-arrow-link" href="https://sumo.dlr.de/releases/ {{Version}}/sumo-game-win64-{{Version}}.zip「>sumo-game-win64-{{Version}}.zip</a><?php getInfo(」sumo-game-win64-{{Version}}.zip「,」r",false);?></li></ul>


### Linux

コミュニティは特に[オープンビルドサービス](https://build.opensuse.org/project/show/science:dlr) で複数のリポジトリを管理しています。
リポジトリの詳細な一覧は以下を参照してください。

LaunchpadリポジトリからUbuntuに最新のsumoを追加するには、以下を実行する必要があります：

```
sudo add-apt-repository ppa:sumo/stable
sudo apt-get update
sudo apt-get install sumo sumo-tools sumo-doc
```

### リポジトリ

ビルドサービスでは、各ディストリビューション向けの[インストール手順](https://software.opensuse.org//download.html?project=science%3Adlr&package=sumo)を提供しています。

リポジトリにライブラリ（projやgdalなど）が含まれていない場合、それらは ディストリビューションの一部であるか、別のリポジトリから入手する必要があります（ こちらのビルドサービスリポジトリも試してみてください。例： [Application:Geo](https://download.opensuse.org/repositories/Application:/Geo/)）。
現時点ではパッケージにドキュメントは含まれていません。
リポジトリには***sumo-git***と呼ばれるナイトリービルドも含まれています。

- [openSUSE Leap 15.2 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/openSUSE_Leap_15.2/)
- [openSUSE Leap 15.3 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/15.3/)
- [openSUSE Leap 15.4 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/15.4/)
- [openSUSE Leap 15.5 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/15.5/)
- [openSUSE Leap 15.6 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/15.6/)
- [openSUSE Tumbleweed リポジトリ](https://download.opensuse.org/repositories/science:/dlr/openSUSE_Tumbleweed/)
- [Fedora 36 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Fedora_36/)
- [Fedora 37 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Fedora_37/)
- [Fedora 38 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Fedora_38/)
- [Fedora 39 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Fedora_39/)
- [Fedora 40 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Fedora_40/)
- [Fedora 41 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Fedora_41/)
- [Fedora 42 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Fedora_42/)
- [Fedora Rawhide リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Fedora_Rawhide/)
- [CentOS 7 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/CentOS_7/)
- [Debian 9 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Debian_9.0/)
- [Debian 10 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Debian_10/)
- [Debian 11 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Debian_11/)
- [Debian 12 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Debian_12/)
- [Debian Testing リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Debian_Testing/)
- [Debian Unstable リポジトリ](https://download.opensuse.org/repositories/science:/dlr/Debian_Unstable/)
- [xUbuntu 16.04 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/xUbuntu_16.04/)
- [xUbuntu 18.04 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/xUbuntu_18.04/)
- [xUbuntu 20.04 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/xUbuntu_20.04/)
- [xUbuntu 22.04 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/xUbuntu_22.04/)
- [xUbuntu 24.04 リポジトリ](https://download.opensuse.org/repositories/science:/dlr/xUbuntu_24.04/)

さらに、Debian および Ubuntu の
Launchpad プロジェクト、ならびに Arch Linux パッケージが存在します:

- <https://salsa.debian.org/science-team/sumo.git>
- <https://launchpad.net/~sumo>
- <https://aur.archlinux.org/packages/sumo/>

SUMO用の[flatpak](https://flathub.org/apps/org.eclipse.sumo)も利用可能です。

#### 例

CentOS 7のyumでリポジトリを追加しインストールする（GPGキーの確認なし）手順は以下の通りです：
```
yum-config-manager --add-repo=https://download.opensuse.org/repositories/science:/dlr/CentOS_7/
yum install -y --nogpgcheck epel-release
yum install -y --nogpgcheck sumo-{{Version}}
```
すべてのビルドサービスリポジトリには最新のナイトリービルドと現行リリースが含まれることにご注意ください。
最新ビルド以外が必要な場合は、必ずバージョンを指定してください。

Ubuntuで利用可能なバージョンを確認するには`apt show sumo -a`を実行してください。

### macOS

macOSでは提供されているパッケージファイルを使用して簡単にインストールできます：

<ul>
<li>pkg インストーラー: <a class="no-arrow-link" href="https://sumo.dlr.de/releases/{{Version}}/sumo-{{Version}}.pkg">sumo-{{Version}}.pkg</a><?php getInfo(「sumo-{{Version}}.pkg」,「r」,false);?></li>
</ul>

MacにPythonとXQuartzがインストールされていることを確認してください。

以下の手順に従ってSUMOをビルドすることも可能です[こちら](Installing/MacOS_Build.md)。


#### Homebrew

Homebrewベースのインストールガイド[こちら](Installing/index.md#macos)を参照するか、[ビルド手順](Installing/MacOS_Build.md)に従ってください。
Homebrewボトルの使用は推奨されません。

!!! caution 重要なお知らせ
    Homebrew経由のインストールは現在メンテナンスされていません。
    古いバージョンのインストールには使用可能ですが、サポートは提供されません。
    インストーラーを使用するか、SUMOを自身でビルドしてください。

***インストーラーを使用した場合、この手順は不要です！***

macOSでよりネイティブな操作感を得るため、アプリケーションランチャー（アイコン／ショートカット）を提供しています。これらのランチャーは***すべてのバージョンのSUMOで動作し、更新の必要はありません***。

<ul>
<li><a class="no-arrow-link" href="https://sumo.dlr.de/daily/SUMO_launchers.dmg">SUMOランチャーをダウンロード</a><?php getInfo("SUMO_launchers.dmg","d",false);?></li>
</ul>

これらのランチャーを使用すると、macOS上で`.sumocfg`ファイルを開くデフォルトアプリケーションとして**sumo-gui**を選択でき、さらに**sumo-gui**、**netedit**、**OSM Web Wizard**をDockに追加できます。

!!! 注意 "重要なお知らせ"
ランチャーを使用するには、事前にSUMO（どのバージョンでも可）をインストールし、[SUMO_HOME](Basics/Basic_Computer_Skills.md#sumo_home)環境変数を設定していることを確認してください。

### ソース

Visual StudioソリューションまたはLinux Makefileを作成するためのソース、サンプル、CMakeファイルをダウンロードします。このダウンロードにはテストは含まれません。ダウンロード形式:

<ul>
<li><a class="no-arrow-link" href="https://sumo.dlr.de/releases/{{Version}}/sumo-src-{{Version}}.tar.gz">sumo-src-{{Version}}.tar.gz</a><?php getInfo(「sumo-src-{{Version}}.tar.gz」,「r」,false);?></li>
<li><a class="no-arrow-link" href="https://sumo.dlr.de/releases/{{Version}}/sumo-src-{{Version}}.zip">sumo-src-{{Version}}.zip</a><?php getInfo(「sumo-src-{{Version}}.zip」,「r」,false);?></li>
</ul>

### Pythonパッケージ / 仮想環境

SUMO 1.8.0以降（macOS版は1.12.0以降）では、[Pythonパッケージインデックス](https://pypi.org/project/eclipse-sumo/)からのインストールも可能です。

アプリケーション全体をインストールする場合: `pip install eclipse-sumo`、または traci のみ (`pip install traci`)、libsumo (`pip install libsumo`)、sumolib (`pip install sumolib`) を個別にインストールできます。

Windows、 
macOS、および2014年より新しいすべてのLinuxバージョンで動作します。
アプリケーションはPython 2とPython 3の両方で利用可能ですが、libsumoはPython 3.6以降専用です。これにより、以下のコマンド（Linux上）を使用して、[仮想環境](https://docs.python.org/3/library/venv.html)やナイトリービルド経由で新しいSUMOバージョンを簡単にテストできます：
```
python -m venv sumo_test
cd sumo_test.
 bin/activate
pip install eclipse-sumo
```

!!! caution "macOS依存関係に関する注意"
macOSでPythonホイールを使用するには、例えば[標準インストール](Installing/index.md#macos)に従い、brew経由ですべての依存関係を一度インストールし最新状態に保つ必要があります。

### 追加ツール
全ての[Pythonツール](Tools/index.md)を最大限活用するには
`pip install -r $SUMO_HOME/tools/requirements.txt`で依存関係をインストールしてください。

## SUMO - 最新開発版

SUMOは活発に開発中です。継続的に更新される
バグ修正と機能強化のリストは
[変更履歴](ChangeLog.md)でご確認いただけます。最新機能を利用し
[(リリース前のフィードバックを提供)](Contact.md)いただくには
[コードリポジトリ](https://github.com/eclipse-sumo/sumo/)から最新版の使用を推奨します。

メインブランチへのプッシュごとに、Windows、Linux、macOS向けのビルドが自動実行されます。
ビルド結果は[該当コミット](https://github.com/eclipse-sumo/sumo/actions)をクリックし、
お使いのプラットフォームに対応するファイルをダウンロードすることで入手可能です（GitHubへのサインインが必要な場合があります）。

### ナイトリースナップショット

<div><span class="badge badge-pill badge-dark"><?php getNightlyFreshness(「sumo-win64-git.zip」);?></span></div>

リポジトリ内のコードは[毎晩コンパイルされます](Developer/Nightly_Build.md)。すべてのWindowsビルドは64ビットプラットフォーム向けです。内容とライセンス（特にGeoTIFF、シェープファイル、3DモデルをサポートするGPLコードを含む「追加」ビルドに関する説明）については、
[下記の注記](Downloads.md#note_on_licensing)を参照してください。
以下のパッケージを入手できます：
 以下のパッケージを入手できます：

<ul>
<li>ソース: <a class="no-arrow-link" href="https://sumo.dlr.de/daily/sumo-src-git.tar.gz">https://sumo.dlr.de/daily/sumo-src-git.tar.gz</a><?php getInfo(「sumo-src-git.tar.gz」,「d」,true) ;?></li>
<li>ソース: <a class="no-arrow-link" href="https://sumo.dlr.de/daily/sumo-src-git.zip">https://sumo.dlr.de/daily/sumo-src-git.zip</a><?php getInfo(「sumo-src-git.zip」,「d」,true);?></li>
<li>ソースと静的HTMLドキュメント: <a class="no-arrow-link" href="https://sumo.dlr.de/daily/sumo_git.orig.tar.gz">https://sumo.dlr.de/daily/sumo_git.orig.tar.gz</a><?php getInfo(「sumo_git.orig.tar.gz」, 「d」,true);?></li>
<li>Windowsインストーラー: <a class="no-arrow-link" href="https://sumo.dlr.de/daily/sumo-win64-git.msi">https://sumo.dlr.de/daily/sumo-win64-git.msi</a><?php getInfo(「sumo-win64-git.msi」,「d」,true);?></li>
<li>Windows zip: <a class="no-arrow-link" href="https://sumo.dlr.de/daily/sumo-win64-git.zip">https://sumo.dlr.de/daily/sumo-win64-git.zip</a><?php getInfo(「sumo-win64-git.zip」,「d」,true);?></li>
<li>すべての追加機能を含む Windows インストーラー (GPL コードを含む): <a class="no-arrow-link" href="https://sumo.dlr.de/daily/sumo-win64extra-git.msi">https://sumo.dlr.de/daily/sumo-win64extra-git.msi</a><?php getInfo(「sumo-win64extra-git.msi」,「d」,true);? ></li>
<li>Windows用zipファイル（すべての追加機能を含む、GPLコードを含む）： <a class="no-arrow-link" href="https://sumo.dlr.de/daily/sumo-win64extra-git.zip">https://sumo.dlr.de/daily/sumo-win64extra-git.zip</a><?php getInfo(「sumo-win64extra-git.zip」," d",true);?></li>
<li>SUMOゲームのWindows 64ビットバイナリ: <a class="no-arrow-link" href="https://sumo.dlr.de/daily/sumo-game-win64-git.zip">https://sumo.dlr.de/daily/sumo-game-win64-git.zip</a><? php getInfo(「sumo-game-win64-git.zip」,「d」,true);?></li>
<li>Windows 64ビット デバッグ版: <a class="no-arrow-link" href="https://sumo.dlr.de/daily/sumo-win64Debug-git.zip">https:// sumo.dlr.de/daily/sumo-win64Debug-git.zip</a><?php getInfo(「sumo-win64Debug-git.zip」,「d」,true);?></li>
<li>macOS pkg インストーラー: <a class="no-arrow-link" href="https://sumo.dlr.de/daily/sumo-git.pkg">sumo-git.pkg</a><?php getInfo(「sumo-git.pkg」,「r」,false);?></li>
</ul>

ナイトリービルドは[Python wheels](https:// sumo.dlr.de/daily/wheels/)としても入手可能です。
最新のナイトリー版をインストールするには（仮想環境での実行を強く推奨します）、[上記の手順](#python_packages_virtual_environments)に従い、インストール行を以下に置き換えてください：
```
pip install -f https://sumo.dlr.de/daily/wheels/ eclipse-sumo
```
これはPythonパッケージですが、コンパイル済みSUMOバイナリを全て含み、完全に機能するはずです（要件については[上記セクション](#python_packages_virtual_environments)を参照）。
libsumo、sumolib、traci用のナイトリーPythonホイールも利用可能です。

Linux向け[リポジトリ](#repositories) (#repositories) にはナイトリービルドも含まれています。

[対応するドキュメント](https://sumo.dlr.de/daily/userdoc) は
ライブで閲覧可能で、[Doxygen
ドキュメント](https://sumo.dlr.de/daily/doxygen) も含まれます。
[テスト結果](https://sumo.dlr.de/daily) や [コードカバレッジ
分析](https://sumo.dlr.de/daily/lcov/html/) などの追加成果物は毎晩生成されます
。

!!! caution "注意"
利用可能な Windows バイナリパッケージは、1日1回 (日本時間朝) のみコンパイルされるため、[最新の Git リビジョン](https://github.com/eclipse-sumo/sumo/commits/main) に遅れる可能性があります。

さらに新しいビルドが必要な場合は、[GitHub Actionsのアーティファクト](https://github.com/eclipse-sumo/sumo/actions)を確認してください。
対象のコミットとプラットフォーム（例：Windowsバイナリの場合は`windows`）をクリックする必要があります。

## 過去のリリースと代替ダウンロード方法

[リリースディレクトリ](https://sumo.dlr.de/releases/)には1.2.0以降の全リリースファイルが格納されています。
これらおよびそれ以前のリリースは[SourceForgeダウンロードポータル](https://sourceforge.net/projects/sumo/files/sumo/)からも入手可能です。
古いバージョンを試したい場合は、仮想環境アプローチ （[上記で説明した方法](#python_packages_virtual_environments)）で固定バージョンを使用することもできます。
例： `pip install eclipse-sumo==1.9.0`（1.8.0以降でのみ動作します）。

リポジトリの完全なzipスナップショット（テストを含む）が必要な場合 が必要な場合は、 ローカルリポジトリ内のタグまたは[GitHubタグ](https://github.com/eclipse-sumo/sumo/tags)を参照してください。

## その他

### リポジトリへの直接アクセス

最新ソースはGitリポジトリから直接取得可能です。
詳細は [リポジトリアクセスに関するFAQ](FAQ.md#how_do_i_access_the_code_repository)を参照してください。
通常、これらはコンパイル可能であり、テストスイートも正常に完了するはずです。
ビルドの現在の状態を評価するには、 [ナイトリーテスト統計](https://sumo.dlr.de/daily/) にアクセスします。

### パッケージ

SUMO はさまざまなパッケージとして入手できます。各パッケージの内容は
以下の表にリストされています。

| | bin | build | src (ソースコード) | ユーザードキュメント | 開発者向けドキュメント (doxygen) | データ | サンプル | チュートリアル | テスト | ツール (jarファイルを除く) | jarファイル |
|---|------|--------|--------------------|------------|---------------------------|-------|-----------|------------|--------|------------ ----------|-------|
| sumo-src-*XXX*.tar.gz<br>sumo-src-*XXX*.zip | | &#10004; | &#10004; | | | &#10004; | &#10004; | &#10004; | | &#10004; | |
| sumo-win??-*XXX*.zip<br>sumo-win??-*XXX*.msi | &#10004; | | | &#10004; | | &#10004; | &#10004; | &#10004; | | &#10004; | &#10004; |
| rpm | (&#10004;) | | | &#10004; | | &#10004; | &#10004; | &#10004; | | &#10004; | |

### 開発者向け依存関係

Windowsプラットフォームでは、Visual Studioで開発する場合、
このリポジトリをクローンすることで全ての依存関係を取得できます: <https://github.com/DLR-TS/SUMOLibraries>。
SUMOを実行するだけなら、上記のバイナリダウンロードを使用してください。これには既にランタイム依存関係が含まれています。

### シナリオとその他のデータ
- [完全なシナリオ](Data/Scenarios.md)
- [ネットワーク](Data/Networks.md)
- [交通データ](Data/Traffic_Data.md)
- [テストケース](Tutorials/index.md#using_examples_from_the_test_suite)

## ライセンスに関する注記

SUMOは
[EPL-2.0](https://www.eclipse.org/legal/epl-2.0/)の下でライセンス供与されており、GPL v2以降を二次ライセンスオプションとして使用します（ただし、[オープンソースライブラリ](Libraries_Licenses.md)のみを対象とします）。

標準の Windows ビルドには、Eclipse 承認ライセンスのコードおよび Windows バイナリのみが含まれています（特に GPL コードは含まれません）。
シェープファイルインポート、GeoTIFF 処理、OpenSceneGraph 3D GUI、
ビデオ生成などの機能が必要な場合は、"extra" ビルドをダウンロードしてください。

Linux パッケージには、外部ライブラリはまったく含まれていません。
