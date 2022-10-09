---
layout: page
title: Week 4 Homework
description: Chapters 3 and 4- Lists
---


## Chapter 3 
* 3-1 --> 3-8
    
## Chapter 4
* 4-1, 4-2, 4-3, 4-6, 4-10, 4-11

### 3-1. Names:


```python
friends = ["Wanda", "Abby", "Ray", "Sam",]

print(friends[0])
print(friends[1])
print(friends[2])
print(friends[3])
```

    Wanda
    Abby
    Ray
    Sam


### 3-2. Greetings:


```python
message = ", I'm proud to call you my friend"

print(friends[0] + message)
print(friends[1] + message)
print(friends[2] + message)
print(friends[3] + message)
```

    Wanda, I'm proud to call you my friend
    Abby, I'm proud to call you my friend
    Ray, I'm proud to call you my friend
    Sam, I'm proud to call you my friend


### 3-3. Your Own List:


```python
transportations = ["Jeepy", "MTA", "Skateboard"]

print(transportations[0] + ", You are my favorite material item in the whole world")
print("Dear " + transportations[1] + ", I know that you're pretty janky but I miss you dearly")
print(transportations[2] + ", one day I'll learn how to use you properly")
```

    Jeepy, You are my favorite material item in the whole world
    Dear MTA, I know that you're pretty janky but I miss you dearly
    Skateboard, one day I'll learn how to use you properly


### 3-4. Guest List: 


```python
guests = ["Malcolm X", "Flora", "Mao"]
message = ", I'd cordially like to invite you to have dinner with me."

print(guests[0] + message)
print(guests[1] + message)
print(guests[2] + message)
```

    Malcolm X, I'd cordially like to invite you to have dinner with me.
    Flora, I'd cordially like to invite you to have dinner with me.
    Mao, I'd cordially like to invite you to have dinner with me.


### 3-5. Changing Guest List: 


```python
#Run with 3-4
print("\nHi " + guests[2] + ", I'm so sorry to hear that you can't make it because you're too busy commiting crimes against humanity in the name of perverting Marxism. You will be missed dearly\n")
guests[2] = "Marx"
print(guests[0] + message)
print(guests[1] + message)
print(guests[2] + message + "\n")

#For 3-6
print("Hi all, WONDERFUL news! I've found a larger table for us which means that we can invite more friends to join us!")
```

    
    Hi Mao, I'm so sorry to hear that you can't make it because you're too busy commiting crimes against humanity in the name of perverting Marxism. You will be missed dearly
    
    Malcolm X, I'd cordially like to invite you to have dinner with me.
    Flora, I'd cordially like to invite you to have dinner with me.
    Marx, I'd cordially like to invite you to have dinner with me.
    
    Hi all, WONDERFUL news! I've found a larger table for us which means that we can invite more friends to join us!


### 3-6. More Guests: 


```python
#Run with 3-4 and 3-5
guests.insert(0,"Angelina Jolie")
guests.insert(2, "Angela Davis")
guests.append("Liang")
print(guests[0] + message)
print(guests[1] + message)
print(guests[2] + message)
print(guests[3] + message)
print(guests[4] + message)
print(guests[5] + message)
```

    Angelina Jolie, I'd cordially like to invite you to have dinner with me.
    Malcolm X, I'd cordially like to invite you to have dinner with me.
    Angela Davis, I'd cordially like to invite you to have dinner with me.
    Flora, I'd cordially like to invite you to have dinner with me.
    Marx, I'd cordially like to invite you to have dinner with me.
    Liang, I'd cordially like to invite you to have dinner with me.


### 3-7. Shrinking Guest List: 


```python
#Run with 3-4, 3-5, and, 3-6
print("Hi all, TERRIBLE NEWS! Our decievingly wonderful table will not be here on time and I only have room for two of the six that I invited\n")

message = ", I'm so sorry. Let's grab a meal at Dewick soon though!"

#Removing guests from list and sending them a message
disinvited = guests.pop()
print(disinvited + message)
disinvited = guests.pop()
print(disinvited + message)
disinvited = guests.pop()
print(disinvited + message)
disinvited = guests.pop()
print(disinvited + message + "\n")

#Confirming dinner with two remaining guests
message = ", Din-Din tonight?"
print(guests[0] + message)
print(guests[1] + message)

#removing final guests from list and printing empty list 
del guests[0]
del guests[0]
print("\n")
print(guests)
```

    Hi all, TERRIBLE NEWS! Our decievingly wonderful table will not be here on time and I only have room for two of the six that I invited
    
    Liang, I'm so sorry. Let's grab a meal at Dewick soon though!
    Marx, I'm so sorry. Let's grab a meal at Dewick soon though!
    Flora, I'm so sorry. Let's grab a meal at Dewick soon though!
    Angela Davis, I'm so sorry. Let's grab a meal at Dewick soon though!
    
    Angelina Jolie, Din-Din tonight?
    Malcolm X, Din-Din tonight?
    
    
    []


### 4-1. Pizzas:


```python
pizzas = ["veggie", "bbq chicken", "eggplant"]
for pizza in pizzas:
    print(f"I like {pizza} pizza!")
print("\nPizza is an incredible food group!")
```

    I like veggie pizza!
    I like bbq chicken pizza!
    I like eggplant pizza!
    
    Pizza is an incredible food group!


### 4-2. Animals:


```python
animals = ["giraffe", "dinosaur", "lion"]
for animal in animals:
    print(f"A {animal} would make a great pet!")
print("These three animals all would be incredible pets!")
```

    A giraffe would make a great pet!
    A dinosaur would make a great pet!
    A lion would make a great pet!
    These three animals all would be incredible pets!


### 4-3. Counting to Twenty:


```python
numbers = []
for number in range(1,21):
    numbers.append(number)
print(numbers)
```

    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]


### 4-10. Slices:


```python
numbers = list(range(1,20,2))
for number in numbers:
    print(number)
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


### 4-10. Slices: 


```python
numbers = list(range(0,10))

print(f"The first three items in the list are: {numbers[:3]}")
print(f"Three items from the middle of the list are: {numbers[3:6]}")
print(f"The last three items in the list are: {numbers[7:10]}")
```

    The first three items in the list are: [0, 1, 2]
    Three items from the middle of the list are: [3, 4, 5]
    The last three items in the list are: [7, 8, 9]


### 4-11. My Pizzas, Your Pizzas:


```python
friends_pizzas = pizzas[:]
friends_pizzas.append("sausage")

print("My favorite pizzas are: ")
for pizza in pizzas:
    print(pizza)

print("\nMy friend’s favorite pizzas are:")
for pizza in friends_pizzas:
    print(pizza)
```

    My favorite pizzas are: 
    veggie
    bbq chicken
    eggplant
    
    My friend’s favorite pizzas are:
    veggie
    bbq chicken
    eggplant
    sausage



```python

```
