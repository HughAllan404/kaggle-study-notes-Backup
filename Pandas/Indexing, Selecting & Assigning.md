---
date: 2025-10-15
aliases:
  - pandas_2
tags:
  - Pandas
  - Python
location: "[[Pandas/]]"
---

**摘自：**[Indexing, Selecting & Assigning](https://www.kaggle.com/code/residentmario/indexing-selecting-assigning)
# 索引、选择和分配
## Native accessors  原生访问器（python自带索引）

In Python, we can access the property of an object by accessing it as an attribute.
在 Python 中，我们可以通过将对象作为属性 (attribute) 来访问其属性 (property)。

例如，一个 **book** 对象可能有一个 **title** 属性，可以通过调用 **book.title**  来访问它。Pandas DataFrame 中的列的工作方式大致相同。
#### 特定 Series 检索
因此，要访问 `reviews` 的 `country` 属性，我们可以使用：
```python
reviews.country
```


如果我们有一个 Python 字典，我们可以使用索引 ( `[]` ) 运算符访问它的值。我们可以对 DataFrame 中的列执行相同的操作：
```python
reviews['country']
```

以上是从 DataFrame 中选择特定 Series 的两种方法。两者在语法上并无优劣之分，但索引运算符 `[]` 优势在于它可以处理包含**保留**字符的列名。
例如，如果我们有一个 `country providence` 列，那么 `reviews.country providence` 就无法正常工作。

#### 单个特定值检索
只需再次使用索引运算符 `[]` 即可：
```python
reviews['country'][0]
```

## Indexing in pandas  Pandas中的索引
Pandas 有自己的访问运算符 **loc** 和 **iloc**。
#### Index-based selection 基于索引的选择
基于索引的选择：根据数据在数据中的数值位置进行选择。

要选择 DataFrame 中的第一行数据，可以使用以下命令：
```python
reviews.iloc[0]
```

- `loc` 和 `iloc` 都是先**行**后**列**的。这与 Python 原生的先**列**后**行**的做法正好**相反**。


要使用 `iloc` 获取列，可以执行以下操作：
```python
reviews.iloc[:, 0]
```
 **:** 运算符本身也源自 Python 原生语言，表示“一切”。然而，当与其他选择器结合使用时，它可以用来指示值的范围。
例如，要从第一、第二和第三行中选择 `country` 列，我们可以这样做：
```python
reviews.iloc[:3, 0]
```
也可以**传递列表** ：
```python
reviews.iloc[[0, 1, 2], 0]
```
负数也可以用于选择，这将从值的_末尾_开始向前计数。
例如，这里是数据集的最后五个元素：
```python
reviews.iloc[-5:]
```
#### Label-based selection 基于标签的选择
基于标签的选择：重要的是数据索引值，而不是它的位置。

例如，要获取 `reviews` 中的第一个条目，我们现在将执行以下操作：
```python
reviews.loc[0, 'country']
```
使用 `iloc` 时，我们将数据集视为一个大矩阵,必须按位置对其进行索引。
相比之下， `loc` 使用索引中的 **信息** 来完成工作。由于数据集通常具有有意义的索引，因此使用 `loc` 通常更容易执行操作。
例如，以下操作使用 `loc` 更容易：

![[Pasted image 20251016001653.png]]

#### Choosing between `loc` and `iloc`
- `iloc` 使用 Python 标准库索引方案，其中包含范围的第一个元素，而不包含最后一个元素。因此 `0:10` 将选择条目 `0,...,9` 。
- `loc` 的索引包含所有元素。因此 `0:10` 将选择条目 `0,...,10` 。`loc` 可以索引任何 stdlib(Standard Library) 类型：例如字符串。在进行字符串等类型的索引时更加方便。

**注：当代码为`reviews.xxx.iloc[]`时切片内所需的是Serise的值，而非整个DataFrame的值，Serise是一维的，只有行，没有列。**

## Manipulating the index  操作索引
索引并非不可改变。我们可以以任何我们认为合适的方式操纵索引。

`set_index()` 方法可以用来完成这项工作。
当我们 `set_index` 为 `title` 字段时，会发生以下情况：

![[Pasted image 20251016003631.png]]
索引名称变为 `title` 字段，而非默认的0,1,2，......

## Conditional selection  条件选择
为了对数据进行_一些有趣的_操作，我们通常需要根据条件提出问题。

1. 可以通过`==` 判断是否符合条件
	例如，判断地点是否为意大利：
```python
reviews.country == 'Italy'
```
此操作根据每条记录的 `country` 生成一系列 `True` / `False` 布尔值。

以上结果随后可在 `loc` 内部用于选择相关数据：
```python
reviews.loc[reviews.country == 'Italy']
```
此操作会筛选出产地为意大利的葡萄酒。

2. 可以使用 与号（ `&` ）将两个问题放在一起,表示两个条件 “**相与**”
	例如，在意大利葡萄酒的基础上筛选出90分以上的葡萄酒：
```python
reviews.loc[(reviews.country == 'Italy') & (reviews.points >= 90)]
```

3. 可以使用 或号（`|`）表示两个条件 "**相或**"
	例如，我们要购买意大利产的葡萄酒 ，或者评价高于平均水平（90分）的葡萄酒：
```python
reviews.loc[(reviews.country == 'Italy') | (reviews.points >= 90)]
```

##### Pandas 带有一些内置条件选择器，重点关注其中两个。
###### `isin`
isin 可以让你选择值“在”值列表中的数据。
例如， `isin` 可以这样使用它来选择仅来自意大利或法国的葡萄酒：
```python
reviews.loc[reviews.country.isin(['Italy', 'France'])]
```
结果：
![[Pasted image 20251016123627.png]]

###### `isnull`以及它的同伴 `notnull`
这些方法可以让你突出显示**为（或不为） 空**（ `NaN` ）的值。
例如，要过滤掉数据集中没有价格标签的葡萄酒（即筛选出有标签价格的葡萄酒），可以这样做：

![[Pasted image 20251016123903.png]]

## Assigning data  分配数据（赋值）
- 可以赋值一个常量值：
![[Pasted image 20251016124127.png]]

- 使用可迭代的值：
![[Pasted image 20251016124159.png]]


