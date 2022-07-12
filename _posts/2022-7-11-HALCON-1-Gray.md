---
layout: post
title: HALCON-①灰度阈值 
date: 2022-07-11 12:30 +0800
tags: [HALCON]
author: LMCube
math: true
toc: true
---
# 灰度图像及阈值
第一章节，使用HALCON处理灰度图像并使用特定算子对数据进行分割
{: .message }

### 灰度值
灰度图像中灰度共有256个级别，从0到255
![灰度图例](https://img1.baidu.com/it/u=765716361,3100067418&fm=253&fmt=auto&app=138&f=JPEG?w=720&h=429)
256级灰度图像中0为纯黑，255为纯白

### 图像读取
~~~
read_image ( ImageName , 'F:/image.jpg')
~~~
读取指定文件夹内图像，并赋予ImageName
可在后去调用。

### 图像信息转换
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
##### 初步分割
~~~
connection ( Region , ConnectedRegions)
~~~
对互相不连接的阈值进行分割，并配以不同的颜色区分分区
![[HALCON_gray.png]]
其中Region为先前已声明的阈值区间变量

#### 特征直方图
指定特定条件，将不同特征的区域信息以直方图形式呈现，其中每一条柱面为一个特征
![[HALCON_specify.png]]
可选多种特征筛选模式：
| 面积 | area | 宽度 | width | 横向坐标 | column |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 高度 | heigh| 纵向坐标 | row |

#### 进一步分割
通过特征直方图，拖动左右两侧界限调整阈值，选出合适区域后点击插入代码。
代码框内则会自动添加代码，算子为；
~~~
select_shape (SelectedRegions, SelectedRegions1, 'row', 'and', 682.73, 1000)
~~~
参数格式为
图像信息→输出信息→特征模式→“和”模式→阈值下限→阈值上限
可直接有直方图内一键生成。
代码执行后可获得指定图像
![[HALCON_selectshape.png]]

#### 数据获取
~~~
area_center(SelectedRegions , Area, Row, Column)
~~~
area_center 算子，用于读取指定区域的面积，中心坐标。通常配合select_shape算子使用，即选出最终目标区域，然后执行area_center算子。
![[HALCON_center.png]]
