---
layout: post
title: [HALCON]灰度阈值 
date: 2022-07-11 12:30 +0800
tags: [HALCON]
author: LMCube
math: true
toc: true
---
# 灰度图像及阈值
### 灰度值
灰度图像中灰度共有256个级别，从0到255
![灰度图例](https://img1.baidu.com/it/u=765716361,3100067418&fm=253&fmt=auto&app=138&f=JPEG?w=720&h=429)
256级灰度图像中0为纯黑，255为纯白

### 读取
~~~
read_image ( ImageName , 'F:/image.jpg')
~~~
读取指定文件夹内图像，并赋予ImageName
可在后去调用

### 转换
~~~
rgb1_to_gray( targetImage , OutPutImage )
~~~
rgb1_to_gray算子可将目标图像转换为灰度图像，并将新图像赋予至新变量名内

### 阈值
HALCON中，threshold算子的 Region（可改命名变量）可以设定高亮显示图像中某阈值以上的部分
~~~
threshold (GrayImage , Region , 70 , 100)
~~~
读取灰度图像，声明变量区间Region，读取灰度值位于70到100之间的像素并高亮显示

### 阈值分割