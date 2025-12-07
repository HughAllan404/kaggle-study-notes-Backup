---
date: 2025-11-02
aliases:
  - machine_learning_5
tags:
  - Machine_Learning
  - Python
location: "[[Machine Learning/]]"
---
**摘自：**[Random Forests](https://www.kaggle.com/code/dansbecker/random-forests)
**视频：**[How do random forests work?](https://www.youtube.com/watch?v=t7PbZ1fvy6M)
# 随机森林
随机森林使用许多决策树，并通过对每棵树的预测结果取平均值来进行预测。它通常比单个决策树具有更高的预测精度，并且在默认参数下也能很好地工作

## bagging 算法

1. 创建新数据集
![[Pasted image 20251102212010.png]]

选取数据时，同一个数据可重复多次被选取。
样本中未使用的数据称为 **袋外样本**（out-of-bag-samples）

2.重复创建，并生成对此生成不同的模型
![[Pasted image 20251102212619.png]]

3. 最终模型
M0 = (M1+M2+M3+...+Mn)/n


## Random Forestes
1. 创建多个子采样数据集