---
jupyter:
  colab:
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

<div class="cell markdown" id="9xZnRXM7x0Cv">

# CUHK-STAT1013: Practical Assignment Part 1: Sharing Your Idea and Data

</div>

<div class="cell markdown" id="xZ7MVo99SGtS">

## Dataset background

### Description:

Dataset describing the different averge living expenses of male and
female mainland students each month in CUHK.

It was collected by myself. The excel link:

'<https://docs.google.com/spreadsheets/d/e/2PACX-1vR05A1BrmTcqMbT8OJHsDIAkltBe8Yhu_i_15wRTmWdGCrz6Zxs60eNzesr748CzQ/pub?output=xlsx>'

Total sample size: 80 
size of each sample:40

Feature documentation: table of markdown

| Feature                      | Dtype  |
|:-----------------------------|:-------|
| Grade                        | int64  |
| Gender                       | object |
| Average living expense/month | int64  |
| Spend most on                | object |
| whether enough               | object |
| whether make extra fee in hk | object |

</div>

<div class="cell markdown" id="S_AP0zMXKIu-">

# Hypothesis

## 1. (2 points) Tell us what your idea is and why you have chosen to pursue this idea. 
Compare whether there is a difference in the monthly living expenses of different sexes of Mainland students coming to cuhk.Since there are differences in the amount of expenses incurred by university students of different genders, we are interested in the amount of monthly living expenses required between male and female cuhk
students.

## 2. (2 points) Carefully explain the following:

### 1. What two groups you are comparing Population:
A:all mainland boys'averge living expenses 
    B:all mainland girls'averge living expenses.

**They are independent!**

I intend to compare the average monthly living expenses of sample boys with the average monthly living expenses of sample girls.
**G1**:average monthly living expenses of boys;
**G2**: average monthly living expenses of girls

### 2. What you will be measuring (i.e., what your response variable willbe) 
What I want to measure is the amount of living expenses between the sample of male and female college students.

### 3. Is your response variable quantitative rather than categorical?
Obviously, the variable(the amount of living expenses) I want to measure is numeric data,they are all 'int'.

## 3. (2 points) Make a prediction about what kind of difference you expect to see between your samples and WHY. Note that when we gather data in statistics in order to compare samples, we often hypothesize that the groups will differ in some way. (You may have a good reason to believe that one group mean would be larger than the other vice versa. If not, you can simply hypothesize that two means are not the same.) 
My prediction is that the monthly living expenses of boys are different from the monthly living expenses of girls.The reason is that the types of items consumed by boys and girls are different from those consumed by girls, and there are differences in prices, and there are differences in consumption. We'd expect that **G2** =/ **G1**
Since:<https://mo.mbd.baidu.com/r/V2POCM79bG?f=cp&rs=1259102171&ruk=m3QQXqqZeCYI584izM5lYg&u=2eb122eef940fffa&urlext=%7B%22cuid%22%3A%220Pvlf_ua2i0ZuStQ0OSou_uY2il68Sa9la2ti_aIvaKu0qqSB%22%7D>

## 4. (2 points) Talk about how you will gather your data (e.g., will you go to certain websites to find your data, will you survey friends and classmates, will you to different stores to gather data, will you ignoresale prices and concentrate on price per ounce if you compare fooditems, etc.).
In order to obtain the required data, I will create a questionnaire and share it in the wechat group which contains all the mainland students in cuhk to obtain a total random sample.

## 5.If you have unlimited resources,how would you collect your data inQ4? 
I wil (i)enlarge my sample size to get more samples, (ii)investigate if the provided dataset is a good random sampling subset ofthe original Titanic population.

</div>

<div class="cell markdown" id="3GOdPWT03PQB">

## Prepare your dataset

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:202}"
id="sRkZzzHVklph" outputId="fe686191-781a-438e-c01e-c1d34bd57f52">

``` python
## load dataset from local machine
import pandas as pd

df = pd.read_excel(r'https://docs.google.com/spreadsheets/d/e/2PACX-1vR05A1BrmTcqMbT8OJHsDIAkltBe8Yhu_i_15wRTmWdGCrz6Zxs60eNzesr748CzQ/pub?output=xlsx')
df.head(5)
```

<div class="output execute_result" execution_count="1">

       Grade  Gender  Average living expense/month Spend most on whether enough  \
    0      1  female                          3000          food            yes   
    1      1  female                          5300          food            yes   
    2      4    male                          7000       average            yes   
    3      4    male                          7000       average            yes   
    4      4  female                          2000          food            yes   

      whether make extra fee in hk  
    0                           no  
    1                           no  
    2                           no  
    3                          yes  
    4                           no  

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="SWMOmfSqaXht" outputId="e0d0e6bb-6af6-4706-81dd-121b164bdf4b">

``` python
df.info()
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 80 entries, 0 to 79
    Data columns (total 6 columns):
     #   Column                        Non-Null Count  Dtype 
    ---  ------                        --------------  ----- 
     0   Grade                         80 non-null     int64 
     1   Gender                        80 non-null     object
     2   Average living expense/month  80 non-null     int64 
     3   Spend most on                 80 non-null     object
     4   whether enough                80 non-null     object
     5   whether make extra fee in hk  80 non-null     object
    dtypes: int64(2), object(4)
    memory usage: 3.9+ KB

</div>

</div>

<div class="cell markdown" id="_i8dPvN8RZrp">

What groups I want to compare: male and female. G1: average monthly living expenses of boys; G2: average monthly living expenses of girls.

**G1** ( Average living expense/month\| gender = male) vs. **G2**
(Average living expense/month \| gender = female)

**G1**(df\[df\['Gender'\] == 'male'\]\['Average living
expense/month'\])vs. **G2**(df\[df\['Gender'\] == 'female'\]\['Average
living expense/month'\])

</div>

<div class="cell markdown" id="13PdL3ht3902">

-   Print first 5 records of each group, respectively.

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="txGiNReNRvMz" outputId="cc28100d-bb35-4f45-e5c8-4e8371c723d2">

``` python
## First 5 records of G1 (male)
(df[df['Gender'] == 'male']['Average living expense/month']).head(5)
```

<div class="output execute_result" execution_count="47">

    2    7000
    3    7000
    5    2000
    6    6000
    9    6000
    Name: Average living expense/month, dtype: int64

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="VoALoCRcTEb3" outputId="34655fda-fc25-420d-dbbc-0f19f07cde07">

``` python
## First 5 records of G1 (female)
(df[df['Gender'] == 'female']['Average living expense/month']).head(5)
```

<div class="output execute_result" execution_count="48">

    0    3000
    1    5300
    4    2000
    7    3500
    8    3000
    Name: Average living expense/month, dtype: int64

</div>

</div>

<div class="cell markdown" id="WuOx-6g19_60">

### Any other data description and visualization you want to add.

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:233}"
id="QCL8F0Tea_2s" outputId="65031759-6d1d-422e-e48c-6ed3bf1efe29">

``` python
df.describe(include='all').T
```

<div class="output execute_result" execution_count="66">

                                 count unique     top freq    mean          std  \
    Grade                         80.0    NaN     NaN  NaN    1.75     1.108083   
    Gender                          80      2  female   40     NaN          NaN   
    Average living expense/month  80.0    NaN     NaN  NaN  5957.5  4388.297874   
    Spend most on                   80      4    food   51     NaN          NaN   
    whether enough                  80      2     yes   75     NaN          NaN   
    whether make extra fee in hk    80      2      no   67     NaN          NaN   

                                    min     25%     50%     75%      max  
    Grade                           1.0     1.0     1.0     2.0      4.0  
    Gender                          NaN     NaN     NaN     NaN      NaN  
    Average living expense/month  700.0  3450.0  5000.0  7000.0  25000.0  
    Spend most on                   NaN     NaN     NaN     NaN      NaN  
    whether enough                  NaN     NaN     NaN     NaN      NaN  
    whether make extra fee in hk    NaN     NaN     NaN     NaN      NaN  

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="2NPv771V-Fdt" outputId="1b0ea3d5-6e2f-42b4-9612-2111dd7a95d3">

``` python
# the mean/median of the whole sample
print('sample mean of Average living expense/month')
print(df['Average living expense/month'].mean())

print('sample median of Average living expense/month')
print(df['Average living expense/month'].median())
```

<div class="output stream stdout">

    sample mean of Average living expense/month
    5957.5
    sample median of Average living expense/month
    5000.0

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="U03AUgRCVdzG" outputId="569f9409-99c0-441b-cc9c-e1836014738d">

``` python
#the describle data of each group
print(df.groupby('Gender')['Average living expense/month'].agg(['min', 'max', 'median', 'mean', 'std']))
```

<div class="output stream stdout">

             min    max  median    mean          std
    Gender                                          
    female   700  20000  5000.0  5847.5  3999.486345
    male    2000  25000  5000.0  6067.5  4794.515430

</div>

</div>

<div class="cell code" id="gJG5VymIWh1V">

``` python
import matplotlib.pyplot as plt
import seaborn as sns
plt.rcParams['figure.figsize'] = [10, 5] 

sns.set()
```

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:341}"
id="9cNu6HR2_66E" outputId="958c6ed3-047c-4711-b4b8-c3f7a85c2eda">

``` python
sns.histplot(df, x='Average living expense/month')
plt.axvline(df['Average living expense/month'].mean(), linestyle='dashed', color='red')
plt.show()
```

<div class="output display_data">

![](02e0f07f65dd7bb453a0b18b0a5ff8bf9c4c94b8.png)

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:339}"
id="LiRg1OMUWq2n" outputId="7c1b3976-d037-4837-81c5-4fdc4598eded">

``` python
sns.histplot(df, x='Average living expense/month', hue='Gender')
plt.axvline(df['Average living expense/month'].mean(), linestyle='dashed', color='red')
plt.show()
```

<div class="output display_data">

![](4d218782744aca6634bf049a2c4de36946eef6c1.png)

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:339}"
id="CJ7Vu8LzDf-P" outputId="a6127b69-0be6-4d7f-ef97-61bf6a603f82">

``` python
sns.histplot(df, x='Average living expense/month', y='Gender')
plt.axvline(df['Average living expense/month'].mean(), linestyle='dashed', color='red')
plt.show()
```

<div class="output display_data">

![](0bb98ff340a7189396595113aeea55f96e8a1b08.png)

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:339}"
id="QdV1a5fTCuGT" outputId="6b7c4f55-1bf6-4e87-c118-643a1cf4d167">

``` python
sns.scatterplot(data=df, x="Gender", y='Average living expense/month')
plt.show()
```

<div class="output display_data">

![](f0378a5532e7e771ede5795176189036a52c7147.png)

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:661}"
id="6l-pYsYDYIUb" outputId="f7657a58-c768-4e0c-e89d-96c976dd2afe">

``` python
sns.stripplot(x=df['Average living expense/month'])#all groups
plt.show()
sns.stripplot(data=df, x="Average living expense/month", y="Gender")#each group
plt.show()
```

<div class="output display_data">

![](d7381d4d593091cd0a97c8a07489ab2857264f23.png)

</div>

<div class="output display_data">

![](5aa59ccbaaa35511efc305faab01d7214fed01c5.png)

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:661}"
id="wrVJB-8OYuGa" outputId="d754d368-a09c-4af2-9be9-e1a588e15586">

``` python
sns.boxplot(x=df["Average living expense/month"])
plt.show()
sns.boxplot(data=df, x="Average living expense/month", y="Gender")
plt.show()
```

<div class="output display_data">

![](e3033b965f800e5d6cfcc78207ab53d6f81b738f.png)

</div>

<div class="output display_data">

![](d3687983eb75383bfc73de045d216c5d81dc294d.png)

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:661}"
id="dSX211-uZOjs" outputId="9a6780cf-7827-4551-e6ab-b69b729472dd">

``` python
sns.violinplot(x=df["Average living expense/month"])
plt.show()
sns.violinplot(data=df, x="Average living expense/month",y='Gender')
plt.show()
```

<div class="output display_data">

![](b83bf9bcd72f810b406d79fe2b5534a881133ea5.png)

</div>

<div class="output display_data">

![](e5b5997abc1504fab8ced7c5320ecd45ecd3c954.png)

</div>

</div>