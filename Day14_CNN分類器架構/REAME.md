### CNN 概念與原理
透過卷積核 (Kernels) 滑動對圖像做訊息提取，並藉由步長 (Strides) 控制 kernel 一步移動的距離與填充 (Padding) 控制圖像的長寬

#### BN 優化 | Batch Normalization

##### 優點 [ref 1](https://ithelp.ithome.com.tw/articles/10204106), [ref 2](https://medium.com/%E5%AD%B8%E4%BB%A5%E5%BB%A3%E6%89%8D/batch-normalization-batch-norm-2015-af1d4d57805f)
1. 不會過度依賴預設值
2. 提高 learning rate 加速收斂
3. 降低 Overfitting (與 Dropout 層、L1 及 L2 正則化類似)
4. 減少梯度消失 (使用 Sigmoid 作為 Activation Function 時最大導數為 0.25 可能會造成梯度消失，先使用 BN 後再使用 Sigmoid 可以減少梯度消失的問題)

##### 程式

- [Ref - Keras Normalization](https://keras.io/zh/layers/normalization/)
- [Ref - Activations](https://keras.io/zh/activations/)

```python=
input_shape = (32, 32, 3)

model = Sequential()

##  Conv2D-BN-Activation('sigmoid') 

#BatchNormalization主要參數：
#momentum: Momentum for the moving mean and the moving variance.
#epsilon: Small float added to variance to avoid dividing by zero.

model.add(Conv2D(32, kernel_size=(3, 3), padding='same',input_shape=input_shape))
model.add(BatchNormalization(momentum=0.99, epsilon=0.001)) 
model.add(Activation('sigmoid'))

##   Conv2D-BN-Activation('relu')
model.add(Conv2D(32, kernel_size=(3, 3), padding='same', input_shape=input_shape))
model.add(BatchNormalization(momentum=0.99, epsilon=0.001)) 
model.add(Activation('relu'))

model.summary()
```