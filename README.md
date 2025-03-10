## 前言
高光譜影像(Hyperspectral)是一種可以捕獲和分析空間區域內逐點上光譜的精細技術，由於其採集之光譜影像含括可見光與不可見光部分，可透過物件的獨特光譜特徵以區別不同的物件材質，因此也可以檢測出人眼視覺上無法區分的物質。
本專題透過Imec Snapscan VNIR 高光譜影像儀採集紅茶、綠茶、烏龍茶之多種不同產地之茶葉影像，針對各產地的多種茶葉進行頻譜分析，並使用 K-means、Fuzzy C-means、DBSCAN等分群演算法，以及SVM、KNN等分類演算法分析其頻譜特徵，進而判斷所照茶葉之種類為何，而不是透過傳統人眼或人工品嘗方式進行辨識，以提升辨識之效能。

## 取像資料與處理
圖為利用儀器所取得之灰階圖，在高光譜影像450nm到900nm的波段中，813.4nm波段影像在觀察中，其茶葉分布差異最為明顯。

- 紅茶 (青心紅8501 、高山小葉種紅茶、 屏東紅茶)

![image](https://github.com/user-attachments/assets/1ede22ba-abc0-423f-9693-63731dbe1277)

- 綠茶 (早春綠茶、金萱0326、金萱1121)

![image](https://github.com/user-attachments/assets/e68803f1-c044-4a28-8c1f-c99b9f203b71)

- 烏龍茶 (梨山烏龍、杉林溪青心烏龍、阿里山烏龍)

![image](https://github.com/user-attachments/assets/b6a71008-69c4-4fea-8669-d956da80945e)

由於資料可能因雜訊、環境光等造成數值落差太大，透過影像平均濾波分析(average filtering)對原收集之高光譜影像進行處理，其中使用固定視窗大小(window)，如圖，視窗大小為3*3，選擇欲分析之點並與周圍資料所得之平均，可視為波段平均強度曲線圖。

![image](https://github.com/user-attachments/assets/b00ccc80-0286-4b6a-8bad-00cd979a7625)

在影像上進行點分析所得之頻譜特徵結果圖。右圖為利用圖中所有像素進行點平均分析而得，經過資料處理之後可發現頻譜特徵曲線圖較平滑。

![image](https://github.com/user-attachments/assets/eecdfa23-da46-436d-872a-43b9bceda3a4)

## 功能介紹與操作介面
使用藉由Imec Snapscan VNIR取得的影像檔利用Matlab GUI介面做各種演算法分析。

- 使用介面
![image](https://github.com/user-attachments/assets/9e27f317-ecd1-4603-9c59-7585d4a55060)

<br>
<br>

- 選擇讀取檔案

此範例為紅茶A(青心紅)、綠茶A(早春綠茶)、烏龍A(梨山烏龍)

![image](https://github.com/user-attachments/assets/3fb64f67-0970-4857-b163-e05b72c50eb1)

<br>
<br>

- 選擇預分群群數、演算法、波段及影像搜尋範圍

![image](https://github.com/user-attachments/assets/4183536f-2f46-4312-a7e0-718e521dcf7e)

<br>
<br>

- 執行

左上圖為所選擇第100波段的影像圖，右上圖為所選擇演算法K-means之集群分析結果，Accuracy為藉由K-means所分群出來的結果準確率。

![image](https://github.com/user-attachments/assets/e8b8ce5b-72da-4a0c-b637-18418edde72c)

<br>
<br>

- 頻譜特徵顯示

點選Clustering圖片，可以選擇所需判讀區域之頻譜特徵以及頻譜特徵各區間分布圖。

![image](https://github.com/user-attachments/assets/256cd903-b66b-4701-b7de-a4234ad2e304)

![image](https://github.com/user-attachments/assets/e0ad9a6f-6df6-4cb2-91d5-eea6207d44d8)

調整數值以查看影像各波段頻譜特徵。

![image](https://github.com/user-attachments/assets/55c6f960-fd1c-44d3-96da-ed99e8bfb3bf)

## 各演算法數據比較

- 非監督式演算法

|        | 紅茶、綠茶、烏龍 | 紅茶  | 綠茶  | 烏龍  |
|--------|---------------|------|------|------|
| Kmeans | 62.96%       | 73.14% | 52.78% | 38.89% |
| FCM    | **84.26%**   | **73.18%** | **64.81%** | **39.81%** |
| Spectral Clustering | 35.19% | 36.11% | 34.26% | 37.03% |
| Hierarchical Clustering | 59.26% | 68.52% | 37.96% | **39.81%** |

- 監督式演算法

|        | 紅茶、綠茶、烏龍 | 紅茶  |
|--------|---------------|--------|
| SVM    | **85.49%**        | **95.37%** |
| KNN    | 78.40%   | 84.26% |
| Decision Tree | 79.01% | 78.70% |





