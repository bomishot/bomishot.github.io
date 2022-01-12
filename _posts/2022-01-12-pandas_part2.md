---
layout: single
title:  "PART2 데이터 입출력"
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


판다스는 다양한 형태의 외부 파일을 읽어와서 데이터프레임으로 변환하는 함수를 제공한다.
어떤 파일이든 데이터프레임으로 변환되고 나면 판다스의 모든 함수, 기능을 자유롭게 사용한다.

# 1. 외부 파일 불러오기
- read_csv() 함수로 데이터프레임 변환
- 열 이름으로 사용할 행 지정
    header=0: 0행을 열로 지정
    header=1: 1행을 열로 지정
    header=None: 행을 열지정하지 않음
- 행 인덱스가 되는 열 지정
    index_cole=False: 인덱스 지정하지 않음
    index_cole='c0': 'c0'열을 인덱스 지정


```python
import pandas as pd
```


```python
file_path = 'C:/Users/USER/Desktop/read_csv_sample.csv' # 속성-위치 복붙, W는 /로 바꾸고 뒤에 이름과 확장자 쓰기
df1 = pd.read_csv(file_path)
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
      <th>c0</th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
      <td>6</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = pd.read_csv(file_path, header=None)
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c0</td>
      <td>c1</td>
      <td>c2</td>
      <td>c3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>3</td>
      <td>6</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3 = pd.read_csv(file_path, header=2)
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
      <th>1</th>
      <th>2</th>
      <th>5</th>
      <th>8</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>3</td>
      <td>6</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
df4= pd.read_csv(file_path, index_col='c0')
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
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
    </tr>
    <tr>
      <th>c0</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>6</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
df5 = pd.read_csv(file_path, index_col=False)
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
      <th>c0</th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
      <td>6</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
Excel 파일
    - xlsx 확장자를 갖는 경우, engine 옵션에 'openpyxl' 지정
    - xls 확장자를 갖는 경우, engine 옵션에 'xlrd' 지정
```


```python
df6 = pd.read_excel('C:/Users/USER/Desktop/남북한발전전력량.xlsx', engine = 'openpyxl')
df6
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



JSON 파일
    - 데이터 공유를 목적으로 개발된 특수한 파일 형식 
    - <key:value> 구조 가짐

# 2. 데이터 저장하기


```python
data1 = {'name':['Jerry','Riah','Paul'],
         'algol':['A','A+','C'],
         'c++':['C','B','A']}
df7 = pd.DataFrame(data1)
df7.set_index('name', inplace=True)
df7
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
      <th>algol</th>
      <th>c++</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jerry</th>
      <td>A</td>
      <td>C</td>
    </tr>
    <tr>
      <th>Riah</th>
      <td>A+</td>
      <td>B</td>
    </tr>
    <tr>
      <th>Paul</th>
      <td>C</td>
      <td>A</td>
    </tr>
  </tbody>
</table>
</div>




```python
# to_csv 메소드를 사용하여 csv 파일로 내보내기/ 파일명은 df_sample.csv로 저장
df7.to_csv("./df_sample.csv")
```


```python
df7.to_json("./df_sample.json")
```


```python
df7.to_excel("./df_sample.xlsx")
```

# 3. 여러 개의 데이터프레임을 하나의 excel 파일로 저장
같은 excel파일의 서로 다른 시트에 데이터프레임 구분


```python
data2 = {'c0':[1,2,3],
         'c1':[4,5,6],
         'c2':[7,8,9]}
df8 = pd.DataFrame(data2)
df8.set_index('c0', inplace=True)
df8
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
    </tr>
    <tr>
      <th>c0</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
# data1를 df7에 저장 / data2를 df8에 저장/ df7를 sheet1에 저장/ df8를 sheet2에 저장
writer = pd.ExcelWriter("./df_excelwriter.xlsx")
df7.to_excel(writer, sheet_name="sheet1")
df8.to_excel(writer, sheet_name = "sheet2")
writer.save()
```
