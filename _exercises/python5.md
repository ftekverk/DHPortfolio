---
layout: page
title: Python Assignment 5
description: Select exercises from Python Crash Course
---


```python
#8-1
def display_message():
    print("I am learning about functions in this chapter.")

display_message()
```

    I am learning about functions in this chapter.



```python
#8-2
def favorite_book(title):
    print("One of my favorite books is " + title + ".")

favorite_book("Alice in Wonderland")
```

    One of my favorite books is Alice in Wonderland.



```python
#8-3
def make_shirt(size, text):
    print("The size of the shirt is " + size + " and the message is " + text + ".")

make_shirt("medium", "This is a shirt with a message.")
make_shirt(text = "This is a shirt with a message.", size = "medium")
```

    The size of the shirt is medium and the message is This is a shirt with a message..
    The size of the shirt is medium and the message is This is a shirt with a message..



```python
#8-5
def describe_city(city, country = "United States"):
    print(city + " is in " + country + ".")

describe_city("New York")
describe_city("Boston")
describe_city("Tokyo", "Japan")
```

    New York is in United States.
    Boston is in United States.
    Tokyo is in Japan.



```python
#8-6
def city_country(city, country):
    return city + ", " + country

print(city_country("New York", "United States"))
print(city_country("Boston", "United States"))
print(city_country("Tokyo", "Japan"))
```

    New York, United States
    Boston, United States
    Tokyo, Japan



```python
#8-7

def make_album(artist, album, tracks = ""):
    albumDict = {"artist": artist, "album": album}
    if tracks:
        albumDict["tracks"] = tracks
    return albumDict

print(make_album("The Beatles", "Abbey Road"))
print(make_album("Rex Orange County", "Apricot Princess"))
print(make_album("Duckwrth", "Super Good", tracks = 16))


```

    {'artist': 'The Beatles', 'album': 'Abbey Road'}
    {'artist': 'Rex Orange County', 'album': 'Apricot Princess'}
    {'artist': 'Duckwrth', 'album': 'Super Good', 'tracks': 16}

