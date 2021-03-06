---
title: Moravec角点检测
date: 2015-01-01 11:00:00
categories: fbFeature
---

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

<!--<img src="http://latex.codecogs.com/gif.latex? a^{i}"/>
<center><img src="{{ site.baseurl }}/images/pdBase/svm_smo1.png"></center>-->

### 概述

   <strong>一种基于灰度方差的角点检测方法。通过滑动二值矩形窗口寻找灰度变化的局部最大值。该算子计算图像中某个像素点沿着水平、垂直、两个对角线四个方向的灰度方差，其中的最小值选为该像素点的角点响应值，再通过局部非极大值抑制来检测是否为角点。</strong>

步骤：

1. 设定窗口，遍历全图，在w*w窗口中计算四个方向相邻像素灰度差的平方和：<img src="{{ site.baseurl }}/images/pdBase/fea_mor1.png">。其中k=w/2。取其中的最小者作为该窗口中心对应像素的兴趣值。
		
2. 给定一经验阈值，将兴趣值大于该阈值的点（即窗口的中心点）作为候选点。阈值的选择应以候选点中包括所需要的主要特征点而又不含过多的非特征点为原则。

3. 在一定大小的窗口内取一个兴趣值最大者的像素点作为特征点。

---

缺点：

1. 对倾斜边缘的相应很强，值考虑了每隔45度的方向变化，利用了像素点四个方向的灰度方差，而没有在全部方向上进行考虑，使得该算子明显具有方向上的局限性，不能反映其他方向上的灰度信息。

2. 由于窗口函数是一个二值函数，不管像素点距离中心点的距离，赋予一样的权重，因此对噪声相应较强。对噪声没有抑制作用。

3. 因为选取了图像像素点四个方向上的灰度方差最小值作为角点相应值进行判定，所以对边缘相应较为敏感，会错把非角点当作角点。

---

总结：虽快，但不很准。


