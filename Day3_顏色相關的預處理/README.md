### 顏色轉換預處理 | Image Preprocessing
> 針對轉換後型態可能有所改變，例如 255(Unit8) -> 飽和度百分比(float)，進行預先處理

#### BGR -> HSV 飽和度轉換
```python=
# BGR to HSV 轉換
img_hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
# 轉換成 float32 格式(存小數點)
img_hsv = img_hsv.astype('float32')
# 將飽和度換算成百分比 (也可以同時做調降飽和度, 下方程式碼為調降兩成)
# 這一步驟還需要檢查是否數值落在合理範圍 0~1 之間
img_hsv[:, :, 1] = 0 if img_hsv[:, :, 1] / 255 - 0.2 < 0 else img_hsv[:, :, 1] / 255 - 0.2 
```

#### 直方圖均衡 Histogram Equalization
> 當對比不強時用來增強對比，除了可以針對灰階圖片增強之外，也可以對 RGB 各個 Channel 增強來達到加強對比的效果
> 透過數學方法來將分布集中的數值打散到 0~255
> OpenCV: `cv2.equalizeHist(ImageSrc)` -> 只針對單個維度做直方圖均衡

- 增強前(分布集中) vs 增強後(分布均勻)
    - ![](https://i.imgur.com/JLzT6xb.png)
    - ![](https://i.imgur.com/cTkIX3S.png)

- 也可以透過簡易方法提升亮度
    - $g(x)=\alpha*f(x)+\beta$
    - $f(x)$ 處理前資料
    - $\alpha$ 對比度 (建議 1.0~3.0)
    - $\beta$ 明亮度 (0~100)
    - 可用 numpy 的 clip 功能來讓資料不超過界線
    ```
    import numpy as np
    np.clip(計算數據, 最小值, 最大值)
    ```
    - 也可以直接使用 `img = cv2.convertScaleAbs(img, alpha = 數值, beta = 數值)`
:::info
- 每個 channel 個別做直方圖均衡
equalHist_by_channel = [img[..., 0], img[..., 1], img[..., 2]]
equalHist_by_channel = [cv2.equalizeHist(i) for i in equalHist_by_channel]
- 組合經過直方圖均衡的每個 channel
img_bgr_equal = np.stack(equalHist_by_channel, axis=-1)
:::