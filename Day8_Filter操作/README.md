### Filter 操作 | Image Filtering
> 需要強化影像中的某些特徵並消除其他不想要的特徵，用特定 kernel(filter) 針對影像重疊區域進行運算，最終便會得出一幅經過 filtered 的新影像，這樣的動作稱為捲積 (convolution)
> ![](https://i.imgur.com/Hy2Gnhi.png)

#### 計算順序

- Cross-correlation
    由左至右, 由上至下 looping
- Convolution
    由右至左, 由下至上 looping

#### Padding
如上圖，由於 n 個點 (如I) 經過 kernel(K) 計算，僅會產生一個點 (I * K)，因此會透過 Padding 的方法來讓圖片計算出來後的圖片大小不變。

##### 方法
- 補零
- 補鄰近 pixel 值
- 補整張圖片 pixel 值的 mean
- 鏡射

#### 模糊及邊緣偵測
![](https://i.imgur.com/20fJJwG.png)

##### 模糊
去除雜訊、使顏色差異變小

- Averaging
    周遭點平均
- Gaussian Blur
    中心點資訊最重要
    ```python=
    # 取得模糊過的圖片，Gaussian Filter size 設為 3*3
    img_blur = cv2.GaussianBlur(img, (3, 3), 0)
    # 最後的 0 -> sigmaX
    # sigmaX: X 軸的標準差，設為 0 會根據 filter size ⾃己算
    # sigmaY default = 0
    ```
- Median
    多用在除噪點上，透過中央除外的周圍點取中間值(找最接近這個值的點)，由於是實際存在的像素值，與計算出來的結果不同，所以多應用在照片除噪
- Bilateral (雙向模糊)
    1. 擁有 Median filter 的除噪效果，又能保留圖片中的不同物件的邊緣(其它三種方式均會造成邊緣同時被模糊化)
    2. Bilateral Filter 執行的效率較差，運算需要的時間較長 (缺點)
    :::info
    傳入的圖片以及 k 值大小之外，它還需要兩個參數 color σ 及 space σ 來計算權重，因此 Bilateral 在計算上除了考慮像素之間幾何上的靠近程度之外，還多考慮了像素之間的光度及色彩差異，這也為什麼 Bilateral Filter 會被稱為雙邊的原因
    :::

##### 邊緣
使顏色差異加大以求得邊緣

![](https://i.imgur.com/yT06bRL.png)
- 垂直
```python=
# 對 x 方向以包含負數的資料格式 (cv2.CV_16S) 進行 Sobel 邊緣檢測
img_x = cv2.Sobel(img_grey,cv2.CV_16S,dx=1, dy=0,ksize=3)
# 將結果正規化(取絕對值)
img_x = cv2.convertScaleAbs(img_x)
```
- 水平
```python=
# 對 x 方向以包含負數的資料格式 (cv2.CV_16S) 進行 Sobel 邊緣檢測
img_y = cv2.Sobel(img_grey,cv2.CV_16S,dx=1, dy=0,ksize=3)
# 將結果正規化(取絕對值)
img_y = cv2.convertScaleAbs(img_x)
```
![](https://i.imgur.com/sEAtnN1.png)
- 合併
```python=
# x, y 方向的邊緣檢測後的圖各以一半的全重進行合成
img_sobel_combine = cv2.addWeighted(img_sobel_x, 0.5, img_sobel_y, 0.5, 0)
```
![](https://i.imgur.com/FMRni21.png)


#### Reference

- [參考 1 - 影像處理 OpenCV 進行捲積操作](https://makerpro.cc/2019/06/the-convolution-of-opencv/)
- [參考 2 - OpenCV-Python教程（6、Sobel算子)](https://blog.csdn.net/sunny2038/article/details/9170013)
- [參考 3 - Python 與 OpenCV - 模糊處理](https://chtseng.wordpress.com/2016/11/17/python-%E8%88%87-opencv-%E6%A8%A1%E7%B3%8A%E8%99%95%E7%90%86/)