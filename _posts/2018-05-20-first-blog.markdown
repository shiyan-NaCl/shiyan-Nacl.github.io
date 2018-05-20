---
layout: post
title:  "Welcome to Jekyll!"
date:   2018-05-20 23:17:20 +0800
categories: blog
---
#细粒度图像识别初步学习
##说明
本篇文章是[「见微知著」——细粒度图像分析进展综述](https://zhuanlan.zhihu.com/p/24738319)的学习
##overview

**细粒度图像识别**是图像分类中一个难点，它的目标是在一个大类中识别子类，比如说在鸟的大类下识别鸟的种类，在车的大类下，识别车的型号。由于相同的子类中物体的动作姿态可能大不相同，不同的子类中物体可能又有着相同的动作姿态，这是识别的一大难点。不止对计算机，对普通人来说，细粒度图像识别的难度和挑战也很巨大。

细粒度图像分类的关键点在寻找一些存在细微差别的局部区域（比如鸟类的喙、眼睛、爪子等），因此，现有的细粒度图像识别算法不但寻找图像中的整个物体（object），还寻找一些有区别的局部（part）。

##细粒度图像分类

###基于强监督信息的细粒度图像分类模型
所谓“强监督细粒度图像分类模型”是指：在模型训练时，为了获得更好的分类精度，除了图像的类别标签外，还使用了物体标注框（Object Bounding Box）和部位标注点（Part Annotation）等额外的人工标注信息，如下图所示。
![icon](https://pic1.zhimg.com/v2-f04c284bb40f1fc3da258bb6764d4728_r.jpg)

####几个经典模型
Part-based R-CNN
总体流程图为
![icon2](https://pic3.zhimg.com/v2-5f59a4da92c0053a8cfd0f22848ed043_r.jpg)

Pose Normalized CNN
![icon3](https://pic2.zhimg.com/v2-117e00184c8dace2fa14926e9a48f59f_r.jpg)

Mask-CNN
![icon4](https://pic3.zhimg.com/80/v2-9f11420b2343318a55523ee68a22a126_hd.jpg)



###基于弱监督信息的分类模型

思路同强监督分类模型类似，也需要借助全局和局部信息来做细粒度级别的分类。而区别在于，弱监督细粒度分类希望在不借助part annotation的情况下，也可以做到较好的局部信息的捕捉。

当然，在分类精度方面，目前最好的弱监督分类模型仍与最好的强监督分类模型存在差距（分类准确度相差约1～2%）。

###三个弱监督细粒度图像分类模型的代表。
Two Level Attention Model

Constellations

Bilinear CNN
