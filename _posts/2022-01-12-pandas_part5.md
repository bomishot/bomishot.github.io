---
layout: single
title:  "PART 5. 데이터 사전 처리"
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
      font-size: 0.7rem;
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





<br>

## 1. 누락 데이터 처리
머신러닝 분석 모형에 데이터를 입력하기 전에 반드시 누락데이터를 제거하거나 다른 적절한 값으로 대체하는 과정이 필요하다.  
누락 데이터가 많아지면 데이터의 품질이 떨어지고, 머신러닝 분석 알고리즘을 왜곡하는 현상이 발생하기 때문이다.  
일반적으로 유효한 데이터 값이 존재하지 않는 누락 데이터를 'NaN'(Not a Number)으로 표시한다.  
 <br>
### 누락 데이터 확인
* Seaborn 라이브러리의 'titanic' 데이터셋 사용.
* dropna=False 옵션 : NaN값, 유효한 데이터의 개수 보여줌

```python
import seaborn as sns
df = sns.load_dataset('titanic')
```


```python
# deck열의 NaN 개수 계산하기
nan_deck = df['deck'].value_counts(dropna=False)
nan_deck
```




    NaN    688
    C       59
    B       47
    D       33
    E       32
    A       15
    F       13
    G        4
    Name: deck, dtype: int64


* 'deck'열에 688개의 누락데이터가 있는 것 확인
* 누락 데이터를 찾는 직접적인 방법
    * isnull() : 누락 데이터면 True 반환, 유효한 데이터가 존재하면 False 반환 
    * notnull() : 누락 데이터면 False 반환, 유효한 데이터가 존재하면 True 반환


```python
df.head().isnull()
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
      <th>survived</th>
      <th>pclass</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
      <th>embarked</th>
      <th>class</th>
      <th>who</th>
      <th>adult_male</th>
      <th>deck</th>
      <th>embark_town</th>
      <th>alive</th>
      <th>alone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



* isnull() 메소드로 누락 데이터 개수 구하기


```python
df.head().isnull().sum(axis=0)
```




    survived       0
    pclass         0
    sex            0
    age            0
    sibsp          0
    parch          0
    fare           0
    embarked       0
    class          0
    who            0
    adult_male     0
    deck           3
    embark_town    0
    alive          0
    alone          0
    dtype: int64



<br>

### 누락데이터 제거
* 각 열에 누락 데이터가 몇 개씩 포함되어 있는지 체크


```python
missing_df = df.isnull()
for col in missing_df.columns:
    missing_count = missing_df[col].value_counts()     # 각 열의 NaN 개수 파악
    try:
        print(col, ':', missing_count[True])           # NaN 값이 있으면 개수 출력
    except:
        print(col,':', 0)                              # NaN 값이 없으면 0 출력
```

    survived : 0
    pclass : 0
    sex : 0
    age : 177
    sibsp : 0
    parch : 0
    fare : 0
    embarked : 2
    class : 0
    who : 0
    adult_male : 0
    deck : 688
    embark_town : 2
    alive : 0
    alone : 0
    

* 누락 데이터 제거 : dropna() 메소드에 **thresh=500** 옵션 적용-> NaN 값을 500개 이상 갖는 모든 열 삭제
    * 'deck'열(891개 중 688개 NaN값을 가지고 있어 이 열만 삭제된 결과를 볼 수 있다.


```python
df_thresh = df.dropna(axis=1, thresh=500)
df_thresh.columns
```




    Index(['survived', 'pclass', 'sex', 'age', 'sibsp', 'parch', 'fare',
           'embarked', 'class', 'who', 'adult_male', 'embark_town', 'alive',
           'alone'],
          dtype='object')



* age 열에 나이 데이터가 없는 모든 행 삭제 - age열(891개 중 177개 NaN 값)
    * dropna() 메소드에 subset을 'age'열로 한정하면, 'age'열의 행 중에서 NaN값이 있는 모든 행(axis=0)을 삭제.
    * 기본값으로 how='any' 옵션이 적용 : NaN값이 하나라도 존재하면 삭제.
    * 예제 - 891개 중 나이 데이터가 누락된 177개 행 삭제하고 나머지 714개를 df_age에 저장.


```python
df_age = df.dropna(subset=['age'], how='any', axis=0)
len(df_age)
```




    714



<br>

### 누락 데이터 치환
* 데이터 중에서 일부가 누락되어있더라도, 나머지 데이터를 최대한 살려서 데이터 분석에 활용하는 것이 good!
* 누락데이터를 치환할 값으로는 평균값, 최빈값 등 사용
* **fillna()** 메소드는 새로운 객체를 반환하기 때문에 원본객체를 변경하려면 inplace=True 옵션 추가

<br>
1. 평균으로 누락 데이터 바꾸기


```python
df['age'].head(10)
```




    0    22.0
    1    38.0
    2    26.0
    3    35.0
    4    35.0
    5     NaN
    6    54.0
    7     2.0
    8    27.0
    9    14.0
    Name: age, dtype: float64




```python
mean_age = df['age'].mean(axis=0)
df['age'].fillna(mean_age, inplace=True)
df['age'].head(10)
```




    0    22.000000
    1    38.000000
    2    26.000000
    3    35.000000
    4    35.000000
    5    29.699118
    6    54.000000
    7     2.000000
    8    27.000000
    9    14.000000
    Name: age, dtype: float64



5번째의 NaN값이 다른 나이데이터의 평균으로 변경된 것 확인okay~!

<br>
2. 가장 많이 나타나는 값으로 바꾸기

* value_counts() 메소드를 사용하여, 승선도시별 승객 수를 찾기
* **idxmax()** 메소드를 사용하여, 가장 큰 값을 갖는 도시를 찾기


```python
df['embark_town'][825:830]
```




    825     Queenstown
    826    Southampton
    827      Cherbourg
    828     Queenstown
    829            NaN
    Name: embark_town, dtype: object




```python
most_freq = df['embark_town'].value_counts(dropna=True).idxmax()
most_freq
```




    'Southampton'




```python
df['embark_town'].fillna(most_freq, inplace=True)
df['embark_town'][825:830]
```




    825     Queenstown
    826    Southampton
    827      Cherbourg
    828     Queenstown
    829    Southampton
    Name: embark_town, dtype: object



829행의 NaN값이 most_freq인 'Southampton'으로 변경된 것 확인 okay~!

<br>
3. 이웃하고 있는 값으로 바꾸기
데이터셋의 특성상 서로 이웃하고 있는 데이터끼리 유사성을 가질 확률이 높다.
<br>
  fillna() method에
<br>

* method = 'ffill'옵션을 추가하면 NaN이 있는 행의 **직전** 행에 있는 값으로 바꿔준다.
* method = 'bfill'옵션을 추가하면 NaN이 있는 행의 바로 **다음** 행에 있는 값으로 바꿔준다.



```python
df['embark_town'][825:830]
```




    825     Queenstown
    826    Southampton
    827      Cherbourg
    828     Queenstown
    829            NaN
    Name: embark_town, dtype: object




```python
df['embark_town'].fillna(method='ffill', inplace=True)
df['embark_town'][825:830]
```




    825     Queenstown
    826    Southampton
    827      Cherbourg
    828     Queenstown
    829     Queenstown
    Name: embark_town, dtype: object



829행의 NaN값이 직전 행인 828행의 값으로 변경 okay~!
<br>

<br>

## 2. 중복 데이터 처리
하나의 데이터셋에서 동일한 관측값이 2개 이상 중복되는 경우, 중복 데이터를 찾아서 삭제해야한다.  
동일한 대상이 중복으로 존재하는 것이므로 분석 결과를 왜곡하기 때문이다.

### 중복 데이터 확인 : duplicated() 메소드 이용
* 각 행의 중복 여부를 나타내는 boolean 시리즈 반환
    * False: 중복이 아니다. 
    * True: 중복이다. ( 앞의 행과 중복되는 값이 있다.)


```python
import pandas as pd
df = pd.DataFrame({'c1':['a','a', 'b', 'a','b'],
                   'c2':[1,1,1,2,2],
                   'c3':[1,1,2,2,2]
                  })
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
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>a</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>b</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.duplicated()
```




    0    False
    1     True
    2    False
    3    False
    4    False
    dtype: bool




```python
# df의 특정 열 데이터에서 중복값 찾기
df['c2'].duplicated() 
```




    0    False
    1     True
    2     True
    3    False
    4     True
    Name: c2, dtype: bool



### 중복 데이터 제거 
* drop_duplicates()
* inplace=True 옵션 추가 (원본 객체 변경)


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
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>a</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>b</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.drop_duplicates()
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
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>b</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



* c2, c3열을 기준으로 중복 행 제거

<br>
1행,4행이 없어진는 결과가 나오겠지?


```python
df.drop_duplicates(subset=['c2', 'c3'])
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
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>b</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



## 3.  데이터 표준화
여러 곳에서 수집한 자료들은 단위 선택, 대소문자 구분, 약칭 활용 등 여러 가지 원인에 의해 다양한 형태로 표현.
<br>
-> 동일한 대상을 표현하는 방법에 차이가 있다 -> 분석의 정확도는 낮아진다.
<br>
-> 데이터 포맷을 일관성 있게 표준화하자!

### <1> 단위 환산
: 측정 단위를 동일하게 맞추자!
* UCL 자동차 연비 데이터셋 사용
* 'mpg'열은 'mile per gallon' 단위로 연비 표시 -> 'km/L' 단위로 변환해보자!
<br>
1mpg = 0.425km/L


```python
import pandas as pd
df = pd.read_csv('C:/Users/USER/Desktop/new/excel_example/auto-mpg.csv')
df.columns = ['mpg', 'cylinders', 'displacement', 'horsepower' , 'weight', 'acceleration', 'model year', 'origin', 'name']
df.head(3)
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
  </tbody>
</table>
</div>




```python
mpg_to_kpl = 0.425
df['kpl'] = df['mpg'] * mpg_to_kpl
df['kpl'] = df['kpl'].round(2) # 소수점 아래 둘째자리에서 반올림
df.head(3)
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
      <th>kpl</th>
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
      <td>6.38</td>
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
      <td>7.65</td>
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
      <td>6.80</td>
    </tr>
  </tbody>
</table>
</div>



### <2>자료형 변환
* dtypes, info() : 각 열의 자료형 확인 
<br>

- 예제에서 엔진 출력을 나타내는 'horsepower'열은 **숫자형**이 적절하고, 
<br>
- 출시 연도를 나타내는 'model year'열은 카테고리를 나타내는 **범주형**이 적절하고,
<br>
- 출시국가를 나타내는 'origin'열은 카테고리를 나타내는 **범주형**이 적절하다.
<br>
적절한 자료형으로 변환해보자!


```python
df.dtypes
```




    mpg             float64
    cylinders         int64
    displacement    float64
    horsepower       object
    weight            int64
    acceleration    float64
    model year        int64
    origin            int64
    name             object
    kpl             float64
    dtype: object



- horsepower 자료형 바꾸기 : **object -> 숫자형(int, float)**
<br>
'horsepower'열은 문자열을 뜻하는 object자료형이다.


```python
df['horsepower'].unique()
```




    array(['165', '150', '140', '198', '220', '215', '225', '190', '170',
           '160', '95', '97', '85', '88', '46', '87', '90', '113', '200',
           '210', '193', '?', '100', '105', '175', '153', '180', '110', '72',
           '86', '70', '76', '65', '69', '60', '80', '54', '208', '155',
           '130', '112', '92', '145', '137', '158', '167', '94', '107', '230',
           '49', '75', '91', '122', '67', '83', '78', '52', '61', '93', '148',
           '129', '96', '71', '98', '115', '53', '81', '79', '120', '152',
           '102', '108', '68', '58', '149', '89', '63', '48', '66', '139',
           '103', '125', '133', '138', '135', '142', '77', '62', '132', '84',
           '64', '74', '116', '82'], dtype=object)



<br>

##### astype() : 자료형 변환
##### unique() : 고유값 확인
##### replace(..)


```python
import numpy as np
df['horsepower'].replace('?', np.nan, inplace=True) # '?'을 np.nan으로 변경
df.dropna(subset = ['horsepower'], axis=0, inplace=True) # 누락데이터 행 삭제
df['horsepower'] = df['horsepower'].astype('int') # 문자열을 실수형으로 변환  
df['horsepower'].dtypes
```




    dtype('int32')




```python
df['horsepower'].unique()
```




    array([165, 150, 140, 198, 220, 215, 225, 190, 170, 160,  95,  97,  85,
            88,  46,  87,  90, 113, 200, 210, 193, 100, 105, 175, 153, 180,
           110,  72,  86,  70,  76,  65,  69,  60,  80,  54, 208, 155, 130,
           112,  92, 145, 137, 158, 167,  94, 107, 230,  49,  75,  91, 122,
            67,  83,  78,  52,  61,  93, 148, 129,  96,  71,  98, 115,  53,
            81,  79, 120, 152, 102, 108,  68,  58, 149,  89,  63,  48,  66,
           139, 103, 125, 133, 138, 135, 142,  77,  62, 132,  84,  64,  74,
           116,  82])



<br>

* 'origin' 열 : 정수형 -> object 자료형(문자열) 변환하자!



```python
df['origin'].unique()
```




    array([1, 3, 2], dtype=int64)




```python
df['origin'].replace({1:'USA', 2:'EU', 3:'JPN'}, inplace=True)
df['origin'].unique()
```




    array(['USA', 'JPN', 'EU'], dtype=object)




```python
df['origin']
```




    0      USA
    1      USA
    2      USA
    3      USA
    4      USA
          ... 
    392    USA
    393     EU
    394    USA
    395    USA
    396    USA
    Name: origin, Length: 391, dtype: object



'origin' 열의 국가이름은 문자열 데이터(object)이다. 
<br>
3개의 국가이름이 계속 반복된다.
<br>
유한 개의 고유값이 반복적으로 나타나는 경우에는 범주형(category) 데이터로 표현하는 것이 효울적이다.

<br>

<br>

* astype('category') : 범주형 데이터로 변환됨.
* astype('str') : 다시 문자열로 변환 (object)


```python
df['origin'] = df['origin'].astype('category')
df['origin'].dtypes
```




    CategoricalDtype(categories=['EU', 'JPN', 'USA'], ordered=False)




```python
df['origin'] = df['origin'].astype('str')
df['origin'].dtypes
```




    dtype('O')



<br>

* 'model year'열 : 정수형 -> 범주형(category) 으로 변환하자!  
sample()메소드를 이용해 'model year'열에서 무작위로 3개 행 선택해 출력해보았다.  
연도를 뜻하기 때문에 숫자형으로 남겨둬도 무방하지만,   
연도는 시간적인 순서는 의미가 있으나  
숫자의 상대적인 크기는 별 의미가 없다.  
 -> 데이터는 숫자 형태를 갖더라도 자료형은 범주형으로 표현하는 것이 적절하다!  




```python
df['model year'].sample(3)
```




    177    75
    242    77
    106    73
    Name: model year, dtype: int64




```python
df['model year'] = df['model year'].astype('category')
df['model year'].sample(3)
```




    165    75
    105    73
    75     72
    Name: model year, dtype: category
    Categories (13, int64): [70, 71, 72, 73, ..., 79, 80, 81, 82]



## 4. 범주형(카테고리) 데이터 처리

### <1> 구간 분할 (binning)

* 데이터 분석 알고리즘에 따라서는 연속 데이터를 그대로 사용하기 보다는  
* 일정한 구간(bin)으로 나눠서 분석하는 것이 효율적일 경우가 있다.  

* 구간 분할 : 연속 변수를 일정한 구간으로 나누고, 각 구간을 범주형 이산 변수로 변환하는 과정
##### pd.cut() : 연속 데이터를 여러 구간으로 나누고 범주형 데이터로 변환
    * 'horsepower'열은 엔진 출력을 나타낸다.
    * 경우에 따라 숫자보다는, '저출력, 보통출력, 고출력'등 구간으로 나누어서 표현이 효율적.
    * 3개 구간 구분 -> 4개의 경계값 필요  
<br> 

##### histogram() : bin개수를 bins 옵션에 입력 시, 각 구간에 속하는 값의 개수(count), 리스트(bin_dividers) 반환
##### include_lowest = True 옵션 : 각 구간의 낮은 경계값 포함


```python
import pandas as pd
import numpy as np

df = pd.read_csv('C:/Users/USER/Desktop/new/excel_example/auto-mpg.csv')
df.columns = ['mpg', 'cylinders', 'displacement', 'horsepower' , 'weight', 'acceleration', 'model year', 'origin', 'name']
df['horsepower'].replace('?', np.nan, inplace=True)
df.dropna(subset=['horsepower'], axis=0, inplace=True)
df['horsepower'] = df['horsepower'].astype('int')

# np.histogram함수로 3개의 bin으로 구분할 경계값의 리스트 구하기
count, bin_dividers = np.histogram(df['horsepower'], bins=3)
print(count,'\n',bin_dividers)
```

    [257 102  32] 
     [ 46.         107.33333333 168.66666667 230.        ]
    

앞서 나온 출력은,  
count : 구간3개에서 구간1은 257개의 데이터가 있다는 뜻..  
bin_dividers : 구간에서의 경계값을 말하는데,  
46-107이 구간 1이라는 뜻..  
<br>
    


```python
bin_names = ['저출력', '보통출력', '고출력']
df['hp_bin'] = pd.cut( x = df['horsepower'],    # 데이터 배열
                       bins = bin_dividers,     # 경계값 리스트
                       labels = bin_names,      # bin 이름
                       include_lowest = True )  # 첫 경계값 포함
df[['horsepower', 'hp_bin']].head(15)
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
      <th>horsepower</th>
      <th>hp_bin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>165</td>
      <td>보통출력</td>
    </tr>
    <tr>
      <th>1</th>
      <td>150</td>
      <td>보통출력</td>
    </tr>
    <tr>
      <th>2</th>
      <td>150</td>
      <td>보통출력</td>
    </tr>
    <tr>
      <th>3</th>
      <td>140</td>
      <td>보통출력</td>
    </tr>
    <tr>
      <th>4</th>
      <td>198</td>
      <td>고출력</td>
    </tr>
    <tr>
      <th>5</th>
      <td>220</td>
      <td>고출력</td>
    </tr>
    <tr>
      <th>6</th>
      <td>215</td>
      <td>고출력</td>
    </tr>
    <tr>
      <th>7</th>
      <td>225</td>
      <td>고출력</td>
    </tr>
    <tr>
      <th>8</th>
      <td>190</td>
      <td>고출력</td>
    </tr>
    <tr>
      <th>9</th>
      <td>170</td>
      <td>고출력</td>
    </tr>
    <tr>
      <th>10</th>
      <td>160</td>
      <td>보통출력</td>
    </tr>
    <tr>
      <th>11</th>
      <td>150</td>
      <td>보통출력</td>
    </tr>
    <tr>
      <th>12</th>
      <td>225</td>
      <td>고출력</td>
    </tr>
    <tr>
      <th>13</th>
      <td>95</td>
      <td>저출력</td>
    </tr>
    <tr>
      <th>14</th>
      <td>95</td>
      <td>저출력</td>
    </tr>
  </tbody>
</table>
</div>



### <2> 더미 변수
* 앞에서 'horsepower'열의 숫자형 연속 데이터를 'hp_bin' 열의 범주형 데이터로 변환했었다.  
* 범주형 데이터를 머신러닝 알고리즘에 바로 사용할 수 없는 경우가 있는데,  
* 컴퓨터가 인식 가능한 입력값으로 변환해야한다. -> 더미 변수(dummy variable) 사용  
* 숫자 0 또는 1로 표현된다.  
    * 0과 1은 수의 크고 작음을 나타내지 않고, 어떤 특성(feature)이 있는지 없는지 여부만 표시 
    * 1 : 해당 특성 존재 o  
      0 : 해당 특성 존재 x  
<br>

**one - hot - encoding(원핫인코딩) ** :  범주형 데이터를 컴퓨터가 인식할 수 있도록  
                            숫자 0,1로만 구성되는 원핫벡터(one - hot - vector)로 변환  
##### pd.get_dummies() : 범주형 변수의 모든 고유값을 각각 새로운 더미 변수로 변환


```python
pd.get_dummies(df['hp_bin'])
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
      <th>저출력</th>
      <th>보통출력</th>
      <th>고출력</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>392</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>393</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>394</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>395</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>396</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>391 rows × 3 columns</p>
</div>



-> 더미 변수가 본래 속해 있던 행에는 1 입력 / 속하지 않았던 다른 행에는 0 입력
<br>

**sklearn라이브러리**를 이용해서 원핫인코딩을 편하게 처리


```python
from sklearn import preprocessing

# 전처리를 위한 encoder 객체 만들기
label_encoder = preprocessing.LabelEncoder()     # label encoder 생성
onehot_encoder = preprocessing.OneHotEncoder()   # one hot encoder 생성

# label encoder로 문자열 범주를 숫자형 범주로 변환
onehot_labeled = label_encoder.fit_transform(df['hp_bin'].head(15))
print(onehot_labeled)
print(type(onehot_labeled))

# 2차원 행렬로 변경
onehot_reshaped = onehot_labeled.reshape(len(onehot_labeled), 1)
print(onehot_reshaped)
print(type(onehot_reshaped))

# 희소행렬로 변경 (행렬의 값이 대부분 0인 경우)
# 희소행렬은 (행,열) 좌표와 값 형태로 정리.
# (0,1)은 0행의 1열 위치를 말하고, 데이터 값은 숫자 1.0이 입력된다.
onehot_fitted = onehot_encoder.fit_transform(onehot_reshaped)
print(onehot_fitted)
print(type(onehot_fitted))
```

    [1 1 1 1 0 0 0 0 0 0 1 1 0 2 2]
    <class 'numpy.ndarray'>
    [[1]
     [1]
     [1]
     [1]
     [0]
     [0]
     [0]
     [0]
     [0]
     [0]
     [1]
     [1]
     [0]
     [2]
     [2]]
    <class 'numpy.ndarray'>
      (0, 1)	1.0
      (1, 1)	1.0
      (2, 1)	1.0
      (3, 1)	1.0
      (4, 0)	1.0
      (5, 0)	1.0
      (6, 0)	1.0
      (7, 0)	1.0
      (8, 0)	1.0
      (9, 0)	1.0
      (10, 1)	1.0
      (11, 1)	1.0
      (12, 0)	1.0
      (13, 2)	1.0
      (14, 2)	1.0
    <class 'scipy.sparse.csr.csr_matrix'>
    

### <5> 정규화
각 변수(데이터프레임의 열)에 들어있는 숫자 데이터의 상대적 크기 차이 때문에 머신러닝 분석 결과가 달라질 수 있다.  
-> 숫자 데이터의 상대적 크기 차이를 제거할 필요가 있다.
* 정규화(normalization): 각 열에 속하는 데이터 값을 동일한크기 기준으로 나눈 비율로 나타내는 것
* 정규화 과정을 거친 데이터의 범위 : 0~1 or -1~1  
<br>

* 각 열의 데이터를 해당 열의 최댓값(의 절대값)으로 나누는 방법  
어떤 열의 원소 값을 그 열의 최댓값으로 나누면 가장 큰 값은 최대값 자기 자신을 나눈 1이다.



```python
# horsepower열의 통계 요약 정보로 최댓값(max) 확인
df.horsepower.describe()
```




    count    391.000000
    mean     104.404092
    std       38.518732
    min       46.000000
    25%       75.000000
    50%       93.000000
    75%      125.000000
    max      230.000000
    Name: horsepower, dtype: float64




```python
# horsepower 열의 최댓값을 절대값으로 모든 데이터를 나눠서 저장
df.horsepower = df.horsepower/abs(df.horsepower.max())
df.horsepower.describe()
```




    count    391.000000
    mean       0.453931
    std        0.167473
    min        0.200000
    25%        0.326087
    50%        0.404348
    75%        0.543478
    max        1.000000
    Name: horsepower, dtype: float64



* 각 열의 데이터 중에서 최대값과 최소값을 뺀 값으로 나누는 방법


```python
min_x = df.horsepower - df.horsepower.min()
min_max = df.horsepower.max() - df.horsepower.min()
df.horsepower = min_x/min_max
df.horsepower.describe()
```




    count    391.000000
    mean       0.317414
    std        0.209341
    min        0.000000
    25%        0.157609
    50%        0.255435
    75%        0.429348
    max        1.000000
    Name: horsepower, dtype: float64



## 6. 시계열 데이터
금융 데이터를 다루기 위해 개발된 판다스는 시계열(time series) 데이터를 다루는 기능을 제공.  
특히 시계열 데이터를 df의 행 인덱스로 사용하면, 시간으로 기록된 데이터 분석이 편리.
* Timestamp : 특정한 시점 기록
* Period : 두 시점 사이의 일정한 기간

### <1> 다른 자료형 -> 시계열 객체로 변환
* 문자열을 Timestamp로 저장하는 방법
##### pd.to_datetime() : 다른 자료형 -> pandas timestamp를 나타내는 datetime64 자료형으로 변경.


```python
import pandas as pd

df = pd.read_csv('C:/Users/USER/Desktop/파이썬머신러닝 자료/part5/stock-data.csv')
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 20 entries, 0 to 19
    Data columns (total 6 columns):
     #   Column  Non-Null Count  Dtype 
    ---  ------  --------------  ----- 
     0   Date    20 non-null     object
     1   Close   20 non-null     int64 
     2   Start   20 non-null     int64 
     3   High    20 non-null     int64 
     4   Low     20 non-null     int64 
     5   Volume  20 non-null     int64 
    dtypes: int64(5), object(1)
    memory usage: 1.1+ KB
    


```python
df['new_date'] = pd.to_datetime(df['Date'])
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
      <th>Date</th>
      <th>Close</th>
      <th>Start</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>new_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-07-02</td>
      <td>10100</td>
      <td>10850</td>
      <td>10900</td>
      <td>10000</td>
      <td>137977</td>
      <td>2018-07-02</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-06-29</td>
      <td>10700</td>
      <td>10550</td>
      <td>10900</td>
      <td>9990</td>
      <td>170253</td>
      <td>2018-06-29</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-06-28</td>
      <td>10400</td>
      <td>10900</td>
      <td>10950</td>
      <td>10150</td>
      <td>155769</td>
      <td>2018-06-28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-06-27</td>
      <td>10900</td>
      <td>10800</td>
      <td>11050</td>
      <td>10500</td>
      <td>133548</td>
      <td>2018-06-27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018-06-26</td>
      <td>10800</td>
      <td>10900</td>
      <td>11000</td>
      <td>10700</td>
      <td>63039</td>
      <td>2018-06-26</td>
    </tr>
  </tbody>
</table>
</div>




```python
type(df['new_date'][0])
```




    pandas._libs.tslibs.timestamps.Timestamp




```python
df.set_index('new_date', inplace=True)
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
      <th>Date</th>
      <th>Close</th>
      <th>Start</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>new_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-07-02</th>
      <td>2018-07-02</td>
      <td>10100</td>
      <td>10850</td>
      <td>10900</td>
      <td>10000</td>
      <td>137977</td>
    </tr>
    <tr>
      <th>2018-06-29</th>
      <td>2018-06-29</td>
      <td>10700</td>
      <td>10550</td>
      <td>10900</td>
      <td>9990</td>
      <td>170253</td>
    </tr>
    <tr>
      <th>2018-06-28</th>
      <td>2018-06-28</td>
      <td>10400</td>
      <td>10900</td>
      <td>10950</td>
      <td>10150</td>
      <td>155769</td>
    </tr>
    <tr>
      <th>2018-06-27</th>
      <td>2018-06-27</td>
      <td>10900</td>
      <td>10800</td>
      <td>11050</td>
      <td>10500</td>
      <td>133548</td>
    </tr>
    <tr>
      <th>2018-06-26</th>
      <td>2018-06-26</td>
      <td>10800</td>
      <td>10900</td>
      <td>11000</td>
      <td>10700</td>
      <td>63039</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 기존 날짜 열 삭제
df.drop('Date', axis=1, inplace=True)
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
      <th>Close</th>
      <th>Start</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>new_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-07-02</th>
      <td>10100</td>
      <td>10850</td>
      <td>10900</td>
      <td>10000</td>
      <td>137977</td>
    </tr>
    <tr>
      <th>2018-06-29</th>
      <td>10700</td>
      <td>10550</td>
      <td>10900</td>
      <td>9990</td>
      <td>170253</td>
    </tr>
    <tr>
      <th>2018-06-28</th>
      <td>10400</td>
      <td>10900</td>
      <td>10950</td>
      <td>10150</td>
      <td>155769</td>
    </tr>
    <tr>
      <th>2018-06-27</th>
      <td>10900</td>
      <td>10800</td>
      <td>11050</td>
      <td>10500</td>
      <td>133548</td>
    </tr>
    <tr>
      <th>2018-06-26</th>
      <td>10800</td>
      <td>10900</td>
      <td>11000</td>
      <td>10700</td>
      <td>63039</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 20 entries, 2018-07-02 to 2018-06-01
    Data columns (total 5 columns):
     #   Column  Non-Null Count  Dtype
    ---  ------  --------------  -----
     0   Close   20 non-null     int64
     1   Start   20 non-null     int64
     2   High    20 non-null     int64
     3   Low     20 non-null     int64
     4   Volume  20 non-null     int64
    dtypes: int64(5)
    memory usage: 960.0 bytes
    

* Timestamp를 Period로 변환
##### to_period() 
##### freq 옵션 
freq 옵션으로 기준이 되는 기간 설정  
'D' - 1일 기간
'M' - 1개월 기간
'A' - 1년 기간. 12월 기준


```python
# Timestamp로 변경
import pandas as pd
dates = ['2019-01-01', '2020-03-01', '2021-06-01']
ts_dates = pd.to_datetime(dates)
ts_dates
```




    DatetimeIndex(['2019-01-01', '2020-03-01', '2021-06-01'], dtype='datetime64[ns]', freq=None)




```python
# Period로 변경
pr_day = ts_dates.to_period(freq='D')
pr_day
```




    PeriodIndex(['2019-01-01', '2020-03-01', '2021-06-01'], dtype='period[D]', freq='D')




```python
pr_month = ts_dates.to_period(freq='M')
pr_month
```




    PeriodIndex(['2019-01', '2020-03', '2021-06'], dtype='period[M]', freq='M')




```python
pr_year = ts_dates.to_period(freq='A')
pr_year
```




    PeriodIndex(['2019', '2020', '2021'], dtype='period[A-DEC]', freq='A-DEC')



### <2> 시계열 데이터 만들기

* timestamp 배열
##### date_range() : 여러 개의 날짜가 들어있는 배열 형태의 시계열 데이터 만든다.  
  
timestamp의 배열 만들기 - 월 간격, 월의 시작일 기준


```python
ts_ms = pd.date_range(start = '2019-01-01',     # 날짜 범위 시작
                      end = None,               # 날짜 범위 끝
                      periods = 6,              # 생성할 Timestamp 개수
                      freq = 'MS',              # 시간 간격 (MS : 월의 시작일)
                      tz = 'Asia/Seoul')        # 한국 시간대 설정 옵션
ts_ms
```




    DatetimeIndex(['2019-01-01 00:00:00+09:00', '2019-02-01 00:00:00+09:00',
                   '2019-03-01 00:00:00+09:00', '2019-04-01 00:00:00+09:00',
                   '2019-05-01 00:00:00+09:00', '2019-06-01 00:00:00+09:00'],
                  dtype='datetime64[ns, Asia/Seoul]', freq='MS')




```python
ts_me = pd.date_range('2019-01-01', 
                      periods = 6,
                      freq = '3M',          # 시간 간격 (M : 월의 마지막 날)
                      tz = 'Asia/Seoul')
ts_me
```




    DatetimeIndex(['2019-01-31 00:00:00+09:00', '2019-04-30 00:00:00+09:00',
                   '2019-07-31 00:00:00+09:00', '2019-10-31 00:00:00+09:00',
                   '2020-01-31 00:00:00+09:00', '2020-04-30 00:00:00+09:00'],
                  dtype='datetime64[ns, Asia/Seoul]', freq='3M')



<br>

* Period 배열


```python
pr_m = pd.period_range(start = '2019-01-01',
                       end = None,
                       periods = 3,
                       freq = 'M')
pr_m
```




    PeriodIndex(['2019-01', '2019-02', '2019-03'], dtype='period[M]', freq='M')




```python
pr_h = pd.period_range(start = '2019-01-01',
                       end = None,
                       periods = 3,
                       freq = 'H')
pr_h
```




    PeriodIndex(['2019-01-01 00:00', '2019-01-01 01:00', '2019-01-01 02:00'], dtype='period[H]', freq='H')



### <3> 시계열 데이터 활용
<br>

* 날짜 데이터 분리  
    * dt 속성을 이용하여 new_date 열의 연-월-일 정보를 년,월,일로 구분  



```python
import pandas as pd

df = pd.read_csv('C:/Users/USER/Desktop/파이썬머신러닝 자료/part5/stock-data.csv')
df['new date'] = pd.to_datetime(df['Date'])
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
      <th>Date</th>
      <th>Close</th>
      <th>Start</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>new date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-07-02</td>
      <td>10100</td>
      <td>10850</td>
      <td>10900</td>
      <td>10000</td>
      <td>137977</td>
      <td>2018-07-02</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-06-29</td>
      <td>10700</td>
      <td>10550</td>
      <td>10900</td>
      <td>9990</td>
      <td>170253</td>
      <td>2018-06-29</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-06-28</td>
      <td>10400</td>
      <td>10900</td>
      <td>10950</td>
      <td>10150</td>
      <td>155769</td>
      <td>2018-06-28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-06-27</td>
      <td>10900</td>
      <td>10800</td>
      <td>11050</td>
      <td>10500</td>
      <td>133548</td>
      <td>2018-06-27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018-06-26</td>
      <td>10800</td>
      <td>10900</td>
      <td>11000</td>
      <td>10700</td>
      <td>63039</td>
      <td>2018-06-26</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['Year'] = df['new date'].dt.year
df['Month'] = df['new date'].dt.month
df['Day'] = df['new date'].dt.day
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
      <th>Date</th>
      <th>Close</th>
      <th>Start</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>new date</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-07-02</td>
      <td>10100</td>
      <td>10850</td>
      <td>10900</td>
      <td>10000</td>
      <td>137977</td>
      <td>2018-07-02</td>
      <td>2018</td>
      <td>7</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-06-29</td>
      <td>10700</td>
      <td>10550</td>
      <td>10900</td>
      <td>9990</td>
      <td>170253</td>
      <td>2018-06-29</td>
      <td>2018</td>
      <td>6</td>
      <td>29</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-06-28</td>
      <td>10400</td>
      <td>10900</td>
      <td>10950</td>
      <td>10150</td>
      <td>155769</td>
      <td>2018-06-28</td>
      <td>2018</td>
      <td>6</td>
      <td>28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-06-27</td>
      <td>10900</td>
      <td>10800</td>
      <td>11050</td>
      <td>10500</td>
      <td>133548</td>
      <td>2018-06-27</td>
      <td>2018</td>
      <td>6</td>
      <td>27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018-06-26</td>
      <td>10800</td>
      <td>10900</td>
      <td>11000</td>
      <td>10700</td>
      <td>63039</td>
      <td>2018-06-26</td>
      <td>2018</td>
      <td>6</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
</div>



<br> 

* to_period() -> 연-월-일 중 연-월 또는 연도 추출


```python
df['Date_yr'] = df['new date'].dt.to_period(freq='A')
df['Date_m'] = df['new date'].dt.to_period(freq='M')
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
      <th>Date</th>
      <th>Close</th>
      <th>Start</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>new date</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
      <th>Date_yr</th>
      <th>Date_m</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-07-02</td>
      <td>10100</td>
      <td>10850</td>
      <td>10900</td>
      <td>10000</td>
      <td>137977</td>
      <td>2018-07-02</td>
      <td>2018</td>
      <td>7</td>
      <td>2</td>
      <td>2018</td>
      <td>2018-07</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-06-29</td>
      <td>10700</td>
      <td>10550</td>
      <td>10900</td>
      <td>9990</td>
      <td>170253</td>
      <td>2018-06-29</td>
      <td>2018</td>
      <td>6</td>
      <td>29</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-06-28</td>
      <td>10400</td>
      <td>10900</td>
      <td>10950</td>
      <td>10150</td>
      <td>155769</td>
      <td>2018-06-28</td>
      <td>2018</td>
      <td>6</td>
      <td>28</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-06-27</td>
      <td>10900</td>
      <td>10800</td>
      <td>11050</td>
      <td>10500</td>
      <td>133548</td>
      <td>2018-06-27</td>
      <td>2018</td>
      <td>6</td>
      <td>27</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018-06-26</td>
      <td>10800</td>
      <td>10900</td>
      <td>11000</td>
      <td>10700</td>
      <td>63039</td>
      <td>2018-06-26</td>
      <td>2018</td>
      <td>6</td>
      <td>26</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.set_index(['Date_m'], inplace=True)
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
      <th>Date</th>
      <th>Close</th>
      <th>Start</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>new date</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
      <th>Date_yr</th>
    </tr>
    <tr>
      <th>Date_m</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-07</th>
      <td>2018-07-02</td>
      <td>10100</td>
      <td>10850</td>
      <td>10900</td>
      <td>10000</td>
      <td>137977</td>
      <td>2018-07-02</td>
      <td>2018</td>
      <td>7</td>
      <td>2</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2018-06</th>
      <td>2018-06-29</td>
      <td>10700</td>
      <td>10550</td>
      <td>10900</td>
      <td>9990</td>
      <td>170253</td>
      <td>2018-06-29</td>
      <td>2018</td>
      <td>6</td>
      <td>29</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2018-06</th>
      <td>2018-06-28</td>
      <td>10400</td>
      <td>10900</td>
      <td>10950</td>
      <td>10150</td>
      <td>155769</td>
      <td>2018-06-28</td>
      <td>2018</td>
      <td>6</td>
      <td>28</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2018-06</th>
      <td>2018-06-27</td>
      <td>10900</td>
      <td>10800</td>
      <td>11050</td>
      <td>10500</td>
      <td>133548</td>
      <td>2018-06-27</td>
      <td>2018</td>
      <td>6</td>
      <td>27</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2018-06</th>
      <td>2018-06-26</td>
      <td>10800</td>
      <td>10900</td>
      <td>11000</td>
      <td>10700</td>
      <td>63039</td>
      <td>2018-06-26</td>
      <td>2018</td>
      <td>6</td>
      <td>26</td>
      <td>2018</td>
    </tr>
  </tbody>
</table>
</div>



<br>

* 날짜 인덱스 활용


```python
df.set_index(['new date'], inplace=True)
df.index
```




    DatetimeIndex(['2018-07-02', '2018-06-29', '2018-06-28', '2018-06-27',
                   '2018-06-26', '2018-06-25', '2018-06-22', '2018-06-21',
                   '2018-06-20', '2018-06-19', '2018-06-18', '2018-06-15',
                   '2018-06-14', '2018-06-12', '2018-06-11', '2018-06-08',
                   '2018-06-07', '2018-06-05', '2018-06-04', '2018-06-01'],
                  dtype='datetime64[ns]', name='new date', freq=None)



날짜 인덱스를 이용하여 데이터 선택하기  
-> 연-월-일 중에서 내가 필요로 하는 레벨을 선택적으로 인덱싱할 수 있다.


```python
df_y = df['2018']
df_y.head()
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
      <th>Date</th>
      <th>Close</th>
      <th>Start</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
      <th>Date_yr</th>
    </tr>
    <tr>
      <th>new date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-07-02</th>
      <td>2018-07-02</td>
      <td>10100</td>
      <td>10850</td>
      <td>10900</td>
      <td>10000</td>
      <td>137977</td>
      <td>2018</td>
      <td>7</td>
      <td>2</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2018-06-29</th>
      <td>2018-06-29</td>
      <td>10700</td>
      <td>10550</td>
      <td>10900</td>
      <td>9990</td>
      <td>170253</td>
      <td>2018</td>
      <td>6</td>
      <td>29</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2018-06-28</th>
      <td>2018-06-28</td>
      <td>10400</td>
      <td>10900</td>
      <td>10950</td>
      <td>10150</td>
      <td>155769</td>
      <td>2018</td>
      <td>6</td>
      <td>28</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2018-06-27</th>
      <td>2018-06-27</td>
      <td>10900</td>
      <td>10800</td>
      <td>11050</td>
      <td>10500</td>
      <td>133548</td>
      <td>2018</td>
      <td>6</td>
      <td>27</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2018-06-26</th>
      <td>2018-06-26</td>
      <td>10800</td>
      <td>10900</td>
      <td>11000</td>
      <td>10700</td>
      <td>63039</td>
      <td>2018</td>
      <td>6</td>
      <td>26</td>
      <td>2018</td>
    </tr>
  </tbody>
</table>
</div>




```python
# loc인덱서 활용
df_ym = df.loc['2018-07']
df_ym.head()
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
      <th>Date</th>
      <th>Close</th>
      <th>Start</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
      <th>Date_yr</th>
    </tr>
    <tr>
      <th>new date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-07-02</th>
      <td>2018-07-02</td>
      <td>10100</td>
      <td>10850</td>
      <td>10900</td>
      <td>10000</td>
      <td>137977</td>
      <td>2018</td>
      <td>7</td>
      <td>2</td>
      <td>2018</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 열 범위 슬라이싱
df_ym_cols = df.loc['2018-07', 'Start':'High']
df_ym_cols.head()
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
      <th>Start</th>
      <th>High</th>
    </tr>
    <tr>
      <th>new date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-07-02</th>
      <td>10850</td>
      <td>10900</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_ymd = df['2018-07-02']
df_ymd
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
      <th>Date</th>
      <th>Close</th>
      <th>Start</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
      <th>Date_yr</th>
    </tr>
    <tr>
      <th>new date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-07-02</th>
      <td>2018-07-02</td>
      <td>10100</td>
      <td>10850</td>
      <td>10900</td>
      <td>10000</td>
      <td>137977</td>
      <td>2018</td>
      <td>7</td>
      <td>2</td>
      <td>2018</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 날짜 범위 지정
df_day_range = df['2018-06-25':'2018-06-20']
df_day_range
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
      <th>Date</th>
      <th>Close</th>
      <th>Start</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
      <th>Date_yr</th>
    </tr>
    <tr>
      <th>new date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-06-25</th>
      <td>2018-06-25</td>
      <td>11150</td>
      <td>11400</td>
      <td>11450</td>
      <td>11000</td>
      <td>55519</td>
      <td>2018</td>
      <td>6</td>
      <td>25</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2018-06-22</th>
      <td>2018-06-22</td>
      <td>11300</td>
      <td>11250</td>
      <td>11450</td>
      <td>10750</td>
      <td>134805</td>
      <td>2018</td>
      <td>6</td>
      <td>22</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2018-06-21</th>
      <td>2018-06-21</td>
      <td>11200</td>
      <td>11350</td>
      <td>11750</td>
      <td>11200</td>
      <td>133002</td>
      <td>2018</td>
      <td>6</td>
      <td>21</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2018-06-20</th>
      <td>2018-06-20</td>
      <td>11550</td>
      <td>11200</td>
      <td>11600</td>
      <td>10900</td>
      <td>308596</td>
      <td>2018</td>
      <td>6</td>
      <td>20</td>
      <td>2018</td>
    </tr>
  </tbody>
</table>
</div>



<br>

Timestamp 객체로 표시된 두 날짜 시간 사이의 시간 간격 계산   
기준일로부터 180~189일 경과한 날짜 사이의 값들만 선택하기


```python
today = pd.to_datetime('2018-12-25')       # 기준일 생성
df['time_delta'] = today - df.index        # 날짜 차이 계산
df.set_index(['time_delta'], inplace=True)
df_180 = df['180 days': '189 days']
df_180
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
      <th>Date</th>
      <th>Close</th>
      <th>Start</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
      <th>Date_yr</th>
    </tr>
    <tr>
      <th>time_delta</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>180 days</th>
      <td>2018-06-28</td>
      <td>10400</td>
      <td>10900</td>
      <td>10950</td>
      <td>10150</td>
      <td>155769</td>
      <td>2018</td>
      <td>6</td>
      <td>28</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>181 days</th>
      <td>2018-06-27</td>
      <td>10900</td>
      <td>10800</td>
      <td>11050</td>
      <td>10500</td>
      <td>133548</td>
      <td>2018</td>
      <td>6</td>
      <td>27</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>182 days</th>
      <td>2018-06-26</td>
      <td>10800</td>
      <td>10900</td>
      <td>11000</td>
      <td>10700</td>
      <td>63039</td>
      <td>2018</td>
      <td>6</td>
      <td>26</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>183 days</th>
      <td>2018-06-25</td>
      <td>11150</td>
      <td>11400</td>
      <td>11450</td>
      <td>11000</td>
      <td>55519</td>
      <td>2018</td>
      <td>6</td>
      <td>25</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>186 days</th>
      <td>2018-06-22</td>
      <td>11300</td>
      <td>11250</td>
      <td>11450</td>
      <td>10750</td>
      <td>134805</td>
      <td>2018</td>
      <td>6</td>
      <td>22</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>187 days</th>
      <td>2018-06-21</td>
      <td>11200</td>
      <td>11350</td>
      <td>11750</td>
      <td>11200</td>
      <td>133002</td>
      <td>2018</td>
      <td>6</td>
      <td>21</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>188 days</th>
      <td>2018-06-20</td>
      <td>11550</td>
      <td>11200</td>
      <td>11600</td>
      <td>10900</td>
      <td>308596</td>
      <td>2018</td>
      <td>6</td>
      <td>20</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>189 days</th>
      <td>2018-06-19</td>
      <td>11300</td>
      <td>11850</td>
      <td>11950</td>
      <td>11300</td>
      <td>180656</td>
      <td>2018</td>
      <td>6</td>
      <td>19</td>
      <td>2018</td>
    </tr>
  </tbody>
</table>
</div>


