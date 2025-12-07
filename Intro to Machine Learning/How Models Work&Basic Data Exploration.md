---
date: 2025-10-20
aliases:
  - machine_learning_1
tags:
  - Machine_Learning
  - Pandas
location: "[[Machine Learning/]]"
---

**摘自：**[How Models Work](https://www.kaggle.com/code/dansbecker/how-models-work)[Basic Data Exploration](https://www.kaggle.com/code/dansbecker/basic-data-exploration)
# 模型如何工作

## Decision trees  决策树

#### Sample decision tree 简易决策树

通过最简单的决策树来预测房地产价格走势：

![[Pasted image 20251020223503.png]]

它只将房屋分为两类，任何房屋的预测价格都是同一类别房屋的历史平均价格。

从数据中捕捉模式的这一步骤称为**拟合**或**训练**模型。
用于**拟合**模型的数据称为**训练数据** 。

模型拟合完成后，您可以将其应用于新数据， **预测**更多房屋的价格。

#### Improving the Decision Tree  改进决策树
你可以使用具有更多“分支”的决策树来捕获更多因素。
这些决策树被称为“更深”的决策树。

如果决策树还考虑了每栋房屋地块的总面积，则可能如下所示：
![[Pasted image 20251020223807.png]]

您可以通过追踪决策树来预测任何房屋的价格，始终选择与该房屋特征相对应的路径。
房屋的预测价格位于树的底部。底部进行预测的点称为**叶子节点。**

叶子的分割和值将由数据决定，因此现在是时候检查您将要处理的数据了。


# Basic Data Exploration  基础数据探索

## Using Pandas to Get Familiar With Your Data

前置知识
使用[[Pandas/]]加载和探索数据：

![[Pasted image 20251020232114.png]]

## Interpreting Data Description  解释数据描述
相关函数参照笔记：[[Summary Functions and Maps]]

1. 结果显示原始数据集中每列 8 个数字。第一个数字（ **计数** ）显示有多少行具有非缺失值

2. 第二个值是 **mean** ，即平均值。

3. 其下的 **std** 是标准差，用于衡量数值的分散程度。

4. 要解释 **min** 、 **25%** 、 **50%** 、 **75%** 和 **max 的**值，想象一下将每列从低到高排序。 第一个（最小）值是 min 。如果遍历列表的四分之一，你会发现一个大于 25% 的值且小于 75% 的值的数字。这就是 **25% 的**值（读作“25 百分位数”）。50 和 75 百分位数的定义类似， **max** 是最大的数字。