### SIFT 概念與實作

#### SIFT 特徵

- 表面特徵
    - 特別的輪廓、邊緣、紋理

1. 尺度不變性
    尺度不同，偵測準度就有所不同
![](https://i.imgur.com/X4uYXUH.png)

2. 尺度空間極值偵測
    - Laplacian of Gaussian (LoG)
        先對圖片做 Gaussian Blur 再算⼆階導數取得邊緣
    - Difference of Gaussian (DoG)
        圖片經過不同程度的縮放後計算出不同程度的 Gaussian Blur最後合併得到⼀個 Gaussian Pyramid，其差值即為 DoG
        ![](https://i.imgur.com/62j8NJJ.png)
        結果可以視為 LoG 的約略略值 (沒有做⼆階導數)

3. 關鍵點定位
- 鄰近資料差補
    - 主要根據相鄰資訊來修正極值的位置
- 過濾不明顯關鍵點
    - 根據計算曲率來判斷是否為不明顯的關鍵點
- 過濾邊緣關鍵點
    - 根據計算曲率來判斷是否為不明顯的關鍵點

4. 方位定向
    - 每 10 度為單位計算周圍的梯度值
    - 梯度值最大的⽅向當作是該關鍵點的主要⽅向

5. 關鍵點描述⼦
    - 關鍵點周圍正規化成 128 維的特徵向量 (16 * 16 的區域共 4 * 4 的子區域，計算 8 個方向的直方圖)
    ![](https://i.imgur.com/ayAfsdh.png)
    
#### 使用 SIFT

1. 安裝
```python=
pip install opencv-contrib-python==3.4.2.16 --user
```
2. 執行
```python=
sift = cv2.xfeatures2d.SIFT_create() # 建立 SIFT 物件
keypoints = sift.detect(img_gray, None) # 抽取關鍵點
img_show = cv2.drawKeypoints(img_gray, keypoints, img)
```