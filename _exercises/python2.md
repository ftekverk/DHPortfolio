---
layout: page
title: Python Assignment 2
description: Select exercises from Python Crash Course Chapter 3
---

```python
# 3-1
friendsNames = ["Ryan", "Adam", "Joe", "Josh"]
for name in friendsNames:
    print(name)
```

    Ryan
    Adam
    Joe
    Josh



```python
# 3-2
for name in friendsNames:
    print("Hello " + name + "!")
```

    Hello Ryan!
    Hello Adam!
    Hello Joe!
    Hello Josh!



```python
# 3-3
transport = ["Bike", "Car", "Plane", "Boat"]
for elem in transport:
    print("I would like to own a " + elem + ".")
```

    I would like to own a Bike.
    I would like to own a Car.
    I would like to own a Plane.
    I would like to own a Boat.



```python
# 3-4
invited = ["Hemingway", "Fitzgerald", "Caesar"]
for person in invited:
    print("Hello " + person + ", would you care to have dinner?")
```

    Hello Hemingway, would you care to have dinner?
    Hello Fitzgerald, would you care to have dinner?
    Hello Caesar, would you care to have dinner?



```python
# 3-5
print("Unfortunately, " + invited[1] + " cannot make it.")
invited.pop(1)
for person in invited:
    print("Hello " + person + ", would you care to have dinner?")
```

    Unfortunately, Fitzgerald cannot make it.
    Hello Hemingway, would you care to have dinner?
    Hello Caesar, would you care to have dinner?



```python
# 3-6
print("We have found a bigger table!")
invited.insert(0, "Einstein")
invited.insert(2, "Newton")
invited.append("Darwin")

# New invitations 
for person in invited:
    print("Hello " + person + ", would you care to have dinner?")
```

    We have found a bigger table!
    Hello Einstein, would you care to have dinner?
    Hello Hemingway, would you care to have dinner?
    Hello Newton, would you care to have dinner?
    Hello Caesar, would you care to have dinner?
    Hello Darwin, would you care to have dinner?



```python
# 3-7
print("We can only have two people to dinner.")

while len(invited) > 2:
    print("Sorry " + invited.pop() + ", you are not invited.")

for person in invited:
    print("Hello " + person + ", you are still invited!")

del(invited[0])
del(invited[0])

print(invited)
```

    We can only have two people to dinner.
    Sorry Darwin, you are not invited.
    Sorry Caesar, you are not invited.
    Sorry Newton, you are not invited.
    Hello Einstein, you are still invited!
    Hello Hemingway, you are still invited!
    []



```python
# 3-8
places = ["Paris", "London", "Cairo" , "New York", "Tokyo"]

#print original list
print(places)
print(sorted(places))
print(places)

#reverse list
places.reverse()
print(places)

#reverse again
places.reverse()
print(places)

# sort list
places.sort()
print(places)

#sort again, reverse
places.sort(reverse=True)
print(places)

```

    ['Paris', 'London', 'Cairo', 'New York', 'Tokyo']
    ['Cairo', 'London', 'New York', 'Paris', 'Tokyo']
    ['Paris', 'London', 'Cairo', 'New York', 'Tokyo']
    ['Tokyo', 'New York', 'Cairo', 'London', 'Paris']
    ['Paris', 'London', 'Cairo', 'New York', 'Tokyo']
    ['Cairo', 'London', 'New York', 'Paris', 'Tokyo']
    ['Tokyo', 'Paris', 'New York', 'London', 'Cairo']



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

