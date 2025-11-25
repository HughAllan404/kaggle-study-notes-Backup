---
date: 2025-10-15
aliases:
  - pandas_1
tags:
  - Pandas
  - Python
location: "[[Pandas/]]"
---

**摘自：**[Creating, Reading and Writing](https://www.kaggle.com/code/residentmario/creating-reading-and-writing)
# 创作、阅读和写作

## 导入pandas库
```python
import pandas as pd
```
Pandas 中有两个核心对象： **DataFrame** 和 **Series** 。

## Creating data 创建数据
#### DataFrame
DataFrame是一个表。它包含一个由多个独立_条目_组成的数组，每个条目都有一个特定的_值_ 。每个条目对应一行（或_记录_ ）和一_列_ 。
**基本语法：**
![[Pasted image 20251015162626.png]]

DataFrame对象的语法是一个字典，其键是列名（本例中为 `Bob` 和 `Sue` ），值是条目列表。

行标签赋值，使用**index参数**为其赋值：
![[Pasted image 20251015162941.png]]

#### Series
Series 是数据值的序列。如果说 DataFrame 是表，那么 Series 就是列表。
本质上，Series 是 DataFrame 中的一列。因此，你可以像之前一样，使用 `index` 参数为 Series 分配行标签。不过，Series 没有列名，只有一个  **name** ：	![[Pasted image 20251015163534.png]]

## Reading data files 读取数据文件

数据可以以多种不同的形式和格式存储。其中最基本的是简单的 CSV 文件。打开 CSV 文件后，您会看到如下所示的内容：
```python
Product A,Product B,Product C,
30,21,9,
35,34,1,
41,11,11
```
CSV 文件是一个用逗号分隔的值表。因此得名“逗号分隔值”（Comma-Separated Values），简称 CSV。

使用 `pd.read_csv()` 函数将数据读入 DataFrame。具体步骤如下：
```python
wine_reviews = pd.read_csv("../input/wine-reviews/winemag-data-130k-v2.csv")
```

使用 **shape** 属性来检查生成的DataFrame有多大：
```python
wine_reviews.shape
```

使用 **head()** 命令检查结果DataFrame的内容，该命令抓取前五行：
![[Pasted image 20251015164713.png]]

**pd.read_csv()** 函数功能强大，拥有超过 30 个可选参数可供指定。例如，您可以看到此数据集中的 CSV 文件有一个内置索引，而 Pandas 并未自动获取该索引。为了让 Pandas 使用该列作为索引（而不是从头创建新索引），我们可以指定 **index_col** 。
![[Pasted image 20251015164848.png]]


## Writing to disk

创建并显示名为 `animals` 的DataFrame：
```python
animals = pd.DataFrame({'Cows': [12, 20], 'Goats': [22, 19]}, index=['Year 1', 'Year 2'])
```

- 使用**to_csv** 将 DataFrame 保存到 CSV 文件。
将此 DataFrame 保存到磁盘作为名为 `cows_and_goats.csv` 的 csv 文件。
```python
animals.to_csv("cows_and_goats.csv")
```

