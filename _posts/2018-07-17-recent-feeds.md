---
layout: post
title: "Recent feeds"
date: 2018-07-17
permalink: /knowledge/:year/:month/:day/:title
section: "knowledge"
---

### About
A brief summary of what I read about recently.

### Machine learning and knowledge discovery
A brief introduction about common interestingness discovery algorithms categorized into different types of machine learning algorithm: classification, association, clustering, correlation and others.

### Decision tree
Concepts of CHI-squre (CHAID), Bonferonni adjustment, Gini coeeficient (C&RT), purity and balance, tree pruning, stopping rules (parent-child sample size, tree depth, significance level vs impurity level), exhaustive CHAID (conservative?)

### 最大似然估计(MLE) VS 最小二乘估计(LSE)
最小二乘估计，最合理的参数估计量应该使得模型能最好地拟合样本数据，也就是估计值和观测值之差的平方和最小。
最大似然法，最合理的参数估计量应该使得从模型中抽取该n组样本观测值的概率最大，也就是概率分布函数或者说是似然函数最大。
最大似然法需要已知这个概率分布函数，一般假设其满足正态分布函数的特性，在这种情况下，最大似然估计和最小二乘估计是等价的，也就是说估计结果是相同的，但是原理和出发点完全不同。

### 马尔科夫链模型
转移概率矩阵。
马尔可夫过程：将来的状态分布只取决于现在，跟过去无关。
马尔可夫链：时间、状态都是离散的马尔可夫过程称为马尔可夫链。

### 隐马尔科夫模型
隐含状态数量，转换概率，可见状态链，隐含状态链（H一个会随时间改变的隐藏的状态，在持续地影响它的外在表现）。
HMM的五样“要素”：
1. 状态和状态间转换的概率
2. 不同状态下，有着不同的外在表现的概率。
3. 最开始设置的初始状态
4. 能转换的所有状态的集合
5. 能观察到外在表现的结合
Hidden 说明的是状态的不可见性；Markov说明的是状态和状态间是markov chain。这就是为什么叫Hidden Markov Model。
遍历算法，向前算法，向后算法，维特比算法，Baum-Welch算法。

![Figure 1]({{ site.url }}/assets/Markov-models.png){:class="post-image"}

### 最大熵
The maximum entropy principle 保留全部的不确定性，将风险降到最小。
对任何一组不自相矛盾的信息，这个最大熵模型不仅存在，而且是唯一的。而且它们都有同一个非常简单的形式 -- 指数函数。

### GMM
简单理解混合高斯模型就是几个高斯的叠加。

### HMM+GMM语音识别
1. 将waveform切成等长frames，对每个frame提取特征（e.g. MFCC）
2. 对每个frame的特征跑GMM，得到每个frame(o_i)属于每个状态的概率b_state(o_i)
3. 根据每个单词的HMM状态转移概率a计算每个状态sequence生成该frame的概率; 哪个词的HMM 序列跑出来概率最大，就判断这段语音属于该词

### ML方法的分类概况
1. 按照输出空间的不同来分类
    - 二元分类
    - 多元分类
    - 线性回归
    - 逻辑(logistic)回归
    - 结构学习
    - ...
2. 按学习方式分类
    - 监督式学习
        - 常见算法有逻辑回归（Logistic Regression）和反向传递神经网络（Back Propagation Neural Network）
    - 非监督式学习（classification vs clustering）
        - 常见算法包括Apriori算法以及k-Means算法。
    - 半监督式学习
        - 常见算法有图论推理算法（Graph Inference）或者拉普拉斯支持向量机（Laplacian SVM.）。
    - 强化学习
        - 常见算法包括Q-Learning以及时间差学习（Temporal difference learning）。
3. 按照获取输入数据集的方式
    - 批量(batch)学习
    - 线上(online)学习
    - 主动(active)学习
4. 按照算法类似性
    - 回归算法
        - 最小二乘法（Ordinary Least Square），逻辑回归（Logistic Regression），逐步式回归（Stepwise Regression），多元自适应回归样条（Multivariate Adaptive Regression Splines）以及本地散点平滑估计（Locally Estimated Scatterplot Smoothing）
    - 基于实例的算法
        - 常见的算法包括 k-Nearest Neighbor(KNN), 学习矢量量化（Learning Vector Quantization， LVQ），以及自组织映射算法（Self-Organizing Map ， SOM）
    - 正则化方法
        - 常见的算法包括：Ridge Regression， Least Absolute Shrinkage and Selection Operator（LASSO），以及弹性网络（Elastic Net）。
    -  决策树学习
        - 常见的算法包括：分类及回归树（Classification And Regression Tree， CART）， ID3 (Iterative Dichotomiser 3)， C4.5， Chi-squared Automatic Interaction Detection(CHAID), Decision Stump, 随机森林（Random Forest）， 多元自适应回归样条（MARS）以及梯度推进机（Gradient Boosting Machine， GBM）
    - 贝叶斯方法
        - 常见算法包括：朴素贝叶斯算法，平均单依赖估计（Averaged One-Dependence Estimators， AODE），以及Bayesian Belief Network（BBN）。
    - 基于核的算法
        - 常见的基于核的算法包括：支持向量机（Support Vector Machine， SVM）， 径向基函数（Radial Basis Function ，RBF)， 以及线性判别分析（Linear Discriminate Analysis ，LDA)等
    - 聚类算法
        - 常见的聚类算法包括 k-Means算法以及期望最大化算法（Expectation Maximization， EM）。
    - 关联规则学习
        - 常见算法包括 Apriori算法和Eclat算法等。
    - 人工神经网络
        - 重要的人工神经网络算法包括：感知器神经网络（Perceptron Neural Network）, 反向传递（Back Propagation）， Hopfield网络，自组织映射（Self-Organizing Map, SOM）。学习矢量量化（Learning Vector Quantization， LVQ）
    - 深度学习
        - 常见的深度学习算法包括：受限波尔兹曼机（Restricted Boltzmann Machine， RBN）， Deep Belief Networks（DBN），卷积网络（Convolutional Network）, 堆栈式自动编码器（Stacked Auto-encoders）。
    - 降低维度算法
        - 常见的算法包括：主成份分析（Principle Component Analysis， PCA），偏最小二乘回归（Partial Least Square Regression，PLS）， Sammon映射，多维尺度（Multi-Dimensional Scaling, MDS）,  投影追踪（Projection Pursuit）等。
    - 集成算法
        - 常见的算法包括：Boosting， Bootstrapped Aggregation（Bagging）， AdaBoost，堆叠泛化（Stacked Generalization， Blending），梯度推进机（Gradient Boosting Machine, GBM），随机森林（Random Forest）。

### ML数据的分类概况
1. 具体特征（concrete）
2. 原始特征
3. 抽象特征

### Reference
1. [Knowledge discovery and Interestingness Measures](https://pdfs.semanticscholar.org/e626/a350597cbbbd02f4b7b017c5db0862d4ccdc.pdf)
2. [Nine laws of Data Mining](http://khabaza.codimension.net/index_files/9laws.htm)
3. [最大似然估计和最小二乘估计的区别与联系](https://blog.csdn.net/xidianzhimeng/article/details/20847289)
4. [最大似然估计和最小二乘法怎么理解](https://www.zhihu.com/question/20447622)
5. [马尔科夫链模型](https://www.zhihu.com/question/26665048) 
6. [隐马尔科夫模型](https://www.zhihu.com/question/20962240)
7. [一文搞懂HMM](http://www.cnblogs.com/skyme/p/4651331.html)
8. [GMM+HMM语音识别](https://blog.csdn.net/abcjennifer/article/details/27346787)
9. [机器学习介绍和分类](https://blog.csdn.net/databatman/article/details/49184451)
10. [机器学习常见分类和方法](https://www.ctocio.com/hotnews/15919.html)