# Pandas Groupby


## Introduction

In this lab, you'll learn how to use the `.groupby()` method in Pandas to summarize datasets.

## Objectives
You will be able to: 

- Use groupby methods to aggregate different groups in a dataframe


## Using `.groupby()` 

Let's bring in the Titantic data set.


```python
import pandas as pd

df = pd.read_csv('titanic.csv')
df = df.drop(columns=['Name','Ticket','Embarked', 'Cabin'])
df = df.dropna()
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>0.0</td>
      <td>3</td>
      <td>male</td>
      <td>22.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>7.2500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>1.0</td>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>71.2833</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>1.0</td>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>7.9250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>1.0</td>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>53.1000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>0.0</td>
      <td>3</td>
      <td>male</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>8.0500</td>
    </tr>
  </tbody>
</table>
</div>



During the Exploratory Data Analysis phase, one of the most common tasks you'll want to do is split the dataset into subgroups and compare them to see if you can notice any trends.  For instance, you may want to group the passengers together by gender or age. You can do this by using the `.groupby()` method built-in to pandas DataFrames. 

To group passengers by gender, you would type:


```python
df.groupby('Sex')
```




    <pandas.core.groupby.generic.DataFrameGroupBy object at 0x107e984c0>




```python
# This line of code is equivalent to the one above
df.groupby(df['Sex'])
```




    <pandas.core.groupby.generic.DataFrameGroupBy object at 0x122608160>



Note that this alone will not display a result -- although you have split the dataset into groups, you don't have a meaningful way to display information until you chain an **_Aggregation Function_** onto the groupby.  This allows you to compute summary statistics.

You can quickly use an aggregation function by chaining the call to the end of the `.groupby()` method.


```python
df.groupby('Sex').sum()
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Fare</th>
    </tr>
    <tr>
      <th>Sex</th>
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
      <th>female</th>
      <td>267590.0</td>
      <td>284.0</td>
      <td>131323132333?33322331222?2333231233333?2321333...</td>
      <td>12812.85</td>
      <td>838.0</td>
      <td>765.0</td>
      <td>19208.2047</td>
    </tr>
    <tr>
      <th>male</th>
      <td>384203.0</td>
      <td>191.0</td>
      <td>331333322111211?3313331333223332?3133331331121...</td>
      <td>23133.01</td>
      <td>997.0</td>
      <td>775.0</td>
      <td>21465.1410</td>
    </tr>
  </tbody>
</table>
</div>



You can use aggregation functions to quickly help us compare subsets of our data.  For example, the aggregate statistics displayed above allow you to quickly notice that there were more female survivors overall than male survivors.

## Aggregation functions


There are many built-in aggregate methods provided for you in the `pandas` package, and you can even write and apply your own. Some of the most common aggregate methods you may want to use are:

* `.min()`: returns the minimum value for each column by group  
* `.max()`: returns the maximum value for each column by group  
* `.mean()`: returns the average value for each column by group  
* `.median()`: returns the median value for each column by group  
* `.count()`: returns the count of each column by group


You can also see a list of all of the built-in aggregation methods by creating a grouped object and then using tab completion to inspect the available methods:


```python
grouped_df = df.groupby('Sex')
# For the following line of code, remove the `#` and then hit the tab after the period.
# grouped_df.<TAB>
```

This will display the following output:

```In [26]: grouped_df.<TAB>
gb.agg        gb.boxplot    gb.cummin     gb.describe   gb.filter     gb.get_group  gb.height     gb.last       gb.median     gb.ngroups    gb.plot       gb.rank       gb.std        gb.transform
gb.aggregate  gb.count      gb.cumprod    gb.dtype      gb.first      gb.groups     gb.hist       gb.max        gb.min        gb.nth        gb.prod       gb.resample   gb.sum        gb.var
gb.apply      gb.cummax     gb.cumsum     gb.fillna     gb.gender     gb.head       gb.indices    gb.mean       gb.name       gb.ohlc       gb.quantile   gb.size       gb.tail       gb.weight```
```

This is a comprehensive list of all built-in methods available to grouped objects. Note that some are aggregation methods, while others, such as `gb.fillna()`, allow us to fill missing values to individual groups independently.  

## Multiple groups

You can also split data into multiple different levels of groups by passing in an array containing the name of every column you want to group by -- for instance, by every combination of both `Sex` and `Pclass`.   


```python
df.groupby(['Sex', 'Pclass']).mean()
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Fare</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th>Pclass</th>
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
      <th rowspan="4" valign="top">female</th>
      <th>1</th>
      <td>594.965812</td>
      <td>0.811966</td>
      <td>34.098291</td>
      <td>1.521368</td>
      <td>1.538462</td>
      <td>84.552209</td>
    </tr>
    <tr>
      <th>2</th>
      <td>602.647059</td>
      <td>0.722689</td>
      <td>26.338992</td>
      <td>1.605042</td>
      <td>1.596639</td>
      <td>26.989777</td>
    </tr>
    <tr>
      <th>3</th>
      <td>550.912162</td>
      <td>0.466216</td>
      <td>25.677973</td>
      <td>1.858108</td>
      <td>1.810811</td>
      <td>21.144596</td>
    </tr>
    <tr>
      <th>?</th>
      <td>758.118644</td>
      <td>0.576271</td>
      <td>32.011356</td>
      <td>3.288136</td>
      <td>2.152542</td>
      <td>50.413771</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">male</th>
      <th>1</th>
      <td>601.886792</td>
      <td>0.415094</td>
      <td>38.287799</td>
      <td>1.440252</td>
      <td>1.490566</td>
      <td>56.046671</td>
    </tr>
    <tr>
      <th>2</th>
      <td>587.170068</td>
      <td>0.258503</td>
      <td>31.630340</td>
      <td>1.414966</td>
      <td>1.122449</td>
      <td>29.693905</td>
    </tr>
    <tr>
      <th>3</th>
      <td>377.919060</td>
      <td>0.151436</td>
      <td>25.757624</td>
      <td>0.973890</td>
      <td>0.506527</td>
      <td>15.446343</td>
    </tr>
    <tr>
      <th>?</th>
      <td>746.051948</td>
      <td>0.376623</td>
      <td>32.862597</td>
      <td>2.428571</td>
      <td>2.324675</td>
      <td>29.516452</td>
    </tr>
  </tbody>
</table>
</div>



## Selecting information from grouped objects

Since the resulting object returned is a DataFrame, you can also slice a selection of columns you're interested in from the DataFrame returned. 

The example below demonstrates the syntax for returning the mean of the `Survived` class for every combination of `Sex` and `Pclass`:


```python
df.groupby(['Sex', 'Pclass'])['Survived'].mean()
```




    Sex     Pclass
    female  1         0.811966
            2         0.722689
            3         0.466216
            ?         0.576271
    male    1         0.415094
            2         0.258503
            3         0.151436
            ?         0.376623
    Name: Survived, dtype: float64



The above example slices by column, but you can also slice by index. Take a look:


```python
grouped = df.groupby(['Sex', 'Pclass'])['Survived'].mean()
print(grouped['female'])
```

    Pclass
    1    0.811966
    2    0.722689
    3    0.466216
    ?    0.576271
    Name: Survived, dtype: float64



```python
print(grouped['female'][1])
```

    0.7226890756302521


Note that you need to provide only the value `female` as the index, and are returned all the groups where the passenger is female, regardless of the `Pclass` value. The second example shows the results for female passengers with a 1st-class ticket.

## Summary

In this lab, you learned about how to split a DataFrame into subgroups using the `.groupby()` method. You also learned to generate aggregate views of these groups by applying built-in methods to a groupby object.
