# SUMOのインストール

[原文ページ](https://sumo.dlr.de/wiki/Installing)

## Windows

使っているプラットフォーム(64bit、32bit)及びSUMOの使いかたに応じて4つのパッケージが存在しています。ローカルマシーンで使用し、管理者権限を持っている場合はインストーラを使うべきです(64bit版が望ましい)。「ポータブル」版が必要であったり、管理者権限を持っていない場合は、zipをダウンロードして[7Zip](https://sevenzip.osdn.jp/)や[Winzip](https://www.winzip.com/win/jp/)などのツールを使って任意のフォルダに解凍してください。全てのパッケージは、バイナリ、必要な全てのdll、使用例、ツール及びHTML版のドキュメント(英語)を含んでいます。

!!! note "訳注"
    Windowsのエクスプローラには標準でzip解凍機能が付いているので、これらのソフトをダウンロードしなくてもzip版を利用することが可能です

- 64bit版インストーラ: [sumo-win64-1.2.0.msi](http://prdownloads.sourceforge.net/sumo/sumo-win64-1.2.0.msi?download)
- 64bit版zip: [sumo-win64-1.2.0.zip](http://prdownloads.sourceforge.net/sumo/sumo-win64-1.2.0.zip?download)
- 32bit版インストーラ: [sumo-win32-1.2.0.msi](http://prdownloads.sourceforge.net/sumo/sumo-win32-1.2.0.msi?download)
- 32bit版zip: [sumo-win32-1.2.0.zip](http://prdownloads.sourceforge.net/sumo/sumo-win32-1.2.0.zip?download)

インストールフォルダには"bin"という名前のフォルダがあります。
ここに実行可能ファイル(プログラム)があります。
[SUMO-GUI]()をダブルクリックして **docs/expample** フォルダにある例を見ることができます。
その他の全てのプログラム([DUAROUTER](), [DEFROUTER]()等) はコマンドラインから実行しなくければなりません。
これを楽にするために、全体の環境をセットアップするstart-comanndline.batもあります。
コマンドラインについて不確かなことがある場合は、[基本的なコンピュータスキル#コマンドラインからのプログラム実行]() を読んでください。

最新のnightly buildや、テスト、ソースが必要な場合は[ダウンロード]()ページからダウンロードすることができます。

SUMOをソースからビルドする際には[WindowsでのSUMOのビルド]()を参照してください。

## Linux

debianかubuntuを使っているならば、SUMOは基本ディストリビューションの一部であり次のようにしてインストールすることができます。

```
sudo apt-get install sumo sumo-tools sumo-doc
```

より最新のubuntu版が欲しい場合は、次のようにしてppaを追加することで見つかるかもしれません。

```
sudo add-apt-repository ppa:sumo/stable
sudo apt-get update
```

そのあともう一度以下を実行してください。

```
sudo apt-get install sumo sumo-tools sumo-doc
```

openSUSEやFedoraのようなディストリビューションむけのコンパイル済みバイナリは[こうしたリポジトリ](http://download.opensuse.org/repositories/home:/behrisch/) にあります。
これらのリポジトリはnightly buildも含んでいます。
ここに挙げた以外のシステムを使っている場合やソースを編集したい場合、[SUMOをソースからビルドする必要があります。]()

## macOS

[ここ]() にHomebrewを使った方法(推奨)かMacportsを使った方法(レガシー) が挙げられています。

## Docker

初心者ユーザーにとってSUMOをソースからビルドするのは簡単なことではありません。
Dockerはこの問題を解決する人気のツールです。
[Docker Hub](https://hub.docker.com/) で"SUMO"と検索することで、SUMOのDocker化に関しての方法をいくつか得ることができるでしょう。

[docker-sumo](https://github.com/bogaotory/docker-sumo) にはUbuntu16.04上でSUMOバージョン0.30.0以上をDocker化するデモがあります。
**sumo**や**traci**と同じく**sumo-gui**についても[docker-sumo](https://github.com/bogaotory/docker-sumo)で取りあげられているのでユーザーはDocker化したSUMO上のGUIを使うことができます。