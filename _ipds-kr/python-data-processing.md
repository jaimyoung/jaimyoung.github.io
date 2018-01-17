---
layout: page
title: 따라 하며 배우는 데이터 과학 - 파이썬 편 2 - 데이터 취득과 가공
date: 2018-01-15
comments: true
---
- TOC
{:toc}
본 장에서는 ["따라 하며 배우는 데이터 과학"](https://dataninja.me/ipds-kr/) 3장의 
"데이터 취득과 데이터 가공: SQL과 dplyr" 내용을 파이썬으로
익혀보도록 하자.

주피터 노트북 버전은 다음 페이지에 있다:
<http://nbviewer.jupyter.org/github/jaimyoung/ipds-kr/blob/master/notebooks/python-data-processing.ipynb>


```python
%matplotlib inline
import pandas as pd
import numpy as np
```

# 1. gapminder 자료 읽어들이기


```python
# gapminder 자료를 다운로드하고 판다스 데이터프레임으로 읽어들이자
gapminder = pd.read_csv("data/gapminder.tsv", sep="\t")
# This also works:
# gapminder = pd.read_csv("https://raw.githubusercontent.com/jennybc/gapminder/master/data-raw/07_gap-merged-with-continent.tsv", sep="\t")
```


```python
gapminder.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>continent</th>
      <th>year</th>
      <th>lifeExp</th>
      <th>pop</th>
      <th>gdpPercap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1952</td>
      <td>28.801</td>
      <td>8425333</td>
      <td>779.445314</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1957</td>
      <td>30.332</td>
      <td>9240934</td>
      <td>820.853030</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1962</td>
      <td>31.997</td>
      <td>10267083</td>
      <td>853.100710</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1967</td>
      <td>34.020</td>
      <td>11537966</td>
      <td>836.197138</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1972</td>
      <td>36.088</td>
      <td>13079460</td>
      <td>739.981106</td>
    </tr>
  </tbody>
</table>
</div>




```python
gapminder.tail()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>continent</th>
      <th>year</th>
      <th>lifeExp</th>
      <th>pop</th>
      <th>gdpPercap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3308</th>
      <td>Zimbabwe</td>
      <td>Africa</td>
      <td>1987</td>
      <td>62.351</td>
      <td>9216418</td>
      <td>706.157306</td>
    </tr>
    <tr>
      <th>3309</th>
      <td>Zimbabwe</td>
      <td>Africa</td>
      <td>1992</td>
      <td>60.377</td>
      <td>10704340</td>
      <td>693.420786</td>
    </tr>
    <tr>
      <th>3310</th>
      <td>Zimbabwe</td>
      <td>Africa</td>
      <td>1997</td>
      <td>46.809</td>
      <td>11404948</td>
      <td>792.449960</td>
    </tr>
    <tr>
      <th>3311</th>
      <td>Zimbabwe</td>
      <td>Africa</td>
      <td>2002</td>
      <td>39.989</td>
      <td>11926563</td>
      <td>672.038623</td>
    </tr>
    <tr>
      <th>3312</th>
      <td>Zimbabwe</td>
      <td>Africa</td>
      <td>2007</td>
      <td>43.487</td>
      <td>12311143</td>
      <td>469.709298</td>
    </tr>
  </tbody>
</table>
</div>




```python
gapminder.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 3313 entries, 0 to 3312
    Data columns (total 6 columns):
    country      3313 non-null object
    continent    3313 non-null object
    year         3313 non-null int64
    lifeExp      3313 non-null float64
    pop          3313 non-null int64
    gdpPercap    3313 non-null float64
    dtypes: float64(2), int64(2), object(2)
    memory usage: 155.4+ KB



```python
gapminder.describe()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>lifeExp</th>
      <th>pop</th>
      <th>gdpPercap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>3313.000000</td>
      <td>3313.000000</td>
      <td>3.313000e+03</td>
      <td>3313.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1980.293088</td>
      <td>65.240457</td>
      <td>3.177325e+07</td>
      <td>11313.820704</td>
    </tr>
    <tr>
      <th>std</th>
      <td>16.931879</td>
      <td>11.772424</td>
      <td>1.045019e+08</td>
      <td>11369.008362</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1950.000000</td>
      <td>23.599000</td>
      <td>5.941200e+04</td>
      <td>241.165877</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1967.000000</td>
      <td>58.333000</td>
      <td>2.680018e+06</td>
      <td>2505.291423</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1982.000000</td>
      <td>69.610000</td>
      <td>7.559776e+06</td>
      <td>7825.823398</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1996.000000</td>
      <td>73.657000</td>
      <td>1.961054e+07</td>
      <td>17355.747100</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2007.000000</td>
      <td>82.670000</td>
      <td>1.318683e+09</td>
      <td>113523.132900</td>
    </tr>
  </tbody>
</table>
</div>



# 데이터를 처리하는 핵심 동사


## 1. 행을 선택하기


```python
# gapminder 데이터에서 한국 데이터, 2007년 데이터, 한국 2007년 데이터를 추출하는 명령은 다음과 같다.
# R dplyr 에서는 filter(gapminder, country=='Korea, Rep.' & year==2007)
gapminder.query("country=='Korea, Rep.' & year==2007")
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>continent</th>
      <th>year</th>
      <th>lifeExp</th>
      <th>pop</th>
      <th>gdpPercap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1651</th>
      <td>Korea, Rep.</td>
      <td>Asia</td>
      <td>2007</td>
      <td>78.623</td>
      <td>49044790</td>
      <td>23348.13973</td>
    </tr>
  </tbody>
</table>
</div>



## 2. 행(관측치)를 정렬하기


```python
#  gapminder 데이터를 year, country 변수순으로 정렬하려면,
# R dplyr 에서는 gapminder %>% arrange(year, country)
gapminder.sort_values(by=["year", "country"]).head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>continent</th>
      <th>year</th>
      <th>lifeExp</th>
      <th>pop</th>
      <th>gdpPercap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>72</th>
      <td>Australia</td>
      <td>Oceania</td>
      <td>1950</td>
      <td>69.020</td>
      <td>8267337</td>
      <td>10031.121380</td>
    </tr>
    <tr>
      <th>128</th>
      <td>Austria</td>
      <td>Europe</td>
      <td>1950</td>
      <td>64.880</td>
      <td>6935100</td>
      <td>5733.098114</td>
    </tr>
    <tr>
      <th>251</th>
      <td>Belgium</td>
      <td>Europe</td>
      <td>1950</td>
      <td>66.350</td>
      <td>8639369</td>
      <td>7990.465840</td>
    </tr>
    <tr>
      <th>308</th>
      <td>Belize</td>
      <td>Americas</td>
      <td>1950</td>
      <td>57.673</td>
      <td>65797</td>
      <td>1731.132728</td>
    </tr>
    <tr>
      <th>395</th>
      <td>Bulgaria</td>
      <td>Europe</td>
      <td>1950</td>
      <td>61.390</td>
      <td>7250500</td>
      <td>2131.563149</td>
    </tr>
  </tbody>
</table>
</div>



## 3. 열(변수)를 선택하기


```python
#  gapminder 데이터에서 pop, gdpPercap 변수만 선택.
# R dplyr 에서는 gapminder %>% select(pop, gdpPercap)
gapminder[["pop", "gdpPercap"]].head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pop</th>
      <th>gdpPercap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8425333</td>
      <td>779.445314</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9240934</td>
      <td>820.853030</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10267083</td>
      <td>853.100710</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11537966</td>
      <td>836.197138</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13079460</td>
      <td>739.981106</td>
    </tr>
  </tbody>
</table>
</div>



## 4. 변수 변환하기


```python
#  gapminder 데이터에서 기존의 변수들을 변환한 결과를 기존 변수나 새 변수에 할당한다. 
# R dplyr 에서는 
# gapminder %>%
#    mutate(total_gdp = pop * gdpPercap,
#    le_gdp_ratio = lifeExp / gdpPercap, lgrk = le_gdp_ratio * 100)
# 1. 파이썬에서는 각 변수 할당에 새로운 assign() 함수를 사용해야 한다.
# 2. x.pop 은 내부의 pop() 함수와 충돌을 일으키므로 x['pop']으로 표현했다.
gapminder.\
    assign(total_gdp = lambda x: (x['pop'] * x['gdpPercap'])).\
    assign(le_gdp_ratio = lambda x: (x['lifeExp'] / x['gdpPercap'])).\
    assign(lgrk = lambda x: x['le_gdp_ratio'] * 100).\
    head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>continent</th>
      <th>year</th>
      <th>lifeExp</th>
      <th>pop</th>
      <th>gdpPercap</th>
      <th>total_gdp</th>
      <th>le_gdp_ratio</th>
      <th>lgrk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1952</td>
      <td>28.801</td>
      <td>8425333</td>
      <td>779.445314</td>
      <td>6.567086e+09</td>
      <td>0.036951</td>
      <td>3.695064</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1957</td>
      <td>30.332</td>
      <td>9240934</td>
      <td>820.853030</td>
      <td>7.585449e+09</td>
      <td>0.036952</td>
      <td>3.695180</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1962</td>
      <td>31.997</td>
      <td>10267083</td>
      <td>853.100710</td>
      <td>8.758856e+09</td>
      <td>0.037507</td>
      <td>3.750671</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1967</td>
      <td>34.020</td>
      <td>11537966</td>
      <td>836.197138</td>
      <td>9.648014e+09</td>
      <td>0.040684</td>
      <td>4.068419</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1972</td>
      <td>36.088</td>
      <td>13079460</td>
      <td>739.981106</td>
      <td>9.678553e+09</td>
      <td>0.048769</td>
      <td>4.876881</td>
    </tr>
  </tbody>
</table>
</div>



## 5. 요약 통계량 계산하기


```python
#  gapminder 데이터에서 기존의 변수들을 변환한 결과를 기존 변수나 새 변수에 할당한다. 
# R dplyr 에서는 
# gapminder %>% summarize(n_obs = n( ),
#   n_countries = n_distinct(country),
#   n_years = n_distinct(year),
#   med_gdpc = median(gdpPercap),
#   max_gdppc = max(gdpPercap))
gapminder.aggregate(['mean', 'median'])
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>lifeExp</th>
      <th>pop</th>
      <th>gdpPercap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mean</th>
      <td>1980.293088</td>
      <td>65.240457</td>
      <td>3.177325e+07</td>
      <td>11313.820704</td>
    </tr>
    <tr>
      <th>median</th>
      <td>1982.000000</td>
      <td>69.610000</td>
      <td>7.559776e+06</td>
      <td>7825.823398</td>
    </tr>
  </tbody>
</table>
</div>



## 6. 랜덤 샘플을 위한 sample()


```python
np.random.seed(12345)
gapminder.sample(n=10)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>continent</th>
      <th>year</th>
      <th>lifeExp</th>
      <th>pop</th>
      <th>gdpPercap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>808</th>
      <td>Denmark</td>
      <td>Europe</td>
      <td>1954</td>
      <td>71.350</td>
      <td>4406000</td>
      <td>10272.200280</td>
    </tr>
    <tr>
      <th>2738</th>
      <td>Spain</td>
      <td>Europe</td>
      <td>1962</td>
      <td>69.690</td>
      <td>31158061</td>
      <td>5693.843879</td>
    </tr>
    <tr>
      <th>3174</th>
      <td>United States</td>
      <td>Americas</td>
      <td>1963</td>
      <td>70.040</td>
      <td>189242000</td>
      <td>16646.257900</td>
    </tr>
    <tr>
      <th>593</th>
      <td>Chile</td>
      <td>Americas</td>
      <td>1957</td>
      <td>56.074</td>
      <td>7048426</td>
      <td>4315.622723</td>
    </tr>
    <tr>
      <th>1662</th>
      <td>Kuwait</td>
      <td>Asia</td>
      <td>2002</td>
      <td>76.904</td>
      <td>2111561</td>
      <td>35110.105660</td>
    </tr>
    <tr>
      <th>3113</th>
      <td>Uganda</td>
      <td>Africa</td>
      <td>1977</td>
      <td>50.350</td>
      <td>11457758</td>
      <td>843.733137</td>
    </tr>
    <tr>
      <th>314</th>
      <td>Belize</td>
      <td>Americas</td>
      <td>1987</td>
      <td>71.879</td>
      <td>176347</td>
      <td>3844.931896</td>
    </tr>
    <tr>
      <th>1488</th>
      <td>Italy</td>
      <td>Europe</td>
      <td>1964</td>
      <td>70.400</td>
      <td>51600200</td>
      <td>8821.596841</td>
    </tr>
    <tr>
      <th>300</th>
      <td>Belgium</td>
      <td>Europe</td>
      <td>1999</td>
      <td>77.800</td>
      <td>10235655</td>
      <td>28937.151400</td>
    </tr>
    <tr>
      <th>854</th>
      <td>Denmark</td>
      <td>Europe</td>
      <td>2000</td>
      <td>76.900</td>
      <td>5337416</td>
      <td>32016.753010</td>
    </tr>
  </tbody>
</table>
</div>




```python
gapminder.sample(frac=.01).shape
```




    (33, 6)



## 7. 고유한 행을 찾아내는 distinct( )


```python
# R dplyr 는
# gapminder %>% select(country) %>% distinct()
# gapminder %>% select(year) %>% distinct()

gapminder.country.unique(), gapminder.year.unique()
```




    (array(['Afghanistan', 'Albania', 'Algeria', 'Angola', 'Argentina',
            'Armenia', 'Aruba', 'Australia', 'Austria', 'Azerbaijan', 'Bahamas',
            'Bahrain', 'Bangladesh', 'Barbados', 'Belarus', 'Belgium', 'Belize',
            'Benin', 'Bhutan', 'Bolivia', 'Bosnia and Herzegovina', 'Botswana',
            'Brazil', 'Brunei', 'Bulgaria', 'Burkina Faso', 'Burundi',
            'Cambodia', 'Cameroon', 'Canada', 'Cape Verde',
            'Central African Republic', 'Chad', 'Chile', 'China', 'Colombia',
            'Comoros', 'Congo, Dem. Rep.', 'Congo, Rep.', 'Costa Rica',
            "Cote d'Ivoire", 'Croatia', 'Cuba', 'Cyprus', 'Czech Republic',
            'Denmark', 'Djibouti', 'Dominican Republic', 'Ecuador', 'Egypt',
            'El Salvador', 'Equatorial Guinea', 'Eritrea', 'Estonia',
            'Ethiopia', 'Fiji', 'Finland', 'France', 'French Guiana',
            'French Polynesia', 'Gabon', 'Gambia', 'Georgia', 'Germany',
            'Ghana', 'Greece', 'Grenada', 'Guadeloupe', 'Guatemala', 'Guinea',
            'Guinea-Bissau', 'Guyana', 'Haiti', 'Honduras', 'Hong Kong, China',
            'Hungary', 'Iceland', 'India', 'Indonesia', 'Iran', 'Iraq',
            'Ireland', 'Israel', 'Italy', 'Jamaica', 'Japan', 'Jordan',
            'Kazakhstan', 'Kenya', 'Korea, Dem. Rep.', 'Korea, Rep.', 'Kuwait',
            'Latvia', 'Lebanon', 'Lesotho', 'Liberia', 'Libya', 'Lithuania',
            'Luxembourg', 'Macao, China', 'Madagascar', 'Malawi', 'Malaysia',
            'Maldives', 'Mali', 'Malta', 'Martinique', 'Mauritania',
            'Mauritius', 'Mexico', 'Micronesia, Fed. Sts.', 'Moldova',
            'Mongolia', 'Montenegro', 'Morocco', 'Mozambique', 'Myanmar',
            'Namibia', 'Nepal', 'Netherlands', 'Netherlands Antilles',
            'New Caledonia', 'New Zealand', 'Nicaragua', 'Niger', 'Nigeria',
            'Norway', 'Oman', 'Pakistan', 'Panama', 'Papua New Guinea',
            'Paraguay', 'Peru', 'Philippines', 'Poland', 'Portugal',
            'Puerto Rico', 'Qatar', 'Reunion', 'Romania', 'Russia', 'Rwanda',
            'Samoa', 'Sao Tome and Principe', 'Saudi Arabia', 'Senegal',
            'Serbia', 'Sierra Leone', 'Singapore', 'Slovak Republic',
            'Slovenia', 'Solomon Islands', 'Somalia', 'South Africa', 'Spain',
            'Sri Lanka', 'Sudan', 'Suriname', 'Swaziland', 'Sweden',
            'Switzerland', 'Syria', 'Taiwan', 'Tajikistan', 'Tanzania',
            'Thailand', 'Timor-Leste', 'Togo', 'Tonga', 'Trinidad and Tobago',
            'Tunisia', 'Turkey', 'Turkmenistan', 'Uganda', 'Ukraine',
            'United Arab Emirates', 'United Kingdom', 'United States',
            'Uruguay', 'Uzbekistan', 'Vanuatu', 'Venezuela', 'Vietnam',
            'West Bank and Gaza', 'Yemen, Rep.', 'Zambia', 'Zimbabwe'], dtype=object),
     array([1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997, 2002,
            2007, 1950, 1951, 1953, 1954, 1955, 1956, 1958, 1959, 1960, 1961,
            1963, 1964, 1965, 1966, 1968, 1969, 1970, 1971, 1973, 1974, 1975,
            1976, 1978, 1979, 1980, 1981, 1983, 1984, 1985, 1986, 1988, 1989,
            1990, 1991, 1993, 1994, 1995, 1996, 1998, 1999, 2000, 2001, 2003,
            2004, 2005, 2006]))




```python
gapminder.drop_duplicates(['country', 'year']).head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>continent</th>
      <th>year</th>
      <th>lifeExp</th>
      <th>pop</th>
      <th>gdpPercap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1952</td>
      <td>28.801</td>
      <td>8425333</td>
      <td>779.445314</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1957</td>
      <td>30.332</td>
      <td>9240934</td>
      <td>820.853030</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1962</td>
      <td>31.997</td>
      <td>10267083</td>
      <td>853.100710</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1967</td>
      <td>34.020</td>
      <td>11537966</td>
      <td>836.197138</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>1972</td>
      <td>36.088</td>
      <td>13079460</td>
      <td>739.981106</td>
    </tr>
  </tbody>
</table>
</div>



# group_by() 를 이용한 그룹 연산


```python
# R dplyr 는
# gapminder %>%
# filter(year == 2007) %>% 
# group_by(continent) %>% 
# summarize(median(lifeExp))

gapminder.\
    query('year == 2007').\
    groupby('continent').\
    agg({'lifeExp':'median'})
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>lifeExp</th>
    </tr>
    <tr>
      <th>continent</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Africa</th>
      <td>52.9470</td>
    </tr>
    <tr>
      <th>Americas</th>
      <td>73.4950</td>
    </tr>
    <tr>
      <th>Asia</th>
      <td>71.9930</td>
    </tr>
    <tr>
      <th>Europe</th>
      <td>78.6085</td>
    </tr>
    <tr>
      <th>FSU</th>
      <td>69.0270</td>
    </tr>
    <tr>
      <th>Oceania</th>
      <td>71.4540</td>
    </tr>
  </tbody>
</table>
</div>



## 조인 연산자;  inner, left, right, full(outer) join
R dplyr 예는 다음과 같다.
```
(df1 <- data_frame(x = c(1, 2), y = 2:1))
(df2 <- data_frame(x = c(1, 3), a = 10, b = "a"))
df1 %>% inner_join(df2)
df1 %>% left_join(df2)
df1 %>% right_join(df2)
df1 %>% full_join(df2)
```
파이썬 판다스에서는 `DataFrame.merge` 함수로 처리하면 된다.


```python
df1 = pd.DataFrame(data={'x':range(2), 'y':range(2, 0, -1)})
df1
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = pd.DataFrame(data={'x':[1,3], 'a':10, 'b':"a"})
df2
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>x</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>a</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10</td>
      <td>a</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.merge(df2, how="inner")
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>10</td>
      <td>a</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.merge(df2, how="left")
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>10.0</td>
      <td>a</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.merge(df2, how="inner")
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>10</td>
      <td>a</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.merge(df2, how="right")
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1.0</td>
      <td>10</td>
      <td>a</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>NaN</td>
      <td>10</td>
      <td>a</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.merge(df2, how="outer")
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1.0</td>
      <td>10.0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>NaN</td>
      <td>10.0</td>
      <td>a</td>
    </tr>
  </tbody>
</table>
</div>


