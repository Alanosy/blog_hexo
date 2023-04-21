---
title: opencv笔记
date: 2023-04-17 16:38
tags: [技术分享]
---
#### 创建和显示
namedWindow() 创建命名窗口
imshow()显示窗口
destroyAllwinds()摧毁窗口
resizewindow()改变窗口大小
waitkey()等待用户输入

#### 显示图片
def cv_show(name, img):
    import cv2
    cv2.imshow(name,img)
    key = cv2.waitKey(0)
    if key & 0xFF == ord('q'):
        cv2.destroyAllWindows()

%run name 执行外部python文件
#### 保存图片
```python
import cv2
cv2.namedWindow('img',cv2.WINDOW_NORMAL)
cv2.resizeWindow('img',640,480)
img = cv2.imread('./IMG_2818.jpg')
while True:
    cv2.imshow('img',img)
    key = cv2.waitKey(0)
    if key == ord('q'):
        break
    elif key == ord('s'):
        cv2.imwrite('./123.jpg',img)
    else:
        print(key)
cv2.destroyAllWindows()
```
