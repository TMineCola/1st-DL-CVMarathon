### 圖片繪圖 | Draw in image

#### 繪製直線
```python=
# 從 x1, y1 畫線到 x2, y2
cv2.line(image, (x1, y1), (x2, y2), (B, G, R), 線寬)
```

#### 繪製矩形
```python=
# 以 x1, y1 及 x2, y2 為左上及右下頂點繪製矩形, 線寬如果是 -1 代表填滿
cv2.rectangle(image, (x1, y1), (x2, y2), (B, G, R), 線寬)
```

#### 繪製文字
> 字型參考 [Ref](https://codeyarns.com/2015/03/11/fonts-in-opencv/)
```python=
# 以左下角 x1, y1 為基礎繪製文字
cv2.putText(image, 'Text', (x1, y1), 字型, 大小, (B, G, R), 粗細)
```