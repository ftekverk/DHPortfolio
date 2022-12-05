---
layout: page
title: NER
description: Named Entity Recognition
---

# NER Assignment
Georeferencing automatically detected place names in Edward Gibbon's *Decline and Fall of the Roman Empire* using the Pleiades gazatteer and `spaCy`.

Your assignment this week is to output a `CSV` file of place names, frequency and coordinates, as we did in class for a chapter of Gibbon of your choice. Try to find a chapter with a lot of places as we will be turning this data into an online map next week. The steps are:

* Choose a chapter from the text
* Begin a function by parsing input text
* Create a `spaCy` dictionary of entities and frequency
* Use the Pleiaes data from class to find coordinates for each place name
* Run your function on your chosen chapter
* Save your final `CSV`
* Come to class on Monday, ready to use it


```python
# import and download any relevant data
import pandas as pd
import collections
import spacy
import wget
import os
nlp = spacy.load('en_core_web_sm')


# downloading gibbon text from Micah's gh
if not os.path.isfile('gibbon_text.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/gibbon_text.csv')



# read in the data
gibbon_by_chapter = pd.read_csv('gibbon_text.csv').rename(columns={'Unnamed: 0':'chapter'})
gibbon_by_chapter
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
      <th>chapter</th>
      <th>StringText</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Chapter 1</td>
      <td>\nIn the second century of the Christian era, ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chapter 2</td>
      <td>\nIt is not alone by the rapidity or extent of...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chapter 3</td>
      <td>\nThe obvious definition of a monarchy seems t...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chapter 4</td>
      <td>\nThe mildness of Marcus, which the rigid disc...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chapter 5</td>
      <td>\nThe power of the sword is more sensibly felt...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>66</th>
      <td>Chapter 67</td>
      <td>\nThe respective merits of Rome and Constantin...</td>
    </tr>
    <tr>
      <th>67</th>
      <td>Chapter 68</td>
      <td>\nThe siege of Constantinople by the Turks att...</td>
    </tr>
    <tr>
      <th>68</th>
      <td>Chapter 69</td>
      <td>\nIn the first ages of the decline and fall of...</td>
    </tr>
    <tr>
      <th>69</th>
      <td>Chapter 70</td>
      <td>\nIn the apprehension of modern times, Petrarc...</td>
    </tr>
    <tr>
      <th>70</th>
      <td>Chapter 71</td>
      <td>\nIn the last days of Pope Eugenius the Fourth...</td>
    </tr>
  </tbody>
</table>
<p>71 rows × 2 columns</p>
</div>




```python
# Choose a chapter to work with 
first_chapter = gibbon_by_chapter['StringText'][0]

# Perform NER on the chapter
first_chapter_doc = nlp(first_chapter)
```


```python
for entity in first_chapter_doc.ents: # can access NER with the .ents attribute
    print(entity.text, entity.label_, sep='\t')
```


```python
# putting all of the data into a dictionary
import collections
place_freq = collections.defaultdict(int)
for entity in first_chapter_doc.ents:
    if (entity.label_ == 'GPE') or (entity.label_ == 'LOC'):
        place_freq[entity.text] += 1 # the utility of defaultdict!
place_freq = dict(place_freq)
```


```python
# put dict into df
place_freq_df = pd.DataFrame.from_dict(place_freq, orient='index').reset_index().rename(columns={'index':'place_name',0:'frequency'})
place_freq_df
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
      <th>place_name</th>
      <th>frequency</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rome</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nerva</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Trajan</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Marcus Antoninus</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aethiopia</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>147</th>
      <td>Great Britain</td>
      <td>1</td>
    </tr>
    <tr>
      <th>148</th>
      <td>Sardinia</td>
      <td>1</td>
    </tr>
    <tr>
      <th>149</th>
      <td>Sicily</td>
      <td>1</td>
    </tr>
    <tr>
      <th>150</th>
      <td>Malta</td>
      <td>1</td>
    </tr>
    <tr>
      <th>151</th>
      <td>the Western Ocean</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>152 rows × 2 columns</p>
</div>




```python
# Get Pleiades URIs for the entities
if not os.path.isfile('places.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/places.csv')
if not os.path.isfile('names.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/names.csv')
```


```python
# save result as CSV
places = pd.read_csv('places.csv')
```
