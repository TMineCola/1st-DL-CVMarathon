### CNN 概念與原理
透過卷積核 (Kernels) 滑動對圖像做訊息提取，並藉由步長 (Strides) 控制 kernel 一步移動的距離與填充 (Padding) 控制圖像的長寬

#### 池化層、全連接層及攤平

##### 池化層 | Pooling
> 用來降低 Feature Map 的尺度連同降低運算量，提取特徵同時加速收斂，同時也會失去部分特徵，透過一到兩層的池化可能可以達到加速收斂提升準度的效果，但仍得看實際應用時的情況如何來使用

- 最大池化 Max pooling：取 Kernel 中最大值
    保留重要紋理、避免 Overfitting，某種層度上能夠提升圖像旋轉、平移、縮放的不變性
- 平均池化 Average pooling：取 Kernel 平均值
    強調的是特徵平滑性，缺點是不管重要不重要的特徵都平均計算

##### 全連接層 | Fully Connected
> 利⽤全連接層的神經元做為分類器各種類 (Classification) 的代表機率

![](https://i.imgur.com/whbx0zD.png)

##### 攤平 | Flatten

> 將一維以上的 Tensor 拉平成二維 (Batch size, Channels)，通常經過 CNN 的 Feature Map 是四維的，攤平成二維才能跟全連接層做合併

:::info
Global Average Pooling 也是常見用來處理 CNN 跟 FC 做連結的方法 [Ref](https://alexisbcook.github.io/2017/global-average-pooling-layers-for-object-localization/)
![](https://i.imgur.com/8XZtkvn.png)
![](https://i.imgur.com/rRibFq9.jpg)
:::