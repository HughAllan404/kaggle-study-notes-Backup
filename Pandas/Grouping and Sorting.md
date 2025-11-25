---
date: 2025-11-05
aliases:
  - pandas_4
tags:
  - Pandas
  - Python
location: "[[Pandas/]]"
---

**摘自：**[Grouping and Sorting](https://www.kaggle.com/code/residentmario/grouping-and-sorting)
# 分组和排序
映射允许我们对 DataFrame 或 Series 中的整列数据进行一次一个值的转换。然而，我们通常希望对数据进行分组，然后针对数据所在的组执行特定操作。

## Groupwise analysis  分组分析
#### `value_counts()` 功能
我们可以通过执行以下操作来复制 `value_counts()` 功能：
![[Pasted image 20251105160751.png]]
`groupby()` 创建了一组评论，这些评论为给定的葡萄酒分配了相同的分值。
然后，对于每个组，我们获取 `points()` 列并计算其出现的次数。

#### 汇总函数
我们可以使用之前用过的任何汇总函数来处理这些数据。例如，要获取每个点值类别中最便宜的葡萄酒，我们可以执行以下操作：
![[Pasted image 20251105160926.png]]

####  `apply()` 方法
你可以把我们生成的每个分组看作是 DataFrame 的一个切片，其中只包含值匹配的数据。
我们可以使用 `apply()` 方法直接访问这个 DataFrame，然后以任何我们想要的方式操作数据。例如，以下是一种从数据集中每个酒庄选择第一款被评论过的葡萄酒名称的方法：
![[Pasted image 20251105161039.png]]

###### 多列分组
为了实现更精细的控制，您还可以**按多个列进行分组**。例如，以下是如何 按国家和省份 挑选最佳葡萄酒的方法：
![[Pasted image 20251105161129.png]]

#### `agg()` 方法
`agg()` 方法允许你同时对 DataFrame 运行多个不同的函数。
例如，我们可以生成数据集的简单统计摘要，如下所示：
![[Pasted image 20251105161618.png]]

## Multi-indexes  多重索引

**详细介绍文档：**[MultiIndex / advanced indexing](https://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html)
多级索引拥有多种处理其分层结构的方法，而单级索引则没有这些方法。此外，多级索引需要两层标签才能检索值。
对于 pandas 新手来说，处理多级索引的输出是一个常见的 “**陷阱**”。
#### `reset_index()` 方法
通常情况下，您最常用的多索引方法是将其转换回常规索引的方法，即 `reset_index()` 方法：
![[Pasted image 20251105162140.png]]

## Sorting  排序
在输出 `groupby` 的结果时，行的顺序取决于索引中的值，而不是数据本身的顺序。

#### `sort_values()` 方法
为了按所需顺序排列数据，我们可以自行排序。`sort_values()` 方法非常适合这项工作。
![[Pasted image 20251105163629.png]]

###### `ascending` 参数
`sort_values()` 函数默认按升序排列，即数值最小的元素排在最前面。然而，大多数情况下我们需要的是降序排列，即数值较大的元素排在最前面。可以指定`ascending` 参数，实现降序排列。
![[Pasted image 20251105163946.png]]

###### 同时按多列排序：
![[Pasted image 20251105164207.png]]
####  `sort_index()` 方法
要按索引值排序，请使用配套方法 `sort_index()` 。此方法具有相同的参数和默认排序顺序：
![[Pasted image 20251105164041.png]]
