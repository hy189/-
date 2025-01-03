# 人工智慧期末報告

11218201方玄伶
11218202呂蕙妤

下載food-11的壓縮檔，並將food-11.zip檔解壓縮至work檔中

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180428.png)
數據格式下載zip檔後解壓縮會有三個資料夾，分别為training、validation以及testing

training以及validation中的照片名稱格式為[類別]_[编號].jpg

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180702.png
)

將數據集上傳

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180715.png)


數據集解壓並移動至工作文件夾，並觀察數據集

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180724.png)


![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180741.png)

圖像預處理

在圖像預處理中，我們定義一個名為preprocess的函數，並做如下預處理：

圖像尺寸調整：將圖像尺寸調整为128*128像素，確保輸入圖像具有相同尺寸；

隨機翻轉（僅用於訓練）：為了使數據更豐富，從而讓模型效果更好；

數據標準化：將圖像轉換為numpy數組，並使其歸一化；

更改數组形狀：以符合CNN的輸入要求

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180751.png)

數據讀取

定義了一个用於處理食物分類任務的自定義數據集類 FoodDataSet，並使用这个類来創建訓練和評估（驗證）的數據加載器（DataLoader），並讀取數據。

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180805.png)

模型構建（網絡配置）

先定義網路結構，這裡選擇的LeNet()模型。 LeNet 是一個經典的卷積神經網路（CNN）架構，最初由 Yann LeCun 等人在1990年代提出，用於手寫數字識別（如 MNIST 資料集）。本範例中的 LeNet 模型基於原始的 LeNet 結構進行了適度的修改，以適應更通用的影像分類任務，特別是針對具有更多類別（如11類）的資料集。此模型使用 PaddlePaddle 深度學習框架實作。

LeNet 模型主要由以下幾個部分組成：

卷積層（Convolutional Layers）：
Conv0：第一個卷積層，輸入通道數為3（適用於RGB影像），輸出通道數為10，卷積核大小為5x5，步長為1，使用SAME填滿策略以保持特徵圖尺寸不變。

Conv1：第二個卷積層，輸入通道數為10，輸出通道數為20，卷積核大小為5x5，步長為1，同樣使用SAME填充。

Conv2：第三個卷積層，輸入通道數為20，輸出通道數為50，卷積核大小為5x5，步長為1，SAME填滿。


池化層（Pooling Layers）：
每個卷積層後面跟著最大池化層（MaxPool2D），池化核大小為2x2，步長為2，用於減少特徵圖的尺寸和參數數量，同時提高模型的泛化能力。


全連接層（Fully Connected Layers）：
FC1：第一個全連接層，將卷積層輸出的特徵圖展平後作為輸入，輸出特徵維度為256。

FC2：第二個全連接層，輸入特徵維度為256，輸出特徵維度為64。

FC3：第三個全連接層，即輸出層，輸入特徵維度為64，輸出特徵維度為11，對應11個類別的分類任務。


激活函數：
在每個卷積層和前兩個全連接層後使用 Leaky ReLU 激活函數，以引入非線性因素，並提高模型的表達能力。

在輸出層使用 Softmax 啟動函數，將輸出轉換為機率分佈，以便進行多分類任務。

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180835.png)

查看模型結構

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180853.png)


 模型訓練

 ![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-02%20115448.png)

簡單導入一張圖，然後進行直觀測試
![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-02%20115501.png)
 
![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-02%20115514.png)

