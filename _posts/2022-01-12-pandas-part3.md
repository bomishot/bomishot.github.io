---
layout: single
title:  "PART3 데이터 살펴보기"
categories: coding
tag: [python, blog, pandas]
toc: true
author_profile: false
---

<head>
  <style>
    table.dataframe {
      white-space: normal;
      width: 100%;
      height: 240px;
      display: block;
      overflow: auto;
      font-family: Arial, sans-serif;
      font-size: 0.9rem;
      line-height: 20px;
      text-align: center;
      border: 0px !important;
    }

    table.dataframe th {
      text-align: center;
      font-weight: bold;
      padding: 8px;
    }

    table.dataframe td {
      text-align: center;
      padding: 8px;
    }

    table.dataframe tr:hover {
      background: #b8d1f3; 
    }

    .output_prompt {
      overflow: auto;
      font-size: 0.9rem;
      line-height: 1.45;
      border-radius: 0.3rem;
      -webkit-overflow-scrolling: touch;
      padding: 0.8rem;
      margin-top: 0;
      margin-bottom: 15px;
      font: 1rem Consolas, "Liberation Mono", Menlo, Courier, monospace;
      color: $code-text-color;
      border: solid 1px $border-color;
      border-radius: 0.3rem;
      word-break: normal;
      white-space: pre;
    }

  .dataframe tbody tr th:only-of-type {
      vertical-align: middle;
  }

  .dataframe tbody tr th {
      vertical-align: top;
  }

  .dataframe thead th {
      text-align: center !important;
      padding: 8px;
  }

  .page__content p {
      margin: 0 0 0px !important;
  }

  .page__content p > strong {
    font-size: 0.8rem !important;
  }

  </style>
</head>





# 1. 데이터프레임의 구조

UCI 머신러닝 저장소에서 제공하는 자동차 연비(auto mpg) 데이터셋 사용.


데이터 내용 미리보기 : head() /tail() /디폴트값:5



```python
import pandas as pd
df = pd.read_csv('C:/Users/USER/Desktop/auto-mpg.csv')
df.columns = ['mpg', 'cylinders','displacement', 'horsepower', 'weight', 'acceleration', 'model year', 'origin', 'name']
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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>model year</th>
      <th>origin</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15.0</td>
      <td>8</td>
      <td>350.0</td>
      <td>165</td>
      <td>3693</td>
      <td>11.5</td>
      <td>70</td>
      <td>1</td>
      <td>buick skylark 320</td>
    </tr>
    <tr>
      <th>1</th>
      <td>18.0</td>
      <td>8</td>
      <td>318.0</td>
      <td>150</td>
      <td>3436</td>
      <td>11.0</td>
      <td>70</td>
      <td>1</td>
      <td>plymouth satellite</td>
    </tr>
    <tr>
      <th>2</th>
      <td>16.0</td>
      <td>8</td>
      <td>304.0</td>
      <td>150</td>
      <td>3433</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>amc rebel sst</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17.0</td>
      <td>8</td>
      <td>302.0</td>
      <td>140</td>
      <td>3449</td>
      <td>10.5</td>
      <td>70</td>
      <td>1</td>
      <td>ford torino</td>
    </tr>
    <tr>
      <th>4</th>
      <td>15.0</td>
      <td>8</td>
      <td>429.0</td>
      <td>198</td>
      <td>4341</td>
      <td>10.0</td>
      <td>70</td>
      <td>1</td>
      <td>ford galaxie 500</td>
    </tr>
  </tbody>
</table>
</div>



```python
df.tail()
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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>model year</th>
      <th>origin</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>392</th>
      <td>27.0</td>
      <td>4</td>
      <td>140.0</td>
      <td>86</td>
      <td>2790</td>
      <td>15.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford mustang gl</td>
    </tr>
    <tr>
      <th>393</th>
      <td>44.0</td>
      <td>4</td>
      <td>97.0</td>
      <td>52</td>
      <td>2130</td>
      <td>24.6</td>
      <td>82</td>
      <td>2</td>
      <td>vw pickup</td>
    </tr>
    <tr>
      <th>394</th>
      <td>32.0</td>
      <td>4</td>
      <td>135.0</td>
      <td>84</td>
      <td>2295</td>
      <td>11.6</td>
      <td>82</td>
      <td>1</td>
      <td>dodge rampage</td>
    </tr>
    <tr>
      <th>395</th>
      <td>28.0</td>
      <td>4</td>
      <td>120.0</td>
      <td>79</td>
      <td>2625</td>
      <td>18.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford ranger</td>
    </tr>
    <tr>
      <th>396</th>
      <td>31.0</td>
      <td>4</td>
      <td>119.0</td>
      <td>82</td>
      <td>2720</td>
      <td>19.4</td>
      <td>82</td>
      <td>1</td>
      <td>chevy s-10</td>
    </tr>
  </tbody>
</table>
</div>


데이터 요약 정보 확인하기

- df의 크기(행,열): shape (행의 갯수, 열의 갯수)

- df의 기본 정보: info (클래스 유형, 행 인덱스의 구성, 열 이름의 종류와 개수, 열의 자료형과 개수, 메모리 할당량...)

- df의 자료형 확인 : dtypes

- df의 열의 자료형 확인 : mpg.dtypes

- df의 기술 통계 정보 요약 : describe (산술데이터값의 평균, 표준편차,최댓값,최소값, 중간값...)



```python
df.shape
```

<pre>
(397, 9)
</pre>

```python
df.info()
```

<pre>
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 397 entries, 0 to 396
Data columns (total 9 columns):
 #   Column        Non-Null Count  Dtype  
---  ------        --------------  -----  
 0   mpg           397 non-null    float64
 1   cylinders     397 non-null    int64  
 2   displacement  397 non-null    float64
 3   horsepower    397 non-null    object 
 4   weight        397 non-null    int64  
 5   acceleration  397 non-null    float64
 6   model year    397 non-null    int64  
 7   origin        397 non-null    int64  
 8   name          397 non-null    object 
dtypes: float64(3), int64(4), object(2)
memory usage: 28.0+ KB
</pre>

```python
df.dtypes
```

<pre>
mpg             float64
cylinders         int64
displacement    float64
horsepower       object
weight            int64
acceleration    float64
model year        int64
origin            int64
name             object
dtype: object
</pre>

```python
df.mpg.dtypes
```

<pre>
dtype('float64')
</pre>

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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>model year</th>
      <th>origin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>397.000000</td>
      <td>397.000000</td>
      <td>397.000000</td>
      <td>397.000000</td>
      <td>397.000000</td>
      <td>397.000000</td>
      <td>397.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>23.528463</td>
      <td>5.448363</td>
      <td>193.139798</td>
      <td>2969.080605</td>
      <td>15.577078</td>
      <td>76.025189</td>
      <td>1.574307</td>
    </tr>
    <tr>
      <th>std</th>
      <td>7.820926</td>
      <td>1.698329</td>
      <td>104.244898</td>
      <td>847.485218</td>
      <td>2.755326</td>
      <td>3.689922</td>
      <td>0.802549</td>
    </tr>
    <tr>
      <th>min</th>
      <td>9.000000</td>
      <td>3.000000</td>
      <td>68.000000</td>
      <td>1613.000000</td>
      <td>8.000000</td>
      <td>70.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>17.500000</td>
      <td>4.000000</td>
      <td>104.000000</td>
      <td>2223.000000</td>
      <td>13.900000</td>
      <td>73.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>23.000000</td>
      <td>4.000000</td>
      <td>146.000000</td>
      <td>2800.000000</td>
      <td>15.500000</td>
      <td>76.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>29.000000</td>
      <td>8.000000</td>
      <td>262.000000</td>
      <td>3609.000000</td>
      <td>17.200000</td>
      <td>79.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>46.600000</td>
      <td>8.000000</td>
      <td>455.000000</td>
      <td>5140.000000</td>
      <td>24.800000</td>
      <td>82.000000</td>
      <td>3.000000</td>
    </tr>
  </tbody>
</table>
</div>



```python
df.describe(include='all') 
# 산술데이터가 아닌 열에 대한 정보도 포함
# unique(고유값 개수), top(최빈값), freq(빈도수)
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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>model year</th>
      <th>origin</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>397.000000</td>
      <td>397.000000</td>
      <td>397.000000</td>
      <td>397</td>
      <td>397.000000</td>
      <td>397.000000</td>
      <td>397.000000</td>
      <td>397.000000</td>
      <td>397</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>94</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>305</td>
    </tr>
    <tr>
      <th>top</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>150</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ford pinto</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>23.528463</td>
      <td>5.448363</td>
      <td>193.139798</td>
      <td>NaN</td>
      <td>2969.080605</td>
      <td>15.577078</td>
      <td>76.025189</td>
      <td>1.574307</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>std</th>
      <td>7.820926</td>
      <td>1.698329</td>
      <td>104.244898</td>
      <td>NaN</td>
      <td>847.485218</td>
      <td>2.755326</td>
      <td>3.689922</td>
      <td>0.802549</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>min</th>
      <td>9.000000</td>
      <td>3.000000</td>
      <td>68.000000</td>
      <td>NaN</td>
      <td>1613.000000</td>
      <td>8.000000</td>
      <td>70.000000</td>
      <td>1.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>17.500000</td>
      <td>4.000000</td>
      <td>104.000000</td>
      <td>NaN</td>
      <td>2223.000000</td>
      <td>13.900000</td>
      <td>73.000000</td>
      <td>1.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>23.000000</td>
      <td>4.000000</td>
      <td>146.000000</td>
      <td>NaN</td>
      <td>2800.000000</td>
      <td>15.500000</td>
      <td>76.000000</td>
      <td>1.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>29.000000</td>
      <td>8.000000</td>
      <td>262.000000</td>
      <td>NaN</td>
      <td>3609.000000</td>
      <td>17.200000</td>
      <td>79.000000</td>
      <td>2.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>max</th>
      <td>46.600000</td>
      <td>8.000000</td>
      <td>455.000000</td>
      <td>NaN</td>
      <td>5140.000000</td>
      <td>24.800000</td>
      <td>82.000000</td>
      <td>3.000000</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>


데이터 개수 확인

- 각 열의 데이터 개수: count()

- 각 열의 고유값 개수: df["특정열"].value_counts()

                       df.특정열.value_counts()



```python
df.count()
```

<pre>
mpg             397
cylinders       397
displacement    397
horsepower      397
weight          397
acceleration    397
model year      397
origin          397
name            397
dtype: int64
</pre>

```python
type(df.count())
```

<pre>
pandas.core.series.Series
</pre>

```python
unique_values = df['origin'].value_counts()
unique_values
```

<pre>
1    248
3     79
2     70
Name: origin, dtype: int64
</pre>

```python
type(unique_values)
```

<pre>
pandas.core.series.Series
</pre>
# 2. 통계 함수 적용

- 평균값: mean()

- 중간값: median()

- 최댓값: max()

- 최솟값: min()

- 표준편차: std()

- 상관계수: corr()



```python
df.mean()
```

<pre>
mpg               23.528463
cylinders          5.448363
displacement     193.139798
weight          2969.080605
acceleration      15.577078
model year        76.025189
origin             1.574307
dtype: float64
</pre>

```python
df[['mpg', 'weight']].median()
```

<pre>
mpg         23.0
weight    2800.0
dtype: float64
</pre>

```python
df.mpg.max()
```

<pre>
46.6
</pre>

```python
df[['mpg','weight']].corr()
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
      <th>mpg</th>
      <th>weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mpg</th>
      <td>1.000000</td>
      <td>-0.831558</td>
    </tr>
    <tr>
      <th>weight</th>
      <td>-0.831558</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



```python
df.corr()
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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>model year</th>
      <th>origin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mpg</th>
      <td>1.000000</td>
      <td>-0.775412</td>
      <td>-0.803972</td>
      <td>-0.831558</td>
      <td>0.419133</td>
      <td>0.578667</td>
      <td>0.562894</td>
    </tr>
    <tr>
      <th>cylinders</th>
      <td>-0.775412</td>
      <td>1.000000</td>
      <td>0.950718</td>
      <td>0.896623</td>
      <td>-0.503016</td>
      <td>-0.344729</td>
      <td>-0.561796</td>
    </tr>
    <tr>
      <th>displacement</th>
      <td>-0.803972</td>
      <td>0.950718</td>
      <td>1.000000</td>
      <td>0.932957</td>
      <td>-0.542083</td>
      <td>-0.367470</td>
      <td>-0.608749</td>
    </tr>
    <tr>
      <th>weight</th>
      <td>-0.831558</td>
      <td>0.896623</td>
      <td>0.932957</td>
      <td>1.000000</td>
      <td>-0.416488</td>
      <td>-0.305150</td>
      <td>-0.580552</td>
    </tr>
    <tr>
      <th>acceleration</th>
      <td>0.419133</td>
      <td>-0.503016</td>
      <td>-0.542083</td>
      <td>-0.416488</td>
      <td>1.000000</td>
      <td>0.284376</td>
      <td>0.204102</td>
    </tr>
    <tr>
      <th>model year</th>
      <td>0.578667</td>
      <td>-0.344729</td>
      <td>-0.367470</td>
      <td>-0.305150</td>
      <td>0.284376</td>
      <td>1.000000</td>
      <td>0.178441</td>
    </tr>
    <tr>
      <th>origin</th>
      <td>0.562894</td>
      <td>-0.561796</td>
      <td>-0.608749</td>
      <td>-0.580552</td>
      <td>0.204102</td>
      <td>0.178441</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>


# 3. 판다스 내장 그래프 도구 활용

판다스는 Matplotlib 함수를 포함하고 있음/ 별도로 임포트X / kind 옵션으로 그래프 종류 선택


- 선 그래프 : df.plot()



```python
df1 = pd.read_excel('C:/Users/USER/Desktop/new/excel_example/남북한발전전력량.xlsx', engine='openpyxl')
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
      <th>전력량 (억㎾h)</th>
      <th>발전 전력별</th>
      <th>1990</th>
      <th>1991</th>
      <th>1992</th>
      <th>1993</th>
      <th>1994</th>
      <th>1995</th>
      <th>1996</th>
      <th>1997</th>
      <th>...</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>남한</td>
      <td>합계</td>
      <td>1077</td>
      <td>1186</td>
      <td>1310</td>
      <td>1444</td>
      <td>1650</td>
      <td>1847</td>
      <td>2055</td>
      <td>2244</td>
      <td>...</td>
      <td>4031</td>
      <td>4224</td>
      <td>4336</td>
      <td>4747</td>
      <td>4969</td>
      <td>5096</td>
      <td>5171</td>
      <td>5220</td>
      <td>5281</td>
      <td>5404</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>수력</td>
      <td>64</td>
      <td>51</td>
      <td>49</td>
      <td>60</td>
      <td>41</td>
      <td>55</td>
      <td>52</td>
      <td>54</td>
      <td>...</td>
      <td>50</td>
      <td>56</td>
      <td>56</td>
      <td>65</td>
      <td>78</td>
      <td>77</td>
      <td>84</td>
      <td>78</td>
      <td>58</td>
      <td>66</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>화력</td>
      <td>484</td>
      <td>573</td>
      <td>696</td>
      <td>803</td>
      <td>1022</td>
      <td>1122</td>
      <td>1264</td>
      <td>1420</td>
      <td>...</td>
      <td>2551</td>
      <td>2658</td>
      <td>2802</td>
      <td>3196</td>
      <td>3343</td>
      <td>3430</td>
      <td>3581</td>
      <td>3427</td>
      <td>3402</td>
      <td>3523</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>원자력</td>
      <td>529</td>
      <td>563</td>
      <td>565</td>
      <td>581</td>
      <td>587</td>
      <td>670</td>
      <td>739</td>
      <td>771</td>
      <td>...</td>
      <td>1429</td>
      <td>1510</td>
      <td>1478</td>
      <td>1486</td>
      <td>1547</td>
      <td>1503</td>
      <td>1388</td>
      <td>1564</td>
      <td>1648</td>
      <td>1620</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>신재생</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>...</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>86</td>
      <td>118</td>
      <td>151</td>
      <td>173</td>
      <td>195</td>
    </tr>
    <tr>
      <th>5</th>
      <td>북한</td>
      <td>합계</td>
      <td>277</td>
      <td>263</td>
      <td>247</td>
      <td>221</td>
      <td>231</td>
      <td>230</td>
      <td>213</td>
      <td>193</td>
      <td>...</td>
      <td>236</td>
      <td>255</td>
      <td>235</td>
      <td>237</td>
      <td>211</td>
      <td>215</td>
      <td>221</td>
      <td>216</td>
      <td>190</td>
      <td>239</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>수력</td>
      <td>156</td>
      <td>150</td>
      <td>142</td>
      <td>133</td>
      <td>138</td>
      <td>142</td>
      <td>125</td>
      <td>107</td>
      <td>...</td>
      <td>133</td>
      <td>141</td>
      <td>125</td>
      <td>134</td>
      <td>132</td>
      <td>135</td>
      <td>139</td>
      <td>130</td>
      <td>100</td>
      <td>128</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>화력</td>
      <td>121</td>
      <td>113</td>
      <td>105</td>
      <td>88</td>
      <td>93</td>
      <td>88</td>
      <td>88</td>
      <td>86</td>
      <td>...</td>
      <td>103</td>
      <td>114</td>
      <td>110</td>
      <td>103</td>
      <td>79</td>
      <td>80</td>
      <td>82</td>
      <td>86</td>
      <td>90</td>
      <td>111</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>원자력</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>...</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
  </tbody>
</table>
<p>9 rows × 29 columns</p>
</div>



```python
df1_ns = df1.iloc[[0,5],3:]
df1_ns.index = ['South', 'North']
df1_ns.columns = df1_ns.columns.map(int) # 열 자료형을 정수형으로 바꿔줌
df1_ns.plot()
```

<pre>
<matplotlib.axes._subplots.AxesSubplot at 0x27cba9c9880>
</pre>
<img src="data:image/png;base64,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"/>


```python
# 행,열을 전치하여 다시 그리기
tdf1_ns = df1_ns.T
tdf1_ns.plot()
```

<pre>
<matplotlib.axes._subplots.AxesSubplot at 0x27cba9e52b0>
</pre>
<img src="data:image/png;base64,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
