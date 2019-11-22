# 深度學習與電腦視覺

## OpenCV

### 簡介
OpenCV (Open source computer Vision) 是電腦視覺領域非常知名的套件，由 Intel 發起從 1999 年年開始主要透過 C++ 程式語⾔言開發的跨平台套件。

### 安裝

> 可以加上 `--user` 參數裝在 User Local
```shell=
pip install opencv-python
```

### 顯示圖片
> imshow 需要在 Windows 環境底下使用

載入圖片的時候有三種模式
1. IMREAD_COLOR 以 RGB 三個 channel 載入
2. IMREAD_GRAYSCALE 以灰階格式載入
3. IMREAD_UNCHANGED 載入圖片中所有 channel

再用 `imshow('{視窗名稱}', 圖片)` 來顯示圖片

```python=
import cv2

img_path = '../img/lena.png'

# 以彩色圖片的方式載入
img = cv2.imread(img_path, cv2.IMREAD_COLOR)

# 以灰階圖片的方式載入
img_gray = cv2.imread(img_path, cv2.IMREAD_GRAYSCALE)

# 為了要不斷顯示圖片，所以使用一個迴圈
while True:
    # 顯示彩圖
    cv2.imshow('bgr', img)
    # 顯示灰圖
    cv2.imshow('gray', img_gray)

    # 直到按下 ESC 鍵才會自動關閉視窗結束程式
    k = cv2.waitKey(0)
    if k == 27:
        cv2.destroyAllWindows()
        break
```

:::info
1. 一張平面的圖可能包含多個 channel，以 RGB 圖為例 (300 x 400)像素就會有三維矩陣 (300 x 400 x 3)
![](https://i.imgur.com/Yp4RUN5.png)

2. 讀取進來的圖片會以 BGR 的方式儲存三個顏色的 channel，如果要轉成 Matplotlib 用的 RGB 格式需要使用 _[Ref](https://blog.gtwang.org/programming/opencv-basic-image-read-and-write-tutorial/)_
    A. `rgb_img = img[:,:,::-1]`
    B. 讀取時使用 `cv2.cvtColor(img_bgr, cv2.COLOR_BGR2RGB)`

3. 讀取單一個 channel (Day 1 作業)
    A. `B = img[...,0]`, `G = img[...,0]`, `R = img[...,0]`
    B. 先複製後將其他兩個 channel 清成 0 _[Ref](https://stackoverflow.com/questions/44554125/python-want-to-display-red-channel-only-in-opencv)_
    ```python=
    blue = img.copy()
    blue[:, :, 1] = 0
    blue[:, :, 2] = 0
    ```
:::
