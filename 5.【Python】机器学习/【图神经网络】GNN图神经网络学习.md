####  一、推荐系统和推荐算法
####  二、GNN（Graph Neural Networks）：图神经网络
##### （一) 传统神经网络存在的不足
* 传统的神经网络和扩展模型在语音、图像、自然语言处理领域都取得了巨大的突破，但处理的数据均为序列或网格数据，均为结构化数据；
* 面对非结构化的数据，比如：社交网络、交通网络、知识图谱等，如果用相同的解决策略，存在：
1. 图的大小是任意的，图的拓扑结构复杂，不具备照片等图片的空间局部性
2. 图没有固定的节点顺序，或者说没有一个参考节点
3. 图经常是动态图，而且包含多模态的特征
* 以常见的VGG16模型为例，该模型要求输入必须为（224 x 224 x 3）；
##### （二) GNN解决的问题
* CNN无法处理Non Euclidean Structure的数据，学术上的表达是传统的离散卷积，在Non Euclidean Structure的数据上无法保持平移不变性；
* 可以理解为在拓扑图中每个顶点的相邻顶点数目都可能不同，那么当然无法用一个同样尺寸的卷积核来进行卷积运算；
* GNN就是在这样的背景下产生的，图神经网络可以有效地提取图形的空间特征；
* 由于CNN无法处理Non Euclidean Structure的数据，又希望在这样的数据结构（拓扑图）上有效地提取空间特征来进行机器学习，所以GCN成为了研究的重点。
* 广义上来讲任何数据在赋范空间内都可以建立拓扑关联，谱聚类就是应用了这样的思想（谱聚类）。所以说拓扑连接是一种广义的数据结构，GCN有很大的应用空间
##### （三) 理解GNN
###### （i）理解何为“图”
* 数学（图论）中的用顶点和边建立相应关系的拓扑图；
* 可以将图神经网络中的“图”，以相同的形式理解为数据结构中的图，包含顶点和边的数据结构；
###### （ii）数学基础：拉普拉斯算子
* 散度的概念：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710073126122.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710073159120.png)
* 拉普拉斯【概念】：拉普拉斯算子或是拉普拉斯算符是由欧几里得空间中的一个函数的梯度的散度给出的微分算子；
* 拉普拉斯【定义】：对函数f先做梯度运算，再做散度运算；
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710073616984.png)
###### （iii）数学基础：拉普拉斯矩阵
* 简单图的拉普拉斯矩阵【定义一】：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710073743886.png)
其中D为简单图的度矩阵，A为简单图的邻接矩阵；
* 简单图的拉普拉斯矩阵【定义二】：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710074051580.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
* 简单图的拉普拉斯计算【举例】：
1. 【标记图】G：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710074344480.png)
2.【 度矩阵】D
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710074333144.png)
3.【邻接矩阵】A
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710074354374.png)
4.【拉普拉斯矩阵】L
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710074404374.png)
2. 拉普拉斯矩阵还常做归一化处理，具体包括：
* 对称归一化：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710074608538.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
* 随机游走归一化：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710074626248.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
###### （iv）数学基础：傅里叶变换
* 略
* 比较于神经网络最基本的网络结构全连接层（MLP），特征矩阵乘以权重矩阵，图神经网络多了一个邻接矩阵。
* 具体计算形式为三个矩阵相乘再加上一个非线性变换。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710071306832.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
##### （四) GNN结构

> 对GNN结构出现的理解：真实世界中，许多重要的数据集都是以图或者网络的形式存在的，比如社交网络，知识图谱，蛋白质相互作用网，世界贸易网等等。GNN的出现就是将神经网络一般化并应用在任意图结构数据中的尝试

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710075140452.png)
###### （i）GNN模型的目标是要学习图G=（V，E）上的信号或特征的一个映射
###### （ii）基本GNN模型的输入：
* 每一个节点i的特征描述 Xi ，可以写成一个N*D的特征矩阵（N表示节点数，D表示输入的特征数）
* 矩阵形式的图结构的特征描述，通常是以邻接矩阵的形式（或者其他的形式）
###### （iii）基本GNN模型的输出：
* 模型会产生一个节点级别的输出Z（一个N*F的特征矩阵，其中F表示每一个节点的输出特征数）；
###### （iv）基本GNN模型的hidden层：
* 每一层神经网络都可以视为一个映射函数H（l）
* L为层数
* A为图的邻接矩阵
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020071008010333.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
* 模型会产生一个节点级别的输出Z（一个N*F的特征矩阵，其中F表示每一个节点的输出特征数）；
###### （v）GNN研究的重点：设计映射函数f（）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710080256646.png)
* 谱卷积方式

> 《Semi-Supervised Classification with Graph Convolutional Networks》

* 空间域卷积方式

> 《Learning Convolutional Neural Networks for Graphs 》

####  三、经典模型GCN
[《Semi-Supervised Classification with Graph Convolutional Networks》](https://arxiv.org/pdf/1609.02907.pdf)
##### （一) 基本信息
###### （i） 传统的GNN的模型计算

> 对于一个大图（例如“文献引用网络”），我们有时需要对其上的节点进行分类。然而，在该图上，仅有少量的节点是有标注的。此时，我们需要依靠这些已标注的节点来对那些没有标注过的节点进行分类，此即半监督节点分类问题。在这类问题中，由于大部分节点都没有已标注的标签，因此往往需要使用某种形式的图正则项对标签信息进行平滑（例如在损失函数中引入图拉普拉斯正则（graph Laplacian regularization））：
> -。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710152329809.png)
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710153353200.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
###### （ii）模型结构（两层的GCN为例）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710152355521.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
###### （iii）具体流程
1. 首先获取节点的特征表示X ，并计算邻接矩阵 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710103307210.png)
2. 将其输入到一个两层的GCN网络中，得到每个标签的预测结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710152621146.png)
其中，
* W0为第1层隐藏层的权值矩阵，用于映射隐藏层；
* W1为第2层输出层的犬只矩阵，用于映射输出层；
* 通过softmax函数输出每一个标签的预测结果；

##### （二）数学推导
###### **【归一化拉普拉斯矩阵】**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710110412268.png)
* 矩阵的特征向量为U
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710111033403.png)
###### **【Motivation 谱图卷积】一阶局部近似**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710110919240.png)
* 滤波器
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710111445304.png)
* 谱卷积表示
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710152530423.png)
* 计算量较大 -> 使用近似计算
1. 进行矩阵乘法运算的计算复杂度为 O(n的平方);
2. 计算大图的拉普拉斯矩阵 [公式] 的特征分解需要很大的计算量。
3. 使用切比雪夫多项式（Chebyshev polynomial） k阶截断 Tk 来获得近似输出：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710152726649.png)
* 使用近似表达式进行替换
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710112325509.png)
* 再次进行替换
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710112551687.png)
* 最终获得
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710112625655.png)
* 通过观察表达式可以发现
谱图卷积不再依赖于整个图，而只是依赖于距离中心节点K步之内的节点（K阶邻居）
###### 【Layer-wise线性模型】
> 进一步简化运算

* 令K = 1,则表达式进一步展开为：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710153019346.png)
* 进行约束后，展开为：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710153002963.png)
* 为解决梯度消失/梯度爆炸问题：renormalization trick
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710153102249.png)
其中，
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710153140201.png)
* 把节点向量代入，再次进行变换，得到：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710152940285.png)
* 理解
1. 每个节点的节点表示被更新成了一个新的N 维向量；
2. 该 N维向量包含了节点的相应的一阶邻居上的信息；
###### 【图卷积神经网络】
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200710152454179.png)
* 解析
* 第l层的输入为H(l)，初始输入H(0)为X；
* N为节点数量，每个节点通过D维的特征向量表示；
* W(l)是被训练的权重参数
* 最后为激活函数



##### （四)  总结
* 提出了一种图卷积神经网络，该网络可以被有效地用于处理图结构的数据；
* 局部特性：图卷积神经网络关注的是图中以某节点为中心，K阶邻居之内的信息，这一点与GNN有本质的区别；
* 一阶特性：经过多种近似之后，GCN变成了一个一阶模型。也就是说，单层的GCN可以被用于处理图中一阶邻居上的信息；若要处理K阶邻居，可以采用多层GCN来实现；
* 参数共享：对于每个节点，其上的滤波器参数W是共享的，这和CNN卷积神经网络类似。

