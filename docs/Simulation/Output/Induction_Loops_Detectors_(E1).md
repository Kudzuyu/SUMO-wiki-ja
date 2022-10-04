<!-- detector : 検出器 -->

# 誘導ループ検出器 (E1)

参考原文バージョン: 2022/6/3, 84ffbb705649e058c8df81963151e02cde590852

## シミュレーション内でのインスタンス化

誘導ループは下記のように{{AdditionalFile}}内に定義されます。

```xml
<additional>
   <inductionLoop id="<ID>" lane="<LANE_ID>" pos="<POSITION_ON_LANE>" period="<AGGREGATION_TIME>"
   file="<OUTPUT_FILE>" friendlyPos="true"/>
</additional>
```

"`id`"は検出器につける任意の文字列の名前です。
"`lane`"と"`pos`"属性は検出器が配置されるlaneとlane上の位置を示します。
"`period`"属性は集計する値の集計期間を示します。
"`file`"属性は検出器の結果を書き込むファイルを示します。

複数の定義を同じ{{AdditionalFile}}に配置し、同じ出力ファイルを参照することもできます。
{{AdditionalFile}}の最初と最後には下記のようにトップレベルのタグが必要です。

```xml
<additional>
  <inductionLoop id="myLoop1" lane="foo_0" pos="42" period="900" file="out.xml"/>
  <inductionLoop id="myLoop2" lane="foo_2" pos="42" period="900" file="out.xml"/>
  ....
</additional>
```

属性について。

| Attribute Name | Value Type         | Description |
| -------------- | ------------------ | -------------------------------------------------------------------------------------- |
| **id**         | id (string)        | 検出器のid                                                                      |
| **lane**       | referenced lane id | 検出器を設置するlaneのid。laneは使用するネットワーク内の一部である必要があります。|
| **pos**        | float              | 検出器を設置するlane上の位置（メートル単位）。位置はlaneの長さに-1を乗じた値からlaneの長さまでの間の値である必要があります。負の値のとき、laneの終端（vehicleの移動方向の位置）から遡った位置が計算されます。|
| period (alias freq) | int (time)| 検出器が収集した値が総計される集計期間（*デフォルト：全シミュレーション時間*）|
| **file**       | filename           | 出力ファイルのパス。詳細は[Writing Files](../../Basics/Using_the_Command_Line_Applications.md#writing_files)を参照してください。|
| friendlyPos    | bool     | もし設定された場合は、検出器がlaneの背後に配置されてもエラーをリポートしません。代わりに、positionが負の値、かつレーン長さに-1を乗じた値よりも小さい場合は、検出器をlaneの終端から0.1 [m]か、positionが0.1の位置に配置します。（*デフォルト: false*）|
| vTypes         | string   | 考慮するvehicle typeのidリスト（スペース区切り）。""は全タイプを意味します。（デフォルトは""）|
| detectPersons  | string   | [vehicleの代わりにperson（歩行者か乗客）を検出する](../Pedestrians.md#detectors_for_pedestrians)  |
| length         | float    | **pos**から下流側の検出する領域の長さ（デフォルトは*0*） |

## 出力の生成

シミュレーションされた誘導ループの出力に書き込まれる1つのデータは次のようになります。

```xml
   <interval begin="''<BEGIN_TIME>''" end="''<END_TIME>''" id="''<DETECTOR_ID>''" \
      nVehContrib="''<MEASURED_VEHICLES>''" flow="''<FLOW>''" occupancy="''<OCCUPANCY>''" \
      speed="''<MEAN_SPEED>''" harmonicMeanSpeed="''<HARM_MEAN_SPEED>''" length="''<MEAN_LENGTH>''" nVehEntered="''<ENTERED_VEHICLES>''"/>
   ... further intervals ...
```

値は次の表の通りです。

| Name              | Type                 | Description                                                        |
| ----------------- | -------------------- | -------------------------------------------------------------------------------------- |
| begin             | (simulation) seconds | 値が収集された最初のタイムステップ |
| end               | (simulation) seconds | 値が収集された最後のタイムステップ＋DELTA_T |
| id                | id                   | 検出器のid |
| nVehContrib       | \#vehicles           | インターバル内で検出器を完全に通過したvehicleの数 |
| flow              | \#vehicles/hour      | 1時間あたりで推計されたvehicleの数 |
| occupancy         | %                    | vehicleが検出器に位置していた時間の割合（0～100%）|
| speed             | m/s                  | 収集された全vehicleの速度の算術平均（-1はvehicleが収集されていないことを表します）。この値から時間平均速度を得られます。|
| harmonicMeanSpeed | m/s                  | 収集された全vehicleの速度の調和平均（-1はvehicleが収集されていないことを表します）。この値から空間平均速度を得られます。|
| length            | m                    | 収集された全vehicleの平均長さ（-1はvehicleが収集されていないことを表します） |
| nVehEntered       | \#vehicles           | 検出器に接触した全vehicle。検出器を完全に通過していないvehicleも含みます（このvehicleは集計値に加味されません）。|

検出器は、vehicleが検出器に進入した時刻と離脱した時刻を判断して値を計算します。
このことは次の2つを暗示します。
a) vehicleが検出器上にいる限り、いくつかの値は利用できない
b) もし、vehicleがレーン変更で検出器に進入した場合、vehicleは検出器を完全に通過していないとみなし、いくつかの値は計算されない

"`nVehEntered`"は（たとえレーン変更で離脱または進入したり、インターバルが終わる時点でまだ検出器上にいたとしても）検出器上にいたすべてのvehicleを含みます。
vehicleについて収集される値は"`nVehContrib`"に対応します。

## 可視化

![induction_loops.svg](../../images/Induction_loops.svg "induction_loops.svg")
**Figure: 誘導ループのあるシナリオ**

![induction_loop_closeup.svg](../../images/Induction_loop_closeup.svg
"induction_loop_closeup.svg") **Figure: 誘導ループの拡大図**

## その他注釈

- [シミュレーションされた誘導ループはTraCIを使ってアクセス可能です](../../TraCI/Induction_Loop_Value_Retrieval.md). 
XML出力が不必要な場合は`file="NUL"`属性が使えます。
- 検出器の定義を自動生成できます。詳細は[output tools](../../Tools/Output.md)を参照してください。
