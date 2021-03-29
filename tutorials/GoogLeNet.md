# 4.GoogLeNet

2014年由Google团队提出，论文地址[Going deeper with convolutions](https://arxiv.org/pdf/1409.4842.pdf)

![](..\figures\图4 Inception module.png)

<center>图4 Inception Module</center>

Filter concatenation是指按深度进行拼接，所以每个分支所得的特征矩阵高和宽必须相同。

（b）相对于（a）多了3个1×1的convolutions进行降维
例如：假设feature map depth=512，不使用1×1conv进行降维与使用1×1conv进行降维的参数对比

![](..\figures\图5 Inception.png)

<center>
    图5 使用1×1卷积参数对比
</center>

![](..\figures\图6 GoogLeNet.png)

<center>
    图6 GoogLeNet网络结构
</center>
本文亮点：
1.引入了Inception结构（融合不同尺度的特征信息）
2.使用1×1conv进行降维以及映射处理
3.添加两个辅助分类器帮助训练
4.丢弃全连接层，使用平均池化层（大大减少模型参数）

辅助分类器：加在了4a，4d后面

![](..\figures\图7 Aux classifier.png)

<center>
    图7 辅助分类器
</center>
[pytorch实现](https://github.com/gdww97/CNN/blob/master/codes/GoogLeNet.py)

@torch.jit.unused：此装饰器向编译器指示应忽略函数或方法，并用引发异常的方法代替。 这样，您就可以在尚不兼容TorchScript的模型中保留代码，并仍然可以导出模型。

namedtuple：具名元组。