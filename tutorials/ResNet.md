# 6.ResNet

2015年由何恺明提出，论文地址[Deep Residual Learning for Image Recognition](https://arxiv.org/pdf/1512.03385.pdf)

![](D:\CSDN\CNN\figures\图19 Bottleneck Block.png)

<center>
    图19 Basicblock，Bottleneck block
</center>
**注意：**主分支与shortcut的输出特征矩阵shape必须相同，1×1的卷积核用来降维和升维