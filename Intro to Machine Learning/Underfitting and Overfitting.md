---
date: 2025-11-01
aliases:
  - machine_learning_4
tags:
  - Machine_Learning
  - Python
location: "[[Machine Learning/]]"
---

**摘自：**[Underfitting and Overfitting](https://www.kaggle.com/code/dansbecker/underfitting-and-overfitting)
# 欠拟合和过拟合
## Overfitting
有很多特征值，并且决策树分支不断增加，不断加深，不断分裂，最终获得一棵能完美预测训练数据的树

过拟合：捕捉到未来不会再次出现的虚假模式，导致预测准确性降低。
## Underfitting
模型无法拟合训练数据本身，且训练误差很大

欠拟合：未能捕捉到相关模式，导致预测准确性降低。

## 误差 & 决策树深度
![[Pasted image 20251102184926.png]]
随着决策树深度的不断加深，模型会完美拟合训练数据，但无法泛化到训练数据之外的验证集。

所以会有一个决策树的最佳深度，超过就会过拟合，低于就会欠拟合。
![[Pasted image 20251102185414.png]]

避免欠拟合和过拟合，得到最具泛化能力的模型