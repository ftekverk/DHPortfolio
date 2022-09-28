---
layout: page
title: Python Assignment 4
description: Select exercises from Python Crash Course
---


```python
#6-1

finn = {'first_name' : 'finn',
        'last_name' : 'tekverk',
        'age' : 21,
        'city' : 'boston'}


print(finn['first_name'])
print(finn['last_name'])
print(finn['age'])
print(finn['city'])
```


```python
#6-2

favorite_numbers = {'finn' : 7,
                    'jake' : 8,
                    'marceline' : 9,
                    'ice king' : 10,
                    'lsp' : 11}

print(f"finn's favorite number is {favorite_numbers['finn']}")
print(f"jake's favorite number is {favorite_numbers['jake']}")
print(f"marceline's favorite number is {favorite_numbers['marceline']}")
print(f"ice king's favorite number is {favorite_numbers['ice king']}")
print(f"lsp's favorite number is {favorite_numbers['lsp']}")
```


```python
#6-3
glossary = {'list' : 'an array of items in order',
            'dictionary' : 'a non-ordered set of key-value pairs',
            'print' : 'a function to display data',
            'if statement' : 'a statement to evaluate a condition',
            'for loop' : 'a loop that runs a number of times',
            'while loop' : 'a loop that runs until a condition is met',
            'function' : 'a block of code that can be called',
            'sort' : 'a function to sort a list',
            'strip' : 'a function to remove chars from a string',
            'fstring' : 'a string that can be formatted'}


print("List: " + glossary['list'])
print("Dictionary: " + glossary['dictionary'])
print("Print: " + glossary['print'])
print("If statement: " + glossary['if statement'])
print("For loop: " + glossary['for loop'])
```

    List: an array of items in order
    Dictionary: a non-ordered set of key-value pairs
    Print: a function to display data
    If statement: a statement to evaluate a condition
    For loop: a loop that runs a number of times



```python
#6-4
for key, value in glossary.items():
    print(f"{key} : {value}")
```

    list : an array of items in order
    dictionary : a non-ordered set of key-value pairs
    print : a function to display data
    if statement : a statement to evaluate a condition
    for loop : a loop that runs a number of times
    while loop : a loop that runs until a condition is met
    function : a block of code that can be called
    sort : a function to sort a list
    strip : a function to remove chars from a string
    fstring : a string that can be formatted



```python
#6-5
rivers = {'nile' : 'egypt',
          'Yeongsan' : 'south korea',
          'amazon' : 'brazil'}

for key, value in rivers.items():
    print(f"The {key} runs through {value}.")
```

    The nile runs through egypt.
    The Yeongsan runs through south korea.
    The amazon runs through brazil.



```python
#6-7

finn = {'first_name' : 'finn',
        'last_name' : 'tekverk',
        'age' : 21,
        'city' : 'boston'}

josh = {'first_name' : 'josh',
        'last_name' : 'kalet',
        'age' : 21,
        'city' : 'boston'}

adam = {'first_name' : 'adam',
        'last_name' : 'peters',
        'age' : 21,
        'city' : 'boston'}

people = [finn, josh, adam]

for person in people:
    print(person)

```

    {'first_name': 'finn', 'last_name': 'tekverk', 'age': 21, 'city': 'boston'}
    {'first_name': 'josh', 'last_name': 'kalet', 'age': 21, 'city': 'boston'}
    {'first_name': 'adam', 'last_name': 'peters', 'age': 21, 'city': 'boston'}



```python
#6-8

sparky = {'animal' : 'dog',
          'owner' : 'finn'}

loona = {'animal' : 'cat',
         'owner' : 'josh'}

max = {'animal' : 'dog',
       'owner' : 'adam'}

meowmeow = {'animal' : 'cat',
            'owner' : 'finn'}

pets = [sparky, loona, max, meowmeow]

for pet in pets:
       print(pet)
```

    {'animal': 'dog', 'owner': 'finn'}
    {'animal': 'cat', 'owner': 'josh'}
    {'animal': 'dog', 'owner': 'adam'}
    {'animal': 'cat', 'owner': 'finn'}



```python
#6-9

favorite_places = { 'finn' : ['paris', 'sydney', 'tokyo'],
                    'josh' : ['boston', 'new york', 'los angeles'],
                    'adam' : ['seoul', 'tokyo', 'hong kong']
                }

for name, places in favorite_places.items():
    print(f"{name}'s favorite places are:")
    for place in places:
        print(f"\t{place}")


```

    finn's favorite places are:
    	paris
    	sydney
    	tokyo
    josh's favorite places are:
    	boston
    	new york
    	los angeles
    adam's favorite places are:
    	seoul
    	tokyo
    	hong kong



```python
#6-11

cities = {'boston' : {'country' : 'united states',
                      'population' : '4 million',
                      'fact' : 'Tufts is nearby!'},

          'tokyo' : {'country' : 'japan',
                     'population' : '13 million',
                     'fact' : 'located in southen Kanto'},

          'paris' : {'country' : 'france',
                     'population' : '2 million',
                     'fact' : 'has the eiffel tower'}
          }

for city, info in cities.items():
    print(f"{city.title()} has info {info}")
```

    Boston has info {'country': 'united states', 'population': '4 million', 'fact': 'Tufts is nearby!'}
    Tokyo has info {'country': 'japan', 'population': '13 million', 'fact': 'located in southen Kanto'}
    Paris has info {'country': 'france', 'population': '2 million', 'fact': 'has the eiffel tower'}

