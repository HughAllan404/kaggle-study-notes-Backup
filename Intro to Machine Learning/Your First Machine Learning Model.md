---
date: 2025-10-25
aliases:
  - machine_learning_2
tags:
  - Machine_Learning
  - Pandas
location: "[[Machine Learning/]]"
---

**摘自：**[Your First Machine Learning Model](https://www.kaggle.com/code/dansbecker/your-first-machine-learning-model)
# 你的第一个机器学习模型
## Selecting Data for Modeling  选择建模数据
选择数据子集的方法有很多种。[[Indexing, Selecting & Assigning]]对这些方法进行了更深入的讲解，但目前我们将重点介绍两种方法。
1. 点符号，我们用它来选择“预测目标”
2. 使用列表进行选择，我们用它来选择“特征”

#### Selecting The Prediction Target  选择预测目标

- 使用**点符号**提取变量。此单列存储在 **Series** 中，该 Series 大致类似于只有一列数据的 DataFrame。

- 使用点符号来选择要预测的列，该列称为**预测目标** 。

- 按照惯例，预测目标称为 **y** 。
```python
y = melbourne_data.Price
```

###### `.dropna`
使用 `.dropna` 方法来删除缺失值，同时删除缺失值所在行并保留原索引
例：
```python
melbourne_data.dropna(axis = 0)
```
#### Choosing "Features"  选择“功能”
输入到我们模型中（稍后用于进行预测）的列称为“特征”。有时，会将除目标列之外的所有列都用作特征。有时，使用较少的特征会更好。

我们通过在括号内提供列名列表来选择多个特征。列表中的每个项目都应该是一个字符串（带引号）。例：
```python
melbourne_features = ['Rooms', 'Bathroom', 'Landsize', 'Lattitude', 'Longtitude']
```

按照惯例，该数据称为 **X** 。
```python
X = melbourne_data[melbourne_features]
```

回顾`describe` 方法和 `head` 方法并使用[[Summary Functions and Maps]]
![[Pasted image 20251029123905.png]]
![[Pasted image 20251029123931.png]]

## Building Your Model
使用 **scikit-learn** 库来创建模型。在编写代码时，该库的写法是 **sklearn** 。
scikit-learn 无疑是目前最流行的用于对通常存储在 DataFrame 中的数据进行建模的库。

构建和使用模型的步骤如下：
- **明确定义：** 模型类型是什么？决策树？还是其他类型的模型？模型类型的其他一些参数也已指定。
- **拟合：** 从提供的数据中捕捉模式。这是建模的核心。
- **预测：** Just what it sounds like  
- **评估** ：确定模型预测的准确性。

下面是使用 scikit-learn 定义决策树模型并用特征和目标变量进行拟合的示例。
1. 导入scikit-learn库
```python
from sklearn.tree import DecisionTreeRegressor
```
2. 定义模型
```python
# Define model. Specify a number for random_state to ensure same results each run
melbourne_model = DecisionTreeRegressor(random_state=1)
```
许多机器学习模型允许在模型训练过程中存在一定的随机性。为 `random_state` 指定一个数值可以确保每次运行都得到相同的结果。

3. 拟合模型
```python
# Fit model
melbourne_model.fit(X, y)
```

我们现在有一个可以用来进行预测的拟合模型。
![[Pasted image 20251029125140.png]]

