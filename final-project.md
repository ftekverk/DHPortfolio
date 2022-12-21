---
layout: page
title: Final Project
permalink: /final-project/
---

# Introduction
My project attempts to analyze the sentiment of the American people over the time period 1950-2021. I measure the sentiment of the American people by selecting the most sold album in each year, and performing a sentiment analysis on the lyrics of each song. This assigns a few numerical values to the sentiment of the album (positive, negative, neutral, and compound sentiments). I am using the sentiment of the album every year to represent the sentiment of the listeners during that year.

There are clear drawbacks to using the lyrics of an album to represent the sentiment of the listeners. While the album may have been the most sold in the year, it may be the case that people want to listen to happy music when they are sad, or vice versa. In other words, the sentiment of the songs on an album may not accurately reflect the sentiment of the listeners.
Selecting only the most popular album also has its drawbacks. While this is easier in terms of computation, it may not capture enough data to truly be representative. It may be the case that a popular artist or group released an album that was not in the sentiment of the listeners, but was successful because of the quality of production. An approach to solve this would be to consider more than just the most popular album as a dataset for each year.

# Data Gathering
The data for the most popular album by year came from Business Insider. I first attempted to use web scraping in order to populate a .csv file with the album and artist information from each year. However, I ran into difficulties, and decided to populate this file manually. This was achievable for an analysis of only about 60 years, but would not be scalable.

Link For Album Data : https://www.businessinsider.com/best-selling-albums-by-year-list-2017-7#1956-harry-belafonte-calypso-62

The second set of data my project used was the actual lyrics from each song. In order to capture this data, I used the getSongs() method that we used in class. This uses API calls to lyricsGenius in order to get song information, given an artist and an album. I performed this for each artist, album pair from the .csv file containing the information of the most popular album in each year.

# Dataset Preparation
The dataset preparation for this project was relatively simple. After failing to use web scraping to extract the most popular album by year information, I manually populated the most popular album by year. I used the pandas dataframe, and removed rows with missing entries (either the artist or album name was not given).

The second dataset that I had to collect was the lyrics from each album. In some cases, the getSong() method was unable to find album data. In these cases, the albums from these years were simply excluded from the dataset. These errors were suppressed using "try-except" functionality, so that the data parsing would continue. In some cases, the songs were listed as years that were not logical. I set a range of valid years to consider, and ignored songs that fell outside of this range.

The calculated sentiment data was then formatted in a plottable way, and normalized so that years with higher quantities of lyrics were not overrepresented.


# Issues With Code
While the code I've shown works, it could be made more modular and optimized further. This is especially true for the first data I collected, the .csv of the most sold album in each year. It would be extremely beneficial to implement this using web scraping in order to have a more scalable project.

The code also does not attempt to remedy errors in data. For albums or years that have invalid data, these are simply excluded from the dataset. I could have cross referenced with an external source if I wanted to use all of the possible information.


# Code

# Sentiment Analysis of Americans Over Time Through Use of Most Popular Album Lyrics of Each Year

# 1.) Parse Year, Artist, Album Information and Use API call to get Album Lyrics


```python
# Get Necessary Imports
from get_lyrics import getSongs
from bs4 import BeautifulSoup
import pandas as pd
import matplotlib.pyplot as plt
```


```python
# Read in data to a pandas dataframe
# Data is in the format of year, artist, album
df = pd.read_csv('year_artist_album.csv')

# Clean the data
df.dropna(inplace=True)

# Print head of dataframe
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
      <th>year</th>
      <th>artist</th>
      <th>album</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>1956</td>
      <td>Harry Belafonte</td>
      <td>Calypso</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1957</td>
      <td>Original Broadway Cast</td>
      <td>My Fair Lady</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1958</td>
      <td>Original Broadway Cast</td>
      <td>My Fair Lady</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1959</td>
      <td>Henry Mancini</td>
      <td>Music from Peter Gunn</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1960</td>
      <td>Original Broadway Cast</td>
      <td>The Sound of Music</td>
    </tr>
  </tbody>
</table>
</div>




```python
# API call to get the lyrics

# Create a dictionary to store the lyrics
lyrics = {}

# for each artist and album, get lyrics
for index, row in df.iterrows():
        year = row['year']
        artist = row['artist']
        album = row['album']

        try:
                # Creates .json files with the lyrics
                lyrics[year] = getSongs(artist, album, max_songs=10)
        except:
                print(f"Error: {artist} - {album} - {year}")   
```

    Searching for "Calypso" by Harry Belafonte...
    Wrote Lyrics_Calypso.json.
    Data saved
    Data loaded
    ...
    Searching for "Divide" by Ed Sheeran...
    Wrote Lyrics_Divide.json.
    Data saved
    Data loaded



```python
# Test to see if lyrics are being collected
# Print the lyrics for the first three years
counter = 0
for year in lyrics:
        if counter < 1:
                print(lyrics[year])
                counter += 1
```

                            song_title  \
    0         Day-O (Banana Boat Song)   
    1                   I Do Adore Her   
    2                 Jamaica Farewell   
    3   Will His Love Be Like His Rum?   
    4                       Dolly Dawn   
    5                           Star-O   
    6                The Jack-Ass Song   
    7                          Hosanna   
    8                   Come Back Liza   
    9                  Brown Skin Girl   
    10       Man Smart (Woman Smarter)   
    
                                                   lyrics  
    0   Day-O (Banana Boat Song) LyricsDay-o, day-ay-a...  
    1   I Do Adore Her Lyrics[Verse 1]\nWhen shadows f...  
    2   Jamaica Farewell Lyrics[Verse 1]\nDown the way...  
    3   Will His Love Be Like His Rum? Lyrics[Verse 1]...  
    4   Dolly Dawn Lyrics[Intro]\nHoo-ooh!\nLook, look...  
    5   Star-O LyricsStar-o, star-o\nStar a come and I...  
    6   The Jack-Ass Song LyricsPlay that ting, man\nJ...  
    7   Hosanna Lyrics[Intro]\nHosanna me built a hous...  
    8   Come Back Liza Lyrics[Verse 1]\nEvery time I'm...  
    9   Brown Skin Girl Lyrics[Verse 1]\nEverything to...  
    10  Man Smart (Woman Smarter) Lyrics[Intro]\nHa-ha...  



# Perform Sentiment Analysis on the data, and graphs the results


```python
# Necessary imports
import glob
import json
import os
import re
import sys
import time
import nltk

import matplotlib.pyplot as plt
import seaborn as sns
color = sns.color_palette()
import plotly.offline as py
py.init_notebook_mode(connected=True)
import plotly.graph_objs as go
import plotly.tools as tls
import plotly.express as px
```


<script type="text/javascript">
window.PlotlyConfig = {MathJaxConfig: 'local'};
if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}
if (typeof require !== 'undefined') {
require.undef("plotly");
requirejs.config({
    paths: {
        'plotly': ['https://cdn.plot.ly/plotly-2.16.1.min']
    }
});
require(['plotly'], function(Plotly) {
    window._Plotly = Plotly;
});
}
</script>




```python
# Create a list of all the json files in the directory
json_files = glob.glob('*.json')


# Test for one file
# Iterate through json files and get lyrics
# filename = 'Lyrics_Thriller.json'
# with open(filename) as f:
#         data = json.load(f)


# Create a dictionary to store the lyrics by year
        # Key : Year, Value : List of lyrics
lyrics_by_year = {}

# Load data for all file
for filename in json_files:
        with open(filename) as f:
                data = json.load(f)


        # Get lyrics from the json file
        lyrics = []
        for song in data['tracks']:
                if song['song']['lyrics'] is not None:
                        lyrics.append(song['song']['lyrics'])

        # Get the year of the song, and add the lyrics to the dictionary
                if song['song']['release_date_components'] is not None:
                        year = song["song"]["release_date_components"]["year"]
                        if year not in lyrics_by_year:
                                lyrics_by_year[year] = []
                        
                        lyrics_by_year[year].append(song['song']['lyrics'])


```


```python
# Print the number of songs per year
for year in lyrics_by_year:
        print(year, len(lyrics_by_year[year]))
```

    1992 21
    2008 14
    1990 11
    1991 2
    2020 2
    1959 16
    1965 12
    1982 14
    1984 13
    1983 5
    2014 14
    1968 6
    1970 1
    1971 2
    1972 16
    1973 20
    1974 4
    1975 3
    1976 8
    1980 11
    1988 13
    1985 11
    1989 19
    1994 2
    1995 14
    1997 12
    1999 17
    2001 5
    2017 12
    1960 16
    2000 23
    2007 12
    2015 14
    1987 11
    1956 27
    2004 19
    2003 17
    2002 21
    2010 20
    1996 9
    2016 19
    2013 13
    1964 12
    1957 16
    1967 10
    1966 4
    1969 1
    1977 11
    2005 16
    1979 28
    1986 10
    2011 11
    659 1
    1978 8



```python
# Get rid of the years outside of the range 1950-2022
year_min = 1950
year_max = 2022
for year in list(lyrics_by_year.keys()):
        if year < year_min or year > year_max:
                del lyrics_by_year[year]
```


```python
# Sentiment Analysis using VADER
from nltk.sentiment.vader import SentimentIntensityAnalyzer
nltk.downloader.download('vader_lexicon')

# Create a SentimentIntensityAnalyzer object.
sid_obj = SentimentIntensityAnalyzer()
```

    [nltk_data] Downloading package vader_lexicon to
    [nltk_data]     /Users/finntekverk/nltk_data...
    [nltk_data]   Package vader_lexicon is already up-to-date!



```python
# Create a dictionary to store the sentiment analysis results
# Key : Year, Value : Sentiment Analysis Results
sentiment_by_year = {}


# Perform sentiment analysis on the lyrics
for year in lyrics_by_year:
        sentiment_by_year[year] = {}
        sentiment_by_year[year]['positive'] = 0
        sentiment_by_year[year]['negative'] = 0
        sentiment_by_year[year]['neutral'] = 0
        sentiment_by_year[year]['compound'] = 0

        for lyric in lyrics_by_year[year]:

                # Perform sentiment analysis on the lyrics
                #   - contains pos, neg, neu, and compound scores.
                sentiment_dict = sid_obj.polarity_scores(lyric)

                if sentiment_dict['compound'] >= 0.05 :
                        sentiment_by_year[year]['positive'] += 1
                elif sentiment_dict['compound'] <= - 0.05 :
                        sentiment_by_year[year]['negative'] += 1
                else :
                        sentiment_by_year[year]['neutral'] += 1
                sentiment_by_year[year]['compound'] += sentiment_dict['compound']

        # Normalize all scores considering the number of lyrics
        sentiment_by_year[year]['positive'] /= len(lyrics_by_year[year])
        sentiment_by_year[year]['negative'] /= len(lyrics_by_year[year])
        sentiment_by_year[year]['neutral'] /= len(lyrics_by_year[year])
        sentiment_by_year[year]['compound'] /= len(lyrics_by_year[year])
```


```python
# Verify the sentiment analysis results by printing a year of your choice
year = 1982
print(sentiment_by_year[year])
```

    {'positive': 0.5714285714285714, 'negative': 0.42857142857142855, 'neutral': 0.0, 'compound': 0.27872142857142856}



```python
# Plot the sentiment analysis results

# Sort the dictionary by year
sentiment_by_year = dict(sorted(sentiment_by_year.items()))

# Plot of Positive Sentiment over the years
x = []
y = []
for year in sentiment_by_year:
        x.append(year)
        y.append(sentiment_by_year[year]['positive'])

plt.figure(figsize=(10,5))
plt.plot(x, y, color='green', marker='o', linestyle='dashed', linewidth=2, markersize=5)
plt.title('Positive Sentiment Over the Years')
plt.xlabel('Year')
plt.ylabel('Positive Sentiment')
plt.show()

# Plot of Negative Sentiment over the years
x = []
y = []
for year in sentiment_by_year:
        x.append(year)
        y.append(sentiment_by_year[year]['negative'])

plt.figure(figsize=(10,5))
plt.plot(x, y, color='red', marker='o', linestyle='dashed', linewidth=2, markersize=5)
plt.title('Negative Sentiment Over the Years')
plt.xlabel('Year')
plt.ylabel('Negative Sentiment')
plt.show()


# Plot of Neutral Sentiment over the years
x = []
y = []
for year in sentiment_by_year:
        x.append(year)
        y.append(sentiment_by_year[year]['neutral'])

plt.figure(figsize=(10,5))
plt.plot(x, y, color='blue', marker='o', linestyle='dashed', linewidth=2, markersize=5)
plt.title('Neutral Sentiment Over the Years')
plt.xlabel('Year')
plt.ylabel('Neutral Sentiment')
plt.show()

# Plot of Compound Sentiment over the years
x = []
y = []
for year in sentiment_by_year:
        x.append(year)
        y.append(sentiment_by_year[year]['compound'])
        
plt.figure(figsize=(10,5))
plt.plot(x, y, color='black', marker='o', linestyle='dashed', linewidth=2, markersize=5)
plt.title('Compound Sentiment Over the Years')
plt.xlabel('Year')
plt.ylabel('Compound Sentiment')
plt.show()
```


    
![png](sentiment_analysis_files/positiveSentiment.png)
    
    
![png](sentiment_analysis_files/negativeSentiment.png)
    
    
![png](sentiment_analysis_files/neutralSentiment.png)

    
![png](sentiment_analysis_files/compoundSentiment.png)



    
# Visualization Explanation
The sentiment data is normalized (range of -1 to 1). A more positive value indicates higher expression of that sentiment. As an example, if the year 2022 was assigned a positive sentiment value of 1, this would indicate the most positive value possible. Similarly, a negative value would indicate the lack of this sentiment.

Positive and negative sentiment refer to positive and negative emotions. Neutral sentiment refers to words that indicate neither positive or negative sentiment. Finally, compound sentiment is similar to a combination of positive and negative sentiment.

It is hard to identify trends in most of the visualizations of sentiment data.

For positive sentiment over the years, we notice a distinct drop around 1965, however this might just be an outlier due to lack of lyric data. For all other years, positive sentiment seems to fall within a range of about 0.4-1.0. The only trend I have identified is that on average, sentiment scores seem to be slightly lower after 1995.

For negative sentiment over the years, there are similar observations to positive sentiment. From year to year, sentiment varies drastically. However, after the year 2000, we see higher peaks than in previous years.

Neutral sentiment is the most consistent over the years, with the exception of two large spikes around 1965 and 1995. 

Compound sentiment seems to fall within a range of values, and very rarely falls outside of that range. However, there are no identifiable trends over time. The sentiment seems to choose a random value within the range each year.

# Conclusion
It is hard to draw conclusions about the sentiment of the American people from the visualizations produced. There are no strong identifiable trends in the plots. Sentiment seems to alter 'randomly', rarely falling outside of certain ranges.

This project could benefit from the use of more lyric data in each year, and perhaps more granularity in time. For example, if I had attempted to analyze sentiment for each quarter of the year, we might see more gradual changes in sentiment.

