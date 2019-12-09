### 影像處理 - 仿射變換 | Affine Transformation

#### 觀念補充
> [Ref 计算机视觉-运动类型总结](https://blog.csdn.net/Anderson_Y/article/details/85759502)
> [Ref 仿射變換及其變換矩陣的理解](https://www.itread01.com/content/1559217783.html)

- 影像處理包含好幾類
    ![](https://i.imgur.com/zcF2mLC.png)
    ![](https://i.imgur.com/WxjLL2m.png)
    ##### 仿射 Affine
    1. 平行不變
    2. 中點不變
    - Translation 平移
        - 具有兩個自由度 (Degree of free) $t_x$、$t_y$
        - $x'=x+t$
        - 公式圖 ![](https://i.imgur.com/0E71ti0.png)
        - 平行、長度、面積、內夾角都不會改變
    - Rotation 旋轉
        - 具有一個自由度 (Degree of free) $\theta$
        - $x'=R(\theta)*x$
        - $R(\theta) = \begin{bmatrix} cos(\theta) & -sin(\theta) \\ sin(\theta) & cos(\theta) \end{bmatrix}$
        - 公式圖 ![](https://i.imgur.com/wp1Qr5V.png)
        - 平行、長度、面積、內夾角都不會改變
    - Euclidean(Rotation + Translation) 歐氏幾何
        - 具有三個自由度 (Degree of free) $\theta$、$t_x$、$t_y$
        - $x'=R(\theta)*x+t$
        - 公式圖 ![](https://i.imgur.com/YRgjU8f.png)
        - 平行、長度、面積、內夾角都不會改變
    - Similarity 近似
        - 具有四個自由度 (Degree of free) $\theta$、$t_x$、$t_y$、$s$
        - $x'=sR(\theta)*x+t$
        - 公式圖 ![](https://i.imgur.com/cFxifEv.png)
        - 會產生縮放，故平行、內夾角都不會改變，面積比也不會改變
    - Affine 仿射
        - 具有四個自由度 (Degree of free) $A_{2x2}$(Matrix/非奇異矩陣)、$t_x$、$t_y$
        > [非奇異矩陣](https://zh.wikipedia.org/wiki/%E9%9D%9E%E5%A5%87%E5%BC%82%E6%96%B9%E9%98%B5)意旨矩陣中不包含 0 
        - $x'=A_{2x2}*x+t$
        - 公式圖 ![](https://i.imgur.com/1wfTJIT.png)
        - 平行線、平行線段的長度比、面積比保持不變
    - Projective 射影幾何
        - 具有八個自由度 (Degree of free) $A_{2x2}$(Matrix/非奇異矩陣)、$t_x$、$t_y$、$v_{1x3}$
        - $\bar{x'}=\begin{bmatrix} A_{2x2} & t_{2x1} \\ v_{1x3} & 1 \end{bmatrix} * x$
        - 公式圖
        - 通通都會變
- 這些影像轉換處理的相依關係
    ![](https://i.imgur.com/pYAN3gE.png)

#### 旋轉縮放

1. 產生旋轉矩陣
```python=
rows, cols = img.shape[:2]

# cv2.getRotationMatrix2D(中⼼心位置, 旋轉⾓角度, 縮放倍率)
M_rotate = cv2.getRotationMatrix2D((cols//2, rows//2), 45, 0.5)
```
2. Apply 仿射
```python=
cv2.warpAffine(img, M_rotate, (cols, rows))
```

#### 點對應仿射
> [Ref 每天一练P18-Python和OpenCV做图像处理(getAffineTransform)](https://zhuanlan.zhihu.com/p/36980767)
> [Ref Opencv-Python学习笔记五——图像翻转，平移，仿射及透视 warpAffine
](https://www.jianshu.com/p/ef67cacf442c)

1. 定義座標組
```python=
rows, cols = img.shape[:2]
pt1 = np.array([[50,50], [300,100], [200,300]], dtype=np.float32)
pt2 = np.array([[80,80], [330,150], [300,300]], dtype=np.float32)
```
2. 建立仿射矩陣
```python=
M_affine = cv2.getAffineTransform(pt1,pt2)
img_affine = cv2.warpAffine(img, M_affine, (cols, rows))
```
3. 可以標記點來看效果
```python=
img_copy = img.copy()
for idx, pts in enumerate(pt1):
    pts = tuple(map(int, pts))
    cv2.circle(img_copy, pts, 3, (0, 255, 0), -1)
    cv2.putText(img_copy, str(idx), (pts[0]+5, pts[1]+5), cv2.FONT_HERSHEY_COMPLEX, 1, (0, 255, 0), 1)

for idx, pts in enumerate(pt2):
    pts = tuple(map(int, pts))
    cv2.circle(img_affine, pts, 3, (0, 255, 0), -1)
    cv2.putText(img_affine, str(idx), (pts[0]+5, pts[1]+5), cv2.FONT_HERSHEY_COMPLEX, 1, (0, 255, 0), 1)
```