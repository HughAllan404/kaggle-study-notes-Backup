---
date: 2025-10-18
aliases:
  - pandas_3
tags:
  - Pandas
  - Python
location: "[[Pandas/]]"
---

**摘自：**[Summary Functions and Maps](https://www.kaggle.com/code/residentmario/summary-functions-and-maps)
# 摘要函数和映射
## Summary functions  摘要函数
Pandas 提供了许多简单的“摘要函数”（非官方名称），它们可以以某种有用的方式重构数据。

#### `describe()` 方法
```python
reviews.points.describe()
```
 此方法生成给定列属性的高级摘要。它具有类型感知功能，这意味着其输出会根据输入的数据类型而变化。
 
#### `mean()` 函数
要查看分配点数的**平均值**，我们可以使用 `mean()` 函数：
```python
reviews.points.mean()
```

#### `median()`函数
要查看分配点数的中位数，我们可以使用`median()`函数：
```python
reviews.points.median()
```

#### `unique()` 函数
要查看唯一值列表，我们可以使用 `unique()` 函数：
in:
```python
reviews.taster_name.unique()
```
out:
```python
array(['Kerin O’Keefe', 'Roger Voss', 'Paul Gregutt',
       'Alexander Peartree', 'Michael Schachner', 'Anna Lee C. Iijima',
       'Virginie Boone', 'Matt Kettmann', nan, 'Sean P. Sullivan',
       'Jim Gordon', 'Joe Czerwinski', 'Anne Krebiehl\xa0MW',
       'Lauren Buzzeo', 'Mike DeSimone', 'Jeff Jenssen',
       'Susan Kostrzewa', 'Carrie Dykes', 'Fiona Adams',
       'Christina Pickard'], dtype=object)
```

#### `value_counts()` 方法
要查看唯一值列表_以及_它们在数据集中出现的频率，我们可以使用 `value_counts()` 方法：
in:
```python
reviews.taster_name.value_counts()
```
out:
```python
Roger Voss           25514
Michael Schachner    15134
                     ...  
Fiona Adams             27
Christina Pickard        6
Name: taster_name, Length: 19, dtype: int64
```

## Maps  映射
**映射（map）** 是一个源自数学的术语，指的是将一组值“映射”到另一组值的函数。

#### `map()`
例如，假设我们想将葡萄酒的得分重新平均为 0。我们可以这样做：
```python
review_points_mean = reviews.points.mean()
reviews.points.map(lambda p: p - review_points_mean)
```
以上代码的作用是计算 `points` 列中每个评分与其平均分的差值。
这在数据分析中非常有用，称为**中心化数据**。

#### `apply()`
如果我们想通过在每一行上调用自定义方法来转换整个 DataFrame， [`apply()`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.apply.html) 是等效方法。
```python
def remean_points(row):
    row.points = row.points - review_points_mean
    return row

reviews.apply(remean_points, axis='columns')
```
- `axis='columns'` 或 `axis=1` 表示**按行应用**。函数 `remean_points` 会被依次调用，每次传入 DataFrame 的一行。
- 如果我们使用 `axis='index'` 调用 `reviews.apply()` ，那么我们就不需要传递一个函数来转换每一行，而是需要提供一个函数来转换每一列 。

请注意，
- `map()` 返回新的、转换后的 Series 。

- `apply()`  返回新的、转换后的DataFrame。

它们不会**修改**调用它们的原始数据。如果我们查看 `reviews` 的第一行，我们会发现它仍然保留了原始的 `points` 值。


#### 常见映射操作
Pandas 内置了许多常见的映射操作。例如，下面是一种更快速地重新定义 points 列的方法：
in:
```python
review_points_mean = reviews.points.mean()
reviews.points - review_points_mean
```
out:
```python
0        -1.447138
1        -1.447138
            ...   
129969    1.552862
129970    1.552862
Name: points, Length: 129971, dtype: float64
```

在这段代码中，我们对左侧的多个值（Series 中的所有内容）和右侧的单个值（平均值）执行运算。Pandas 会查看这个表达式，并计算出我们必须从数据集中的每个值中减去该平均值。



如果我们在**等长度的 Series 之间**执行这些操作，Pandas 也能理解该怎么做。

例如，在数据集中合并国家和地区信息的一种简单方法是执行以下操作：
in:
```python
reviews.country + " - " + reviews.region_1
```
out:
```python
0            Italy - Etna
1                     NaN
               ...       
129969    France - Alsace
129970    France - Alsace
Length: 129971, dtype: object
```
所有标准 Python 运算符（ `>` 、 `<` 、 `==` 等等）都以这种方式工作。这些运算符比 `map()` 或 `apply()` 更快，因为它们使用了 Pandas 内置的加速机制。