# 5.Inception V2 V3

2015年由google团队提出，论文地址[Batch Normalization: Accelerating Deep Network Training b y Reducing Internal Covariate Shift](https://arxiv.org/pdf/1502.03167.pdf), [Rethinking the Inception Architecture for Computer Vision](https://arxiv.org/pdf/1512.00567.pdf)

**问题**：representatial bottleneck，特征描述瓶颈是指中间某层对特征空间维度进行较大比例的压缩（比如使用pooling），**导致很多特征丢失**，虽然pooling是CNN结构中必须的功能，但我们可以通过一些优化方法来减少pooling造成的损失。特征数目越多收敛的越快。

**一些特征的结构**

1.卷积分解

将5×5的卷积分解成2个3×3的卷积运算以提升计算速度。
在本文中，作者将n×n的卷积核尺寸分解为1×n和n×1两个卷积。

<img src="D:\CSDN\CNN\figures\图8 卷积分解.png" style="zoom:60%;" />

<center>
    图8 卷积分解
</center>

模块中的滤波器组被扩展（变得更宽而不是更深），以解决特征瓶颈。如果该模块没有被扩展宽度，而是变得更深，那么维度会过多减少，造成信息损失。

<img src="D:\CSDN\CNN\figures\图9 特征扩展.png" style="zoom:70%;" />

<center>
    图9 特征扩展
</center>

2.辅助分类器的效用

辅助分类器在训练前期并没有起什么作用，到了训练的后期才开始在精度上超过没有辅助分类器的网络，并达到稍微高的平稳期。并且，在去除这两个辅助分类器后并没有不利的影响，因此在Inception V1中提到的帮助低层网络更快的训练是有问题的。如果这两个分支有BN或Dropout住分类器的效果会更好，这是BN可充当正则化器的一个微弱证据。

3.高效降低Grid Size

有两种方式：（1）先池化再Inception，（2）先Inception再池化

<img src="D:\CSDN\CNN\figures\图10 降低Grid Size.png" style="zoom:80%;" />

<center>
    图10 降低Grid Size
</center>

左边特征先减少的话容易造成特征丢失，即bottleneck问题；右边会极大增加计算量

![](D:\CSDN\CNN\figures\图11 降低Grid Size_.png)

<center>
    图11 降低Grid Size
</center>

并行操作，一边减小特征图尺寸，一边增加特征图数量

**辅助分类器：**

![](D:\CSDN\CNN\figures\图12 辅助分类器.png)

<center>
    图12 辅助分类器
</center>

![](D:\CSDN\CNN\figures\图13 Inception V3结构.png)

<center>
    图13 Inception V2 V3 结构
</center>
[pytorch实现](https://github.com/gdww97/CNN/blob/master/codes/Inception.py)

**Inception模块**

<img src="D:\CSDN\CNN\figures\图14 InceptionA.png" style="zoom: 67%;" />

<center>
    图14 InceptionA
</center>

<img src="D:\CSDN\CNN\figures\图15 InceptionB.png" style="zoom: 67%;" />

<center>
    图15 InceptionB
</center>

<img src="D:\CSDN\CNN\figures\图16 InceptionC.png" style="zoom: 67%;" />

<center>
    图16 InceptionC
</center>

<img src="D:\CSDN\CNN\figures\图17 InceptionD.png" style="zoom: 67%;" />

<center>
    图17 InceptionD
</center>

<img src="D:\CSDN\CNN\figures\图18 InceptionE.png" style="zoom: 67%;" />

<center>
    图18 InceptionE
</center>