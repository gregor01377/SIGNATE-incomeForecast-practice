# README
## About this repository
こちらは、Pythonとデータ分析の練習の一環で参加したコンペティションで使用したコードと分析結果をまとめたものになります。

運営：DX推進プラットフォームSIGNATE（https://signate.jp/ ） <br>
コンペティション：【練習問題】国勢調査からの収入予測（https://signate.jp/competitions/107 ） <br>
マイページ：https://signate.jp/profile <br>

## About files
### rankdata.csv & rankdata.ipynb
rankdata.csvは、コンペティションのリーダーボードをデータスクレイピングしたものになります。データスクレイピングにはUiPathを用い、必要な情報（順位と評価点）のみを抽出した後、csvに出力しました。<br>
![実際のUiPathの画面](/img/datascraping_0.jpg)<br>

rankdata.ipynbは、rankdata.csvについてPythonで見たものになります。<br>
上位25％ラインを目安に、順位と評価点の目標を設定しました。2月時点のデータのため、現在とは異なる部分があります。<br> 
|順位|評価点|
|---|---|
|167/666|0.871200|

### 0_organize.ipynb
