### 圖片矩陣操作 | Image array operate

#### 垂直、水平翻轉 Flip
> 圖片矩陣表示 image[Height, Width, Layer]
> - 矩陣操作
>   - list[start : end : step] 從 Start 位置開始到 End 位置，每次走 Step 步
>   - 不寫則是從頭到最尾端
>   ```python=
>   a = [1,2,3,4,5]
>   a[::-1] # [5,4,3,2,1]
>   a[4:2:-1] # [5,4]
>   ```

- 垂直翻轉
    - image[::-1,:,:]
- 水平翻轉
    - image[:,::-1,:]

#### 縮放 Scale

1. 指定大小, 如：長 300 x 寬 400
```python=
cv2.resize(img, (300,400))
```
2. 指定倍數, 如：長 3 倍, 寬 4 倍
```python=
cv2.resize(img, None, fx = 3, fy = 4)
```

- 縮放操作
    - `cv2.INTER_NEAREST` 最鄰近插點法
    - `cv2.INTER_LINEAR` 雙線性插補(預設)
        - 參考周遭四個點的距離去決定權重 (比較不會有鋸齒狀邊緣) ![](https://i.imgur.com/3oCPImV.png)
    - `cv2.INTER_AREA` 臨域像素再取樣插補
    - `cv2.INTER_CUBIC` 雙立⽅方插補，4×4⼤大⼩小的補點
        - ![](https://i.imgur.com/wyt2rD1.png)
    - `cv2.INTER_LANCZOS4` Lanczos插補，8×8⼤大⼩小的補點
    :::info
    縮小建議用 `INTER_AREA`
    放大建議用 `INTER_CUBIC` or `INTER_LINEARINTER_AREA`
    :::
    
- 平移操作
    - `x' = ax+cy+e;`、`y' = bx+dy+f`
    - 建一個 np array 決定移動位置, x 移動 100, y 移動 50 (pixel)
        ```python=
         np.array([[1, 0, 100],
         [0, 1, 50]], dtype=np.float32)
        ```
    - 透過 `cv2.warpAffine(img, Matrix, (column, row))` 變換
    - ![](https://i.imgur.com/gwnkDOK.png)