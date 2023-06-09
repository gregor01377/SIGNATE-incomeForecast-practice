# README
## About this repository
こちらは、Pythonとデータ分析の練習の一環で参加したコンペティションで使用したコードと分析結果をまとめたものになります。
Git、GitHub活用前のため、複数のファイルでバージョン管理を行っていました。About files以降では、各ファイルについて軽い説明を載せています。

運営：DX推進プラットフォームSIGNATE（https://signate.jp/ ） <br>
コンペティション：【練習問題】国勢調査からの収入予測（https://signate.jp/competitions/107 ） <br>
順位(2023/04/03現在)：102/672 <br>
評価点：0.8728579<br>
※評価点は、1に近いほどハイスコア。

## About files
### rankdata.csv & rankdata.ipynb
rankdata.csvは、コンペティションのリーダーボードをデータスクレイピングしたものになります。データスクレイピングにはUiPathを用い、出来たデータテーブルについて必要な情報（順位と評価点）をフィルターを通して抽出した後、csvに出力しました。<br>
![実際のUiPathの画面](/img/datascraping_0.jpg)<br>

rankdata.ipynbは、rankdata.csvについてPythonで見たものになります。<br>
上位25％ラインを目安に、順位と評価点の目標を設定しました。2月時点のデータのため、現在とは異なる部分があります。<br> 
目標順位：167/666 <br>
目標評価点：0.87

### 0_organize.ipynb & 5.5_organize2.ipynb
データを見た際のコードになります。ここで見たデータに基づき、必要があればデータの加工（ダミー変数化や標準化など）を行いました。<br>
0_organize.ipynbでは主にデータを見ており、5.5_orgamize2.ipynbではデータ間の相関を見ています。

### 1_forecast_DT.ipynb
まずはとりあえずやって評価点を出しました。DecisionTreeClassifierは、このコンペティションに取り組む前に知っていた唯一の分類モデルになります。<br>
予測値が0と1ではなく0～1の間の小数値で出てきていた（予測結果を確率で出していた）ため、0と1に変換する際どの値をボーダーにするのが精度が高いのかを算出しグラフの形で視覚化しました。

この手法での最高評価点：0.8555371

### 2_forecast_LightGBM.ipynb
先人の知恵を借りようと同じ課題に取り組んだ方のブログを見た際、精度を高める方法として紹介されていたLightGBMを見つけました。<br>
こちらも予測値を確率の形で出していたため、1_forecast_DT.ipynb同様0＆1変換をするボーダーを算出しました。

この手法での最高評価点：0.8705853

### 3_forecast_LightGBM_dataArrangement.ipynb
2_forecast_LightGBM.ipynbと使用するモデルは変えずに、データ加工を変えるとどうなるのかを見ました。<br>
具体的には、とある項目について属性ごとに比率を出し、比率が近いものを1つのグループとして置き換えました。<br>
![実際にグループ化した一例](/img/dataArrangement.jpg)<br>
予測値を確率の形で出していたため、1_forecast_DT.ipynb同様0＆1変換をするボーダーを算出しました。

この手法での最高評価点：0.8692955

### 4_forecast_LightGBM_Tuning.ipynb
LightGBMで作成するモデルについて、最適のパラメータを探してチューニングを試みました。optuna等を検討してみましたが、精度が上がらなかったのもあり深くはやりませんでした。

この手法での最高評価点：0.8697254

### 5_forecast_Blending(average).ipynb
この課題に取り組んだ方のブログを見た際、精度を高める方法としてブレンディング（スタッキング）が紹介されていました。複数モデル（DT、LGB、XGB）で予測を出し、それらの平均値から最終予測をしたものになります。

この手法での最高評価点：0.8697869

### 6_forecast_Blending(metamodel).ipynb
5_forecast_Blending(average).ipynb同様、複数モデル（決定木系3種）で予測を出しました。その結果を更に分類モデル（XGB）にかけることで、最終予測をしたものになります。

この手法での最高評価点：0.8717523

### 7_forecast_normalization_Blending(metamodel).ipynb
分析について調べていた際に、正規化・標準化の概念が出てきました。決定木系、ランダムフォレストを用いる場合normalizationは必要ないものの、勉強のためにとりあえずやってみようと、元データから数値だったものに関して標準化を行いました。<br>
それ以外については、6_forecast_Blending(metamodel).ipynbと同じことを、モデルの種類を増やして行ったりしました。

この手法での最高評価点：0.8724894

### 8_forecast_Stacking_manymodel.ipynb
6種モデル（DT、XGB、LGB、ランダムフォレスト、ロジステック回帰、サポートベクターマシン）で1次予測を出しました。その結果を3種モデル（XGB、LGB、ランダムフォレスト）にかけて2次予測を出し、更に分類モデル（LGB）にかけることで最終予測をしたものになります。

この手法での最高評価点：0.8728579
