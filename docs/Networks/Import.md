# ネットワークのインポート

[NETCONVERT]は異なるサードパーティのフォーマットから道路ネットワークを読みこむことができます。
現在、以下のフォーマットがサポートされています。

* OpenStreetMapデータベース [OpenStreetMapのインポート]を参照
* PTV VISUM(巨視的交通シミュレーションパッケージ) [VISUMのインポート]を参照
* PTV VISSIM(微視的交通シミュレーションパッケージ) [Vissimのインポート]を参照
* OpenDRIVEネットワーク [OpenDRIVEのインポート]を参照
* MATsimネットワーク [MATsimのインポート]を参照
* ArcViewデータベース [ArcViewデータベースのインポート]を参照
* Elmar Brockfelds unsplitted/splitted NavTeqデータ [DlrNavteqのインポート]を参照
* RoboCup Rescue Leagueフォルダ [RoboCupデータのインポート]を参照

ほとんどの場合で、[NETCONVERT]は二つの引数しか必要としません: ソースとなるアプリケーション/フォーマットの名前とそれに続く出力ファイルの名前です(**--output-file**)。
VISUMネットワークをインポートしたい場合は、次のコードでSUMOネットワークに変換することができます。

```
netconvert --visum=MyVisumNet.inp --output-file=MySUMONet.net.xml
```

インポートは[NETCONVERTのオプション]に影響を受けます。

本来のフォーマットは[*plain-xml*]の変種で[NETCONVERT]のための単純な入力としてデザインされており、*.net.xml*ファイルは[NETCONVERT]の出力として右側通行(日本では左側)ルールや交差点での幾何学形態などヒューリスティックに得られたデータで強化されています。
両方のフォーマットは互いに損失なく変換することができます。