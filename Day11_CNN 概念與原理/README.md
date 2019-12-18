### CNN 概念與原理
透過卷積核 (Kernels) 滑動對圖像做訊息提取，並藉由步長 (Strides) 與填充 (Padding) 控制圖像的長寬

![](https://i.imgur.com/huNg6i7.png)

#### 卷積核 | Filter, Kernel

- kernel_size：捲積核大小，通常 `3*3` 或 `5*5` (有些論文是用偶數邊長的)
    - 起始值：通常使用常態分布隨機產生
    - 大小：會影響提取資訊的尺度 (目前普遍是用各種大小之後再來合併或取平均)
    - 奇數 Size：Kernel
        - 有中心點，較容易確認位置資訊
        - 能確保 Padding 的對稱性
- 張數：控制學習的參數，通常是 16、32、64，如果張數低學習效果就好的話，就不用再用更高的張數

#### 重點及優勢

- 權值共享 -> 大大減少參數數量，增加計算速度
    - 以 FC 架構來說輸入一張28*28*1的灰階照片(784個特徵)，隱藏層使用100個神經元 $100*784(weights)+100(bias)=78500$ 個參數
    - 特定的輪廓或線條可以使用相同的 kernel 來學習特徵，透過滑動 kernel 來對整張圖進行捲積
    ![](https://i.imgur.com/P4GHJC0.png)
- 保留空間資訊
    - FC 架構會拉成一維向量，導致空間訊息遺失

![](https://i.imgur.com/LBxU1AB.png)


#### Reference

- [[實戰系列] 使用 Keras 搭建一個 CNN 魔法陣（模型）](https://ithelp.ithome.com.tw/articles/10205389)
- [Keras 中文文檔](https://keras.io/zh/layers/convolutional/)
- [Keras 中文文檔 API 指引](https://keras.io/zh/getting-started/functional-api-guide/)