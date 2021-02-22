# SUMO のインストール

[原文ページ](https://sumo.dlr.de/wiki/Installing)

## Windows

使っているプラットフォーム(64bit、32bit)及び SUMO の使いかたに応じて 4 つのパッケージが存在しています。ローカルマシーンで使用し、管理者権限を持っている場合はインストーラを使うべきです(64bit 版が望ましい)。「ポータブル」版が必要であったり、管理者権限を持っていない場合は、zip をダウンロードして[7Zip](https://sevenzip.osdn.jp/)や[Winzip](https://www.winzip.com/win/jp/)などのツールを使って任意のフォルダに解凍してください。全てのパッケージは、バイナリ、必要な全ての dll、使用例、ツール及び HTML 版のドキュメント(英語)を含んでいます。

!!! note "訳注"
    Windows のエクスプローラには標準で zip 解凍機能が付いているので、これらのソフトをダウンロードしなくても zip 版を利用することが可能です

- 64bit 版インストーラ: [sumo-win64-1.6.0.msi](http://prdownloads.sourceforge.net/sumo/sumo-win64-1.6.0.msi?download)
- 64bit 版 zip: [sumo-win64-1.6.0.zip](http://prdownloads.sourceforge.net/sumo/sumo-win64-1.6.0.zip?download)
- 32bit 版インストーラ: [sumo-win32-1.6.0.msi](http://prdownloads.sourceforge.net/sumo/sumo-win32-1.6.0.msi?download)
- 32bit 版 zip: [sumo-win32-1.6.0.zip](http://prdownloads.sourceforge.net/sumo/sumo-win32-1.6.0.zip?download)

インストールフォルダには"bin"という名前のフォルダがあります。
ここに実行可能ファイル(プログラム)があります。
[SUMO-GUI]()をダブルクリックして **docs/expample** フォルダにある例を見ることができます。
その他の全てのプログラム([DUAROUTER](), [DEFROUTER]()等) はコマンドラインから実行しなくければなりません。
これを楽にするために、全体の環境をセットアップする start-comanndline.bat もあります。
コマンドラインについて不確かなことがある場合は、[基本的なコンピュータスキル#コマンドラインからのプログラム実行]() を読んでください。

最新の nightly build や、テスト、ソースが必要な場合は[ダウンロード]()ページからダウンロードすることができます。

SUMO をソースからビルドする際には[Windows での SUMO のビルド]()を参照してください。

## Linux

debian か ubuntu を使っているならば、SUMO は基本ディストリビューションの一部であり次のようにしてインストールすることができます。

```
sudo apt-get install sumo sumo-tools sumo-doc
```

より最新の ubuntu 版が欲しい場合は、次のようにして ppa を追加することで見つかるかもしれません。

```
sudo add-apt-repository ppa:sumo/stable
sudo apt-get update
```

そのあともう一度以下を実行してください。

```
sudo apt-get install sumo sumo-tools sumo-doc
```

openSUSE や Fedora のようなディストリビューションむけのコンパイル済みバイナリは[こうしたリポジトリ](http://download.opensuse.org/repositories/home:/behrisch/) にあります。
これらのリポジトリは nightly build も含んでいます。
ここに挙げた以外のシステムを使っている場合やソースを編集したい場合、[SUMO をソースからビルドする必要があります。]()

## macOS

Homebrew[http://brew.sh/]を使って SUMO を簡単にインストールできます。
もしまだ homebrew をインストールしていない時は、次のようにします。

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

homebrew を最新にしておいてください。

```
brew update
```

以下のコマンドで最新安定版の SUMO をインストールできます。

```
brew tap dlr-ts/sumo
brew install sumo
```

セットアップを完了させるために、環境変数**SUMO_HOME**を設定し SUMO のインストールディレクトリを指すようにしてください。


## Docker

初心者ユーザーにとって SUMO をソースからビルドするのは簡単なことではありません。
Docker はこの問題を解決する人気のツールです。
[Docker Hub](https://hub.docker.com/) で"SUMO"と検索することで、SUMO の Docker 化に関しての方法をいくつか得ることができるでしょう。

[docker-sumo](https://github.com/bogaotory/docker-sumo) には Ubuntu16.04 上で SUMO バージョン 0.30.0 以上を Docker 化するデモがあります。
**sumo**や**traci**と同じく**sumo-gui**についても[docker-sumo](https://github.com/bogaotory/docker-sumo)で取りあげられているのでユーザーは Docker 化した SUMO 上の GUIを使うことができます。
