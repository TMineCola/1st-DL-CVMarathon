### CNN 概念與原理
透過卷積核 (Kernels) 滑動對圖像做訊息提取，並藉由步長 (Strides) 控制 kernel 一步移動的距離與填充 (Padding) 控制圖像的長寬

#### 步長(Strides)、填充(Padding)
```python=
keras.layers.Conv2D(filters, kernel_size, strides=(1, 1), padding='valid', data_format=None, dilation_rate=(1, 1), activation=None, use_bias=True, kernel_initializer='glorot_uniform', bias_initializer='zeros', kernel_regularizer=None, bias_regularizer=None, activity_regularizer=None, kernel_constraint=None, bias_constraint=None)
```

![](https://i.imgur.com/66fCFat.png)
[_Ref_](https://keras.io/layers/convolutional)

##### 步長
> 指 Kernel 每次卷積移動的水平、垂直距離

- height: 垂直移動的步伐
- width: 水平移動的步伐

##### 填充
> 指在原先圖片周圍填充數值(通常為0)，避免輸出圖片大小與原圖不符

- Padding={valid | same}
    - valid：多餘的像素質直接捨去
    ![](https://i.imgur.com/9DBOUga.png)
    - same：透過補 0 的方式讓輸出的 feature map 跟原圖大小一樣