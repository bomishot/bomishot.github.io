---
layout: single
title:  "PART7. 머신러닝 - 회귀분석"
categories: coding
tag: [python, blog, ML]
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


# part7. 머신러닝 데이터 분석


## 1. 머신러닝 개요

<br>



### <1> 머신러닝이란? 

**기계(컴퓨터 알고리즘) 스스로 데이터를 학습하여 서로 다른 변수 간의 관계를 찾아 나가는 과정**

해결하려는 문제에 따라 예측(prediction), 분류(classification), 군집(clustering) 알고리즘 등으로 분류된다.  

* 예를 들어,

    * 주가, 환율 등 경제 지표 예측  

    * 은행에서 고객을 분류하여 대출을 승인하거나 거절하는 문제  

    * 비슷한 소비 패턴을 가진 고객 유형을 군집으로 묶어내는 문제  

<br>

<br>



### <2> 지도 학습 vs 비지도 학습



* 머신러닝은 크게 두 가지 유형으로 분류한다.

    * 지도 학습 (**supervised learning**) : 정답 데이터를 다른 데이터와 함께 컴퓨터 알고리즘을 입력하는 방식

        * 알고리즘(분석모형) : 회귀분석, 분류

        * 모형 평가가 다양한 편

        <br>

        

    * 비지도 학습 (**unsupervised learning**) : 정답 데이터 없이 컴퓨터 알고리즘 스스로 데이터로부터 숨은 패턴 찾는 방식  

        * 알고리즘(분석모형) : 군집분석

        * 모형 평가 방법이 제한적

        

### <3> 머신러닝 프로세스

: 데이터 정리 -> 데이터 분리 -> 알고리즘 준비 -> 모형 학습 -> 예측 -> 모형 평가 -> 모형 활용  

머신러닝 데이터 분석을 시작하기 전에 컴퓨터 알고리즘이 이해할 수 있는 형태로 데이터를 변환하는 작업이 선행되야한다.  

    


<br>





## 2. 회귀분석

* 가격, 매출, 주가, 환율, 수량 등 연속적인 값을 갖는 연속 변수를 예측하는데 주로 활용  

* 예측을 위해 모형이 사용하는 속성(x) : **독립변수**(independent)/ **설명변수**(explanatory)

* 분석 모형이 예측하고자 하는 목표(y) : **종속 변수**(dependent) / **예측변수**(predictor)


### <1> 단순회귀분석 (Simple Linear Regression)

* 대표적인 지도학습 유형

* 두 변수 사이에 일대일로 대응되는 확률적, 통계적 상관성을 찾는 알고리즘

* 수학적으로 독립 변수X와 종속 변수Y 사이의 관계를 1차함수 Y=aX+b로 나타낸다.

    * 변수 X와 Y에 대한 정보를 가지고, 일차방정식의 계수 a,b를 찾는 과정이 단순회귀분석 알고리즘이다.


#### Step1 - 데이터 준비

* UCI 자동차 연비 데이터셋 다시 사용함.



```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv('C:/Users/USER/Desktop/파이썬머신러닝 자료/part7/auto-mpg.csv', header=None)
df.columns = ['mpg', 'cylinders', 'displacement', 'horsepower', 'weight', 'acceleration', 'model year', 'origin', 'name']

# IPython 디스플레이 설정 - 출력할 열의 개수 한도 늘리기
pd.set_option('display.max_columns', 10)
print(df.head())
```

<pre>
    mpg  cylinders  displacement horsepower  weight  acceleration  model year  \
0  18.0          8         307.0      130.0  3504.0          12.0          70   
1  15.0          8         350.0      165.0  3693.0          11.5          70   
2  18.0          8         318.0      150.0  3436.0          11.0          70   
3  16.0          8         304.0      150.0  3433.0          12.0          70   
4  17.0          8         302.0      140.0  3449.0          10.5          70   

   origin                       name  
0       1  chevrolet chevelle malibu  
1       1          buick skylark 320  
2       1         plymouth satellite  
3       1              amc rebel sst  
4       1                ford torino  
</pre>
<br>



#### Step 2 - 데이터 탐색  

* 데이터에 대한 기본적인 정보를 탐색한다.  

* info() 메소드로 데이터의 자료형, 개수 확인  

* describe() 메소드로 주요 통계 정보 확인  



```python
df.info()
```

<pre>
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 398 entries, 0 to 397
Data columns (total 9 columns):
 #   Column        Non-Null Count  Dtype  
---  ------        --------------  -----  
 0   mpg           398 non-null    float64
 1   cylinders     398 non-null    int64  
 2   displacement  398 non-null    float64
 3   horsepower    398 non-null    object 
 4   weight        398 non-null    float64
 5   acceleration  398 non-null    float64
 6   model year    398 non-null    int64  
 7   origin        398 non-null    int64  
 8   name          398 non-null    object 
dtypes: float64(4), int64(3), object(2)
memory usage: 28.1+ KB
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
      <td>398.000000</td>
      <td>398.000000</td>
      <td>398.000000</td>
      <td>398.000000</td>
      <td>398.000000</td>
      <td>398.000000</td>
      <td>398.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>23.514573</td>
      <td>5.454774</td>
      <td>193.425879</td>
      <td>2970.424623</td>
      <td>15.568090</td>
      <td>76.010050</td>
      <td>1.572864</td>
    </tr>
    <tr>
      <th>std</th>
      <td>7.815984</td>
      <td>1.701004</td>
      <td>104.269838</td>
      <td>846.841774</td>
      <td>2.757689</td>
      <td>3.697627</td>
      <td>0.802055</td>
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
      <td>104.250000</td>
      <td>2223.750000</td>
      <td>13.825000</td>
      <td>73.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>23.000000</td>
      <td>4.000000</td>
      <td>148.500000</td>
      <td>2803.500000</td>
      <td>15.500000</td>
      <td>76.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>29.000000</td>
      <td>8.000000</td>
      <td>262.000000</td>
      <td>3608.000000</td>
      <td>17.175000</td>
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


descibe() 메소드의 실행 결과, 엔진출력을 나타내는 'horsepower'열이 포함되지 않는다.  

'horsepower'열의 자료형이 문자열(object)이므로 숫자형으로 변경해야 한다.  

-> 'horsepower'열의 고유값 중에서 누락 데이터를 뜻하는 '?' 문자가 있는 행들을 찾아서 제거하고, astped() 메소드로 실수형으로 변환한다.



```python
df['horsepower'].unique()    # horsepower 열의 고유값 확인
```

<pre>
array(['130.0', '165.0', '150.0', '140.0', '198.0', '220.0', '215.0',
       '225.0', '190.0', '170.0', '160.0', '95.00', '97.00', '85.00',
       '88.00', '46.00', '87.00', '90.00', '113.0', '200.0', '210.0',
       '193.0', '?', '100.0', '105.0', '175.0', '153.0', '180.0', '110.0',
       '72.00', '86.00', '70.00', '76.00', '65.00', '69.00', '60.00',
       '80.00', '54.00', '208.0', '155.0', '112.0', '92.00', '145.0',
       '137.0', '158.0', '167.0', '94.00', '107.0', '230.0', '49.00',
       '75.00', '91.00', '122.0', '67.00', '83.00', '78.00', '52.00',
       '61.00', '93.00', '148.0', '129.0', '96.00', '71.00', '98.00',
       '115.0', '53.00', '81.00', '79.00', '120.0', '152.0', '102.0',
       '108.0', '68.00', '58.00', '149.0', '89.00', '63.00', '48.00',
       '66.00', '139.0', '103.0', '125.0', '133.0', '138.0', '135.0',
       '142.0', '77.00', '62.00', '132.0', '84.00', '64.00', '74.00',
       '116.0', '82.00'], dtype=object)
</pre>

```python
# horsepower 열의 자료형 변경(문자열->숫자)
df['horsepower'].replace('?', np.nan, inplace=True)       # '?'을 NaN으로 변경
df.dropna(subset=['horsepower'], axis=0, inplace=True)    # 누락 데이터 행 삭제
df['horsepower'] = df['horsepower'].astype('float')       # 자료형 변경
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
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>model year</th>
      <th>origin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>392.000000</td>
      <td>392.000000</td>
      <td>392.000000</td>
      <td>392.000000</td>
      <td>392.000000</td>
      <td>392.000000</td>
      <td>392.000000</td>
      <td>392.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>23.445918</td>
      <td>5.471939</td>
      <td>194.411990</td>
      <td>104.469388</td>
      <td>2977.584184</td>
      <td>15.541327</td>
      <td>75.979592</td>
      <td>1.576531</td>
    </tr>
    <tr>
      <th>std</th>
      <td>7.805007</td>
      <td>1.705783</td>
      <td>104.644004</td>
      <td>38.491160</td>
      <td>849.402560</td>
      <td>2.758864</td>
      <td>3.683737</td>
      <td>0.805518</td>
    </tr>
    <tr>
      <th>min</th>
      <td>9.000000</td>
      <td>3.000000</td>
      <td>68.000000</td>
      <td>46.000000</td>
      <td>1613.000000</td>
      <td>8.000000</td>
      <td>70.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>17.000000</td>
      <td>4.000000</td>
      <td>105.000000</td>
      <td>75.000000</td>
      <td>2225.250000</td>
      <td>13.775000</td>
      <td>73.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>22.750000</td>
      <td>4.000000</td>
      <td>151.000000</td>
      <td>93.500000</td>
      <td>2803.500000</td>
      <td>15.500000</td>
      <td>76.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>29.000000</td>
      <td>8.000000</td>
      <td>275.750000</td>
      <td>126.000000</td>
      <td>3614.750000</td>
      <td>17.025000</td>
      <td>79.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>46.600000</td>
      <td>8.000000</td>
      <td>455.000000</td>
      <td>230.000000</td>
      <td>5140.000000</td>
      <td>24.800000</td>
      <td>82.000000</td>
      <td>3.000000</td>
    </tr>
  </tbody>
</table>
</div>


descibe() 메소드 실행 시, horsepower열까지 잘 나온 것을 확인하였다!


<br>



#### Step 3 - 속성 선택

* 단순회귀분석에 변수로 사용할 후보 열 선택

* 독립 변수(X)로 사용할 후보로 3개의 열 : cylinders, horsepower, weight

* 종속 변수(Y) 열 : mpg -> 예측 목표



```python
# 분석에 활용할 열(속성) 선택: 연비, 실린더, 출력, 중량
ndf = df[['mpg', 'cylinders', 'horsepower', 'weight']]
ndf.head()
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
      <th>horsepower</th>
      <th>weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>18.0</td>
      <td>8</td>
      <td>130.0</td>
      <td>3504.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0</td>
      <td>8</td>
      <td>165.0</td>
      <td>3693.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18.0</td>
      <td>8</td>
      <td>150.0</td>
      <td>3436.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16.0</td>
      <td>8</td>
      <td>150.0</td>
      <td>3433.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.0</td>
      <td>8</td>
      <td>140.0</td>
      <td>3449.0</td>
    </tr>
  </tbody>
</table>
</div>


<br>



* 3개의 후보 중에서 단순회귀분석에 사용할 독립 변수 선택

* X와 Y간의 일대일 관계를 찾는 것이므로, 두 변수 간에 선형관계가 있는지 그래프를 그려서 확인  

-> x: weight, y: mpg 와의 관계부터 예시로 들어보자!



```python
ndf.plot(kind='scatter', x='weight', y='mpg',c='coral', s=10, figsize=(10,5))
plt.show()
plt.close()
```

<img src="data:image/png;base64,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"/>

<br>



* Seaborn 라이브러리의 **regplot()함수**를 이용하여 두 변수에 대한 산점도 그리자

    * 기본적으로 회귀선 표시

    * 회귀선 제거 시 **fit_reg=False옵션** 적용



```python
# seaborn으로 산점도 그리기
fig = plt.figure(figsize=(10,5))
ax1 = fig.add_subplot(1,2,2)              
sns.regplot(x='weight', y='mpg', data=ndf, ax=ax1, fit_reg=False) # 회귀선 미표시
plt.show()
plt.close()
```

<img src="data:image/png;base64,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
