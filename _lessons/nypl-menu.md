---
layout: page
title: Crowdsourced-Data Normalization with Python and Pandas
description: This lesson uses pandas to normalize a large datasett
---
## Source
[Halle Burns, "Crowdsourced-Data Normalization with Python and Pandas"](https://programminghistorian.org/en/lessons/crowdsourced-data-normalization-with-pandas#removing-columns)

## Reflection
The pandas library introduces many incentivizing methods for data manipulation. It is able to easily parse data from .csv files and apply methods on the data. In this lesson, the library was used to print the data from the file, remove duplicate data, and remove data based on the values of certain entries. The lesson also introduced a method to reformat date/time data from human format to a standardized computer science format. 

The tools introduced in this lesson seem widely applicable across projects and data sets. While this lesson focused on the use of these methods in crowdsourced-data environments, the methods can easily be used for any project with large amounts of data. As an example, if a DH project combines multiple datasets, we could use the methods described in this lesson to remove duplicate data if the datasets have overlapping information. Another method that I believe would be useful across multiple projects is the ability to remove data with missing entries. For example, if a project is tracking human immigration patterns but certain points of data do not have entries for destinations, these points might not be useful in visualizing trends. It is a valuable tool to be able to disregard data based on aspects of the data, which is made simple by using pandas.



```python
import pandas as pd
```


```python
#Read in data
df = pd.read_csv("Menu.csv")
print(df.head())
print(df.columns)
```


```python
# Remove columns
dropped_col = ['notes', 'call_number', 'currency', 'currency_symbol', 'physical_description', 'status']
df.drop(dropped_col, inplace=True, axis=1)

print(df.shape)
```

    (17546, 14)



```python
# Duplicate rows
print(df[df.duplicated(keep=False)])

```


```python
df.drop_duplicates(inplace=True)

print(df.shape)
print(df.isnull().sum())
```


```python
# Missing Data
# remove columns with more than 25% missing data
menu = df.dropna(thresh=df.shape[0]*0.25,how='all',axis=1)
print(menu.shape)
print(menu.columns)
```


```python
# remove rows with missing data
dropped_na = menu.dropna()
print(dropped_na)
```


```python
# DateTime formatting

#pd.to_datetime(dropped_na['date'], dayfirst = False, yearfirst = False)

replaced_dates = dropped_na.replace('0190-03-06', '12-31-2200')

replaced_dates.to_csv("NYPL_NormalMenus.csv")
```
