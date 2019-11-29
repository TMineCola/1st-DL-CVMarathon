### 顏色表示法 | Color Presentation

一般來說是透過上面提到的 RGB 三個維度來表示圖片顏色，也可以`增加維度`來提供更多顏色的定義，或透過`改變維度的意義`來改變顏色的表示。

![](https://i.imgur.com/oGLF63Q.png)

- HSB = HSV 
    > 認為飽和度是從白色(0%) ~ 選擇的色相(100%)
    - Hue: 透過 360 度來決定顏色
    - Saturation: 透過 0 ~ 100%(半徑) 來決定飽和度
    - Brightness: 透過 0 ~ 100%(深) 來決定明度
        - 0% = 黑色
    - ![](https://i.imgur.com/CESCgDH.png)
- HSL (HLS)
    > 飽和度是從灰色(0%) ~ 選擇的色相(100%)
    > 而白色是 Lightness 100% 時顯示的顏色
    - Hue: 透過 360 度來決定顏色
    - Saturation: 透過 0 ~ 100%(半徑) 來決定飽和度
    - Lightness: 透過 0 ~ 100%(深) 來決定亮度
    - ![](https://i.imgur.com/eJskjkW.png)
    - ![](https://i.imgur.com/47basG9.png)
- LAB
    - Lighitness: 0(黑) ~ 100%(白)
    - 維度 A (對立顏色): -128(綠) ~ 127(紅)
    - 維度 B (對立顏色): -128(藍) ~ 127(黃)
    - ![](https://i.imgur.com/od2XtCY.png)
- RGB / BGR 紅綠藍三維度
- RGBA 紅綠藍加上透明度四維度

```python=
import cv2

# 模式
# BGR to HSV
# cv2.COLOR_BGR2HSV
# BGR to HSL(HLS)
# cv2.COLOR_BGR2HLS
# BGR to LAB
# cv2.COLOR_BGR2LAB

cv2.cvtColor(ImageSrc, 模式)
```