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

<div class="cell markdown" id="dBKp4LCwVegl">

**Description:**

Dataset describing the infection of new crown virus among the citizens
of different age group. Including the classification (Import case or
local case) ,Case status (Asymptomatic, confirmed, deleted, pending,
Repositive), Age group of the citizens and so on

Github: <http://www.chp.gov.hk/files/misc/enhanced_sur_covid_19_eng.csv>

Sample size: 15441

</div>

<div class="cell code" id="mQUd9AydVQy0">

``` python
```

</div>

<div class="cell markdown" id="RO6i1JQ4Vumq">

Tell us what your idea is and why you have chosen to pursue this idea.

**We are interested in "Is the older age group has a higher deathrate
than younger age group after infected Covid-19 ?"**

What two groups you are comparing:

**G1: Age group smaller or equal than 65 ; G2: Age group greater than
65**

What you will be measuring (i.e., what your response variables will be)

**Case status and age**

Make a prediction about what kind of difference you expect to see
between your samples and WHY.

**We'd expect that G1 \> G2.As the body of teenagers are usually
healthier**

Talk about how you will gather your data

**From Data.Gov.hk link:
<http://www.chp.gov.hk/files/misc/enhanced_sur_covid_19_eng.csv>**

If you had unlimited resources (time, money, staff, etc.) how would you
collect your data?

\*\*(i) I will try to collect data by Survey. as if i had unlimited
course, i will encourge people by prize after coducting suvrvey so that
i can enlarge sample size. When the sample size is greater, better and
accurate to estimate the result.

\(ii\) If i had more money, i will collect other data from other region
like Mainland china and so on. So that i can increase the sample
size.\*\*

</div>

<div class="cell code" id="RQpfjNwqFh6w">

``` python
import pandas as pd

df = pd.read_csv('enhanced_sur_covid_19_eng.csv')
```

</div>

<div class="cell code" id="faqzw1ZgMd9n">

``` python
```

</div>

<div class="cell markdown" id="CSYH-yB5F1L9">

G1 ( Deceased \| Age \<= 65) vs. G2 ( Deceased \| Age \>65 )

Print first 5 records of each group, respectively.

</div>

<div class="cell markdown" id="CsZo4giuHQhi">

If i only select the column that are age and
Hospitalised/Discharged/Deceased

then the result will be

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:206}"
id="jjGuwpLlKs1c" outputId="f395f3e4-aa55-48c8-b975-7fbaf40ccf2a">

``` python
df[['Hospitalised/Discharged/Deceased', 'Age']].head(5)
```

<div class="output execute_result" execution_count="69">

      Hospitalised/Discharged/Deceased Age
    0                       Discharged  39
    1                       Discharged  56
    2                       Discharged  62
    3                       Discharged  62
    4                       Discharged  63

</div>

</div>

<div class="cell markdown" id="G1v5gq3qK9ht">

</div>

<div class="cell markdown" id="irk7F_wjKwo3">

If i print first 5 information with all column , the the result will be

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:444}"
id="bEqMoa02FxJF" outputId="de7a5222-ee05-4b6d-a3b1-9ada4f0ac73f">

``` python
df[(df['Age'] > str(65)) & (df['Hospitalised/Discharged/Deceased'] == 'Deceased')].head(5)
```

<div class="output execute_result" execution_count="70">

          Case no. Report date Date of onset Gender Age  \
    54          55   14/2/2020      2/2/2020      M  70   
    88          89   26/2/2020     25/2/2020      M  80   
    98          99    1/3/2020     28/2/2020      F  76   
    594        595   29/3/2020     24/3/2020      F  75   
    1091      1092    2/6/2020      1/6/2020      F  78   

          Name of hospital admitted Hospitalised/Discharged/Deceased  \
    54                          NaN                         Deceased   
    88                          NaN                         Deceased   
    98                          NaN                         Deceased   
    594                         NaN                         Deceased   
    1091                        NaN                         Deceased   

         HK/Non-HK resident                                    Classification*  \
    54          HK resident                                Possibly local case   
    88          HK resident  Epidemiologically linked with possibly local case   
    98          HK resident                                         Local case   
    594         HK resident                                      Imported case   
    1091        HK resident           Epidemiologically linked with local case   

         Case status*  
    54      Confirmed  
    88      Confirmed  
    98      Confirmed  
    594     Confirmed  
    1091    Confirmed  

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:409}"
id="sz6UEVtMUWQ3" outputId="0c4477a6-c06b-4610-da17-6d1cb8a766e1">

``` python
df[(df['Age'] <= str(65)) & (df['Hospitalised/Discharged/Deceased'] == 'Deceased')].head(5)
```

<div class="output execute_result" execution_count="52">

          Case no. Report date Date of onset Gender Age  \
    12          13   31/1/2020     29/1/2020      M  39   
    1179      1180   24/6/2020     13/6/2020      M  55   
    1601      1602   16/7/2020     13/7/2020      F  64   
    1639      1640   16/7/2020  Asymptomatic      M  63   
    2479      2480   25/7/2020     21/7/2020      M  60   

          Name of hospital admitted Hospitalised/Discharged/Deceased  \
    12                          NaN                         Deceased   
    1179                        NaN                         Deceased   
    1601                        NaN                         Deceased   
    1639                        NaN                         Deceased   
    2479                        NaN                         Deceased   

         HK/Non-HK resident                           Classification* Case status*  
    12          HK resident                             Imported case    Confirmed  
    1179        HK resident                             Imported case    Confirmed  
    1601        HK resident  Epidemiologically linked with local case    Confirmed  
    1639        HK resident                                Local case    Confirmed  
    2479        HK resident                                Local case    Confirmed  

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:940}"
id="thBheZqXCKbR" outputId="1b5f687c-17e1-4547-c9b6-ded817cbc03d">

``` python
df.info()

print('conditional prob of People age 65 above | Deceased')

print(len(df[(df['Age'] > str(65)) & (df['Hospitalised/Discharged/Deceased'] == 'Deceased')])/len(df[df['Hospitalised/Discharged/Deceased'] == 'Deceased']))

print('conditional prob of People age 65 above | Deceased')

print(len(df[(df['Age'] <= str(65)) & (df['Hospitalised/Discharged/Deceased'] == 'Deceased')])/len(df[df['Hospitalised/Discharged/Deceased'] == 'Deceased']))

print('freq of who is age 65 above ')

print(len(df[df['Age'] > str(65)])/len(df))

df.describe(include='all').T

import matplotlib.pyplot as plt
import seaborn as sns
sns.histplot(df, x='Age')
plt.show()

sns.histplot(data=df, x="Age", y="Hospitalised/Discharged/Deceased")
plt.show()


##print('conditional mean of Deceased | Gender')
##print(df.groupby('Gender')['Deceased'].mean())
##print('sample median of Age')
##print(df['Age'].median())

```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 15441 entries, 0 to 15440
    Data columns (total 10 columns):
     #   Column                            Non-Null Count  Dtype  
    ---  ------                            --------------  -----  
     0   Case no.                          15441 non-null  int64  
     1   Report date                       15441 non-null  object 
     2   Date of onset                     15421 non-null  object 
     3   Gender                            15435 non-null  object 
     4   Age                               15435 non-null  object 
     5   Name of hospital admitted         0 non-null      float64
     6   Hospitalised/Discharged/Deceased  15435 non-null  object 
     7   HK/Non-HK resident                15435 non-null  object 
     8   Classification*                   15435 non-null  object 
     9   Case status*                      15441 non-null  object 
    dtypes: float64(1), int64(1), object(8)
    memory usage: 1.2+ MB
    conditional prob of People age 65 above | Deceased
    0.875
    conditional prob of People age 65 above | Deceased
    0.125
    freq of who is age 65 above 
    0.15374651900783629

</div>

<div class="output display_data">

![](706da836616cdf1f2d24d13e3fef83e3f156f9f0.png)

</div>

<div class="output display_data">

![](7db3c3f1dc28fa5fec2b6be95a394b5f43d2cd5f.png)

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:295}"
id="ufc9WI3PRSSU" outputId="0ce8f237-afa3-441a-8c7f-c65e4983a670">

``` python
#if ('Hospitalised/Discharged/Deceased'=='Discharged'and 'Case status'=='Confirmed'):
#print('get well soon')

print('sample mean of age')
df['Age'] = df['Age'].astype(int)
print(df['Age'].mean()).astype(int)
```

<div class="output stream stdout">

    sample mean of age

</div>

<div class="output error" ename="ValueError" evalue="ignored">

    ---------------------------------------------------------------------------
    ValueError                                Traceback (most recent call last)
    <ipython-input-14-450a9eb01534> in <module>
          3 
          4 print('sample mean of age')
    ----> 5 df['Age'] = df['Age'].astype(int)
          6 print(df['Age'].mean()).astype(int)

    /usr/local/lib/python3.8/dist-packages/pandas/core/generic.py in astype(self, dtype, copy, errors)
       5813         else:
       5814             # else, only a single dtype is given
    -> 5815             new_data = self._mgr.astype(dtype=dtype, copy=copy, errors=errors)
       5816             return self._constructor(new_data).__finalize__(self, method="astype")
       5817 

    /usr/local/lib/python3.8/dist-packages/pandas/core/internals/managers.py in astype(self, dtype, copy, errors)
        416 
        417     def astype(self: T, dtype, copy: bool = False, errors: str = "raise") -> T:
    --> 418         return self.apply("astype", dtype=dtype, copy=copy, errors=errors)
        419 
        420     def convert(

    /usr/local/lib/python3.8/dist-packages/pandas/core/internals/managers.py in apply(self, f, align_keys, ignore_failures, **kwargs)
        325                     applied = b.apply(f, **kwargs)
        326                 else:
    --> 327                     applied = getattr(b, f)(**kwargs)
        328             except (TypeError, NotImplementedError):
        329                 if not ignore_failures:

    /usr/local/lib/python3.8/dist-packages/pandas/core/internals/blocks.py in astype(self, dtype, copy, errors)
        589         values = self.values
        590 
    --> 591         new_values = astype_array_safe(values, dtype, copy=copy, errors=errors)
        592 
        593         new_values = maybe_coerce_values(new_values)

    /usr/local/lib/python3.8/dist-packages/pandas/core/dtypes/cast.py in astype_array_safe(values, dtype, copy, errors)
       1307 
       1308     try:
    -> 1309         new_values = astype_array(values, dtype, copy=copy)
       1310     except (ValueError, TypeError):
       1311         # e.g. astype_nansafe can fail on object-dtype of strings

    /usr/local/lib/python3.8/dist-packages/pandas/core/dtypes/cast.py in astype_array(values, dtype, copy)
       1255 
       1256     else:
    -> 1257         values = astype_nansafe(values, dtype, copy=copy)
       1258 
       1259     # in pandas we don't store numpy str dtypes, so convert to object

    /usr/local/lib/python3.8/dist-packages/pandas/core/dtypes/cast.py in astype_nansafe(arr, dtype, copy, skipna)
       1172         # work around NumPy brokenness, #1987
       1173         if np.issubdtype(dtype.type, np.integer):
    -> 1174             return lib.astype_intsafe(arr, dtype)
       1175 
       1176         # if we have a datetime/timedelta array of objects

    /usr/local/lib/python3.8/dist-packages/pandas/_libs/lib.pyx in pandas._libs.lib.astype_intsafe()

    ValueError: invalid literal for int() with base 10: '<1'

</div>

</div>
