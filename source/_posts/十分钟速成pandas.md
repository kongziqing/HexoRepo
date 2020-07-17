---
title: 十分钟速成pandas
author: ziqing
top: true
cover: true
toc: true
mathjax: false
summary: 十分钟速成pandas
categories: 机器学习
tags:
  - Typora
  - 标签
date: 2020-07-17 13:30:42
img:
coverImg:
password:
---

# 生成对象

https://www.pypandas.cn/docs/getting_started/dsintro.html#dsintro
### 用值列表生成Series时，pandas默认自动生成整数索引


```python
import pandas as pd
import numpy as np
s=pd.Series([1,3,5,np.nan,6,8])
s
```




    0    1.0
    1    3.0
    2    5.0
    3    NaN
    4    6.0
    5    8.0
    dtype: float64



### 用含日期时间索引与标签的numpy数组生成dataframe


```python
dates = pd.date_range('20130101',periods=6)
dates
```




    DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
                   '2013-01-05', '2013-01-06'],
                  dtype='datetime64[ns]', freq='D')




```python
df = pd.DataFrame(np.random.randn(6,4),index=dates,columns=list('ABCD'))
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.262766</td>
      <td>0.809830</td>
      <td>1.678840</td>
      <td>0.956233</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>0.700293</td>
      <td>0.482185</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>-0.647583</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
      <td>0.297964</td>
      <td>-0.111197</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.691460</td>
      <td>-0.865262</td>
      <td>-0.418769</td>
      <td>0.468469</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.472262</td>
      <td>-0.804500</td>
      <td>0.855885</td>
      <td>-1.462069</td>
    </tr>
  </tbody>
</table>
</div>



### 用Series字典对象生成DataFrame


```python
df2 = pd.DataFrame({'A': 1.,
                    'B': pd.Timestamp('20130102'),
                    'C': pd.Series(1, index=list(range(4)), dtype='float32'),
                      'D': np.array([3] * 4, dtype='int32'),
                   'E': pd.Categorical(["test", "train", "test", "train"]),
                    'F': 'foo'})
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
  </tbody>
</table>
</div>



### DataFrame的列有不同的数据类型


```python
df2.dtypes
```




    A           float64
    B    datetime64[ns]
    C           float32
    D             int32
    E          category
    F            object
    dtype: object



### 查看数据
#### 下列代码说明如何查看DataFrame头部和尾部数据：


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.262766</td>
      <td>0.809830</td>
      <td>1.678840</td>
      <td>0.956233</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>0.700293</td>
      <td>0.482185</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>-0.647583</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
      <td>0.297964</td>
      <td>-0.111197</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.691460</td>
      <td>-0.865262</td>
      <td>-0.418769</td>
      <td>0.468469</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail(3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
      <td>0.297964</td>
      <td>-0.111197</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.691460</td>
      <td>-0.865262</td>
      <td>-0.418769</td>
      <td>0.468469</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.472262</td>
      <td>-0.804500</td>
      <td>0.855885</td>
      <td>-1.462069</td>
    </tr>
  </tbody>
</table>
</div>



### 显示列名和索引


```python
df.index
```




    DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
                   '2013-01-05', '2013-01-06'],
                  dtype='datetime64[ns]', freq='D')




```python
df.columns
```




    Index(['A', 'B', 'C', 'D'], dtype='object')



### DataFrame.to_numpy()由底层数据的Numpy对象，注意，DataFrame的列由多种数据类型组成的，该操作耗费系统资源较大，这也是Pandas和Numpy的本质区别：Numpy数组只有一种数据类型，DataFrame每列的数据类型各不相同，调用DataFrame。to_numpy()时，Pandas查找支持DataFrame里所有数据类型的Numpy数据类型，还有一种数据类型是object，可以把DataFrame列里的值强制转换为Python对象


### 下面的df这个DataFrame里的值都是浮点数，DataFrame.to_numpy()的操作会很快，而且不复制数据


```python
df.to_numpy()
```




    array([[ 0.26276601,  0.80983001,  1.67883966,  0.95623315],
           [-0.74781111, -0.10969203,  0.70029285,  0.4821846 ],
           [ 0.81345282,  0.68269668,  0.18365048, -0.647583  ],
           [ 1.06430643,  0.57110293,  0.29796359, -0.11119723],
           [ 0.69145971, -0.86526218, -0.41876866,  0.4684694 ],
           [ 0.47226151, -0.80449998,  0.85588534, -1.46206911]])



### df2这个DataFrame包含了多种类型，DataFrame.to_numpy()操作就会耗费较多资源
https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html#pandas.DataFrame
https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_numpy.html#pandas.DataFrame.to_numpy


```python
df2.to_numpy()
```




    array([[1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'test', 'foo'],
           [1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'train', 'foo'],
           [1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'test', 'foo'],
           [1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'train', 'foo']],
          dtype=object)



### 提醒：DataFrame.to_numpy()的输出不包含行索引和列标签
https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_numpy.html#pandas.DataFrame.to_numpy

### describe()可以快速查看数据的统计摘要：
https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html#pandas.DataFrame.describe


```python
df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.426073</td>
      <td>0.047363</td>
      <td>0.549644</td>
      <td>-0.052327</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.637909</td>
      <td>0.753993</td>
      <td>0.710870</td>
      <td>0.885358</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-0.747811</td>
      <td>-0.865262</td>
      <td>-0.418769</td>
      <td>-1.462069</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.315140</td>
      <td>-0.630798</td>
      <td>0.212229</td>
      <td>-0.513487</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.581861</td>
      <td>0.230705</td>
      <td>0.499128</td>
      <td>0.178636</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.782955</td>
      <td>0.654798</td>
      <td>0.816987</td>
      <td>0.478756</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.064306</td>
      <td>0.809830</td>
      <td>1.678840</td>
      <td>0.956233</td>
    </tr>
  </tbody>
</table>
</div>



### 转置数据


```python
df.T
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2013-01-01 00:00:00</th>
      <th>2013-01-02 00:00:00</th>
      <th>2013-01-03 00:00:00</th>
      <th>2013-01-04 00:00:00</th>
      <th>2013-01-05 00:00:00</th>
      <th>2013-01-06 00:00:00</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>0.262766</td>
      <td>-0.747811</td>
      <td>0.813453</td>
      <td>1.064306</td>
      <td>0.691460</td>
      <td>0.472262</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.809830</td>
      <td>-0.109692</td>
      <td>0.682697</td>
      <td>0.571103</td>
      <td>-0.865262</td>
      <td>-0.804500</td>
    </tr>
    <tr>
      <th>C</th>
      <td>1.678840</td>
      <td>0.700293</td>
      <td>0.183650</td>
      <td>0.297964</td>
      <td>-0.418769</td>
      <td>0.855885</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.956233</td>
      <td>0.482185</td>
      <td>-0.647583</td>
      <td>-0.111197</td>
      <td>0.468469</td>
      <td>-1.462069</td>
    </tr>
  </tbody>
</table>
</div>



### 按轴排序：


```python
df.sort_index(axis=1,ascending=False)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>D</th>
      <th>C</th>
      <th>B</th>
      <th>A</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.956233</td>
      <td>1.678840</td>
      <td>0.809830</td>
      <td>0.262766</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.482185</td>
      <td>0.700293</td>
      <td>-0.109692</td>
      <td>-0.747811</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.647583</td>
      <td>0.183650</td>
      <td>0.682697</td>
      <td>0.813453</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.111197</td>
      <td>0.297964</td>
      <td>0.571103</td>
      <td>1.064306</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.468469</td>
      <td>-0.418769</td>
      <td>-0.865262</td>
      <td>0.691460</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-1.462069</td>
      <td>0.855885</td>
      <td>-0.804500</td>
      <td>0.472262</td>
    </tr>
  </tbody>
</table>
</div>



### 按值排序


```python
df.sort_values(by='B')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-05</th>
      <td>0.691460</td>
      <td>-0.865262</td>
      <td>-0.418769</td>
      <td>0.468469</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.472262</td>
      <td>-0.804500</td>
      <td>0.855885</td>
      <td>-1.462069</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>0.700293</td>
      <td>0.482185</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
      <td>0.297964</td>
      <td>-0.111197</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>-0.647583</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>0.262766</td>
      <td>0.809830</td>
      <td>1.678840</td>
      <td>0.956233</td>
    </tr>
  </tbody>
</table>
</div>



### 选择

### 提醒：选择、设置标准Python、Numpy的表达式已经非常直观，交互也很方便，但对于生产代码，我们还是推荐优化过的Pandas数据访问方法：.at,.iat,.loc,.iloc

#### 详见索引与选择数据、多层索引与高级索引文档
https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#indexing
https://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html#advanced

### 获取数据

#### 选择单列，产生Seri，与df.A等效


```python
df['A']
```




    2013-01-01    0.262766
    2013-01-02   -0.747811
    2013-01-03    0.813453
    2013-01-04    1.064306
    2013-01-05    0.691460
    2013-01-06    0.472262
    Freq: D, Name: A, dtype: float64



#### 用【】切片


```python
df[0:3]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.262766</td>
      <td>0.809830</td>
      <td>1.678840</td>
      <td>0.956233</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>0.700293</td>
      <td>0.482185</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>-0.647583</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['20130102':'20130104']
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>0.700293</td>
      <td>0.482185</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>-0.647583</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
      <td>0.297964</td>
      <td>-0.111197</td>
    </tr>
  </tbody>
</table>
</div>



### 按标签选择
https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#indexing-label

#### 详见按标签选择

#### 用标签提取一行数据


```python
df.loc[dates[0]]
```




    A    0.262766
    B    0.809830
    C    1.678840
    D    0.956233
    Name: 2013-01-01 00:00:00, dtype: float64



#### 用标签选择多列数据


```python
df.loc[:,['A','B']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.262766</td>
      <td>0.809830</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.691460</td>
      <td>-0.865262</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.472262</td>
      <td>-0.804500</td>
    </tr>
  </tbody>
</table>
</div>



### 用标签切片，包含行与列结束点


```python
df.loc['20130102':'20130104',['A','B']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
    </tr>
  </tbody>
</table>
</div>



### 返回对象降维


```python
df.loc['20130102',['A','B']]
```




    A   -0.747811
    B   -0.109692
    Name: 2013-01-02 00:00:00, dtype: float64



### 提取标量值


```python
df.loc[dates[0],'A']
```




    0.26276600784681275



### 快速访问标量，与上述方法等效


```python
df.at[dates[0],'A']
```




    0.26276600784681275



### 按位置选择

#### 详见按位置选择

#### 用整数位置选择


```python
df.iloc[3]
```




    A    1.064306
    B    0.571103
    C    0.297964
    D   -0.111197
    Name: 2013-01-04 00:00:00, dtype: float64



#### 类似Numpy、Python，用整数切片：


```python
df.iloc[3:5,0:2]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.691460</td>
      <td>-0.865262</td>
    </tr>
  </tbody>
</table>
</div>



#### 显式整行切片


```python
df.iloc[1:3,:]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>0.700293</td>
      <td>0.482185</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>-0.647583</td>
    </tr>
  </tbody>
</table>
</div>



#### 显式整列切片


```python
df.iloc[:,1:3]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.809830</td>
      <td>1.678840</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.109692</td>
      <td>0.700293</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.682697</td>
      <td>0.183650</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.571103</td>
      <td>0.297964</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-0.865262</td>
      <td>-0.418769</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.804500</td>
      <td>0.855885</td>
    </tr>
  </tbody>
</table>
</div>



#### 显示提取值


```python
df.iloc[1,1]
```




    -0.10969202933176875



#### 快速访问标量，与上述方法等效


```python
df.iat[1,1]
```




    -0.10969202933176875



#### 布尔索引

#### 用单列的值选择数据


```python
df[df.A>0]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.262766</td>
      <td>0.809830</td>
      <td>1.678840</td>
      <td>0.956233</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>-0.647583</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
      <td>0.297964</td>
      <td>-0.111197</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.691460</td>
      <td>-0.865262</td>
      <td>-0.418769</td>
      <td>0.468469</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.472262</td>
      <td>-0.804500</td>
      <td>0.855885</td>
      <td>-1.462069</td>
    </tr>
  </tbody>
</table>
</div>



#### 选择DataFrame里满足条件的值


```python
df[df>0]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.262766</td>
      <td>0.809830</td>
      <td>1.678840</td>
      <td>0.956233</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.700293</td>
      <td>0.482185</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
      <td>0.297964</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.691460</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.468469</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.472262</td>
      <td>NaN</td>
      <td>0.855885</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



#### 用isin()筛选
https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.isin.html#pandas.Series.isin


```python
df2=df.copy()
```


```python
df2['E']=['one','one','two','three','four','three']
```


```python
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.262766</td>
      <td>0.809830</td>
      <td>1.678840</td>
      <td>0.956233</td>
      <td>one</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>0.700293</td>
      <td>0.482185</td>
      <td>one</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>-0.647583</td>
      <td>two</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
      <td>0.297964</td>
      <td>-0.111197</td>
      <td>three</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.691460</td>
      <td>-0.865262</td>
      <td>-0.418769</td>
      <td>0.468469</td>
      <td>four</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.472262</td>
      <td>-0.804500</td>
      <td>0.855885</td>
      <td>-1.462069</td>
      <td>three</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2[df2['E'].isin(['two','four'])]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>-0.647583</td>
      <td>two</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.691460</td>
      <td>-0.865262</td>
      <td>-0.418769</td>
      <td>0.468469</td>
      <td>four</td>
    </tr>
  </tbody>
</table>
</div>



#### 赋值

#### 用索引自动对齐新增列的数据


```python
s1=pd.Series([1,2,3,4,5,6],index=pd.date_range('20130102',periods=6))
```


```python
s1
```




    2013-01-02    1
    2013-01-03    2
    2013-01-04    3
    2013-01-05    4
    2013-01-06    5
    2013-01-07    6
    Freq: D, dtype: int64



#### 按标签赋值


```python
df.at[dates[0],'A']=0
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.809830</td>
      <td>1.678840</td>
      <td>0.956233</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>0.700293</td>
      <td>0.482185</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>-0.647583</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
      <td>0.297964</td>
      <td>-0.111197</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.691460</td>
      <td>-0.865262</td>
      <td>-0.418769</td>
      <td>0.468469</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.472262</td>
      <td>-0.804500</td>
      <td>0.855885</td>
      <td>-1.462069</td>
    </tr>
  </tbody>
</table>
</div>



#### 按位置赋值


```python
df.iat[0,1]=0
```

#### 按Numpy数组赋值


```python
df.loc[:,'D']=np.array([5]*len(df))*len(df)
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.678840</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>0.700293</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
      <td>0.297964</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.691460</td>
      <td>-0.865262</td>
      <td>-0.418769</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.472262</td>
      <td>-0.804500</td>
      <td>0.855885</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>



#### 用where条件赋值


```python
df2=df.copy()
```


```python
df2[df2>0]=-df2
```


```python
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-1.678840</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>-0.700293</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.813453</td>
      <td>-0.682697</td>
      <td>-0.183650</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-1.064306</td>
      <td>-0.571103</td>
      <td>-0.297964</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-0.691460</td>
      <td>-0.865262</td>
      <td>-0.418769</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.472262</td>
      <td>-0.804500</td>
      <td>-0.855885</td>
      <td>-5</td>
    </tr>
  </tbody>
</table>
</div>



### 缺失值
https://pandas.pydata.org/pandas-docs/stable/user_guide/missing_data.html#missing-data

#### pandas主要用np.nan表示缺失值数据。计算时，默认不包含空值，详见缺失数据

#### 重建索引（reindex）可以更改，添加，删除指定轴的索引，并返回数据副本，即不更改原数据


```python
df1=df.reindex(index=dates[0:4],columns=list(df.columns)+['E'])
```


```python
df1.loc[dates[0]:dates[1],'E']=1
df1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.678840</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>0.700293</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
      <td>0.297964</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



#### 删除所有含缺失值的行


```python
df1.dropna(how='any')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.678840</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>0.700293</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



#### 填充缺失值


```python
df1.fillna(value=5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.678840</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>0.700293</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.813453</td>
      <td>0.682697</td>
      <td>0.183650</td>
      <td>5</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.064306</td>
      <td>0.571103</td>
      <td>0.297964</td>
      <td>5</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>



#### 提取nan值得布尔掩码


```python
pd.isna(df1)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



#### 运算

#### 详见二进制操作
https://pandas.pydata.org/pandas-docs/stable/getting_started/basics.html#basics-binop

### 统计

#### 一般情况下，运算时排除缺失值

##### 描述性统计：


```python
df.mean()
```




    A     0.382278
    B    -0.087609
    C     0.549644
    D    30.000000
    dtype: float64



##### 在另一个轴（即行）上执行同样的操作


```python
df.mean(1)
```




    2013-01-01    7.919710
    2013-01-02    7.460697
    2013-01-03    7.919950
    2013-01-04    7.983343
    2013-01-05    7.351857
    2013-01-06    7.630912
    Freq: D, dtype: float64



#### 不同维度对象运算时，要先对齐，此外，Pandas自动沿指定维度广播


```python
s=pd.Series([1,3,4,np.nan,6,8],index=dates).shift(2)
```


```python
s
```




    2013-01-01    NaN
    2013-01-02    NaN
    2013-01-03    1.0
    2013-01-04    3.0
    2013-01-05    4.0
    2013-01-06    NaN
    Freq: D, dtype: float64




```python
df.sub(s,axis='index')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.186547</td>
      <td>-0.317303</td>
      <td>-0.816350</td>
      <td>29.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-1.935694</td>
      <td>-2.428897</td>
      <td>-2.702036</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-3.308540</td>
      <td>-4.865262</td>
      <td>-4.418769</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### Apply函数

##### Apply函数处理数据


```python
df.apply(np.cumsum)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.678840</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.747811</td>
      <td>-0.109692</td>
      <td>2.379133</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.065642</td>
      <td>0.573005</td>
      <td>2.562783</td>
      <td>90</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.129948</td>
      <td>1.144108</td>
      <td>2.860747</td>
      <td>120</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.821408</td>
      <td>0.278845</td>
      <td>2.441978</td>
      <td>150</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>2.293669</td>
      <td>-0.525655</td>
      <td>3.297863</td>
      <td>180</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.apply(lambda x:x.max()-x.min())
```




    A    1.812118
    B    1.547959
    C    2.097608
    D    0.000000
    dtype: float64



### 直方图

#### 详见直方图与离散化
https://pandas.pydata.org/pandas-docs/stable/getting_started/basics.html#basics-discretization


```python
s=pd.Series(np.random.randint(0,7,size=10))
```


```python
s
```




    0    3
    1    6
    2    2
    3    5
    4    6
    5    1
    6    1
    7    1
    8    3
    9    6
    dtype: int32




```python
s.value_counts()
```




    6    3
    1    3
    3    2
    5    1
    2    1
    dtype: int64



### 字符串方法

#### Series的str属性包含一组字符串处理功能，如下代码所示，注意，str的模式匹配默认使用正则表达式，详见矢量字符串方法
https://docs.python.org/3/library/re.html
https://pandas.pydata.org/pandas-docs/stable/user_guide/text.html#text-string-methods


```python
s=pd.Series(['A','B','C','Aaba','Baca',np.nan,'CABA','dog','cat'])
s.str.lower()
```




    0       a
    1       b
    2       c
    3    aaba
    4    baca
    5     NaN
    6    caba
    7     dog
    8     cat
    dtype: object



### 合并（Merge）
https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html#merging

#### 结合（Concat）

#### pandas提供了多种将Series、DataFrame对象组合在一起的功能，用索引与关联代数功能的多种设置逻辑可执行连接（join）与合并（merge）操作

###### 详见合并

##### concat()用于连接pandas对象


```python
df=pd.DataFrame(np.random.randn(10,4))
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.683871</td>
      <td>-0.307501</td>
      <td>0.781197</td>
      <td>0.109609</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.856883</td>
      <td>-1.691144</td>
      <td>-2.162697</td>
      <td>0.730544</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.061789</td>
      <td>-0.104611</td>
      <td>-0.964397</td>
      <td>0.423338</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.905998</td>
      <td>-0.776029</td>
      <td>0.493028</td>
      <td>0.670062</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.051434</td>
      <td>0.658247</td>
      <td>-1.969625</td>
      <td>0.375110</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.868136</td>
      <td>-2.012614</td>
      <td>-0.919476</td>
      <td>-0.655467</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.966757</td>
      <td>-0.371955</td>
      <td>-0.771078</td>
      <td>-0.675249</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.023109</td>
      <td>1.741892</td>
      <td>1.146302</td>
      <td>0.037703</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-0.264920</td>
      <td>0.103909</td>
      <td>0.341002</td>
      <td>-1.335885</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.015047</td>
      <td>1.291835</td>
      <td>-0.522114</td>
      <td>1.246330</td>
    </tr>
  </tbody>
</table>
</div>




```python
pieces=[df[:3],df[3:7],df[7:]]
pieces
```




    [          0         1         2         3
     0  0.683871 -0.307501  0.781197  0.109609
     1 -0.856883 -1.691144 -2.162697  0.730544
     2 -0.061789 -0.104611 -0.964397  0.423338,
               0         1         2         3
     3 -0.905998 -0.776029  0.493028  0.670062
     4  1.051434  0.658247 -1.969625  0.375110
     5 -0.868136 -2.012614 -0.919476 -0.655467
     6 -0.966757 -0.371955 -0.771078 -0.675249,
               0         1         2         3
     7 -0.023109  1.741892  1.146302  0.037703
     8 -0.264920  0.103909  0.341002 -1.335885
     9  0.015047  1.291835 -0.522114  1.246330]




```python
pd.concat(pieces)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.683871</td>
      <td>-0.307501</td>
      <td>0.781197</td>
      <td>0.109609</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.856883</td>
      <td>-1.691144</td>
      <td>-2.162697</td>
      <td>0.730544</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.061789</td>
      <td>-0.104611</td>
      <td>-0.964397</td>
      <td>0.423338</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.905998</td>
      <td>-0.776029</td>
      <td>0.493028</td>
      <td>0.670062</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.051434</td>
      <td>0.658247</td>
      <td>-1.969625</td>
      <td>0.375110</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.868136</td>
      <td>-2.012614</td>
      <td>-0.919476</td>
      <td>-0.655467</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.966757</td>
      <td>-0.371955</td>
      <td>-0.771078</td>
      <td>-0.675249</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.023109</td>
      <td>1.741892</td>
      <td>1.146302</td>
      <td>0.037703</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-0.264920</td>
      <td>0.103909</td>
      <td>0.341002</td>
      <td>-1.335885</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.015047</td>
      <td>1.291835</td>
      <td>-0.522114</td>
      <td>1.246330</td>
    </tr>
  </tbody>
</table>
</div>



#### 连接（join）

#### SQL风格的合并，详见数据库风格连接
https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html#merging-join


```python
left=pd.DataFrame({'key':['foo','foo'],'lval':[1,2]})
right=pd.DataFrame({'key':['foo','foo'],'rval':[4,5]})
```


```python
left
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>lval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
right
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(left,right,on='key')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>foo</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



#### 这里还有一个例子


```python
left=pd.DataFrame({'key':['foo','bar'],'lval':[1,2]})
right=pd.DataFrame({'key':['foo','bar'],'rval':[4,5]})
left
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>lval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
right
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(left,right,on='key')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



#### 追加（Append）
https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html#merging-concatenation

#### 为DataFrame追加行


```python
df=pd.DataFrame(np.random.randn(8,4),columns=['A','B','C','D'])
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.474797</td>
      <td>0.546078</td>
      <td>-0.056160</td>
      <td>2.089108</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.876803</td>
      <td>-1.449375</td>
      <td>0.210751</td>
      <td>1.356666</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.293453</td>
      <td>1.541196</td>
      <td>1.562039</td>
      <td>-0.836808</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-1.134979</td>
      <td>0.319237</td>
      <td>1.457403</td>
      <td>0.035583</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.975654</td>
      <td>-1.191270</td>
      <td>0.460296</td>
      <td>0.469146</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.491615</td>
      <td>-1.027147</td>
      <td>-0.908517</td>
      <td>-0.680785</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1.195610</td>
      <td>-0.856739</td>
      <td>-0.667872</td>
      <td>-1.390102</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.045546</td>
      <td>2.003214</td>
      <td>0.322452</td>
      <td>0.601702</td>
    </tr>
  </tbody>
</table>
</div>




```python
s=df.iloc[3]
df.append(s,ignore_index=True)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.474797</td>
      <td>0.546078</td>
      <td>-0.056160</td>
      <td>2.089108</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.876803</td>
      <td>-1.449375</td>
      <td>0.210751</td>
      <td>1.356666</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.293453</td>
      <td>1.541196</td>
      <td>1.562039</td>
      <td>-0.836808</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-1.134979</td>
      <td>0.319237</td>
      <td>1.457403</td>
      <td>0.035583</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.975654</td>
      <td>-1.191270</td>
      <td>0.460296</td>
      <td>0.469146</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.491615</td>
      <td>-1.027147</td>
      <td>-0.908517</td>
      <td>-0.680785</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1.195610</td>
      <td>-0.856739</td>
      <td>-0.667872</td>
      <td>-1.390102</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.045546</td>
      <td>2.003214</td>
      <td>0.322452</td>
      <td>0.601702</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-1.134979</td>
      <td>0.319237</td>
      <td>1.457403</td>
      <td>0.035583</td>
    </tr>
  </tbody>
</table>
</div>



#### 分组（Grouping）
https://pandas.pydata.org/pandas-docs/stable/user_guide/groupby.html#groupby

#### ‘group by’指的是涵盖下列一项或多项步骤的处理流程：
##### 分割：按条件数据分割成多组
##### 应用：为每组单独应用函数
##### 组合：将处理结果组合成一个数据结构
##### 详见分组


```python
df = pd.DataFrame({'A': ['foo', 'bar', 'foo', 'bar',
                          'foo', 'bar', 'foo', 'foo'],
                   'B': ['one', 'one', 'two', 'three',
                           'two', 'two', 'one', 'three'],
                    'C': np.random.randn(8),
                   'D': np.random.randn(8)})
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>one</td>
      <td>0.777193</td>
      <td>0.180939</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>one</td>
      <td>-1.203252</td>
      <td>-0.012245</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>two</td>
      <td>0.571687</td>
      <td>-0.242212</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bar</td>
      <td>three</td>
      <td>0.627642</td>
      <td>0.096572</td>
    </tr>
    <tr>
      <th>4</th>
      <td>foo</td>
      <td>two</td>
      <td>0.109057</td>
      <td>-1.048548</td>
    </tr>
    <tr>
      <th>5</th>
      <td>bar</td>
      <td>two</td>
      <td>-1.114232</td>
      <td>0.939454</td>
    </tr>
    <tr>
      <th>6</th>
      <td>foo</td>
      <td>one</td>
      <td>0.931676</td>
      <td>-0.774002</td>
    </tr>
    <tr>
      <th>7</th>
      <td>foo</td>
      <td>three</td>
      <td>0.721041</td>
      <td>-0.759950</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('A').sum()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>A</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>bar</th>
      <td>-1.689842</td>
      <td>1.023782</td>
    </tr>
    <tr>
      <th>foo</th>
      <td>3.110655</td>
      <td>-2.643773</td>
    </tr>
  </tbody>
</table>
</div>



#### 分列分组后，生成多层索引，也可以应用sum函数：
https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sum.html#pandas.DataFrame.sum


```python
df.groupby(['A','B']).sum()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">bar</th>
      <th>one</th>
      <td>-1.203252</td>
      <td>-0.012245</td>
    </tr>
    <tr>
      <th>three</th>
      <td>0.627642</td>
      <td>0.096572</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-1.114232</td>
      <td>0.939454</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">foo</th>
      <th>one</th>
      <td>1.708870</td>
      <td>-0.593063</td>
    </tr>
    <tr>
      <th>three</th>
      <td>0.721041</td>
      <td>-0.759950</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.680744</td>
      <td>-1.290759</td>
    </tr>
  </tbody>
</table>
</div>



### 重塑（Reshaping）

#### 详见多层索引与重塑
https://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html#advanced-hierarchical
https://pandas.pydata.org/pandas-docs/stable/user_guide/reshaping.html#reshaping-stacking

### 堆叠（Stack）


```python
tuples = list(zip(*[['bar', 'bar', 'baz', 'baz',
                      'foo', 'foo', 'qux', 'qux'],
                     ['one', 'two', 'one', 'two',
                     'one', 'two', 'one', 'two']]))
```


```python
tuples
```




    [('bar', 'one'),
     ('bar', 'two'),
     ('baz', 'one'),
     ('baz', 'two'),
     ('foo', 'one'),
     ('foo', 'two'),
     ('qux', 'one'),
     ('qux', 'two')]




```python
index=pd.MultiIndex.from_tuples(tuples,names=['first','second'])
```


```python
index
```




    MultiIndex(levels=[['bar', 'baz', 'foo', 'qux'], ['one', 'two']],
               codes=[[0, 0, 1, 1, 2, 2, 3, 3], [0, 1, 0, 1, 0, 1, 0, 1]],
               names=['first', 'second'])




```python
df=pd.DataFrame(np.random.randn(8,2),index=index,columns=['A','B'])
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>-0.481402</td>
      <td>0.798669</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-0.850446</td>
      <td>1.998825</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>0.131606</td>
      <td>-0.209346</td>
    </tr>
    <tr>
      <th>two</th>
      <td>1.925047</td>
      <td>0.549490</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">foo</th>
      <th>one</th>
      <td>-0.338106</td>
      <td>0.120898</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-1.997789</td>
      <td>1.941219</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">qux</th>
      <th>one</th>
      <td>-0.696257</td>
      <td>0.394193</td>
    </tr>
    <tr>
      <th>two</th>
      <td>1.166970</td>
      <td>0.490899</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2=df[:4]
```


```python
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>0.093482</td>
      <td>0.755837</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.599578</td>
      <td>0.786312</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>-0.937135</td>
      <td>-1.263839</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-0.470650</td>
      <td>1.134036</td>
    </tr>
  </tbody>
</table>
</div>



### stack()方法把DataFrame列压缩至一层


```python
stacked=df2.stack()
```


```python
stacked
```




    first  second   
    bar    one     A    0.093482
                   B    0.755837
           two     A    0.599578
                   B    0.786312
    baz    one     A   -0.937135
                   B   -1.263839
           two     A   -0.470650
                   B    1.134036
    dtype: float64



#### 压缩后的DataFrame或Series具有多层索引，stack（）的逆操作是unstack()，默认为拆叠最后一层：
https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.stack.html#pandas.DataFrame.stack
https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.unstack.html#pandas.DataFrame.unstack


```python
stacked.unstack()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>0.093482</td>
      <td>0.755837</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.599578</td>
      <td>0.786312</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>-0.937135</td>
      <td>-1.263839</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-0.470650</td>
      <td>1.134036</td>
    </tr>
  </tbody>
</table>
</div>




```python
stacked.unstack(1)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>second</th>
      <th>one</th>
      <th>two</th>
    </tr>
    <tr>
      <th>first</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>A</th>
      <td>0.093482</td>
      <td>0.599578</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.755837</td>
      <td>0.786312</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>A</th>
      <td>-0.937135</td>
      <td>-0.470650</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-1.263839</td>
      <td>1.134036</td>
    </tr>
  </tbody>
</table>
</div>




```python
stacked.unstack(0)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>first</th>
      <th>bar</th>
      <th>baz</th>
    </tr>
    <tr>
      <th>second</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">one</th>
      <th>A</th>
      <td>0.093482</td>
      <td>-0.937135</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.755837</td>
      <td>-1.263839</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">two</th>
      <th>A</th>
      <td>0.599578</td>
      <td>-0.470650</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.786312</td>
      <td>1.134036</td>
    </tr>
  </tbody>
</table>
</div>



### 数据透视表（pivot Tables）

#### 详见数据透视表
https://pandas.pydata.org/pandas-docs/stable/user_guide/reshaping.html#reshaping-pivot


```python
df = pd.DataFrame({'A': ['one', 'one', 'two', 'three'] * 3,
                   'B': ['A', 'B', 'C'] * 4,
                   'C': ['foo', 'foo', 'foo', 'bar', 'bar', 'bar'] * 2,
                    'D': np.random.randn(12),
                    'E': np.random.randn(12)})
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>one</td>
      <td>A</td>
      <td>foo</td>
      <td>1.512700</td>
      <td>-0.778148</td>
    </tr>
    <tr>
      <th>1</th>
      <td>one</td>
      <td>B</td>
      <td>foo</td>
      <td>-0.649081</td>
      <td>0.437823</td>
    </tr>
    <tr>
      <th>2</th>
      <td>two</td>
      <td>C</td>
      <td>foo</td>
      <td>-0.499864</td>
      <td>0.043016</td>
    </tr>
    <tr>
      <th>3</th>
      <td>three</td>
      <td>A</td>
      <td>bar</td>
      <td>0.665239</td>
      <td>-0.549835</td>
    </tr>
    <tr>
      <th>4</th>
      <td>one</td>
      <td>B</td>
      <td>bar</td>
      <td>1.584777</td>
      <td>-0.871298</td>
    </tr>
    <tr>
      <th>5</th>
      <td>one</td>
      <td>C</td>
      <td>bar</td>
      <td>-0.444866</td>
      <td>-1.379180</td>
    </tr>
    <tr>
      <th>6</th>
      <td>two</td>
      <td>A</td>
      <td>foo</td>
      <td>-1.061343</td>
      <td>1.000738</td>
    </tr>
    <tr>
      <th>7</th>
      <td>three</td>
      <td>B</td>
      <td>foo</td>
      <td>1.653209</td>
      <td>0.504661</td>
    </tr>
    <tr>
      <th>8</th>
      <td>one</td>
      <td>C</td>
      <td>foo</td>
      <td>0.664697</td>
      <td>0.680470</td>
    </tr>
    <tr>
      <th>9</th>
      <td>one</td>
      <td>A</td>
      <td>bar</td>
      <td>1.095752</td>
      <td>0.701052</td>
    </tr>
    <tr>
      <th>10</th>
      <td>two</td>
      <td>B</td>
      <td>bar</td>
      <td>-0.597174</td>
      <td>-0.628091</td>
    </tr>
    <tr>
      <th>11</th>
      <td>three</td>
      <td>C</td>
      <td>bar</td>
      <td>0.311608</td>
      <td>-1.797560</td>
    </tr>
  </tbody>
</table>
</div>



#### 用上述数据生成数据透视表非常简单


```python
pd.pivot_table(df,values='D',index=['A','B'],columns=['C'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>C</th>
      <th>bar</th>
      <th>foo</th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">one</th>
      <th>A</th>
      <td>1.095752</td>
      <td>1.512700</td>
    </tr>
    <tr>
      <th>B</th>
      <td>1.584777</td>
      <td>-0.649081</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-0.444866</td>
      <td>0.664697</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">three</th>
      <th>A</th>
      <td>0.665239</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>B</th>
      <td>NaN</td>
      <td>1.653209</td>
    </tr>
    <tr>
      <th>C</th>
      <td>0.311608</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">two</th>
      <th>A</th>
      <td>NaN</td>
      <td>-1.061343</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.597174</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>C</th>
      <td>NaN</td>
      <td>-0.499864</td>
    </tr>
  </tbody>
</table>
</div>



#### 时间序列（TimeSeries）

#### Pandas为频率转换时重采样提供了虽然简单易用，但强大高效的功能，如，将秒级的数据转换为5分钟为频率的数据，这种操作常见于财务应用程序，但又不仅限于此
https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#timeseries


```python
rng = pd.date_range('1/1/2012',periods=100,freq='S')
rng
```




    DatetimeIndex(['2012-01-01 00:00:00', '2012-01-01 00:00:01',
                   '2012-01-01 00:00:02', '2012-01-01 00:00:03',
                   '2012-01-01 00:00:04', '2012-01-01 00:00:05',
                   '2012-01-01 00:00:06', '2012-01-01 00:00:07',
                   '2012-01-01 00:00:08', '2012-01-01 00:00:09',
                   '2012-01-01 00:00:10', '2012-01-01 00:00:11',
                   '2012-01-01 00:00:12', '2012-01-01 00:00:13',
                   '2012-01-01 00:00:14', '2012-01-01 00:00:15',
                   '2012-01-01 00:00:16', '2012-01-01 00:00:17',
                   '2012-01-01 00:00:18', '2012-01-01 00:00:19',
                   '2012-01-01 00:00:20', '2012-01-01 00:00:21',
                   '2012-01-01 00:00:22', '2012-01-01 00:00:23',
                   '2012-01-01 00:00:24', '2012-01-01 00:00:25',
                   '2012-01-01 00:00:26', '2012-01-01 00:00:27',
                   '2012-01-01 00:00:28', '2012-01-01 00:00:29',
                   '2012-01-01 00:00:30', '2012-01-01 00:00:31',
                   '2012-01-01 00:00:32', '2012-01-01 00:00:33',
                   '2012-01-01 00:00:34', '2012-01-01 00:00:35',
                   '2012-01-01 00:00:36', '2012-01-01 00:00:37',
                   '2012-01-01 00:00:38', '2012-01-01 00:00:39',
                   '2012-01-01 00:00:40', '2012-01-01 00:00:41',
                   '2012-01-01 00:00:42', '2012-01-01 00:00:43',
                   '2012-01-01 00:00:44', '2012-01-01 00:00:45',
                   '2012-01-01 00:00:46', '2012-01-01 00:00:47',
                   '2012-01-01 00:00:48', '2012-01-01 00:00:49',
                   '2012-01-01 00:00:50', '2012-01-01 00:00:51',
                   '2012-01-01 00:00:52', '2012-01-01 00:00:53',
                   '2012-01-01 00:00:54', '2012-01-01 00:00:55',
                   '2012-01-01 00:00:56', '2012-01-01 00:00:57',
                   '2012-01-01 00:00:58', '2012-01-01 00:00:59',
                   '2012-01-01 00:01:00', '2012-01-01 00:01:01',
                   '2012-01-01 00:01:02', '2012-01-01 00:01:03',
                   '2012-01-01 00:01:04', '2012-01-01 00:01:05',
                   '2012-01-01 00:01:06', '2012-01-01 00:01:07',
                   '2012-01-01 00:01:08', '2012-01-01 00:01:09',
                   '2012-01-01 00:01:10', '2012-01-01 00:01:11',
                   '2012-01-01 00:01:12', '2012-01-01 00:01:13',
                   '2012-01-01 00:01:14', '2012-01-01 00:01:15',
                   '2012-01-01 00:01:16', '2012-01-01 00:01:17',
                   '2012-01-01 00:01:18', '2012-01-01 00:01:19',
                   '2012-01-01 00:01:20', '2012-01-01 00:01:21',
                   '2012-01-01 00:01:22', '2012-01-01 00:01:23',
                   '2012-01-01 00:01:24', '2012-01-01 00:01:25',
                   '2012-01-01 00:01:26', '2012-01-01 00:01:27',
                   '2012-01-01 00:01:28', '2012-01-01 00:01:29',
                   '2012-01-01 00:01:30', '2012-01-01 00:01:31',
                   '2012-01-01 00:01:32', '2012-01-01 00:01:33',
                   '2012-01-01 00:01:34', '2012-01-01 00:01:35',
                   '2012-01-01 00:01:36', '2012-01-01 00:01:37',
                   '2012-01-01 00:01:38', '2012-01-01 00:01:39'],
                  dtype='datetime64[ns]', freq='S')




```python
ts = pd.Series(np.random.randint(0,500,len(rng)),index=rng)
ts.head()
```




    2012-01-01 00:00:00    112
    2012-01-01 00:00:01    184
    2012-01-01 00:00:02     63
    2012-01-01 00:00:03    307
    2012-01-01 00:00:04    206
    Freq: S, dtype: int32




```python
ts.resample('1Min').sum()
```




    2012-01-01 00:00:00    13530
    2012-01-01 00:01:00    10207
    Freq: T, dtype: int32



#### 时区表示


```python
rng=pd.date_range('3/6/2012 00:00',periods=5,freq='D')
rng
```




    DatetimeIndex(['2012-03-06', '2012-03-07', '2012-03-08', '2012-03-09',
                   '2012-03-10'],
                  dtype='datetime64[ns]', freq='D')




```python
ts = pd.Series(np.random.randn(len(rng)),rng)
ts
```




    2012-03-06   -0.904154
    2012-03-07    0.184860
    2012-03-08    0.685790
    2012-03-09   -0.310129
    2012-03-10   -2.030353
    Freq: D, dtype: float64




```python
ts_utc = ts.tz_localize('UTC')
ts_utc
```




    2012-03-06 00:00:00+00:00   -0.904154
    2012-03-07 00:00:00+00:00    0.184860
    2012-03-08 00:00:00+00:00    0.685790
    2012-03-09 00:00:00+00:00   -0.310129
    2012-03-10 00:00:00+00:00   -2.030353
    Freq: D, dtype: float64



#### 转换成其他时区


```python
ts_utc.tz_convert('US/Eastern')
```




    2012-03-05 19:00:00-05:00   -0.904154
    2012-03-06 19:00:00-05:00    0.184860
    2012-03-07 19:00:00-05:00    0.685790
    2012-03-08 19:00:00-05:00   -0.310129
    2012-03-09 19:00:00-05:00   -2.030353
    Freq: D, dtype: float64



#### 转换时间段


```python
rng=pd.date_range('1/1/2012',periods=5,freq='M')
rng
```




    DatetimeIndex(['2012-01-31', '2012-02-29', '2012-03-31', '2012-04-30',
                   '2012-05-31'],
                  dtype='datetime64[ns]', freq='M')




```python
ts=pd.Series(np.random.randn(len(rng)),index=rng)
ts
```




    2012-01-31   -1.225980
    2012-02-29    0.655696
    2012-03-31    1.574129
    2012-04-30   -0.673129
    2012-05-31    0.601269
    Freq: M, dtype: float64




```python
ps=ts.to_period()
ps
```




    2012-01   -1.225980
    2012-02    0.655696
    2012-03    1.574129
    2012-04   -0.673129
    2012-05    0.601269
    Freq: M, dtype: float64




```python
ps.to_timestamp()
```




    2012-01-01   -1.225980
    2012-02-01    0.655696
    2012-03-01    1.574129
    2012-04-01   -0.673129
    2012-05-01    0.601269
    Freq: MS, dtype: float64



#### Pandas函数可以很方便地转换时间段与时间戳。下例把以11月为结束年份的季度频率转换为下一季度月末上午9点


```python
prng=pd.period_range('1990Q1','2000Q4',freq='Q-NOV')
ts=pd.Series(np.random.randn(len(prng)),prng)
ts
```




    1990Q1    1.192696
    1990Q2   -2.128740
    1990Q3    1.174372
    1990Q4    0.318501
    1991Q1    0.113189
    1991Q2   -1.151977
    1991Q3   -1.092579
    1991Q4    0.468274
    1992Q1   -0.545375
    1992Q2   -1.248419
    1992Q3   -0.351470
    1992Q4    0.146982
    1993Q1   -0.721067
    1993Q2   -1.455432
    1993Q3    0.857321
    1993Q4   -2.034842
    1994Q1    0.427791
    1994Q2   -0.175506
    1994Q3   -0.291836
    1994Q4   -0.801929
    1995Q1    0.305602
    1995Q2   -0.809480
    1995Q3    0.111699
    1995Q4   -0.192220
    1996Q1    0.768556
    1996Q2    0.534286
    1996Q3    0.161583
    1996Q4   -1.547316
    1997Q1   -0.706564
    1997Q2    0.748592
    1997Q3   -1.199196
    1997Q4   -0.298750
    1998Q1   -1.335666
    1998Q2    0.835708
    1998Q3   -0.500230
    1998Q4    0.585607
    1999Q1    0.279487
    1999Q2   -0.632584
    1999Q3   -1.539243
    1999Q4    1.124178
    2000Q1    0.043956
    2000Q2   -1.360061
    2000Q3   -1.473730
    2000Q4    0.573552
    Freq: Q-NOV, dtype: float64




```python
ts.index=(prng.asfreq('M','e')+1).asfreq('H','s')+9
ts.head()
```




    1990-03-01 09:00    1.192696
    1990-06-01 09:00   -2.128740
    1990-09-01 09:00    1.174372
    1990-12-01 09:00    0.318501
    1991-03-01 09:00    0.113189
    Freq: H, dtype: float64



### 类别型（Categoricals）

#### Pandas的DataFrame里可以包含类别数据，完整文档详见类别简介和API文档
https://pandas.pydata.org/pandas-docs/stable/user_guide/categorical.html#categorical
https://pandas.pydata.org/pandas-docs/stable/reference/arrays.html#api-arrays-categorical


```python
df = pd.DataFrame({"id": [1, 2, 3, 4, 5, 6],
                  "raw_grade": ['a', 'b', 'b', 'a', 'a', 'e']})
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>raw_grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>b</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>a</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>a</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>e</td>
    </tr>
  </tbody>
</table>
</div>



#### 将grade的原生数据转换为类别型数据：


```python
df["grade"]=df["raw_grade"].astype("category")
df["grade"]
```




    0    a
    1    b
    2    b
    3    a
    4    a
    5    e
    Name: grade, dtype: category
    Categories (3, object): [a, b, e]



#### 用有含义的名字重命名不同类型，调用Series.cat.categories


```python
df['grade'].cat.categories=["very good","good","very bad"]
```


```python
df["grade"] = df["grade"].cat.set_categories(["very bad", "bad", "medium",
                                          "good", "very good"])
df["grade"]
```




    0    very good
    1         good
    2         good
    3    very good
    4    very good
    5     very bad
    Name: grade, dtype: category
    Categories (5, object): [very bad, bad, medium, good, very good]



#### 注意，这里是按生成类别时的顺序排序，不是按词汇排序


```python
df.sort_values(by='grade')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>raw_grade</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>e</td>
      <td>very bad</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
      <td>good</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>b</td>
      <td>good</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>a</td>
      <td>very good</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('grade').size()
```




    grade
    very bad     1
    bad          0
    medium       0
    good         2
    very good    3
    dtype: int64



## 可视化
https://pandas.pydata.org/pandas-docs/stable/user_guide/visualization.html#visualization


```python
ts = pd.Series(np.random.randn(1000),
              index=pd.date_range('1/1/2000', periods=1000))
ts.head()
```




    2000-01-01    0.539169
    2000-01-02    0.796706
    2000-01-03   -0.978084
    2000-01-04   -1.062247
    2000-01-05   -0.183271
    Freq: D, dtype: float64




```python
ts=ts.cumsum()
ts
```




    2000-01-01     0.539169
    2000-01-02     1.335875
    2000-01-03     0.357791
    2000-01-04    -0.704456
    2000-01-05    -0.887727
    2000-01-06    -0.471479
    2000-01-07    -1.869325
    2000-01-08    -1.368183
    2000-01-09    -3.793193
    2000-01-10    -5.117582
    2000-01-11    -4.604941
    2000-01-12    -3.919434
    2000-01-13    -3.325861
    2000-01-14    -3.189620
    2000-01-15    -3.020213
    2000-01-16    -4.207355
    2000-01-17    -4.641775
    2000-01-18    -3.972796
    2000-01-19    -2.934364
    2000-01-20    -2.613719
    2000-01-21    -2.412777
    2000-01-22    -2.364340
    2000-01-23    -1.556202
    2000-01-24    -1.936749
    2000-01-25    -2.141850
    2000-01-26    -1.545098
    2000-01-27    -1.263451
    2000-01-28    -2.803169
    2000-01-29    -1.499460
    2000-01-30     1.015585
                    ...    
    2002-08-28    -5.612502
    2002-08-29    -4.804984
    2002-08-30    -5.073604
    2002-08-31    -6.157469
    2002-09-01    -5.938957
    2002-09-02    -5.660344
    2002-09-03    -7.114066
    2002-09-04    -6.953511
    2002-09-05    -7.299286
    2002-09-06    -8.741551
    2002-09-07   -10.627062
    2002-09-08    -9.811652
    2002-09-09   -10.358743
    2002-09-10    -8.890961
    2002-09-11    -9.689909
    2002-09-12   -10.249948
    2002-09-13   -10.457405
    2002-09-14    -9.538685
    2002-09-15   -10.089912
    2002-09-16   -10.286512
    2002-09-17    -8.763835
    2002-09-18    -8.820550
    2002-09-19   -10.975909
    2002-09-20   -12.731910
    2002-09-21   -13.607184
    2002-09-22   -15.331946
    2002-09-23   -15.694736
    2002-09-24   -16.374717
    2002-09-25   -15.365212
    2002-09-26   -15.376312
    Freq: D, Length: 1000, dtype: float64




```python
ts.plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x203044a5940>




![png](output_214_1.png)


#### dataframe的plot方法可以快速绘制所有带标签的列
https://pandas.pydata.org/pandas-docs/stable/user_guide/visualization.html#visualization


```python
df = pd.DataFrame(np.random.randn(1000, 4), index=ts.index,
                  columns=['A', 'B', 'C', 'D'])
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-01</th>
      <td>-0.403820</td>
      <td>-0.861685</td>
      <td>0.262125</td>
      <td>0.654910</td>
    </tr>
    <tr>
      <th>2000-01-02</th>
      <td>1.768612</td>
      <td>-0.213129</td>
      <td>-0.719914</td>
      <td>-0.036541</td>
    </tr>
    <tr>
      <th>2000-01-03</th>
      <td>0.102498</td>
      <td>1.443473</td>
      <td>-0.068096</td>
      <td>0.871774</td>
    </tr>
    <tr>
      <th>2000-01-04</th>
      <td>0.747066</td>
      <td>-0.673786</td>
      <td>-0.294567</td>
      <td>-0.555684</td>
    </tr>
    <tr>
      <th>2000-01-05</th>
      <td>2.122246</td>
      <td>-0.445726</td>
      <td>0.382663</td>
      <td>1.273366</td>
    </tr>
    <tr>
      <th>2000-01-06</th>
      <td>0.205880</td>
      <td>-0.725008</td>
      <td>0.713592</td>
      <td>1.050615</td>
    </tr>
    <tr>
      <th>2000-01-07</th>
      <td>-0.266623</td>
      <td>-0.836566</td>
      <td>1.113839</td>
      <td>-0.409689</td>
    </tr>
    <tr>
      <th>2000-01-08</th>
      <td>-0.441420</td>
      <td>-0.152557</td>
      <td>0.219731</td>
      <td>0.732548</td>
    </tr>
    <tr>
      <th>2000-01-09</th>
      <td>-1.517168</td>
      <td>-1.266140</td>
      <td>0.526676</td>
      <td>0.157710</td>
    </tr>
    <tr>
      <th>2000-01-10</th>
      <td>-0.555196</td>
      <td>-0.817628</td>
      <td>-0.619053</td>
      <td>-1.357579</td>
    </tr>
    <tr>
      <th>2000-01-11</th>
      <td>1.216180</td>
      <td>1.004558</td>
      <td>0.754348</td>
      <td>0.119537</td>
    </tr>
    <tr>
      <th>2000-01-12</th>
      <td>-1.560071</td>
      <td>1.356160</td>
      <td>0.659727</td>
      <td>-0.578732</td>
    </tr>
    <tr>
      <th>2000-01-13</th>
      <td>-0.344310</td>
      <td>-2.712881</td>
      <td>-1.729452</td>
      <td>0.354977</td>
    </tr>
    <tr>
      <th>2000-01-14</th>
      <td>-0.657705</td>
      <td>0.185932</td>
      <td>0.371227</td>
      <td>-1.030777</td>
    </tr>
    <tr>
      <th>2000-01-15</th>
      <td>-1.073826</td>
      <td>-0.441367</td>
      <td>-1.706187</td>
      <td>-0.512045</td>
    </tr>
    <tr>
      <th>2000-01-16</th>
      <td>0.900098</td>
      <td>0.188637</td>
      <td>0.230351</td>
      <td>1.310940</td>
    </tr>
    <tr>
      <th>2000-01-17</th>
      <td>0.797040</td>
      <td>0.268900</td>
      <td>0.533550</td>
      <td>-1.080641</td>
    </tr>
    <tr>
      <th>2000-01-18</th>
      <td>-0.391943</td>
      <td>0.196713</td>
      <td>0.033671</td>
      <td>-0.482255</td>
    </tr>
    <tr>
      <th>2000-01-19</th>
      <td>0.557491</td>
      <td>-0.085030</td>
      <td>-1.418595</td>
      <td>1.677838</td>
    </tr>
    <tr>
      <th>2000-01-20</th>
      <td>0.392006</td>
      <td>0.087150</td>
      <td>0.804150</td>
      <td>-0.148844</td>
    </tr>
    <tr>
      <th>2000-01-21</th>
      <td>-0.609433</td>
      <td>-0.687186</td>
      <td>-0.516820</td>
      <td>1.500974</td>
    </tr>
    <tr>
      <th>2000-01-22</th>
      <td>-0.060579</td>
      <td>0.462088</td>
      <td>0.616453</td>
      <td>0.615896</td>
    </tr>
    <tr>
      <th>2000-01-23</th>
      <td>-0.490724</td>
      <td>-2.208678</td>
      <td>0.187790</td>
      <td>-0.699064</td>
    </tr>
    <tr>
      <th>2000-01-24</th>
      <td>0.841364</td>
      <td>-0.120559</td>
      <td>1.021754</td>
      <td>0.285857</td>
    </tr>
    <tr>
      <th>2000-01-25</th>
      <td>1.712944</td>
      <td>0.479250</td>
      <td>-0.411576</td>
      <td>-2.496946</td>
    </tr>
    <tr>
      <th>2000-01-26</th>
      <td>2.476162</td>
      <td>-0.742174</td>
      <td>0.384957</td>
      <td>-1.561012</td>
    </tr>
    <tr>
      <th>2000-01-27</th>
      <td>-0.169507</td>
      <td>1.491176</td>
      <td>0.225953</td>
      <td>-0.171110</td>
    </tr>
    <tr>
      <th>2000-01-28</th>
      <td>-0.326795</td>
      <td>-0.928639</td>
      <td>-0.077926</td>
      <td>-0.383463</td>
    </tr>
    <tr>
      <th>2000-01-29</th>
      <td>0.914927</td>
      <td>-1.116768</td>
      <td>-1.123061</td>
      <td>1.152875</td>
    </tr>
    <tr>
      <th>2000-01-30</th>
      <td>-0.365077</td>
      <td>1.626579</td>
      <td>-0.919300</td>
      <td>-0.557889</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2002-08-28</th>
      <td>0.547606</td>
      <td>0.101673</td>
      <td>1.701981</td>
      <td>0.655521</td>
    </tr>
    <tr>
      <th>2002-08-29</th>
      <td>-0.932057</td>
      <td>-0.732842</td>
      <td>-0.435287</td>
      <td>-0.412881</td>
    </tr>
    <tr>
      <th>2002-08-30</th>
      <td>0.302205</td>
      <td>-1.569959</td>
      <td>-1.974306</td>
      <td>0.325171</td>
    </tr>
    <tr>
      <th>2002-08-31</th>
      <td>1.094880</td>
      <td>-0.491747</td>
      <td>1.469688</td>
      <td>1.004903</td>
    </tr>
    <tr>
      <th>2002-09-01</th>
      <td>-1.469820</td>
      <td>0.060895</td>
      <td>0.365955</td>
      <td>-1.579292</td>
    </tr>
    <tr>
      <th>2002-09-02</th>
      <td>0.607064</td>
      <td>-0.198070</td>
      <td>0.816608</td>
      <td>1.396972</td>
    </tr>
    <tr>
      <th>2002-09-03</th>
      <td>0.321749</td>
      <td>1.838613</td>
      <td>-0.883205</td>
      <td>-0.385823</td>
    </tr>
    <tr>
      <th>2002-09-04</th>
      <td>-0.169855</td>
      <td>1.845828</td>
      <td>1.493554</td>
      <td>-0.889160</td>
    </tr>
    <tr>
      <th>2002-09-05</th>
      <td>-0.511920</td>
      <td>-0.768413</td>
      <td>-0.789903</td>
      <td>1.801745</td>
    </tr>
    <tr>
      <th>2002-09-06</th>
      <td>-0.391134</td>
      <td>-0.528561</td>
      <td>0.381485</td>
      <td>0.708959</td>
    </tr>
    <tr>
      <th>2002-09-07</th>
      <td>0.587261</td>
      <td>0.755504</td>
      <td>-0.214899</td>
      <td>-1.053086</td>
    </tr>
    <tr>
      <th>2002-09-08</th>
      <td>-0.541301</td>
      <td>0.941833</td>
      <td>0.615887</td>
      <td>0.826595</td>
    </tr>
    <tr>
      <th>2002-09-09</th>
      <td>0.082876</td>
      <td>-0.923984</td>
      <td>-1.156417</td>
      <td>-1.812171</td>
    </tr>
    <tr>
      <th>2002-09-10</th>
      <td>-2.176130</td>
      <td>-0.112087</td>
      <td>0.632639</td>
      <td>-1.752319</td>
    </tr>
    <tr>
      <th>2002-09-11</th>
      <td>0.839755</td>
      <td>-0.022035</td>
      <td>0.269522</td>
      <td>-2.404917</td>
    </tr>
    <tr>
      <th>2002-09-12</th>
      <td>-0.835131</td>
      <td>0.620688</td>
      <td>-0.547198</td>
      <td>2.732546</td>
    </tr>
    <tr>
      <th>2002-09-13</th>
      <td>0.156933</td>
      <td>1.559828</td>
      <td>-1.184098</td>
      <td>1.929225</td>
    </tr>
    <tr>
      <th>2002-09-14</th>
      <td>0.154408</td>
      <td>-2.932961</td>
      <td>0.716624</td>
      <td>2.171355</td>
    </tr>
    <tr>
      <th>2002-09-15</th>
      <td>0.444060</td>
      <td>-0.201634</td>
      <td>-0.779404</td>
      <td>-0.384433</td>
    </tr>
    <tr>
      <th>2002-09-16</th>
      <td>0.595584</td>
      <td>-0.175267</td>
      <td>1.235172</td>
      <td>-1.034966</td>
    </tr>
    <tr>
      <th>2002-09-17</th>
      <td>1.040263</td>
      <td>0.276437</td>
      <td>2.503130</td>
      <td>0.301420</td>
    </tr>
    <tr>
      <th>2002-09-18</th>
      <td>-0.093274</td>
      <td>1.253880</td>
      <td>-0.368740</td>
      <td>0.556873</td>
    </tr>
    <tr>
      <th>2002-09-19</th>
      <td>0.271189</td>
      <td>1.276170</td>
      <td>-0.430888</td>
      <td>-1.451746</td>
    </tr>
    <tr>
      <th>2002-09-20</th>
      <td>-0.519482</td>
      <td>1.282916</td>
      <td>0.362977</td>
      <td>-1.652116</td>
    </tr>
    <tr>
      <th>2002-09-21</th>
      <td>1.457945</td>
      <td>0.275183</td>
      <td>-0.416305</td>
      <td>0.443211</td>
    </tr>
    <tr>
      <th>2002-09-22</th>
      <td>-1.193204</td>
      <td>0.541779</td>
      <td>-2.297856</td>
      <td>1.231795</td>
    </tr>
    <tr>
      <th>2002-09-23</th>
      <td>2.216243</td>
      <td>-0.720179</td>
      <td>-0.005217</td>
      <td>-0.564854</td>
    </tr>
    <tr>
      <th>2002-09-24</th>
      <td>1.407387</td>
      <td>1.876326</td>
      <td>0.949953</td>
      <td>0.304899</td>
    </tr>
    <tr>
      <th>2002-09-25</th>
      <td>1.351301</td>
      <td>-1.515127</td>
      <td>-0.182580</td>
      <td>-0.315225</td>
    </tr>
    <tr>
      <th>2002-09-26</th>
      <td>-0.044114</td>
      <td>-0.367083</td>
      <td>-0.261423</td>
      <td>-0.938703</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 4 columns</p>
</div>




```python
df.cumsum()
import matplotlib.pyplot as plt
plt.figure()
```




    <Figure size 432x288 with 0 Axes>




    <Figure size 432x288 with 0 Axes>



```python
df.plot()
#plt.legend(loc='best')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x203040c7e10>




![png](output_218_1.png)


### 数据的输入输出

### CSV

### 写入CSV文件
https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-store-in-csv


```python
df.to_csv('foo.csv')
```

### 读取CSV文件数据


```python
pd.read_csv('foo.csv')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000-01-01</td>
      <td>-0.403820</td>
      <td>-0.861685</td>
      <td>0.262125</td>
      <td>0.654910</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000-01-02</td>
      <td>1.768612</td>
      <td>-0.213129</td>
      <td>-0.719914</td>
      <td>-0.036541</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000-01-03</td>
      <td>0.102498</td>
      <td>1.443473</td>
      <td>-0.068096</td>
      <td>0.871774</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000-01-04</td>
      <td>0.747066</td>
      <td>-0.673786</td>
      <td>-0.294567</td>
      <td>-0.555684</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000-01-05</td>
      <td>2.122246</td>
      <td>-0.445726</td>
      <td>0.382663</td>
      <td>1.273366</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2000-01-06</td>
      <td>0.205880</td>
      <td>-0.725008</td>
      <td>0.713592</td>
      <td>1.050615</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2000-01-07</td>
      <td>-0.266623</td>
      <td>-0.836566</td>
      <td>1.113839</td>
      <td>-0.409689</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2000-01-08</td>
      <td>-0.441420</td>
      <td>-0.152557</td>
      <td>0.219731</td>
      <td>0.732548</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2000-01-09</td>
      <td>-1.517168</td>
      <td>-1.266140</td>
      <td>0.526676</td>
      <td>0.157710</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2000-01-10</td>
      <td>-0.555196</td>
      <td>-0.817628</td>
      <td>-0.619053</td>
      <td>-1.357579</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2000-01-11</td>
      <td>1.216180</td>
      <td>1.004558</td>
      <td>0.754348</td>
      <td>0.119537</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2000-01-12</td>
      <td>-1.560071</td>
      <td>1.356160</td>
      <td>0.659727</td>
      <td>-0.578732</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2000-01-13</td>
      <td>-0.344310</td>
      <td>-2.712881</td>
      <td>-1.729452</td>
      <td>0.354977</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2000-01-14</td>
      <td>-0.657705</td>
      <td>0.185932</td>
      <td>0.371227</td>
      <td>-1.030777</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2000-01-15</td>
      <td>-1.073826</td>
      <td>-0.441367</td>
      <td>-1.706187</td>
      <td>-0.512045</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2000-01-16</td>
      <td>0.900098</td>
      <td>0.188637</td>
      <td>0.230351</td>
      <td>1.310940</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2000-01-17</td>
      <td>0.797040</td>
      <td>0.268900</td>
      <td>0.533550</td>
      <td>-1.080641</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2000-01-18</td>
      <td>-0.391943</td>
      <td>0.196713</td>
      <td>0.033671</td>
      <td>-0.482255</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2000-01-19</td>
      <td>0.557491</td>
      <td>-0.085030</td>
      <td>-1.418595</td>
      <td>1.677838</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2000-01-20</td>
      <td>0.392006</td>
      <td>0.087150</td>
      <td>0.804150</td>
      <td>-0.148844</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2000-01-21</td>
      <td>-0.609433</td>
      <td>-0.687186</td>
      <td>-0.516820</td>
      <td>1.500974</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2000-01-22</td>
      <td>-0.060579</td>
      <td>0.462088</td>
      <td>0.616453</td>
      <td>0.615896</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2000-01-23</td>
      <td>-0.490724</td>
      <td>-2.208678</td>
      <td>0.187790</td>
      <td>-0.699064</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2000-01-24</td>
      <td>0.841364</td>
      <td>-0.120559</td>
      <td>1.021754</td>
      <td>0.285857</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2000-01-25</td>
      <td>1.712944</td>
      <td>0.479250</td>
      <td>-0.411576</td>
      <td>-2.496946</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2000-01-26</td>
      <td>2.476162</td>
      <td>-0.742174</td>
      <td>0.384957</td>
      <td>-1.561012</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2000-01-27</td>
      <td>-0.169507</td>
      <td>1.491176</td>
      <td>0.225953</td>
      <td>-0.171110</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2000-01-28</td>
      <td>-0.326795</td>
      <td>-0.928639</td>
      <td>-0.077926</td>
      <td>-0.383463</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2000-01-29</td>
      <td>0.914927</td>
      <td>-1.116768</td>
      <td>-1.123061</td>
      <td>1.152875</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2000-01-30</td>
      <td>-0.365077</td>
      <td>1.626579</td>
      <td>-0.919300</td>
      <td>-0.557889</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>970</th>
      <td>2002-08-28</td>
      <td>0.547606</td>
      <td>0.101673</td>
      <td>1.701981</td>
      <td>0.655521</td>
    </tr>
    <tr>
      <th>971</th>
      <td>2002-08-29</td>
      <td>-0.932057</td>
      <td>-0.732842</td>
      <td>-0.435287</td>
      <td>-0.412881</td>
    </tr>
    <tr>
      <th>972</th>
      <td>2002-08-30</td>
      <td>0.302205</td>
      <td>-1.569959</td>
      <td>-1.974306</td>
      <td>0.325171</td>
    </tr>
    <tr>
      <th>973</th>
      <td>2002-08-31</td>
      <td>1.094880</td>
      <td>-0.491747</td>
      <td>1.469688</td>
      <td>1.004903</td>
    </tr>
    <tr>
      <th>974</th>
      <td>2002-09-01</td>
      <td>-1.469820</td>
      <td>0.060895</td>
      <td>0.365955</td>
      <td>-1.579292</td>
    </tr>
    <tr>
      <th>975</th>
      <td>2002-09-02</td>
      <td>0.607064</td>
      <td>-0.198070</td>
      <td>0.816608</td>
      <td>1.396972</td>
    </tr>
    <tr>
      <th>976</th>
      <td>2002-09-03</td>
      <td>0.321749</td>
      <td>1.838613</td>
      <td>-0.883205</td>
      <td>-0.385823</td>
    </tr>
    <tr>
      <th>977</th>
      <td>2002-09-04</td>
      <td>-0.169855</td>
      <td>1.845828</td>
      <td>1.493554</td>
      <td>-0.889160</td>
    </tr>
    <tr>
      <th>978</th>
      <td>2002-09-05</td>
      <td>-0.511920</td>
      <td>-0.768413</td>
      <td>-0.789903</td>
      <td>1.801745</td>
    </tr>
    <tr>
      <th>979</th>
      <td>2002-09-06</td>
      <td>-0.391134</td>
      <td>-0.528561</td>
      <td>0.381485</td>
      <td>0.708959</td>
    </tr>
    <tr>
      <th>980</th>
      <td>2002-09-07</td>
      <td>0.587261</td>
      <td>0.755504</td>
      <td>-0.214899</td>
      <td>-1.053086</td>
    </tr>
    <tr>
      <th>981</th>
      <td>2002-09-08</td>
      <td>-0.541301</td>
      <td>0.941833</td>
      <td>0.615887</td>
      <td>0.826595</td>
    </tr>
    <tr>
      <th>982</th>
      <td>2002-09-09</td>
      <td>0.082876</td>
      <td>-0.923984</td>
      <td>-1.156417</td>
      <td>-1.812171</td>
    </tr>
    <tr>
      <th>983</th>
      <td>2002-09-10</td>
      <td>-2.176130</td>
      <td>-0.112087</td>
      <td>0.632639</td>
      <td>-1.752319</td>
    </tr>
    <tr>
      <th>984</th>
      <td>2002-09-11</td>
      <td>0.839755</td>
      <td>-0.022035</td>
      <td>0.269522</td>
      <td>-2.404917</td>
    </tr>
    <tr>
      <th>985</th>
      <td>2002-09-12</td>
      <td>-0.835131</td>
      <td>0.620688</td>
      <td>-0.547198</td>
      <td>2.732546</td>
    </tr>
    <tr>
      <th>986</th>
      <td>2002-09-13</td>
      <td>0.156933</td>
      <td>1.559828</td>
      <td>-1.184098</td>
      <td>1.929225</td>
    </tr>
    <tr>
      <th>987</th>
      <td>2002-09-14</td>
      <td>0.154408</td>
      <td>-2.932961</td>
      <td>0.716624</td>
      <td>2.171355</td>
    </tr>
    <tr>
      <th>988</th>
      <td>2002-09-15</td>
      <td>0.444060</td>
      <td>-0.201634</td>
      <td>-0.779404</td>
      <td>-0.384433</td>
    </tr>
    <tr>
      <th>989</th>
      <td>2002-09-16</td>
      <td>0.595584</td>
      <td>-0.175267</td>
      <td>1.235172</td>
      <td>-1.034966</td>
    </tr>
    <tr>
      <th>990</th>
      <td>2002-09-17</td>
      <td>1.040263</td>
      <td>0.276437</td>
      <td>2.503130</td>
      <td>0.301420</td>
    </tr>
    <tr>
      <th>991</th>
      <td>2002-09-18</td>
      <td>-0.093274</td>
      <td>1.253880</td>
      <td>-0.368740</td>
      <td>0.556873</td>
    </tr>
    <tr>
      <th>992</th>
      <td>2002-09-19</td>
      <td>0.271189</td>
      <td>1.276170</td>
      <td>-0.430888</td>
      <td>-1.451746</td>
    </tr>
    <tr>
      <th>993</th>
      <td>2002-09-20</td>
      <td>-0.519482</td>
      <td>1.282916</td>
      <td>0.362977</td>
      <td>-1.652116</td>
    </tr>
    <tr>
      <th>994</th>
      <td>2002-09-21</td>
      <td>1.457945</td>
      <td>0.275183</td>
      <td>-0.416305</td>
      <td>0.443211</td>
    </tr>
    <tr>
      <th>995</th>
      <td>2002-09-22</td>
      <td>-1.193204</td>
      <td>0.541779</td>
      <td>-2.297856</td>
      <td>1.231795</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2002-09-23</td>
      <td>2.216243</td>
      <td>-0.720179</td>
      <td>-0.005217</td>
      <td>-0.564854</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2002-09-24</td>
      <td>1.407387</td>
      <td>1.876326</td>
      <td>0.949953</td>
      <td>0.304899</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2002-09-25</td>
      <td>1.351301</td>
      <td>-1.515127</td>
      <td>-0.182580</td>
      <td>-0.315225</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2002-09-26</td>
      <td>-0.044114</td>
      <td>-0.367083</td>
      <td>-0.261423</td>
      <td>-0.938703</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 5 columns</p>
</div>



### HDF5

### 详见HDFStores文档
https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-hdf5

#### 写入HDF5Store


```python
df.to_hdf('foo.h5','df')
```

#### 读取HDF5 Store


```python
pd.read_hdf('foo.h5','df')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-01</th>
      <td>-0.403820</td>
      <td>-0.861685</td>
      <td>0.262125</td>
      <td>0.654910</td>
    </tr>
    <tr>
      <th>2000-01-02</th>
      <td>1.768612</td>
      <td>-0.213129</td>
      <td>-0.719914</td>
      <td>-0.036541</td>
    </tr>
    <tr>
      <th>2000-01-03</th>
      <td>0.102498</td>
      <td>1.443473</td>
      <td>-0.068096</td>
      <td>0.871774</td>
    </tr>
    <tr>
      <th>2000-01-04</th>
      <td>0.747066</td>
      <td>-0.673786</td>
      <td>-0.294567</td>
      <td>-0.555684</td>
    </tr>
    <tr>
      <th>2000-01-05</th>
      <td>2.122246</td>
      <td>-0.445726</td>
      <td>0.382663</td>
      <td>1.273366</td>
    </tr>
    <tr>
      <th>2000-01-06</th>
      <td>0.205880</td>
      <td>-0.725008</td>
      <td>0.713592</td>
      <td>1.050615</td>
    </tr>
    <tr>
      <th>2000-01-07</th>
      <td>-0.266623</td>
      <td>-0.836566</td>
      <td>1.113839</td>
      <td>-0.409689</td>
    </tr>
    <tr>
      <th>2000-01-08</th>
      <td>-0.441420</td>
      <td>-0.152557</td>
      <td>0.219731</td>
      <td>0.732548</td>
    </tr>
    <tr>
      <th>2000-01-09</th>
      <td>-1.517168</td>
      <td>-1.266140</td>
      <td>0.526676</td>
      <td>0.157710</td>
    </tr>
    <tr>
      <th>2000-01-10</th>
      <td>-0.555196</td>
      <td>-0.817628</td>
      <td>-0.619053</td>
      <td>-1.357579</td>
    </tr>
    <tr>
      <th>2000-01-11</th>
      <td>1.216180</td>
      <td>1.004558</td>
      <td>0.754348</td>
      <td>0.119537</td>
    </tr>
    <tr>
      <th>2000-01-12</th>
      <td>-1.560071</td>
      <td>1.356160</td>
      <td>0.659727</td>
      <td>-0.578732</td>
    </tr>
    <tr>
      <th>2000-01-13</th>
      <td>-0.344310</td>
      <td>-2.712881</td>
      <td>-1.729452</td>
      <td>0.354977</td>
    </tr>
    <tr>
      <th>2000-01-14</th>
      <td>-0.657705</td>
      <td>0.185932</td>
      <td>0.371227</td>
      <td>-1.030777</td>
    </tr>
    <tr>
      <th>2000-01-15</th>
      <td>-1.073826</td>
      <td>-0.441367</td>
      <td>-1.706187</td>
      <td>-0.512045</td>
    </tr>
    <tr>
      <th>2000-01-16</th>
      <td>0.900098</td>
      <td>0.188637</td>
      <td>0.230351</td>
      <td>1.310940</td>
    </tr>
    <tr>
      <th>2000-01-17</th>
      <td>0.797040</td>
      <td>0.268900</td>
      <td>0.533550</td>
      <td>-1.080641</td>
    </tr>
    <tr>
      <th>2000-01-18</th>
      <td>-0.391943</td>
      <td>0.196713</td>
      <td>0.033671</td>
      <td>-0.482255</td>
    </tr>
    <tr>
      <th>2000-01-19</th>
      <td>0.557491</td>
      <td>-0.085030</td>
      <td>-1.418595</td>
      <td>1.677838</td>
    </tr>
    <tr>
      <th>2000-01-20</th>
      <td>0.392006</td>
      <td>0.087150</td>
      <td>0.804150</td>
      <td>-0.148844</td>
    </tr>
    <tr>
      <th>2000-01-21</th>
      <td>-0.609433</td>
      <td>-0.687186</td>
      <td>-0.516820</td>
      <td>1.500974</td>
    </tr>
    <tr>
      <th>2000-01-22</th>
      <td>-0.060579</td>
      <td>0.462088</td>
      <td>0.616453</td>
      <td>0.615896</td>
    </tr>
    <tr>
      <th>2000-01-23</th>
      <td>-0.490724</td>
      <td>-2.208678</td>
      <td>0.187790</td>
      <td>-0.699064</td>
    </tr>
    <tr>
      <th>2000-01-24</th>
      <td>0.841364</td>
      <td>-0.120559</td>
      <td>1.021754</td>
      <td>0.285857</td>
    </tr>
    <tr>
      <th>2000-01-25</th>
      <td>1.712944</td>
      <td>0.479250</td>
      <td>-0.411576</td>
      <td>-2.496946</td>
    </tr>
    <tr>
      <th>2000-01-26</th>
      <td>2.476162</td>
      <td>-0.742174</td>
      <td>0.384957</td>
      <td>-1.561012</td>
    </tr>
    <tr>
      <th>2000-01-27</th>
      <td>-0.169507</td>
      <td>1.491176</td>
      <td>0.225953</td>
      <td>-0.171110</td>
    </tr>
    <tr>
      <th>2000-01-28</th>
      <td>-0.326795</td>
      <td>-0.928639</td>
      <td>-0.077926</td>
      <td>-0.383463</td>
    </tr>
    <tr>
      <th>2000-01-29</th>
      <td>0.914927</td>
      <td>-1.116768</td>
      <td>-1.123061</td>
      <td>1.152875</td>
    </tr>
    <tr>
      <th>2000-01-30</th>
      <td>-0.365077</td>
      <td>1.626579</td>
      <td>-0.919300</td>
      <td>-0.557889</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2002-08-28</th>
      <td>0.547606</td>
      <td>0.101673</td>
      <td>1.701981</td>
      <td>0.655521</td>
    </tr>
    <tr>
      <th>2002-08-29</th>
      <td>-0.932057</td>
      <td>-0.732842</td>
      <td>-0.435287</td>
      <td>-0.412881</td>
    </tr>
    <tr>
      <th>2002-08-30</th>
      <td>0.302205</td>
      <td>-1.569959</td>
      <td>-1.974306</td>
      <td>0.325171</td>
    </tr>
    <tr>
      <th>2002-08-31</th>
      <td>1.094880</td>
      <td>-0.491747</td>
      <td>1.469688</td>
      <td>1.004903</td>
    </tr>
    <tr>
      <th>2002-09-01</th>
      <td>-1.469820</td>
      <td>0.060895</td>
      <td>0.365955</td>
      <td>-1.579292</td>
    </tr>
    <tr>
      <th>2002-09-02</th>
      <td>0.607064</td>
      <td>-0.198070</td>
      <td>0.816608</td>
      <td>1.396972</td>
    </tr>
    <tr>
      <th>2002-09-03</th>
      <td>0.321749</td>
      <td>1.838613</td>
      <td>-0.883205</td>
      <td>-0.385823</td>
    </tr>
    <tr>
      <th>2002-09-04</th>
      <td>-0.169855</td>
      <td>1.845828</td>
      <td>1.493554</td>
      <td>-0.889160</td>
    </tr>
    <tr>
      <th>2002-09-05</th>
      <td>-0.511920</td>
      <td>-0.768413</td>
      <td>-0.789903</td>
      <td>1.801745</td>
    </tr>
    <tr>
      <th>2002-09-06</th>
      <td>-0.391134</td>
      <td>-0.528561</td>
      <td>0.381485</td>
      <td>0.708959</td>
    </tr>
    <tr>
      <th>2002-09-07</th>
      <td>0.587261</td>
      <td>0.755504</td>
      <td>-0.214899</td>
      <td>-1.053086</td>
    </tr>
    <tr>
      <th>2002-09-08</th>
      <td>-0.541301</td>
      <td>0.941833</td>
      <td>0.615887</td>
      <td>0.826595</td>
    </tr>
    <tr>
      <th>2002-09-09</th>
      <td>0.082876</td>
      <td>-0.923984</td>
      <td>-1.156417</td>
      <td>-1.812171</td>
    </tr>
    <tr>
      <th>2002-09-10</th>
      <td>-2.176130</td>
      <td>-0.112087</td>
      <td>0.632639</td>
      <td>-1.752319</td>
    </tr>
    <tr>
      <th>2002-09-11</th>
      <td>0.839755</td>
      <td>-0.022035</td>
      <td>0.269522</td>
      <td>-2.404917</td>
    </tr>
    <tr>
      <th>2002-09-12</th>
      <td>-0.835131</td>
      <td>0.620688</td>
      <td>-0.547198</td>
      <td>2.732546</td>
    </tr>
    <tr>
      <th>2002-09-13</th>
      <td>0.156933</td>
      <td>1.559828</td>
      <td>-1.184098</td>
      <td>1.929225</td>
    </tr>
    <tr>
      <th>2002-09-14</th>
      <td>0.154408</td>
      <td>-2.932961</td>
      <td>0.716624</td>
      <td>2.171355</td>
    </tr>
    <tr>
      <th>2002-09-15</th>
      <td>0.444060</td>
      <td>-0.201634</td>
      <td>-0.779404</td>
      <td>-0.384433</td>
    </tr>
    <tr>
      <th>2002-09-16</th>
      <td>0.595584</td>
      <td>-0.175267</td>
      <td>1.235172</td>
      <td>-1.034966</td>
    </tr>
    <tr>
      <th>2002-09-17</th>
      <td>1.040263</td>
      <td>0.276437</td>
      <td>2.503130</td>
      <td>0.301420</td>
    </tr>
    <tr>
      <th>2002-09-18</th>
      <td>-0.093274</td>
      <td>1.253880</td>
      <td>-0.368740</td>
      <td>0.556873</td>
    </tr>
    <tr>
      <th>2002-09-19</th>
      <td>0.271189</td>
      <td>1.276170</td>
      <td>-0.430888</td>
      <td>-1.451746</td>
    </tr>
    <tr>
      <th>2002-09-20</th>
      <td>-0.519482</td>
      <td>1.282916</td>
      <td>0.362977</td>
      <td>-1.652116</td>
    </tr>
    <tr>
      <th>2002-09-21</th>
      <td>1.457945</td>
      <td>0.275183</td>
      <td>-0.416305</td>
      <td>0.443211</td>
    </tr>
    <tr>
      <th>2002-09-22</th>
      <td>-1.193204</td>
      <td>0.541779</td>
      <td>-2.297856</td>
      <td>1.231795</td>
    </tr>
    <tr>
      <th>2002-09-23</th>
      <td>2.216243</td>
      <td>-0.720179</td>
      <td>-0.005217</td>
      <td>-0.564854</td>
    </tr>
    <tr>
      <th>2002-09-24</th>
      <td>1.407387</td>
      <td>1.876326</td>
      <td>0.949953</td>
      <td>0.304899</td>
    </tr>
    <tr>
      <th>2002-09-25</th>
      <td>1.351301</td>
      <td>-1.515127</td>
      <td>-0.182580</td>
      <td>-0.315225</td>
    </tr>
    <tr>
      <th>2002-09-26</th>
      <td>-0.044114</td>
      <td>-0.367083</td>
      <td>-0.261423</td>
      <td>-0.938703</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 4 columns</p>
</div>



#### 详见Excel文档
https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-excel

#### 写入Excel文件


```python
df.to_excel('foo.xlsx',sheet_name='Sheet1')
```

#### 读取Excel文件


```python
pd.read_excel('foo.xlsx','Sheet1',index_col=None,na_values=['NA'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000-01-01</td>
      <td>-0.403820</td>
      <td>-0.861685</td>
      <td>0.262125</td>
      <td>0.654910</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000-01-02</td>
      <td>1.768612</td>
      <td>-0.213129</td>
      <td>-0.719914</td>
      <td>-0.036541</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000-01-03</td>
      <td>0.102498</td>
      <td>1.443473</td>
      <td>-0.068096</td>
      <td>0.871774</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000-01-04</td>
      <td>0.747066</td>
      <td>-0.673786</td>
      <td>-0.294567</td>
      <td>-0.555684</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000-01-05</td>
      <td>2.122246</td>
      <td>-0.445726</td>
      <td>0.382663</td>
      <td>1.273366</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2000-01-06</td>
      <td>0.205880</td>
      <td>-0.725008</td>
      <td>0.713592</td>
      <td>1.050615</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2000-01-07</td>
      <td>-0.266623</td>
      <td>-0.836566</td>
      <td>1.113839</td>
      <td>-0.409689</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2000-01-08</td>
      <td>-0.441420</td>
      <td>-0.152557</td>
      <td>0.219731</td>
      <td>0.732548</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2000-01-09</td>
      <td>-1.517168</td>
      <td>-1.266140</td>
      <td>0.526676</td>
      <td>0.157710</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2000-01-10</td>
      <td>-0.555196</td>
      <td>-0.817628</td>
      <td>-0.619053</td>
      <td>-1.357579</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2000-01-11</td>
      <td>1.216180</td>
      <td>1.004558</td>
      <td>0.754348</td>
      <td>0.119537</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2000-01-12</td>
      <td>-1.560071</td>
      <td>1.356160</td>
      <td>0.659727</td>
      <td>-0.578732</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2000-01-13</td>
      <td>-0.344310</td>
      <td>-2.712881</td>
      <td>-1.729452</td>
      <td>0.354977</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2000-01-14</td>
      <td>-0.657705</td>
      <td>0.185932</td>
      <td>0.371227</td>
      <td>-1.030777</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2000-01-15</td>
      <td>-1.073826</td>
      <td>-0.441367</td>
      <td>-1.706187</td>
      <td>-0.512045</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2000-01-16</td>
      <td>0.900098</td>
      <td>0.188637</td>
      <td>0.230351</td>
      <td>1.310940</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2000-01-17</td>
      <td>0.797040</td>
      <td>0.268900</td>
      <td>0.533550</td>
      <td>-1.080641</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2000-01-18</td>
      <td>-0.391943</td>
      <td>0.196713</td>
      <td>0.033671</td>
      <td>-0.482255</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2000-01-19</td>
      <td>0.557491</td>
      <td>-0.085030</td>
      <td>-1.418595</td>
      <td>1.677838</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2000-01-20</td>
      <td>0.392006</td>
      <td>0.087150</td>
      <td>0.804150</td>
      <td>-0.148844</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2000-01-21</td>
      <td>-0.609433</td>
      <td>-0.687186</td>
      <td>-0.516820</td>
      <td>1.500974</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2000-01-22</td>
      <td>-0.060579</td>
      <td>0.462088</td>
      <td>0.616453</td>
      <td>0.615896</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2000-01-23</td>
      <td>-0.490724</td>
      <td>-2.208678</td>
      <td>0.187790</td>
      <td>-0.699064</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2000-01-24</td>
      <td>0.841364</td>
      <td>-0.120559</td>
      <td>1.021754</td>
      <td>0.285857</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2000-01-25</td>
      <td>1.712944</td>
      <td>0.479250</td>
      <td>-0.411576</td>
      <td>-2.496946</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2000-01-26</td>
      <td>2.476162</td>
      <td>-0.742174</td>
      <td>0.384957</td>
      <td>-1.561012</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2000-01-27</td>
      <td>-0.169507</td>
      <td>1.491176</td>
      <td>0.225953</td>
      <td>-0.171110</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2000-01-28</td>
      <td>-0.326795</td>
      <td>-0.928639</td>
      <td>-0.077926</td>
      <td>-0.383463</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2000-01-29</td>
      <td>0.914927</td>
      <td>-1.116768</td>
      <td>-1.123061</td>
      <td>1.152875</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2000-01-30</td>
      <td>-0.365077</td>
      <td>1.626579</td>
      <td>-0.919300</td>
      <td>-0.557889</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>970</th>
      <td>2002-08-28</td>
      <td>0.547606</td>
      <td>0.101673</td>
      <td>1.701981</td>
      <td>0.655521</td>
    </tr>
    <tr>
      <th>971</th>
      <td>2002-08-29</td>
      <td>-0.932057</td>
      <td>-0.732842</td>
      <td>-0.435287</td>
      <td>-0.412881</td>
    </tr>
    <tr>
      <th>972</th>
      <td>2002-08-30</td>
      <td>0.302205</td>
      <td>-1.569959</td>
      <td>-1.974306</td>
      <td>0.325171</td>
    </tr>
    <tr>
      <th>973</th>
      <td>2002-08-31</td>
      <td>1.094880</td>
      <td>-0.491747</td>
      <td>1.469688</td>
      <td>1.004903</td>
    </tr>
    <tr>
      <th>974</th>
      <td>2002-09-01</td>
      <td>-1.469820</td>
      <td>0.060895</td>
      <td>0.365955</td>
      <td>-1.579292</td>
    </tr>
    <tr>
      <th>975</th>
      <td>2002-09-02</td>
      <td>0.607064</td>
      <td>-0.198070</td>
      <td>0.816608</td>
      <td>1.396972</td>
    </tr>
    <tr>
      <th>976</th>
      <td>2002-09-03</td>
      <td>0.321749</td>
      <td>1.838613</td>
      <td>-0.883205</td>
      <td>-0.385823</td>
    </tr>
    <tr>
      <th>977</th>
      <td>2002-09-04</td>
      <td>-0.169855</td>
      <td>1.845828</td>
      <td>1.493554</td>
      <td>-0.889160</td>
    </tr>
    <tr>
      <th>978</th>
      <td>2002-09-05</td>
      <td>-0.511920</td>
      <td>-0.768413</td>
      <td>-0.789903</td>
      <td>1.801745</td>
    </tr>
    <tr>
      <th>979</th>
      <td>2002-09-06</td>
      <td>-0.391134</td>
      <td>-0.528561</td>
      <td>0.381485</td>
      <td>0.708959</td>
    </tr>
    <tr>
      <th>980</th>
      <td>2002-09-07</td>
      <td>0.587261</td>
      <td>0.755504</td>
      <td>-0.214899</td>
      <td>-1.053086</td>
    </tr>
    <tr>
      <th>981</th>
      <td>2002-09-08</td>
      <td>-0.541301</td>
      <td>0.941833</td>
      <td>0.615887</td>
      <td>0.826595</td>
    </tr>
    <tr>
      <th>982</th>
      <td>2002-09-09</td>
      <td>0.082876</td>
      <td>-0.923984</td>
      <td>-1.156417</td>
      <td>-1.812171</td>
    </tr>
    <tr>
      <th>983</th>
      <td>2002-09-10</td>
      <td>-2.176130</td>
      <td>-0.112087</td>
      <td>0.632639</td>
      <td>-1.752319</td>
    </tr>
    <tr>
      <th>984</th>
      <td>2002-09-11</td>
      <td>0.839755</td>
      <td>-0.022035</td>
      <td>0.269522</td>
      <td>-2.404917</td>
    </tr>
    <tr>
      <th>985</th>
      <td>2002-09-12</td>
      <td>-0.835131</td>
      <td>0.620688</td>
      <td>-0.547198</td>
      <td>2.732546</td>
    </tr>
    <tr>
      <th>986</th>
      <td>2002-09-13</td>
      <td>0.156933</td>
      <td>1.559828</td>
      <td>-1.184098</td>
      <td>1.929225</td>
    </tr>
    <tr>
      <th>987</th>
      <td>2002-09-14</td>
      <td>0.154408</td>
      <td>-2.932961</td>
      <td>0.716624</td>
      <td>2.171355</td>
    </tr>
    <tr>
      <th>988</th>
      <td>2002-09-15</td>
      <td>0.444060</td>
      <td>-0.201634</td>
      <td>-0.779404</td>
      <td>-0.384433</td>
    </tr>
    <tr>
      <th>989</th>
      <td>2002-09-16</td>
      <td>0.595584</td>
      <td>-0.175267</td>
      <td>1.235172</td>
      <td>-1.034966</td>
    </tr>
    <tr>
      <th>990</th>
      <td>2002-09-17</td>
      <td>1.040263</td>
      <td>0.276437</td>
      <td>2.503130</td>
      <td>0.301420</td>
    </tr>
    <tr>
      <th>991</th>
      <td>2002-09-18</td>
      <td>-0.093274</td>
      <td>1.253880</td>
      <td>-0.368740</td>
      <td>0.556873</td>
    </tr>
    <tr>
      <th>992</th>
      <td>2002-09-19</td>
      <td>0.271189</td>
      <td>1.276170</td>
      <td>-0.430888</td>
      <td>-1.451746</td>
    </tr>
    <tr>
      <th>993</th>
      <td>2002-09-20</td>
      <td>-0.519482</td>
      <td>1.282916</td>
      <td>0.362977</td>
      <td>-1.652116</td>
    </tr>
    <tr>
      <th>994</th>
      <td>2002-09-21</td>
      <td>1.457945</td>
      <td>0.275183</td>
      <td>-0.416305</td>
      <td>0.443211</td>
    </tr>
    <tr>
      <th>995</th>
      <td>2002-09-22</td>
      <td>-1.193204</td>
      <td>0.541779</td>
      <td>-2.297856</td>
      <td>1.231795</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2002-09-23</td>
      <td>2.216243</td>
      <td>-0.720179</td>
      <td>-0.005217</td>
      <td>-0.564854</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2002-09-24</td>
      <td>1.407387</td>
      <td>1.876326</td>
      <td>0.949953</td>
      <td>0.304899</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2002-09-25</td>
      <td>1.351301</td>
      <td>-1.515127</td>
      <td>-0.182580</td>
      <td>-0.315225</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2002-09-26</td>
      <td>-0.044114</td>
      <td>-0.367083</td>
      <td>-0.261423</td>
      <td>-0.938703</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 5 columns</p>
</div>



### 各种坑（Gotchas）

#### 执行某些操作，将触发异常，如


```python
if pd.Series([False,True,False]):
    print('I was true')
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-197-4386126a9bba> in <module>
    ----> 1 if pd.Series([False,True,False]):
          2     print('I was true')
    

    D:\Anaconda3\lib\site-packages\pandas\core\generic.py in __nonzero__(self)
       1476         raise ValueError("The truth value of a {0} is ambiguous. "
       1477                          "Use a.empty, a.bool(), a.item(), a.any() or a.all()."
    -> 1478                          .format(self.__class__.__name__))
       1479 
       1480     __bool__ = __nonzero__
    

    ValueError: The truth value of a Series is ambiguous. Use a.empty, a.bool(), a.item(), a.any() or a.all().


#### 参阅比较操作文档，查看错误提示与解决方案
https://pandas.pydata.org/pandas-docs/stable/getting_started/basics.html#basics-compare

#### 详见各种坑文档


```python

```
