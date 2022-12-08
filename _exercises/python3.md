---
layout: page
title: Python Assignment 3
description: Select exercises from Python Crash Course Chapter 4
---




```python
# 4-1
pizzas = ["Pepperoni", "Cheese", "Buffalo Chicken"]
for pizza in pizzas:
    print("I like " + pizza + " pizza.")

print("I really love pizza!")
```

    I like Pepperoni pizza.
    I like Cheese pizza.
    I like Buffalo Chicken pizza.
    I really love pizza!



```python
# 4-2
animals = ["Dog", "Bird", "Cat"]
for animal in animals:
    print("A " + animal + " would make a great pet.")

print("Any of these animals would make a great pet!")

```

    A Dog would make a great pet.
    A Bird would make a great pet.
    A Cat would make a great pet.
    Any of these animals would make a great pet!



```python
# 4-6
list = range(1, 21, 2)

for num in list:
    print(num)
```

    1
    3
    5
    7
    9
    11
    13
    15
    17
    19



```python
# 4-10
print("The first three items in the list are:")
print(places[:3])

print("Three items from the middle of the list are:")
print(places[1:4])

print("The last three items in the list are:")
print(places[-3:])
```

    The first three items in the list are:
    ['Tokyo', 'Paris', 'New York']
    Three items from the middle of the list are:
    ['Paris', 'New York', 'London']
    The last three items in the list are:
    ['New York', 'London', 'Cairo']



```python
# 4-11

friend_pizzas = pizzas[:]

pizzas.append("Hawaiian")
friend_pizzas.append("Meat Lovers")

print("My favorite pizzas are:")
for pizza in pizzas:
    print(pizza)

print("My friend's favorite pizzas are:")
for pizza in friend_pizzas:
    print(pizza)
```

    My favorite pizzas are:
    Pepperoni
    Cheese
    Buffalo Chicken
    Hawaiian
    My friend's favorite pizzas are:
    Pepperoni
    Cheese
    Buffalo Chicken
    Meat Lovers

