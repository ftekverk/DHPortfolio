---
layout: page
title: Python Assignment 3
description: Select exercises from Python Crash Course
---


```python
# 5-1
name = 'finn'
print("Is name == 'finn'? I predict True.")
print(name == 'finn')

print("\nIs name == 'Finn'? I predict False.")
print(name == 'Finn')
```

    Is name == 'finn'? I predict True.
    True
    
    Is name == 'Finn'? I predict False.
    False



```python
# 5-2
name = 'finn'
lastName = 'tekverk'
print("Is name == 'finn' and lastName == 'tekverk'? I predict True.")
print(name == 'finn' and lastName == 'tekverk')

print("Is name == lastName? I predict False.")
print(name == lastName)

upperName = 'Finn'
print("Is name == upperName? I predict False.")
print(name == upperName)

# lower() method
print("Is name == upperName.lower()? I predict True.")
print(name == upperName.lower())

print("Is name.lower() == upperName? I predict False.")
print(name.lower() == upperName)

# numerical tests
age = 18
print("Is age == 18? I predict True.")
print(age == 18)

print("Is age != 18? I predict False.")
print(age != 18)

# and and or
print("Is age == 18 and name == 'finn'? I predict True.")
print(age == 18 and name == 'finn')

print("Is age == 18 or name == 'finn'? I predict True.")
print(age == 18 or name == 'finn')

print("Is age == 19 or name == 'Finn'? I predict True.")
print(age == 19 or name == 'Finn')

print("Is age == 19 or name == 'Sam'? I predict False.")
print(age == 19 or name == 'Sam')



# check if a value is in a list
names = ['finn', 'sam', 'joe']
print("Is 'finn' in names? I predict True.")
print('finn' in names)

print("Is 'david' in names? I predict False.")
print('david' in names)

# check if a value is not in a list
print("Is 'finn' not in names? I predict False.")
print('finn' not in names)

print("Is 'david' not in names? I predict True.")
print('david' not in names)
```

    Is name == 'finn' and lastName == 'tekverk'? I predict True.
    True
    Is name == lastName? I predict False.
    False
    Is name == upperName? I predict False.
    False
    Is name == upperName.lower()? I predict True.
    True
    Is name.lower() == upperName? I predict False.
    False
    Is age == 18? I predict True.
    True
    Is age != 18? I predict False.
    False
    Is age == 18 and name == 'finn'? I predict True.
    True
    Is age == 18 or name == 'finn'? I predict True.
    True
    Is age == 19 or name == 'Finn'? I predict True.
    False
    Is age == 19 or name == 'Sam'? I predict False.
    False
    Is 'finn' in names? I predict True.
    True
    Is 'david' in names? I predict False.
    False
    Is 'finn' not in names? I predict False.
    False
    Is 'david' not in names? I predict True.
    True



```python
# 5-6
age = 10

if age < 2:
    print("the person is a baby")
elif age >= 2 and age < 4:
    print("the person is a toddler")
elif age >= 4 and age < 13:
    print("the person is a kid")
elif age >= 13 and age < 20:
    print("the person is a teenager")
elif age >= 20 and age < 65:
    print("the person is an adult")
else:
    print("the person is an elder")
```

    the person is a kid



```python
# 5-7
favorite_fruits = ['apple', 'banana', 'strawberry']

if 'apple' in favorite_fruits:
    print("You really like apples!")
if 'banana' in favorite_fruits:
    print("You really like bananas!")
if 'strawberry' in favorite_fruits:
    print("You really like strawberries!")
if 'orange' in favorite_fruits:
    print("You really like oranges!")
if 'watermelon' in favorite_fruits:
    print("You really like watermelons!")
```

    You really like apples!
    You really like bananas!
    You really like strawberries!



```python
# 5-8

usernames = ['admin', 'finn', 'sam', 'joe', 'david']

for username in usernames:
    if username == 'admin':
        print("Hello admin, would you like to see a status report?")
    else:
        print("Hello " + username + ", thank you for logging in again.")
```

    Hello admin, would you like to see a status report?
    Hello finn, thank you for logging in again.
    Hello sam, thank you for logging in again.
    Hello joe, thank you for logging in again.
    Hello david, thank you for logging in again.



```python
# 5-9

usernames = []

if len(usernames) == 0:
    print("We need to find some users!")
```

    We need to find some users!



```python
# 5-10
current_users = ['admin', 'finn', 'sam', 'joe', 'david']
new_users = ['finn', 'joe', 'adam', 'ryan', 'josh']

for new_user in new_users:
    if new_user in current_users:
        print("The username " + new_user + " has already been used. Enter a new username.")
    else:
        print("The username " + new_user + " is available.")
```

    The username finn has already been used. Enter a new username.
    The username joe has already been used. Enter a new username.
    The username adam is available.
    The username ryan is available.
    The username josh is available.

