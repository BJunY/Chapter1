#**PRML学习心得：Chapter1---Introduction**
---
本章主要介绍了机器学习的3种重要理论：概率理论（Probability Theory）、决策理论（Decision Theory）以及信息学理论（Information Theory），并根据多项式曲线拟合这一实例引出了解决机器学习的一般流程，包括模型选择（Model Selection）、过拟合（overfitting）以及维度灾难等问题。
______
##**概率理论（Probability Theory)**
###   概率理论中最为基本的两大定理：加法定理与乘法定理，
   几乎所有复杂的概率理论都是基于下面这两个式子推导出来的，因此一定要深刻理解式子的含义。而我自认为概率理论在PRML一书中也算是最难理解的部分了。
            加法定理：$$p(X) = \sum_Yp(X, Y)$$
            乘法定理：$$p(X, Y) = p(Y|X)p(X)$$
___
###贝叶斯定理（后验分布的求解）
这是贯穿PRML一书中另外一个重要的定理， 其原理很简单：posterior ~ likelihood * prior，可以用如下式子来表示：$$p(Y|X) = \frac{p(X|Y)p(Y)}{p(X)}$$
                                  $$p(X) = \sum_Yp(X|Y)p(Y)$$
##**决策理论（Decision Theory）**
###解决决策问题的3种方法：
1. 利用贝叶斯的观点，对于生成模型（generative model），如高斯判定模型（GDA），朴素贝叶斯模型
2. 利用频率的观点，对应于判定模型（descrimitive model），如逻辑回归（Logistic Regression）.
3. 直接利用判定函数（descimiant function）,如感知机（Perceptron）、费时判定（Fisher Descimiant）
这一部分内容会在第4章讲解分类问题时，会详细讲解
##**信息学理论 （Information Theory）**
### 熵（entropy）的概念
若为离散变量，则熵定义为：$$H[p] = - \sum_ip(x_i)lnp(x_i)$$ 其中熵最大时的分布为$p(x_i) = \frac{1}{M}$  ，其中M为离散变量可能出现的情况的个数。           
若为连续变量，则熵定义为：$$H[x] = - \int p(x)lnp(x)$$                                    
其中熵最大时的分布为:$p(x)$服从高斯分布
###条件熵
$$H[Y|X] = -\int\int p(y, x)lnp(y|x)dydx $$$$H[x,y] = H[x] + H[y|x]$$  
###杰森不等式(Jensen's inequality)
$$f\left(\sum_{i=1}^M\lambda_ix_i\right) \leq \sum_{i=1}^M\lambda_if(x_i)$$ 
###KL距离（Kullback-Leibler divergence）
$$KL(p||q) = -\int p(x)lnq(x)dx - \left(-\int p(x)lnp(x)dx\right)=  -\int p(x)ln\frac{q(x)}{p(x)}dx $$
由Jessen不等式可知：$$KL(p||q)\geq -\int ln\left(p(x)\frac{q(x)}{p(x)}dx\right) = - \int lnq(x) \geq0$$当且仅当$p(x) = q(x)$时等号成立，KL距离在PRML后边章节运用很多，要明白具体含义。
###ML（Mutual Information）
$$I[x, y] \equiv KL(p(x, y) || p(x)p(y) = - \int\int p(x, y)ln\left(\frac{p(x)p(y)}{p(x, y)}\right)dxdy$$
与熵的关系：$$I[x,y] = H[x] – H[x|y] = H[y] – H[y|x]$$
ML可以通过比较特征与输出的相关性，进行特征选取(feature extraction)，PRML一书中Learning Theory提到的较少，具体可参考[Andrew Ng斯坦福公开课Feature Selection部分](http://open.163.com/special/opencourse/machinelearning.html)
##**其他问题**
   1. 机器学习问题的分类
       监督学习（Supervised learning），无监督学习（Unsupervised learning）以及强制学习（Reinforcement learning）
   2.  机器学习中的过拟合问题(overfitting)
      过拟合的问题实质是模型对于训练样本的契合度过高，以至于可能对于测试样本（或者预测样本）的预测误差较大，泛化（genarization）能力较差。
      预防过拟合的方法：
          a.	合适的特征数量
          b.	数量足够大的数据集，一般数量为特征数量的5~10倍为宜
          c.	利用贝叶斯的角度去考虑问题，具体来说利用MAP(Maximum a Posterior)而少用     ML（Maximum       Likelihood）
          d.	利用修正（Regularization）的方法添加惩罚项
          e.	利用交叉验证的方法选择合适的模型
***
<font color=red size=5>PS.终于写完了，第一次写这么长的博客，又是第一次用MarkDown编辑器来写，费了好大功夫，有错误的地方欢迎指正哈~</font>
       
