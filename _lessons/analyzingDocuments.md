---
layout: page
title: Analyzing Documents with TF-IDF
description: Using TF-IDF Natural Language Processing
---
## Source
[Matthew J. Lavin, "Analyzing Documents with TF-IDF"](https://programminghistorian.org/en/lessons/analyzing-documents-with-tfidf)

## Reflection
The lesson introduced a few compelling methods which could be widely applicable across digital humanities studies. These methods included natural language processing with a choice of a natural language, models to show the relationship between people and places, and a visualization software.

The method of NLP used in this lesson could be immensely helpful for analysis of regions and histories with languages that are foreign to the researcher. In this lesson, libraries  specific to the German language were used, which I am completely unfamiliar with. However, using German language datasets, I was able to perform analysis on text I am completely unable to read. These methods could be used for a wide variety of languages, allowing more people to access and work with data from different regions of the world.

Another method that could be useful in other projects is the model to show relationships between people and places in a text. Using larger datasets, we are able to visualize connections between certain words, such as part of speech. This could be used to link a person to their geographical location, which could be very useful in other digital humanities projects.

Furthermore, this lesson introduced a website that could take a tsv file and show the locations mentioned on a world map. This could be immensely helpful in producing visualizations for the scope of a region that is investigated or mentioned in a particular analysis.


## Code

```python
#Retrieve all .txt files from the folder

from pathlib import Path

all_txt_files =[]
for file in Path("txt").rglob("*.txt"):
     all_txt_files.append(file.parent / file.name)
# counts the length of the list
n_files = len(all_txt_files)
print(n_files)
```

    366



```python
#Sort the list of files in numerical order
all_txt_files.sort()

#print the first file
all_txt_files[0]
```




    PosixPath('txt/0101.txt')




```python
#load each file, and convert to python format

all_docs = []
for txt_file in all_txt_files:
    with open(txt_file) as f:
        txt_file_as_string = f.read()
    all_docs.append(txt_file_as_string)
```


```python
#import the TfidfVectorizer from Scikit-Learn.
from sklearn.feature_extraction.text import TfidfVectorizer

vectorizer = TfidfVectorizer(max_df=.65, min_df=1, stop_words=None, use_idf=True, norm=None)
transformed_documents = vectorizer.fit_transform(all_docs)
```


```python
transformed_documents_as_array = transformed_documents.toarray()
# use this line of code to verify that the numpy array represents the same number of documents that we have in the file list
len(transformed_documents_as_array)
```




    366




```python
import pandas as pd

# make the output folder if it doesn't already exist
Path("./tf_idf_output").mkdir(parents=True, exist_ok=True)

# construct a list of output file paths using the previous list of text files the relative path for tf_idf_output
output_filenames = [str(txt_file).replace(".txt", ".csv").replace("txt/", "tf_idf_output/") for txt_file in all_txt_files]

# loop each item in transformed_documents_as_array, using enumerate to keep track of the current position
for counter, doc in enumerate(transformed_documents_as_array):
    # construct a dataframe
    tf_idf_tuples = list(zip(vectorizer.get_feature_names(), doc))
    one_doc_as_df = pd.DataFrame.from_records(tf_idf_tuples, columns=['term', 'score']).sort_values(by='score', ascending=False).reset_index(drop=True)

    # output to a csv using the enumerated value for the filename
    one_doc_as_df.to_csv(output_filenames[counter])
```


```python

```
