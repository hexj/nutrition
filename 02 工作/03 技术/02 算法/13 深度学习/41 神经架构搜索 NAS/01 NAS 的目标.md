
# NAS 的目标

在开发神经网络的过程中，架构工程事关重大，架构先天不足，再怎么训练也难以得到优秀的结果。

当然，提到架构，很多人会想到迁移学习：

- 把 ImageNet 上训练的 ResNet 拿来，换个我需要的数据集再训练训练更新一下权重，不就好了嘛！

这种方法的确也可行，但是要想得到最好的效果，还是根据实际情况设计自己的网络架构比较靠谱。

设计神经网络架构，能称得上机器学习过程中门槛最高的一项任务了。想要设计出好架构，需要专业的知识技能，还要大量试错。

NAS 就为了搞定这个费时费力的任务而生。
