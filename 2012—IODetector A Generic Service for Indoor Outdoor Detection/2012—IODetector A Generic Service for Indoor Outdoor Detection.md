# IODetector A Generic Service for Indoor Outdoor Detection

## 1. Introduction

GPS传感器耗能多且不能准确判断用户位置是在室内还是urban canyons或是半独立式住宅。

本文关键动机：

在本文中，我们提出了一个使用SenseIO的现实且无处不在的基于Android的室内智能手机检测系统。



## 3. System design

### 3.1 System overview

IODetector 主要使用三种轻量级的检测器：light detector；cellular detector; magnetism detector。

### 3.2 Light detector 

#### 3.2.1 Light intensity measurement

Light detector主要检测光强，一般来说自然光强大于室内光强即使实在多云和雨天。

室外自然光强范围：大于2000Lux

室内光强范围：100Lux

#### 3.2.2 Detection process in light detector

![image-20200326172727779](image-20200326172727779.png)

$L$是测量的光强；$\sigma_1=2000$Lux、$\sigma_2=50$Lux为阈值，如果光线传感器可用：

* $L > \sigma_1$：有很高的可能性在室外；
* $L \leq \sigma_1$：需要去进一步判断是在室内还是在晚上的室外/半室内
  * 如果当前时间为白天，则有很大可能在室内
  * 如果是晚上，则比较$L$和$\sigma_2$的大小
    * $\sigma_2 < L \leq \sigma_1$：在室内的概率为$\frac{\sigma_1-L}{\sigma_1}$
    * $L \leq \sigma_2$: 在室外的概率为$\frac{\sigma_2-L}{\sigma_2}$

