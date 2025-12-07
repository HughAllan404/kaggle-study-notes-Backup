---
date: 2025-10-29
aliases:
  - machine_learning_3
tags:
  - Machine_Learning
  - Python
location: "[[Machine Learning/]]"
---

**摘自：**[Model Validation](https://www.kaggle.com/code/dansbecker/model-validation)
# 模型验证
## What is Model Validation 
首先，你需要用一种易于理解的方式概括模型的质量。如果你比较1万套房屋的预测房价和实际房价，很可能会发现预测结果好坏参半。逐一查看这1万个预测值和实际值的列表毫无意义。我们需要将其概括为一个**单一的指标**。

有很多指标可以用来概括模型质量，但我们先从一个名为**Mean Absolute Error**( **平均绝对误差**（**也称MAE** ）)的指标开始。让我们从最后一个词“误差”开始，来详细解读这个指标。
```python
#误差=实际值-预测值
error=actual−predicted
```
使用平均绝对误差 (MAE) 指标时，我们取每个误差的绝对值，将每个误差转换为正数。然后，我们计算这些绝对误差的平均值。这就是我们衡量模型质量的指标。

要计算平均绝对误差 (MAE)，我们首先需要一个模型。
建立模型后，我们可以这样计算平均绝对误差了（两种方法）：
1. 导入sklearn中的相关函数
```python
from sklearn.metrics import mean_absolute_error

predicted_home_prices = melbourne_model.predict(X)
print(mean_absolute_error(y, predicted_home_prices))
```
2. 自定义函数
```python
import numpy as np
def mae(y_true,y_pred)
	return np.sum(np.abs(y_true - y_pred)) / len(y_true)
print(mae(y, predicted_home_prices))
```
## "In-Sample" Scores  样本内分数

用所有数据（数据集和目标变量）来训练一个模型，然后在同一个数据集运行模型，会生成预测值。这些预测值就是**样本内分数**。

如果模型用来预测它训练过的数据来预测，它就叫样本内分数。

由于模型的实际价值在于对新数据进行预测，因此我们会评估模型在未用于构建模型的数据上的性能。最直接的方法是将**部分数据**从模型构建过程中排除，然后用这些数据来测试模型在之前未见过的数据上的准确性。这些数据被称为**验证数据** 。

![[Pasted image 20251029183539.png]]

## Coding It
scikit-learn 库有一个函数 `train_test_split` ，可以将数据分成两部分。
我们将使用其中一部分数据作为训练数据来拟合模型，并将另一部分数据作为验证数据来计算 `mean_absolute_error` 。
```python
from sklearn.model_selection import train_test_split

# split data into training and validation data, for both features and target
# The split is based on a random number generator. Supplying a numeric value to
# the random_state argument guarantees we get the same split every time we
# run this script.
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state = 0,test_size=0.1)#test_size指定验证集占总数据的比例
# Define model
melbourne_model = DecisionTreeRegressor()
# Fit model
melbourne_model.fit(train_X, train_y)

# get predicted prices on validation data
val_predictions = melbourne_model.predict(val_X)
print(mean_absolute_error(val_y, val_predictions))
```
