---
layout: page
title: Crowdsourced-Data Normalization with Python and Pandas
description: This lesson uses the pandas library to manipulate the data from a crowd-sourced dataset.
---
## Source
[Halle Burns, "Crowdsourced-Data Normalization with Python and Pandas"](https://programminghistorian.org/en/lessons/crowdsourced-data-normalization-with-pandas#removing-columns)

## Reflection
The pandas library introduces many incentivizing methods for data manipulation. It is able to easily parse data from .csv files and apply methods on the data. In this lesson, the library was used to print the data from the file, remove duplicate data, and remove data based on the values of certain entries. The lesson also introduced a method to reformat date/time data from human format to a standardized computer science format. 

The tools introduced in this lesson seem widely applicable across projects and data sets. While this lesson focused on the use of these methods in crowdsourced-data environments, the methods can easily be used for any project with large amounts of data. As an example, if a DH project combines multiple datasets, we could use the methods described in this lesson to remove duplicate data if the datasets have overlapping information. Another method that I believe would be useful across multiple projects is the ability to remove data with missing entries. For example, if a project is tracking human immigration patterns but certain points of data do not have entries for destinations, these points might not be useful in visualizing trends. It is a valuable tool to be able to disregard data based on aspects of the data, which is made simple by using pandas.

## Code

```python
import pandas as pd
```


```python
#Read in data
df = pd.read_csv("Menu.csv")
print(df.head())
print(df.columns)
```

          id name                     sponsor                 event       venue  \
    0  12463  NaN               HOTEL EASTMAN             BREAKFAST  COMMERCIAL   
    1  12464  NaN            REPUBLICAN HOUSE              [DINNER]  COMMERCIAL   
    2  12465  NaN  NORDDEUTSCHER LLOYD BREMEN  FRUHSTUCK/BREAKFAST;  COMMERCIAL   
    3  12466  NaN  NORDDEUTSCHER LLOYD BREMEN                LUNCH;  COMMERCIAL   
    4  12467  NaN  NORDDEUTSCHER LLOYD BREMEN               DINNER;  COMMERCIAL   
    
                                    place         physical_description occasion  \
    0                     HOT SPRINGS, AR              CARD; 4.75X7.5;  EASTER;   
    1                    MILWAUKEE, [WI];   CARD; ILLUS; COL; 7.0X9.0;  EASTER;   
    2  DAMPFER KAISER WILHELM DER GROSSE;    CARD; ILLU; COL; 5.5X8.0;      NaN   
    3  DAMPFER KAISER WILHELM DER GROSSE;    CARD; ILLU; COL; 5.5X8.0;      NaN   
    4  DAMPFER KAISER WILHELM DER GROSSE;  FOLDER; ILLU; COL; 5.5X7.5;      NaN   
    
                                                   notes call_number  keywords  \
    0                                                NaN   1900-2822       NaN   
    1  WEDGEWOOD BLUE CARD; WHITE EMBOSSED GREEK KEY ...   1900-2825       NaN   
    2  MENU IN GERMAN AND ENGLISH; ILLUS, STEAMSHIP A...   1900-2827       NaN   
    3  MENU IN GERMAN AND ENGLISH; ILLUS, HARBOR SCEN...   1900-2828       NaN   
    4  MENU IN GERMAN AND ENGLISH; ILLUS, HARBOR SCEN...   1900-2829       NaN   
    
       language       date                    location  location_type currency  \
    0       NaN  4/15/1900               Hotel Eastman            NaN      NaN   
    1       NaN  4/15/1900            Republican House            NaN      NaN   
    2       NaN  4/16/1900  Norddeutscher Lloyd Bremen            NaN      NaN   
    3       NaN  4/16/1900  Norddeutscher Lloyd Bremen            NaN      NaN   
    4       NaN  4/16/1900  Norddeutscher Lloyd Bremen            NaN      NaN   
    
      currency_symbol    status  page_count  dish_count  
    0             NaN  complete           2          67  
    1             NaN  complete           2          34  
    2             NaN  complete           2          84  
    3             NaN  complete           2          63  
    4             NaN  complete           4          33  
    Index(['id', 'name', 'sponsor', 'event', 'venue', 'place',
           'physical_description', 'occasion', 'notes', 'call_number', 'keywords',
           'language', 'date', 'location', 'location_type', 'currency',
           'currency_symbol', 'status', 'page_count', 'dish_count'],
          dtype='object')



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

              id name        sponsor      event       venue            place  \
    0      12463  NaN  HOTEL EASTMAN  BREAKFAST  COMMERCIAL  HOT SPRINGS, AR   
    17545  12463  NaN  HOTEL EASTMAN  BREAKFAST  COMMERCIAL  HOT SPRINGS, AR   
    
          occasion  keywords  language       date       location  location_type  \
    0      EASTER;       NaN       NaN  4/15/1900  Hotel Eastman            NaN   
    17545  EASTER;       NaN       NaN  4/15/1900  Hotel Eastman            NaN   
    
           page_count  dish_count  
    0               2          67  
    17545           2          67  



```python
df.drop_duplicates(inplace=True)

print(df.shape)
print(df.isnull().sum())
```

    (17545, 14)
    id                   0
    name             14348
    sponsor           1561
    event             9391
    venue             9426
    place             9422
    occasion         13754
    keywords         17545
    language         17545
    date               586
    location             0
    location_type    17545
    page_count           0
    dish_count           0
    dtype: int64



```python
# Missing Data
# remove columns with more than 25% missing data
menu = df.dropna(thresh=df.shape[0]*0.25,how='all',axis=1)
print(menu.shape)
print(menu.columns)
```

    (17545, 9)
    Index(['id', 'sponsor', 'event', 'venue', 'place', 'date', 'location',
           'page_count', 'dish_count'],
          dtype='object')



```python
# remove rows with missing data
dropped_na = menu.dropna()
print(dropped_na)
```

              id                                            sponsor  \
    0      12463                                      HOTEL EASTMAN   
    1      12464                                   REPUBLICAN HOUSE   
    2      12465                         NORDDEUTSCHER LLOYD BREMEN   
    3      12466                         NORDDEUTSCHER LLOYD BREMEN   
    4      12467                         NORDDEUTSCHER LLOYD BREMEN   
    ...      ...                                                ...   
    10212  27695  CONFRERIE DE LA CHAINE DES ROTISSEURS, NEW ORL...   
    10213  27696  CONFRERIE DE LA CHAINE DES ROTISSEURS, GEORGIA...   
    10214  27697                                  FRANKFURTER STUBB   
    10215  27698                             HOTEL EUROPAISCHER HOF   
    10216  27699  CONFRERIE DE LA CHAINE DES ROTISSEURS, OKLAHOM...   
    
                                          event                 venue  \
    0                                 BREAKFAST            COMMERCIAL   
    1                                  [DINNER]            COMMERCIAL   
    2                      FRUHSTUCK/BREAKFAST;            COMMERCIAL   
    3                                    LUNCH;            COMMERCIAL   
    4                                   DINNER;            COMMERCIAL   
    ...                                     ...                   ...   
    10212                                DINNER  OTHER (PRIVATE CLUB)   
    10213                                DINNER  OTHER (PRIVATE CLUB)   
    10214                            DAILY MENU            HOTEL; FOR   
    10215                                DINNER            HOTEL; FOR   
    10216  INAUGURATION OF THE OKLAHOME CHAPTER  OTHER (PRIVATE CLUB)   
    
                                                       place       date  \
    0                                        HOT SPRINGS, AR  4/15/1900   
    1                                       MILWAUKEE, [WI];  4/15/1900   
    2                     DAMPFER KAISER WILHELM DER GROSSE;  4/16/1900   
    3                     DAMPFER KAISER WILHELM DER GROSSE;  4/16/1900   
    4                     DAMPFER KAISER WILHELM DER GROSSE;  4/16/1900   
    ...                                                  ...        ...   
    10212                     PLIMSOLL CLUB, NEW ORLEANS, LA  5/13/1968   
    10213        PIEDMONT DRIVING  CLUB,  [ATLANTA?] GEORGIA  5/18/1968   
    10214       HOTEL FRANKFURTER, FRANFURT AM MAIN, GERMANY   6/3/1968   
    10215                                HEIDELBERG, GERMANY  6/26/1968   
    10216  OKLAHOMA CITY GOLF AND COUNTRY CLUB, OKLAHOMA ...   7/1/1968   
    
                                                    location  page_count  \
    0                                          Hotel Eastman           2   
    1                                       Republican House           2   
    2                             Norddeutscher Lloyd Bremen           2   
    3                             Norddeutscher Lloyd Bremen           2   
    4                             Norddeutscher Lloyd Bremen           4   
    ...                                                  ...         ...   
    10212  Confrerie De La Chaine Des Rotisseurs, New Orl...           5   
    10213              Confrerie De La Chaine Des Rotisseurs           3   
    10214              Confrerie De La Chaine Des Rotisseurs           3   
    10215  Confrerie De La Chaine Des Rotisseurs, New Orl...           1   
    10216              Confrerie De La Chaine Des Rotisseurs           4   
    
           dish_count  
    0              67  
    1              34  
    2              84  
    3              63  
    4              33  
    ...           ...  
    10212          37  
    10213          22  
    10214          34  
    10215          31  
    10216          24  
    
    [7236 rows x 9 columns]



```python
# DateTime formatting

#pd.to_datetime(dropped_na['date'], dayfirst = False, yearfirst = False)

replaced_dates = dropped_na.replace('0190-03-06', '12-31-2200')

replaced_dates.to_csv("NYPL_NormalMenus.csv")
```
