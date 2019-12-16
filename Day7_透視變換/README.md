### 透視變換 | Perspective Transformation
> 將圖像投影至一個新的平面

#### 仿射 Affine VS 透視 Perspective [Ref](https://blog.csdn.net/flyyufenfei/article/details/80208361)

##### 仿射

- 二維座標到二維座標的線性轉換
- 變換後直線與平行線依然保持
- 為平行四邊形故只需要提供三個點
![](https://i.imgur.com/zHNpqMi.png)


##### 透視

- 二維空間轉到三維空間後再映射回原本的二維空間
- 由於平行關係會改變，故要提供四個點
![](https://i.imgur.com/eMAb3xm.png)

#### 齊次座標
> 可以視為多了一個遠近距離 $w'$

![](https://i.imgur.com/K6wEtFw.png)
![](https://i.imgur.com/p8S4DqA.png)

#### 轉換矩陣

![](https://i.imgur.com/l4OfTZR.png)

#### 點對應透視

1. 建立對應點
```python=
point1 = np.array([[60, 40], [420, 40], [420, 510], [60, 510]], dtype=np.float32)
point2 = np.array([[0, 80], [w, 120], [w, 430], [0, 470]], dtype=np.float32)
```
2. 建立轉換矩陣
```python=
M = cv2.getPerspectiveTransform(point1, point2)
```
3. 轉換
```python=
img_perspective = cv2.warpPerspective(img, M, (w, h))
```

#### More Issue

在問答區有人提出想要抓取圖片中四個點的方法，看到額外有趣的東西
- [書本偵測(四點輪廓)](https://pythontips.com/2015/03/11/a-guide-to-finding-books-in-images-using-python-and-opencv/)