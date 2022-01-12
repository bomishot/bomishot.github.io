---
layout: single
title:  "PART1 판다스 입문"
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



# < series (1차원 배열) >


```python
import pandas as pd
```


```python
# 딕셔너리->시리즈 변경
dict_data = {'송이':0,'뚜뚜':1,'꿀이':2} #<key:value>쌍으로 딕셔너리 만들고, 변수 dict_data에 저장
sr = pd.Series(dict_data) #판다스 Series()함수이용해 딕셔너리->시리즈 변경
sr
```




    송이    0
    뚜뚜    1
    꿀이    2
    dtype: int64




```python
# 인덱스 배열
idx = sr.index
idx
```




    Index(['송이', '뚜뚜', '꿀이'], dtype='object')




```python
# 데이터 값 배열
val = sr.values
val
```




    array([0, 1, 2], dtype=int64)




```python
# 튜플->시리즈 / 시리즈 원소 선택
tup_data = ('보미', '2021-12-28', '여', True)
sr = pd.Series(tup_data, index = ['이름', '오늘날짜', '성별', '학생여부']) 
sr
```




    이름              보미
    오늘날짜    2021-12-28
    성별               여
    학생여부          True
    dtype: object




```python
sr[0]
```




    '보미'




```python
sr[[0]] # sr의 0번째 원소 선택 (정수형 위치 인덱스)
```




    이름    보미
    dtype: object




```python
sr[[1,2]]  # 대괄호 두개 주의! (인덱스 리스트 이용)
```




    오늘날짜    2021-12-28
    성별               여
    dtype: object




```python
sr[1:2] # 범위 끝 포함X
```




    오늘날짜    2021-12-28
    dtype: object




```python
sr['이름'] #'이름' 라벨을 가진 원소 선택 (인덱스 이름 이용)
```




    '보미'




```python
sr[['이름', '학생여부']]
```




    이름        보미
    학생여부    True
    dtype: object




```python
sr['이름': '학생여부'] # 범위 끝 포함ㅇ (헷갈리지말기 숫자일때만 범위 끝 포함안함)
```




    이름              보미
    오늘날짜    2021-12-28
    성별               여
    학생여부          True
    dtype: object



# < DataFrame (2차원 배열) >
데이터 프레임은 여러개의 시리즈(column)을 모아 놓은 집합

- dictionary -> DataFrame : pd.DataFrame(dictionary)
- 행인덱스/ 열 이름 설정 : pd.DataFrame(2차원 배열 , 
                                        index =  행 인덱스 배열
                                        columns = 열 이름 배열)
- 행 인덱스 변경  
  열 이름 변경  
- 행 삭제
  열 삭제
- 행 선택
  열 선택
- 행 추가
  열 추가
- 원소 값 변경
- 행,열 위치 바꾸기



```python
# 딕셔너리 ->데이터 프레임 변환
dict_data = {'c0': [1,2,3],
            'c1': [4,5,6],
            'c2': [7,8,9],
            'c3': [10,11,12],
            'c4': [13,14,15]}
df = pd.DataFrame(dict_data)
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
      <th>c0</th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
      <th>c4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>4</td>
      <td>7</td>
      <td>10</td>
      <td>13</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>5</td>
      <td>8</td>
      <td>11</td>
      <td>14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>6</td>
      <td>9</td>
      <td>12</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
df = pd.DataFrame([[15, '여', '동일'],
                  [15, '남', '하계']],
                  index =['보미', '송이'],
                  columns = ['age', 'sex', 'school'])
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
      <th>age</th>
      <th>sex</th>
      <th>school</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>15</td>
      <td>여</td>
      <td>동일</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>15</td>
      <td>남</td>
      <td>하계</td>
    </tr>
  </tbody>
</table>
</div>



# 행/열 이름 변환 (rename)


```python
df.index
```




    Index(['보미', '송이'], dtype='object')




```python
df.columns
```




    Index(['age', 'sex', 'school'], dtype='object')




```python
df.index = ['student1', 'student2']
df.index
```




    Index(['student1', 'student2'], dtype='object')




```python
df.rename(index = {'student1':'보미', 'student2':'송이'}, inplace = True)
df.index
```




    Index(['보미', '송이'], dtype='object')




```python
df.columns = ['연령', '성별', '학교']
df.columns
```




    Index(['연령', '성별', '학교'], dtype='object')




```python
df.rename(columns = {'연령':'나이', '성별':'성', '학교':'스쿨'}, inplace = True)
df.columns
```




    Index(['나이', '성', '스쿨'], dtype='object')



# 행/열 삭제 (drop)
inplace=True : 원본 객체 직접 변경 
inplace=False: 새로운 객체 생성, 원본 객체 그대로 유지됨
행 : axis=0
열 : axis=1


```python
exam_data = {'수학':[70,80,90], 
             '영어':[89,79,69], 
             '음악':[100,90,80], 
             '체육':[20,30,40]}
df = pd.DataFrame(exam_data, index = ['보미', '송이', '뚜뚜'])
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>70</td>
      <td>89</td>
      <td>100</td>
      <td>20</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>80</td>
      <td>79</td>
      <td>90</td>
      <td>30</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>90</td>
      <td>69</td>
      <td>80</td>
      <td>40</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = df.copy()
df2.drop('뚜뚜', inplace=True)
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>70</td>
      <td>89</td>
      <td>100</td>
      <td>20</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>80</td>
      <td>79</td>
      <td>90</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3 = df.copy()
df3.drop(['송이', '뚜뚜'], inplace=True)
df3
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>70</td>
      <td>89</td>
      <td>100</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>




```python
df4 = df.copy()
df4.drop('체육', axis=1, inplace=True)
df4
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>70</td>
      <td>89</td>
      <td>100</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>80</td>
      <td>79</td>
      <td>90</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>90</td>
      <td>69</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>




```python
df5 = df.copy()
df5.drop(['음악', '수학'], axis =1, inplace=True)
df5
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
      <th>영어</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>89</td>
      <td>20</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>79</td>
      <td>30</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>69</td>
      <td>40</td>
    </tr>
  </tbody>
</table>
</div>



# 행 선택 (loc, iloc)
- loc: 인덱스 이름  
- iloc : 정수형 위치 인덱스


```python
label1 = df.loc['보미']
label1
```




    수학     70
    영어     89
    음악    100
    체육     20
    Name: 보미, dtype: int64




```python
position1 = df.iloc[0]
position1
```




    수학     70
    영어     89
    음악    100
    체육     20
    Name: 보미, dtype: int64




```python
label2 = df.loc[['보미', '송이']]
label2
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>70</td>
      <td>89</td>
      <td>100</td>
      <td>20</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>80</td>
      <td>79</td>
      <td>90</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>




```python
position2 = df.iloc[[0,1]]
position2
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>70</td>
      <td>89</td>
      <td>100</td>
      <td>20</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>80</td>
      <td>79</td>
      <td>90</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>




```python
label3 = df.loc['보미': '송이']
label3
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>70</td>
      <td>89</td>
      <td>100</td>
      <td>20</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>80</td>
      <td>79</td>
      <td>90</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>




```python
position3 = df.iloc[0:2] # 범위 끝 제외
position3
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>70</td>
      <td>89</td>
      <td>100</td>
      <td>20</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>80</td>
      <td>79</td>
      <td>90</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>



# 열 선택


```python
math1 = df['수학']
math1
```




    보미    70
    송이    80
    뚜뚜    90
    Name: 수학, dtype: int64




```python
type(math1)
```




    pandas.core.series.Series




```python
math2 = df[['수학']]
math2
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
      <th>수학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>70</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>80</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
type(math2) 
```




    pandas.core.frame.DataFrame




```python
English = df.영어
English
```




    보미    89
    송이    79
    뚜뚜    69
    Name: 영어, dtype: int64




```python
music_gym = df[['음악', '체육']]
music_gym
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
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>100</td>
      <td>20</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>90</td>
      <td>30</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>80</td>
      <td>40</td>
    </tr>
  </tbody>
</table>
</div>



# 범위 슬라이싱


```python
#iloc의 범위 슬라이싱    [시작 인덱스: 끝 인덱스 : 간격] 끝 인덱스보다 1작게 출력
df.iloc[::2] # 아무것도 안쓰여져 있는 것은 모든 행 출력
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>70</td>
      <td>89</td>
      <td>100</td>
      <td>20</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>90</td>
      <td>69</td>
      <td>80</td>
      <td>40</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.iloc[::-1] # 역순
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>뚜뚜</th>
      <td>90</td>
      <td>69</td>
      <td>80</td>
      <td>40</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>80</td>
      <td>79</td>
      <td>90</td>
      <td>30</td>
    </tr>
    <tr>
      <th>보미</th>
      <td>70</td>
      <td>89</td>
      <td>100</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>



# 원소 선택


```python
exam_data = {'이름':['보미','송이','뚜뚜'],
             '수학':[100,90,80], 
             '영어':[90,80,70],
             '음악':[80,90,89],
             '체육':[70,80,90]}
df = pd.DataFrame(exam_data)
dff = df.copy()
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
      <th>이름</th>
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>보미</td>
      <td>100</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>송이</td>
      <td>90</td>
      <td>80</td>
      <td>90</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>뚜뚜</td>
      <td>80</td>
      <td>70</td>
      <td>89</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.set_index('이름', inplace=True) # '이름' 열을 새롱누 인덱스로 정하고, df 객체에 변경 사항 반영
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
    <tr>
      <th>이름</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>100</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>90</td>
      <td>80</td>
      <td>90</td>
      <td>80</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>80</td>
      <td>70</td>
      <td>89</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
#원소 1개 지정
a = df.loc['보미','음악']
a
```




    80




```python
b = df.iloc[0,[2]]
b
```




    음악    80
    Name: 보미, dtype: int64




```python
# 원소 2개 이상
c = df.loc['보미',['수학', '영어']]
c
```




    수학    100
    영어     90
    Name: 보미, dtype: int64




```python
d = df.iloc[0,[0,1]]
d
```




    수학    100
    영어     90
    Name: 보미, dtype: int64




```python
e = df.iloc[0,2:]
e
```




    음악    80
    체육    70
    Name: 보미, dtype: int64




```python
# 행 인덱스와 열 이름 각각2개이상 선택
f = df.loc[['송이','뚜뚜'],['음악', '체육']]
f
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
      <th>음악</th>
      <th>체육</th>
    </tr>
    <tr>
      <th>이름</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>송이</th>
      <td>90</td>
      <td>80</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>89</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
g = df.iloc[[1,2],[2,3]]
g
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
      <th>음악</th>
      <th>체육</th>
    </tr>
    <tr>
      <th>이름</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>송이</th>
      <td>90</td>
      <td>80</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>89</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
h = df.loc['보미':'송이', '음악':'체육']
h
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
      <th>음악</th>
      <th>체육</th>
    </tr>
    <tr>
      <th>이름</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>90</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>




```python
f = df.iloc[0:2, 2:]
f
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
      <th>음악</th>
      <th>체육</th>
    </tr>
    <tr>
      <th>이름</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>90</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>



# 행/열 추가


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
      <th>이름</th>
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>보미</td>
      <td>100</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>송이</td>
      <td>90</td>
      <td>80</td>
      <td>90</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>뚜뚜</td>
      <td>80</td>
      <td>70</td>
      <td>89</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['new'] = 80
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
      <th>이름</th>
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
      <th>new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>보미</td>
      <td>100</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
      <td>80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>송이</td>
      <td>90</td>
      <td>80</td>
      <td>90</td>
      <td>80</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>뚜뚜</td>
      <td>80</td>
      <td>70</td>
      <td>89</td>
      <td>90</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.drop('new', axis=1, inplace=True)
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
      <th>이름</th>
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>보미</td>
      <td>100</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>송이</td>
      <td>90</td>
      <td>80</td>
      <td>90</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>뚜뚜</td>
      <td>80</td>
      <td>70</td>
      <td>89</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 행 추가
df.loc[3]=0
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
      <th>이름</th>
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>보미</td>
      <td>100</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>송이</td>
      <td>90</td>
      <td>80</td>
      <td>90</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>뚜뚜</td>
      <td>80</td>
      <td>70</td>
      <td>89</td>
      <td>90</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[4] = ['new', 100, 100, 100,100]
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
      <th>이름</th>
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>보미</td>
      <td>100</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>송이</td>
      <td>90</td>
      <td>80</td>
      <td>90</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>뚜뚜</td>
      <td>80</td>
      <td>70</td>
      <td>89</td>
      <td>90</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>new</td>
      <td>100</td>
      <td>100</td>
      <td>100</td>
      <td>100</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 기존 행 복사해 새로운 행 추가
df.loc['new'] = df.loc[3]
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
      <th>이름</th>
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>보미</td>
      <td>100</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>송이</td>
      <td>90</td>
      <td>80</td>
      <td>90</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>뚜뚜</td>
      <td>80</td>
      <td>70</td>
      <td>89</td>
      <td>90</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>new</td>
      <td>100</td>
      <td>100</td>
      <td>100</td>
      <td>100</td>
    </tr>
    <tr>
      <th>new</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



# 원소 값 변경


```python
dff
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
      <th>이름</th>
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>보미</td>
      <td>100</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>송이</td>
      <td>90</td>
      <td>80</td>
      <td>90</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>뚜뚜</td>
      <td>80</td>
      <td>70</td>
      <td>89</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
dff.set_index('이름', inplace=True)
dff
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
    <tr>
      <th>이름</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>100</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>90</td>
      <td>80</td>
      <td>90</td>
      <td>80</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>80</td>
      <td>70</td>
      <td>89</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
dff.iloc[1][2] = 100
dff.loc['뚜뚜']['영어'] = 100
dff.loc['보미','체육'] =100
dff
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
    <tr>
      <th>이름</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>100</td>
      <td>90</td>
      <td>80</td>
      <td>100</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>90</td>
      <td>80</td>
      <td>100</td>
      <td>80</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>80</td>
      <td>100</td>
      <td>89</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
dff.iloc[0,[1,2]] = 0
dff.loc['송이',['수학', '영어']] = 0, 1
dff
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
    <tr>
      <th>이름</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>100</td>
      <td>0</td>
      <td>0</td>
      <td>100</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>0</td>
      <td>1</td>
      <td>100</td>
      <td>80</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>80</td>
      <td>100</td>
      <td>89</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>



# 행/열 위치 바꾸기 (전치 T)


```python
dff.transpose()
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
      <th>이름</th>
      <th>보미</th>
      <th>송이</th>
      <th>뚜뚜</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>수학</th>
      <td>100</td>
      <td>0</td>
      <td>80</td>
    </tr>
    <tr>
      <th>영어</th>
      <td>0</td>
      <td>1</td>
      <td>100</td>
    </tr>
    <tr>
      <th>음악</th>
      <td>0</td>
      <td>100</td>
      <td>89</td>
    </tr>
    <tr>
      <th>체육</th>
      <td>100</td>
      <td>80</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
dff2 = dff.T
dff
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
      <th>수학</th>
      <th>영어</th>
      <th>음악</th>
      <th>체육</th>
    </tr>
    <tr>
      <th>이름</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>보미</th>
      <td>100</td>
      <td>0</td>
      <td>0</td>
      <td>100</td>
    </tr>
    <tr>
      <th>송이</th>
      <td>0</td>
      <td>1</td>
      <td>100</td>
      <td>80</td>
    </tr>
    <tr>
      <th>뚜뚜</th>
      <td>80</td>
      <td>100</td>
      <td>89</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
addd = {
    '이름은 바로바로바로':['최소연'],
    '~20':['소추'],
    21:['솢추'],
    22:['야추'],
    23:['송충이?']
}
addd = pd.DataFrame(addd)
ad = addd.set_index(['이름은 바로바로바로'])
ad
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
      <th>~20</th>
      <th>21</th>
      <th>22</th>
      <th>23</th>
    </tr>
    <tr>
      <th>이름은 바로바로바로</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>최소연</th>
      <td>소추</td>
      <td>솢추</td>
      <td>야추</td>
      <td>송충이?</td>
    </tr>
  </tbody>
</table>
</div>



# 행 인덱스 : 
- 재배열 reindex() 
- 초기화 reset_index() 
- 정렬 - (행 기준) sort_index() 
       - (열 기준) sort_values()
       - ascending=True: 오름차순
       - ascending=False: 내림차순


```python
dict_data = {'c0':[1,2,3], 'c1':[4,5,6], 'c2':[7,8,9], 'c3':[10,11,12], 'c4':[13,14,15]}
df = pd.DataFrame(dict_data, index = ['r0','r1','r2']) # 인덱스 설정 
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
      <th>c0</th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
      <th>c4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>r0</th>
      <td>1</td>
      <td>4</td>
      <td>7</td>
      <td>10</td>
      <td>13</td>
    </tr>
    <tr>
      <th>r1</th>
      <td>2</td>
      <td>5</td>
      <td>8</td>
      <td>11</td>
      <td>14</td>
    </tr>
    <tr>
      <th>r2</th>
      <td>3</td>
      <td>6</td>
      <td>9</td>
      <td>12</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
new_index = ['r0','r1','r2','r3','r4']
ndf = df.reindex(new_index)
ndf
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
      <th>c0</th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
      <th>c4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>r0</th>
      <td>1.0</td>
      <td>4.0</td>
      <td>7.0</td>
      <td>10.0</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>r1</th>
      <td>2.0</td>
      <td>5.0</td>
      <td>8.0</td>
      <td>11.0</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>r2</th>
      <td>3.0</td>
      <td>6.0</td>
      <td>9.0</td>
      <td>12.0</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>r3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>r4</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
ndf2 = df.reindex(new_index, fill_value=0) # reindex로 발생한 NaN 값을 숫자 0으로 채우기
ndf2
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
      <th>c0</th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
      <th>c4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>r0</th>
      <td>1</td>
      <td>4</td>
      <td>7</td>
      <td>10</td>
      <td>13</td>
    </tr>
    <tr>
      <th>r1</th>
      <td>2</td>
      <td>5</td>
      <td>8</td>
      <td>11</td>
      <td>14</td>
    </tr>
    <tr>
      <th>r2</th>
      <td>3</td>
      <td>6</td>
      <td>9</td>
      <td>12</td>
      <td>15</td>
    </tr>
    <tr>
      <th>r3</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>r4</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




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
      <th>c0</th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
      <th>c4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>r0</th>
      <td>1</td>
      <td>4</td>
      <td>7</td>
      <td>10</td>
      <td>13</td>
    </tr>
    <tr>
      <th>r1</th>
      <td>2</td>
      <td>5</td>
      <td>8</td>
      <td>11</td>
      <td>14</td>
    </tr>
    <tr>
      <th>r2</th>
      <td>3</td>
      <td>6</td>
      <td>9</td>
      <td>12</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 행 인덱스 초기화
ndf3 = df.reset_index()
ndf3
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
      <th>index</th>
      <th>c0</th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
      <th>c4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>r0</td>
      <td>1</td>
      <td>4</td>
      <td>7</td>
      <td>10</td>
      <td>13</td>
    </tr>
    <tr>
      <th>1</th>
      <td>r1</td>
      <td>2</td>
      <td>5</td>
      <td>8</td>
      <td>11</td>
      <td>14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>r2</td>
      <td>3</td>
      <td>6</td>
      <td>9</td>
      <td>12</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
ndf4 = df.sort_index(ascending=False)
ndf4
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
      <th>c0</th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
      <th>c4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>r2</th>
      <td>3</td>
      <td>6</td>
      <td>9</td>
      <td>12</td>
      <td>15</td>
    </tr>
    <tr>
      <th>r1</th>
      <td>2</td>
      <td>5</td>
      <td>8</td>
      <td>11</td>
      <td>14</td>
    </tr>
    <tr>
      <th>r0</th>
      <td>1</td>
      <td>4</td>
      <td>7</td>
      <td>10</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>




```python
ndf5 = df.sort_values(by='c1', ascending=False) # 'c1' 열을 기준으로 내림차순 정리한 것.
ndf5
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
      <th>c0</th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
      <th>c4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>r2</th>
      <td>3</td>
      <td>6</td>
      <td>9</td>
      <td>12</td>
      <td>15</td>
    </tr>
    <tr>
      <th>r1</th>
      <td>2</td>
      <td>5</td>
      <td>8</td>
      <td>11</td>
      <td>14</td>
    </tr>
    <tr>
      <th>r0</th>
      <td>1</td>
      <td>4</td>
      <td>7</td>
      <td>10</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>



# < 산술연산 > 
- 판다스에서 NaN : 유효한 값이 존재하지 않는다는 의미
- fill_value=0 옵션 사용 시 : NaN 대신 0으로 사용됨

# 시리즈 연산


```python
student1 = pd.Series({'국어':100,'수학':80, '영어':90})
student1
```




    국어    100
    수학     20
    영어     34
    dtype: int64




```python
student2 = pd.Series({'수학':80,'국어':90, '영어' :80})
student2
```




    수학    80
    국어    90
    영어    80
    dtype: int64




```python
addition = student1 + student2
substraction = student1 - student2
multiplication = student1 * student2
division = student1 / student2

result = pd.DataFrame([addition, substraction, multiplication, division] , index = ['덧셈', '뺄셈', '곱셈','나눗셈'])
result
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
      <th>국어</th>
      <th>수학</th>
      <th>영어</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>덧셈</th>
      <td>190.000000</td>
      <td>100.00</td>
      <td>114.000</td>
    </tr>
    <tr>
      <th>뺄셈</th>
      <td>10.000000</td>
      <td>-60.00</td>
      <td>-46.000</td>
    </tr>
    <tr>
      <th>곱셈</th>
      <td>9000.000000</td>
      <td>1600.00</td>
      <td>2720.000</td>
    </tr>
    <tr>
      <th>나눗셈</th>
      <td>1.111111</td>
      <td>0.25</td>
      <td>0.425</td>
    </tr>
  </tbody>
</table>
</div>




```python
import pandas as pd
import numpy as np
student3 = pd.Series({'국어': np.nan, '영어':80, '수학':90})
student3
```




    국어     NaN
    영어    80.0
    수학    90.0
    dtype: float64




```python
student4 = pd.Series({'수학':80, '국어':90})
student4
```




    수학    80
    국어    90
    dtype: int64




```python
addition1 = student3 + student4
substraction1 = student3 - student4
multiplication1 = student3 * student4
division1 = student3 / student4

result2 = pd.DataFrame([addition1, substraction1, multiplication1, division1], index=['덧셈', '뺄셈', '곱셈', '나눗셈'])
result2
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
      <th>국어</th>
      <th>수학</th>
      <th>영어</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>덧셈</th>
      <td>NaN</td>
      <td>170.000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>뺄셈</th>
      <td>NaN</td>
      <td>10.000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>곱셈</th>
      <td>NaN</td>
      <td>7200.000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>나눗셈</th>
      <td>NaN</td>
      <td>1.125</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 연산 메소드 : Series1.add(Series2, fill_value=0) / add,sub,mul,div
# 출력값 inf : 무한대
sr_add = student3.add(student4, fill_value=0)
sr_sub = student3.sub(student4, fill_value=0)
sr_mul = student3.mul(student4, fill_value=0)
sr_div = student3.div(student4, fill_value=0)

sr_result = pd.DataFrame([sr_add, sr_sub, sr_mul, sr_div], index = ['덧셈', '뺄셈', '곱셈', '나눗셈'])
sr_result
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
      <th>국어</th>
      <th>수학</th>
      <th>영어</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>덧셈</th>
      <td>90.0</td>
      <td>170.000</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>뺄셈</th>
      <td>-90.0</td>
      <td>10.000</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>곱셈</th>
      <td>0.0</td>
      <td>7200.000</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>나눗셈</th>
      <td>0.0</td>
      <td>1.125</td>
      <td>inf</td>
    </tr>
  </tbody>
</table>
</div>



# DataFrame 연산
- Seaborn 라이브러리에서 제공하는 데이터셋 중에서 타이타닉('titanic') 데이터셋 사용
   : 타이타닉호에 대한 인적사항과 구조 여부 등을 정리한 자료
   : load_dataset() 함수로 불러온다.
- head() 첫 5행만 표시
- tail() 마지막 5행만 표시


```python
import pandas as pd
import seaborn as sns

# titanic 데이터셋이서 age, fare 두 개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
ti_df = titanic.loc[:, ['age', 'fare']]
ti_df.head() # 첫 5행만 표시
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
      <th>age</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>22.0</td>
      <td>7.2500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>38.0</td>
      <td>71.2833</td>
    </tr>
    <tr>
      <th>2</th>
      <td>26.0</td>
      <td>7.9250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>35.0</td>
      <td>53.1000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>35.0</td>
      <td>8.0500</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 데이터프레임 + 숫자
ti_addtion = ti_df + 10  
ti_addtion.head()
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
      <th>age</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>32.0</td>
      <td>17.2500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>48.0</td>
      <td>81.2833</td>
    </tr>
    <tr>
      <th>2</th>
      <td>36.0</td>
      <td>17.9250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45.0</td>
      <td>63.1000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45.0</td>
      <td>18.0500</td>
    </tr>
  </tbody>
</table>
</div>




```python
ti_df.tail() # 마지막 5행 표시
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
      <th>age</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>886</th>
      <td>27.0</td>
      <td>13.00</td>
    </tr>
    <tr>
      <th>887</th>
      <td>19.0</td>
      <td>30.00</td>
    </tr>
    <tr>
      <th>888</th>
      <td>NaN</td>
      <td>23.45</td>
    </tr>
    <tr>
      <th>889</th>
      <td>26.0</td>
      <td>30.00</td>
    </tr>
    <tr>
      <th>890</th>
      <td>32.0</td>
      <td>7.75</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 데이터프레임 + 데이터프레임
import pandas as pd
import seaborn as sns

titanic = sns.load_dataset('titanic')
ti_df = titanic.loc[:, ['age', 'fare']]

ti_add = ti_df + 10

ti_sub = ti_add - ti_df
ti_sub.tail()
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
      <th>age</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>886</th>
      <td>10.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>887</th>
      <td>10.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>888</th>
      <td>NaN</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>889</th>
      <td>10.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>890</th>
      <td>10.0</td>
      <td>10.0</td>
    </tr>
  </tbody>
</table>
</div>

