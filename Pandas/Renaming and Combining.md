---
date: 2025-11-08
aliases:
  - Pandas_6
tags:
  - Pandas
  - Python
location: "[[Pandas/]]"
---

**摘自：**[Renaming and Combining](https://www.kaggle.com/code/residentmario/renaming-and-combining)
# 重命名和合并
## Renaming  重命名
#### `rename()` 函数
首先要介绍的是 `rename()` 函数，它允许您更改索引名称和/或列名称。例如，要将数据集中的 `points` 列更改为 `score` ，我们可以这样做：
![[PixPin_2025-11-08_15-42-53.png]]

###### 指定参数
`rename()` 允许您通过分别指定 `index` 或 `column` 关键字参数来重命名索引_或_列值。它支持多种输入格式，但通常 Python 字典是最方便的。以下示例演示如何使用它重命名索引中的一些元素。
![[PixPin_2025-11-08_15-43-27.png]]

你可能经常需要重命名列，但很少需要重命名索引值。对于**重命名索引值**，使用 x 通常更方便。

#### `rename_axis()` 方法
行索引和列索引都可以拥有自己的 `name` 属性。可以使用配套的 `rename_axis()` 方法更改这些名称。例如：
![[PixPin_2025-11-08_15-44-59.png]]

## Combining  合并
在对数据集进行操作时，我们有时需要以复杂的方式合并不同的 DataFrame 和/或 Series。Pandas 提供了三个核心方法来实现这一点。
按**复杂度递增**的顺序，它们分别是 `concat()` 、 `join()` 和 `merge()` 。`merge()` 的大部分功能也可以用 `join()`更简单的完成 ，因此重点介绍前两个函数。

####  `concat()`
最简单的合并方法是 `concat()` 。给定一个元素列表，该函数会将这些元素沿某个轴合并在一起。

当我们的数据存储在不同的 DataFrame 或 Series 对象中，但具有相同的字段（列）时，这种方法非常有用。
例如： [YouTube 视频数据集](https://www.kaggle.com/datasnaek/youtube-new) ，它根据来源国家/地区（例如本例中的加拿大和英国）对数据进行了划分。如果我们想同时研究多个国家/地区的数据，可以使用 `concat()` 将它们合并在一起：

![[PixPin_2025-11-08_15-52-54.png]]

#### `join()` 
复杂度中等的组合器是 `join()` 。`join()` 允许你将具有共同索引的不同 DataFrame 对象组合在一起。例如，要获取在加拿大和英国同一天都热门的视频，我们可以这样做：

![[PixPin_2025-11-08_15-53-52.png]]

这里需要使用 `lsuffix` 和 `rsuffix` 参数，因为英国和加拿大数据集中的数据列名相同。如果列名不同（例如，我们事先重命名了列），则不需要这些参数。