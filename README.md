# 人工智慧期末報告
下載food-11的壓縮檔，並將food-11.zip檔解壓縮至work檔中

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180428.png)

数据格式下载zip档后解压缩会有三个资料夹，分别为training、validation以及testing

training以及validation中的照片名称格式为[类别]_[编号].jpg

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180702.png
)

將數據集上傳

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180715.png)


数据集解压并移动至工作文件夹，并观察数据集

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180724.png)


![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180741.png)

图像预处理

在图像预处理中，我们定义一个名为preprocess的函数，并做如下预处理：

图像尺寸调整：蒋图像尺寸调整为128*128像素，确保输入图像具有相同尺寸；

随机翻转（仅用于训练）：为了使数据更加丰富，从而让模型效果更好；

數據標準化：将图像转换为numpy数组，并使其归一化；

更改数组形状：以符合CNN的输入要求

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180751.png)

数据读取

定义了一个用于处理食物分类任务的自定义数据集类 FoodDataSet，并使用这个类来创建训练和评估（验证）的数据加载器（DataLoader），并读取数据。

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180805.png)

模型构建（网络配置）

先定義網路結構，這裡選擇的LeNet()模型。 LeNet 是一個經典的捲積神經網路（CNN）架構，最初由 Yann LeCun 等人在1990年代提出，用於手寫數字識別（如 MNIST 資料集）。本範例中的 LeNet 模型基於原始的 LeNet 結構進行了適度的修改，以適應更通用的影像分類任務，特別是針對具有更多類別（如11類）的資料集。此模型使用 PaddlePaddle 深度學習框架實作。

LeNet 模型主要由以下幾個部分組成：

卷積層（Convolutional Layers）：
Conv0：第一個卷積層，輸入通道數為3（適用於RGB影像），輸出通道數為10，卷積核大小為5x5，步長為1，使用SAME填滿策略以保持特徵圖尺寸不變。

Conv1：第二個卷積層，輸入通道數為10，輸出通道數為20，卷積核大小為5x5，步長為1，同樣使用SAME填充。

Conv2：第三個卷積層，輸入通道數為20，輸出通道數為50，卷積核大小為5x5，步長為1，SAME填滿。


池化層（Pooling Layers）：
每個卷積層後面跟著最大池化層（MaxPool2D），池化核大小為2x2，步長為2，用於減少特徵圖的尺寸和參數數量，同時提高模型的泛化能力。


全連接層（Fully Connected Layers）：
FC1：第一個全連接層，將捲積層輸出的特徵圖展平後作為輸入，輸出特徵維度為256。

FC2：第二個全連接層，輸入特徵維度為256，輸出特徵維度為64。

FC3：第三個全連接層，即輸出層，輸入特徵維度為64，輸出特徵維度為11，對應11個類別的分類任務。


激活函數：
在每個卷積層和前兩個全連接層後使用 Leaky ReLU 激活函數，以引入非線性因素，並提高模型的表達能力。

在輸出層使用 Softmax 啟動函數，將輸出轉換為機率分佈，以便進行多分類任務。

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180835.png)

查看模型结构

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-01%20180853.png)


 模型训练

 ![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-02%20115448.png)

简单地导入一张图，然后进行直观测试

![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-02%20115501.png)
 
![image](https://github.com/hy189/-/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-01-02%20115514.png)

