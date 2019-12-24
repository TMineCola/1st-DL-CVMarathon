### CNN 概念與原理
透過卷積核 (Kernels) 滑動對圖像做訊息提取，並藉由步長 (Strides) 控制 kernel 一步移動的距離與填充 (Padding) 控制圖像的長寬

#### 總整理

![](https://i.imgur.com/oMGdO77.png)

##### 卷積層 + 池化層 + 扁平層 | Convolution & Pooling + Flatten
> 在 Tensorflow 及 Keras 格式為 Batch Size , Height , Width , Channels

- 卷積層 Convolution
    - 輸入圖片
    - 卷積提取特徵 Feature Map | Convolution
    - 批次正規化 | Batch Normalization
    - 激發函式 | Activation Function
    :::info
    (近期論文)也有先丟入 Activation Function 再進行 Batch Normalization 的做法
    :::
- 池化層 Pooling
    > 降低 Feature Map 尺度及強化特徵
    - Average Pooling (取平均值)
    - Max Pooling (取最大值)
- 扁平層 Flatten
    - Global Average Pooling (取全部中最大值)
    ![](https://i.imgur.com/9dkM2AV.png)

##### 全連接層 | Fully Connected Layers
> 由於 FC 層會產生大量參數，因此現在比較多文獻建議 FC 層越少越好
> FC層的最後⼀一層要使⽤用與預分類類別⼀一樣多的神經元
> 最後透過 `Softmax` 換算成機率

![](https://i.imgur.com/uOpApg5.png)

- Softmax 函數：將輸出值總合統整成1，轉換成機率的型態，通常⽤用於多類的分類器輸出

![](https://i.imgur.com/fKZZAHj.png)