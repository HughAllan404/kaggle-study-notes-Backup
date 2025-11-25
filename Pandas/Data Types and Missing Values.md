---
date: 2025-11-08
aliases:
  - Pandas_5
tags:
  - Pandas
  - Python
location: "[[Pandas/]]"
---

**摘自：**[Data Types and Missing Values](https://www.kaggle.com/code/residentmario/data-types-and-missing-values)
# 数据类型和缺失值
## Dtypes  数据类型
可以使用 `dtype` 属性来获取特定列的类型。例如，我们可以获取 `reviews` DataFrame 中 `price` 列的 dtype：
```python
reviews.price.dtype
```

或者， `dtypes` 属性返回 DataFrame 中_每一_列的 `dtype` ：
```python
reviews.dtypes
```

需要特别注意的是，完全由字符串组成的列没有自己的类型；它们被赋予 `object` 类型。

可以使用 `astype()` 函数将一种类型的列转换为另一种类型，只要这种转换有意义即可。
例如，我们可以将 `points` 列从现有的 `int64` 数据类型转换为 `float64` 数据类型：
```python
reviews.points.astype('float64')
```
DataFrame 或 Series 索引也有自己的 `dtype` ：
```python
#In:
reviews.index.dtype

#Out:
dtype('int64')
```

## Missing data  数据缺失
缺失值的条目会被赋予 `NaN` 值，即“非数字”的缩写。由于技术原因，这些 `NaN` 值始终为 `float64` 数据类型。
Pandas 提供了一些专门处理缺失数据的方法。要选择 `NaN` 值，可以使用 `pd.isnull()` （或其对应的 `pd.notnull()` ）。其用法如下：
![[PixPin_2025-11-08_14-27-16.png]]

#### 替换缺失值
替换缺失值是一项常见操作。Pandas 提供了一个非常方便的方法来解决这个问题： `fillna()` 。 `fillna()` 提供了几种不同的策略来处理此类数据。
#### `unknown`填充
例如，我们可以简单地将每个 `NaN` 替换为 `"Unknown"` ：
![[PixPin_2025-11-08_14-42-08.png]]

#### 回填策略
或者，我们可以用数据库中给定记录之后出现的第一个非空值来填充每个缺失值。这被称为回填策略。

####  `replace()` 方法
或者，我们可能需要替换一个非空值。
例如，假设自该数据集发布以来，审稿人 Kerin O'Keefe 已将其 Twitter 用户名从 `@kerinokeefe` 更改为 `@kerino` 。一种反映此更改的方法是使用 `replace()` 方法：
![[PixPin_2025-11-08_14-54-20.png]]

这里值得一提的是 `replace()` 方法，因为它对于替换数据集中给定某种哨兵值的缺失数据非常方便，例如 `"Unknown"` 、 `"Undisclosed"` 、 `"Invalid"` 等等。