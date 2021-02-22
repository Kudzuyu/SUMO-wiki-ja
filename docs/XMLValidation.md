# XMLのバリデーション

[原文ページ](https://sumo.dlr.de/docs/XMLValidation.html)

## XML入力のバリデーション

[SUMOアプリケーション]()は全て、入力に対するXMLバリデーションをサポートしています。
有効化するには、以下のオプションを使います。

|オプション|説明
|--|--|
**-X {{DT_STRING}}** <br/> **--xml-validation {{DT_STRING}}**|XML入力に対するschemaバリデーションを設定("never", "auto", "always") デフォルト値: **auto**
**-xmlm-validation.net {{DT_STRING}}** |SUMOネットワークの入力に対するスキーマバリデーションを設定("never", "auto", "always") デフォルト値: **never**

バリデーションはXMLパーサ中で[XML scheme processing](https://xerces.apache.org/xerces-c/schema-3.html)を起動させることによって行なわれます。
スペルミスや属性の誤挿入など多くの一般的な入力エラーを補足します。

スキーマバリデーションのためのもう一つの必要条件はルート要素に以下のようなスキーマ宣言が含まれていることです。

```
<routes xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://sumo.dlr.de/xsd/routes_file.xsd">
```

バリデーション設定が*always*に設定されている時には、この宣言を削除するようにエラーがでます。
スキーマバリデーションはXMLのパースを大幅に遅くさせることがあり、従ってネットワーク入力に対してはデフォルトで無効化されています(ネットワークは手作業で編集すべきではなく、有効であることが想定されるから)。

!!! note "注"
    自動生成された巨大な入力を扱う場合にはスキーマバリデーションを完全に無効化することを考慮すべきです。
    詳しくは[このFAQ]()を参照してください。

## スキーマ宣言の追加

SUMOアプリケーションのどれかによって作られたファイルには自動的にそのファイルにあったスキーマ宣言が付与されます。
入力ファイルを一から書く場合、以下のようなスキーマ宣言をルート要素に追加する必要があります。

```
<ROOT_ELEMENT xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="http://sumo.dlr.de/xsd/SCHEMA_FILE">
```

ROOT_ELEMENTとSCHEME_FILEは以下の表を参考に設定してください。

|アプリケーションオプション|ルート要素|スキーマファイル|
|---|---|---|
**--route-files**, **--trip-files**, **--flow-files**|routes|routes_file.xsd
**--additional-files**|add|additional_files.xsd
**--node-files**|nodes|nodes_file.xsd
**--edge-files**|edges|edges_file.xsd
**--connection-files**|connections|connetions_file.xsd
**--tllogic-files**|flLogics|tllogic_file.xsd
**--type-files**|types|types_file.xsd
**-weight-files**|meandata|meandata_file.xsd

!!! note "注"
    ROOT_ELEMENTの値は慣習的に決まっているものであり、実際には任意の値を取ることができます。

## スキーマファイル

スキーマファイルはSUMOインストール中の**`<SUMO_HOME>`**/data/xsdディレクトリにあるでしょう。
環境変数[SUMO_HOME](./Basics/Basic_Computer_Skills/#sumo_home)が設定されていれば、これらのファイルはバリデーションが入力された時に使用されます。

## SUMOファイルタイプ

[SUMOアプリケーション]()が扱うファイル拡張子の完全なリストは[ファイル拡張子]()にあります。

## スキーマバリデーションの無効化

スキーマバリデーションを無効化するには、次のどれかを実行してください。

* オプション **--xml-validation never**を設定する
* 入力のXMLファイルの先頭から `xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"` `xsi:noNamespaceSchemaLocation="http://sumo.dlr.de/xsd/....xsd"`の属性を削除する
