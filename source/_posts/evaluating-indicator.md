---
title: 机器学习相关评估指标，分类，回归，聚类
date: 2019-02-18 21:02:18
tags: deeplearning
categories: 学习笔记
mathjax: true
---

# 分类算法



## 混淆矩阵

|          |      | 实际表现 |      |
| -------- | :--: | :------: | :--: |
|          |      |   1  P   | 0  N |
| 预测表现 | 1  P |    TP    |  FP  |
|          | 0  N |    FN    |  TN  |



<!--more-->



**P（Positive）：** 代表分类1

**N（Negative）：** 代表分类0

**T（True）：** 代表预测正确

**F（False）：** 代表预测错误

于是乎:

**TP：** 预测为1，预测正确，实际1

**FP：** 预测为1，预测错误，实际0

**FN：** 预测为0，预测错确，实际1

**TN：** 预测为0，预测正确，实际0



## 准确率

准确率的定义是**预测正确的结果占总样本的百分比** .

准确率=**(TP+TN)/(TP+TN+FP+FN)** 

**样本不平衡**的情况下，并不能作为很好的指标来衡量结果。 

##  精准率

精准率（Precision）又叫**查准率**，它是**针对预测结果**而言的，它的含义是**在所有被预测为正的样本中实际为正的样本的概率**，意思就是在预测为正样本的结果中，我们有多少把握可以预测正确，其公式如下：

精准率=**TP/(TP+FP)** 

###  精准率与准确率区别

精准率代表对正样本结果中的预测准确程度，而准确率则代表整体的预测准确程度，既包括正样本，也包括负样本。 

## 召回率

召回率（Recall）又叫**查全率**，它是**针对原样本**而言的，它的含义是**在实际为正的样本中被预测为正样本的概率**，其公式如下：

精准率=**TP/(TP+FN)**

## F1分数

通常，如果想要找到二者之间的一个**平衡点**，我们就需要一个新的指标：**F1分数**。F1分数同时考虑了查准率和查全率，让二者同时达到最高，取一个平衡。

F1分数 = 2\*查准率\*查全率 / (查准率 + 查全率)

## P-R曲线（查准率-查全率）

横坐标为查全率（召回率（Recall）），纵坐标为查准率（精准率（Precision） ） 

## 真正率&假正率

灵敏度（Sensitivity） = **TP/(TP+FN)**

特异度（Specificity） = **TN/(FP+TN)**

真正率（TPR） = 灵敏度 = **TP/(TP+FN)**

假正率（FPR） = 1- 特异度 = **FP/(FP+TN)**

 ## ROC（接受者操作特征曲线）

横坐标为假正率（FPR），纵坐标为真正率（TPR） 

## AUC（曲线下的面积）

**AUC的一般判断标准**

**0.5 - 0.7：** 效果较低，但用于预测股票已经很不错了

**0.7 - 0.85：** 效果一般

**0.85 - 0.95：** 效果很好

**0.95 - 1：** 效果非常好，但一般不太可能

# 回归算法
f表示预测值，y表示实际值
## MAE(Mean Absolute Error) 平均绝对误差 
平均绝对误差MAE（Mean Absolute Error）又被称为 *l1* 范数损失

$$MAE = \frac{ 1}{ n}\sum\limits_{ i = 1}^n { \left| { { f_i} - { y_i}} \right|} $$



### MAE不足
MAE虽能较好衡量回归模型的好坏，但是绝对值的存在导致函数不光滑，在某些点上不能求导，可以考虑将绝对值改为残差的平方，这就是均方误差。

## MSE(Mean Square Error) 平均平方差/均方误差 
均方误差MSE(Mean Squared Error)又被称为 *l2* 范数损失

$$MSE = \frac{ 1}{ n}\sum\limits_{ i = 1}^n { { { \left( { { f_i} - { y_i}} \right)}^2}} $$

### MSE不足
MSE和方差的性质比较类似，与我们的目标变量的量纲不一致，为了保证量纲一致性，我们需要对MSE进行开方得到RMSE。

## RMSE(Root Mean Square Error) 均方根误差 

$$RMSE = \sqrt { MSE}  = \sqrt { \frac{ 1}{ n}\sum\limits_{ i = 1}^n { { { \left( { { f_i} - { y_i}} \right)}^2}} } $$
### RMSE不足

上面的几种衡量标准的取值大小与具体的应用场景有关系，很难定义统一的规则来衡量模型的好坏。比如说利用机器学习算法预测上海的房价RMSE在2000元，我们是可以接受的，但是当四五线城市的房价RMSE为2000元，我们还可以接受吗？下面介绍的决定系数就是一个无量纲化的指标。 

## **R2**（R-Square）决定系数Coefficient of determination
$ \bar y $ 表示观测数据的平均值

### 残差平方和

$$S{ S_{ res}} = \sum\limits_{ i = 1}^n { { { \left( { { f_i} - { y_i}} \right)}^2}}$$

### 总平方和

$$
 S{ S_{ tot}} = \sum\limits_{ i = 1}^n { { { \left( { { y_i} - \bar y} \right)}^2}} 
$$

### R方

$$
 { r^2} = 1 - \frac{ { S{ S_{ res}}}}{ { S{ S_{ tot}}}} = 1 - \frac{ { \sum\limits_{ i = 1}^n { { { \left( { { f_i} - { y_i}} \right)}^2}} }}{ { \sum\limits_{ i = 1}^n { { { \left( { { y_i} - \bar y} \right)}^2}} }}
$$

分母理解为原始数据的离散程度，分子为预测数据和原始数据的误差，二者相除可以消除原始数据离散程度的影响

## Adjusted R-Square (校正决定系数）

$$
 r_{ adj}^2 = 1 - \frac{ { \left( { 1 - { r^2}} \right)\left( { n - 1} \right)}}{ { n - p - 1}}
$$

n为样本数量，p为特征数量
消除了样本数量和特征数量的影响




# 聚类算法

## 轮廓系数（Silhouette Coefficient） 
对于其中的一个点 i 来说：




$$a(i) = average(i向量到所有它属于的簇中其它点的距离)$$



$$b(i) = min
(i向量到各个非本身所在簇的所有点的平均距离)$$


那么 i 向量轮廓系数就为：

$$ s\left( i \right) = \frac {    {   b\left( i \right) - a\left( i \right)}} {    {   \max \left\ {     {   a\left( i \right)
,b\left( i \right)} \right\}}} = \left\ {     {   \begin {   array} {   * {   20} {   c}}
   {   1 - \frac {    {   a\left( i \right)}} {    {   b\left( i \right)}}}& {   
   ,a\left( i \right) < b\left( i \right)} &  \\ 
  0& {   
  ,a\left( i \right) = b\left( i \right)} &  \\ 
   {   \frac {    {   b\left( i \right)}} {    {   a\left( i \right)}} - 1}& {   
   ,a\left( i \right) > b\left( i \right)} &  
\end {   array}} \right. $$