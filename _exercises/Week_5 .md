---
layout: page
title: Week 5 Homework 
description: Chapter 5- If Statements 
---

## Chapter 5 Excercises 
Python Crash Course: 5-1, 5-2, 5-6, 5-7, 5-8, 5-9, 5-10

### 5-1. Conditional Tests:


```python
print("TEST 1")
dog = "Scout"
print("Is Scout a dog? I'd bet she is.")
print(dog == "Scout")
print("Is Scout not a dog? I'd think false.")
print("Scout" != dog)
print("----------")

print("TEST 2")
a = 17
b = 22
print("Is 17 < 22? I'd predict true.")
print(a < b)
print("Is 17 > 22? I'd predict false.")
print(a > b)
print("----------")

print("TEST 3")
dad = "Tony"
print("Is John Cena my dad? I don't think so but lets check.")
print(dad == "John Cena")
print("Is Tony my dad? I'm pretty sure he is.")
print(dad == "Tony")
print("----------")

print("TEST 4")
money = 10
shirt = 40
print("Do I have enough money to buy this new shirt? I don't think I do.")
print(money >= shirt)
print("At least I have 20 dollars right? I don't think I do but lets check.")
print(money >= 20)
print("----------")

print("TEST 5")
friend = "sam"
print("Did I forget to capitalize my friend's name? I think true.")
print(friend != friend.title())
print("Did I write my friend's whole name in uppercase? I think false.")
print(friend == friend.upper())


```

    TEST 1
    Is Scout a dog? I'd bet she is.
    True
    Is Scout not a dog? I'd think false.
    False
    ----------
    TEST 2
    Is 17 < 22? I'd predict true.
    True
    Is 17 > 22? I'd predict false.
    False
    ----------
    TEST 3
    Is John Cena my dad? I don't think so but lets check.
    False
    Is Tony my dad? I'm pretty sure he is.
    True
    ----------
    TEST 4
    Do I have enough money to buy this new shirt? I don't think I do.
    False
    At least I have 20 dollars right? I don't think I do but lets check.
    False
    ----------
    TEST 5
    Did I forget to capitalize my friend's name? I think true.
    True
    Did I write my friend's whole name in uppercase? I think false.
    False


### 5-2. More Conditional Tests: 


```python
#Tests for equality and inequality with strings
print("TEST 1")
Friend = "Sam"
friend = "sam"
print("Did I type exactly the same thing when I was spelling my friends name? I think False.")
print (Friend == friend)
print("So does that mean that I typed the something different. I think true.")
print (Friend != friend)
print("----------")

#Tests using the lower() function
print("TEST 2")
print("Did I write the variable'friend'? in lowercase? I think true.")
print(friend != friend.lower())
print("Wait, is the variable 'Friend' written in lowercase as well? I think false.")
print(Friend == Friend.lower())
print("----------")

#Numerical tests involving equality and inequality, greater than and less than, greater than or equal to, and less than or equal to
print("TEST 3")
age = 22
old = 30
print("Am I old yet? I think false.")
print (age >= old)
print("I thought I was 22, is that true? I think true. ")
print(age == 22)
print("----------")

#Tests using the and keyword and the or keyword
print("TEST 4")
vote = 18
print("Am I not old AND old enough to vote? I think true.")
print(age < old and age > vote)
print("Am I either 22 or old? I think that I'm one of them, so true.")
print(age == 22 or age >= old)
print("----------")

#Test whether an item is/isn't in a list
print("TEST 5")
shades = ["black", "gray", "white"]
print("Is purple a shade? I think false.")
print("purple" in shades)
print("Is gray a shade? I think true.")
print("gray" in shades)


```

    TEST 1
    Did I type exactly the same thing when I was spelling my friends name? I think False.
    False
    So does that mean that I typed the something different. I think true.
    True
    ----------
    TEST 2
    Did I write the variable'friend'? in lowercase? I think true.
    False
    Wait, is the variable 'Friend' written in lowercase as well? I think false.
    False
    ----------
    TEST 3
    Am I old yet? I think false.
    False
    I thought I was 22, is that true? I think true. 
    True
    ----------
    TEST 4
    Am I not old AND old enough to vote? I think true.
    True
    Am I either 22 or old? I think that I'm one of them, so true.
    True
    ----------
    TEST 5
    Is purple a shade? I think false.
    False
    Is gray a shade? I think true.
    True


### 5-6. Stages of Life:


```python
age = 22

if (age < 2):
    print("You are a baby.")
elif (age >= 2 and age < 4):
    print("You are a toddler.")
elif (age >= 4 and age < 13):
    print("You are a kid.")
elif (age >=13 and age < 20):
    print("You are a teenager.")
elif (age >=20 and age < 65):
    print("You are an adult.")
else:
    print("You are an elder.")
```

    You are an adult.


### 5-7. Favorite Fruit:


```python
favorite_fruits = ["mango", "rasberry", "watermelon"]

if ("mango" in favorite_fruits):
    print("Mango is one of your favorite fruits!")
if ("cantaloupe" in favorite_fruits):
    print("Cantaloupe is one of your favorite fruits? You should go to therapy.")
if ("watermelon" in favorite_fruits):
    print("Watermelon is one of your favotire fruits! That's incredible taste")
if ("blueberry" in favorite_fruits):
    print("Blueberry is one of your favorite fruits!")
if ("rasberry" in favorite_fruits):
    print ("Rasberry is one of your favorite fruits! It is objectively the best type of berry!")
```

    Mango is one of your favorite fruits!
    Watermelon is one of your favotire fruits! That's incredible taste
    Rasberry is one of your favorite fruits! It is objectively the best type of berry!


### 5-8. Hello Admin: 


```python
users = ["Scout", "Max", "Zach", "Admin", "Jake"]
for user in users:
    if (user == "Admin"):
        print("Hello Admin, would you like to see a status report?")
    else:
        print(f"Welcome {user}")
```

    Welcome Scout
    Welcome Max
    Welcome Zach
    Hello Admin, would you like to see a status report?
    Welcome Jake


### 5-9. No Users: 


```python
#Run with 5-8
if users:
    print("There are users in your list.")
else:
    print("There are no users in your list!")

users.clear()

if users:
    print("There are users in your list.")
else:
    print("There are no users in your list!")
```

    There are users in your list.
    There are no users in your list!


### 5-10. Checking Usernames:


```python
current_users = ["Rachel", "Tony", "Max", "Zach", "Jake"]
new_users = ["Abby", "Sam", "Rachel", "Ray", "Jake"]

for user in new_users:
    if(user in current_users):
        print(f"Username '{user}' in use. Please enter a new username.")
```

    Username 'Rachel' in use. Please enter a new username.
    Username 'Jake' in use. Please enter a new username.

