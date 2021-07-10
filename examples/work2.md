## 损失函数方法补充
### 0-1损失函数(zero-one loss)
0-1损失是指预测值和目标值不相等为1， 否则为0:
特点：

(1)0-1损失函数直接对应分类判断错误的个数，但是它是一个非凸函数，不太适用.

(2)感知机就是用的这种损失函数。但是相等这个条件太过严格，因此可以放宽条件，即满足 |Y-f(x)|<t时认为相等，

### Hinge Loss 

在机器学习中，**Hinge loss**（铰链损失函数）作为损失函数，通常被用于最大间隔算法(maximum-margin)，而最大间隔算法又是SVM(支持向量机support vector machines)用到的重要算法。

Hinge loss专用于二分类问题，标签值y=±1，预测值$\hat{y}$∈R。该二分类问题的目标函数的要求如下：当$\hat{y}$等于+1或者小于等于-1时，都是分类器确定的分类结果，此时的损失函数loss为0；而当$\hat{y}$预测值∈(−1,1)时，分类器对分类结果不确定，loss不为0。显然，当y^=0时，loss达到最大值。


```python
def update_weights_Hinge(m1, m2, b, X1, X2, Y, learning_rate):
    m1_deriv = 0
    m2_deriv = 0
    b_deriv = 0
    N = len(X1)
    for i in range(N):
        # 计算偏导数
        if Y[i]*(m1*X1[i] + m2*X2[i] + b) <= 1:
            m1_deriv += -X1[i] * Y[i]
            m2_deriv += -X2[i] * Y[i]
            b_deriv += -Y[i]
        # 否则偏导数为0
    # 我们减去它，因为导数指向最陡的上升方向
    m1 -= (m1_deriv / float(N)) * learning_rate
    m2 -= (m2_deriv / float(N)) * learning_rate
    b -= (b_deriv / float(N)) * learning_rate
return m1, m2, b
```


## 池化方法补充
Stochastic-pooling（随机池化）：只需对feature map中的元素按照其概率值大小随机选择，即元素值大的被选中的概率也大。而不像max-pooling那样，永远只取那个最大值元素。


## 数据增强方法补充

### 色彩抖动

在实际工程中为了消除图像在不同背景中存在的差异性，通常会做一些色彩抖动操作，扩充数据集合。色彩抖动主要是在图像的颜色方面做增强，主要调整的是图像的亮度，饱和度和对比度。工程中不是任何数据集都适用，通常如果不同背景的图像较多，加入色彩抖动操作会有很好的提升。

### 几何变换类

几何变换类即对图像进行几何变换，包括翻转，旋转，裁剪，变形，缩放等各类操作。

### 颜色变换

包括噪声、模糊、颜色变换、擦除、填充等等。

### GAN

通过生成对抗网络生成同类型的数据。比如生成汽车、人脸图片。通过图像风格迁移的手段，还可以生成同一物体再不同环境下的图片。

## 图像分类方法综述

### 传统方法

#### SVM支持向量机<br></br>
支持向量机（SVM）是一种强大而灵活的有监督机器学习算法是多维空间中超平面上不同类的表示。目标是分裂
将数据集分成类，寻找最大边缘超平面。它建立了一个超平面或一组
高维空间中的超平面和两类之间的良好分离是通过
到任何类中最近的训练数据点距离最大的超平面。真正的力量
该算法的性能取决于所使用的核函数。

#### KNN<br></br>
K-最近邻（K-NN）是一种非参数的惰性学习算法，用于分类和分类
回归。该算法简单地依赖于特征向量和分类器之间的距离
通过在k-最近的例子中找到最常见的类来获得未知的数据点。

### 深度学习方法

#### 卷积神经网络<br></br>
卷积神经网络（CNN，或ConvNet）是一种多层神经网络，旨在通过最少的预处理直接从像素图像中识别视觉模式。这是一个特殊的人工神经网络结构。它包括两个重要的元素，即卷积层和池化层。
<br></br>

#### 迁移学习<br></br>
转移学习是一种机器学习技术，首先在机器上训练神经网络模型与正在解决的问题类似的问题，并且存储在解决过程中获得的知识解决一个问题并将其应用于不同但相关的问题。

