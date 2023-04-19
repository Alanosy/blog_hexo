---
title: opencv调用手机摄像头来进行拍照采集数据
date: 2023-04-19 18:03
tags: [技术分析]
---
第一步：
下载一个工具：IP摄像头（app）,Android，iOS都可以下载
下载安装后，打开app，点击下方的打开IP摄像头服务器，确保手机和电脑处于同一局域网。
同一局域网示例：
示例一：电脑连上手机开的热点
示例二：电脑和手机连上同一个wifi
```python
# coding=utf-8
import cv2
import time

if __name__ == '__main__':

    cv2.namedWindow("camera", 1)
    # 开启ip摄像头
    # admin是账号，admin是密码
    video = "http://admin:admin@192.168.10.107:8081/"  # 此处@后的ipv4 地址需要修改为自己的地址
    capture = cv2.VideoCapture(video)

    num = 0
    while True:
        success, img = capture.read()
        cv2.imshow("camera", img)

        # 按键处理，注意，焦点应当在摄像头窗口，不是在终端命令行窗口
        key = cv2.waitKey(10)

        if key == 27:
            # esc键断开连接
            print("esc break...")
            break
        if key == ord(' '):
            # 保存一张图像到工作目录
            num = num + 1
            filename = "frames_%s.jpg" % num
            cv2.imwrite(filename, img)

    capture.release()
    cv2.destroyWindow("camera")
```
