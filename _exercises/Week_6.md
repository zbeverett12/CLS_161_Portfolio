---
layout: page
title: Week 6 Homework
description: Chapter 6: Dictionaries 
---

### Exercises: 6-1, 6-2, 6-3, 6-4, 6-5, 6-7, 6-8, 6-9, 6-11

## 6-1. Person: 
Use a dictionary to store information about a person you know. Store their first name, last name, age, and the city in which they live. You should have keys such as first_name, last_name, age, and city. Print each piece of information stored in your dictionary.


```python
person = {
    'first_name':'zach',
    'last_name':'everett',
    'age': 22,
    'city':"new york",
}

print(person)
```

    {'first_name': 'zach', 'last_name': 'everett', 'age': 22, 'city': 'new york'}


## 6-2. Favorite Numbers: 
Use a dictionary to store people’s favorite numbers. Think of five names, and use them as keys in your dictionary. Think of a favorite number for each person, and store each as a value in your dictionary. Print each person’s name and their favorite number. For even more fun, poll a few friends and get some actual data for your program.


```python
friends = {
    "AJ":7,
    "Becca":21,
    "Carol":3,
    "Delma": 97,
    "Emma": 4
}

print(friends)
```

    {'AJ': 7, 'Becca': 21, 'Carol': 3, 'Delma': 97, 'Emma': 4}


## 6-3. Glossary: 
A Python dictionary can be used to model an actual dictionary. However, to avoid confusion, let’s call it a glossary.

• Think of five programming words you’ve learned about in the previous chapters. Use these words as the keys in your glossary, and store their meanings as values.

• Print each word and its meaning as neatly formatted output. You might print the word followed by a colon and then its meaning, or print the word on one line and then print its meaning indented on a second line. Use the newline character (\n) to insert a blank line between each word-meaning pair in your output.


```python
glossary = {
    'int':"a whole number",
    'float':"a whole number with a decimal or negative",
    'char':"a single character",
    'string':"a series of chars",
    'bool':"a true of false statement"
}
for token in glossary:
    print(f" a {token} is {glossary[token]}.")
```

     a int is a whole number.
     a float is a whole number with a decimal or negative.
     a char is a single character.
     a string is a series of chars.
     a bool is a true of false statement.


## 6-4. Glossary 2:
Now that you know how to loop through a dictionary, clean up the code from Exercise 6-3 (page 102) by replacing your series of print statements with a loop that runs through the dictionary’s keys and values. When you’re sure that your loop works, add five more Python terms to your glossary. When you run your program again, these new words and meanings should automatically be included in the output.


```python
glossary = {
    'int':"a whole number",
    'float':"a whole number with a decimal or negative",
    'char':"a single character",
    'string':"a series of chars",
    'bool':"a true of false statement"
}
for term, definition in glossary.items():
    print(f" a {term} is {definition}.")
```

     a int is a whole number.
     a float is a whole number with a decimal or negative.
     a char is a single character.
     a string is a series of chars.
     a bool is a true of false statement.


## 6-5. Rivers: 
Make a dictionary containing three major rivers and the country each river runs through. One key-value pair might be 'nile': 'egypt'.

• Use a loop to print a sentence about each river, such as The Nile runs through Egypt.

• Use a loop to print the name of each river included in the dictionary.

• Use a loop to print the name of each country included in the dictionary.


```python
rivers = {
    "nile": "egypt",
    "mississippi": "united states", 
    "amazon": "south america"
}
for name, location in rivers.items():
    print(f"The {name.title()} runs through {location.title()}.")
```

    The Nile runs through Egypt.
    The Mississippi runs through United States.
    The Amazon runs through South America.


## 6-7. People: 
Start with the program you wrote for Exercise 6-1 (page 102). Make two new dictionaries representing different people, and store all three dictionaries in a list called people. Loop through your list of people. As you loop through the list, print everything you know about each person.


```python
person_0 = {
    'first_name':'zach',
    'last_name':'everett',
    'age': 22,
    'city':"new york",
}

person_1 = {
    "first_name": "sam",
    "last_name": "markowitz",
    "age":22,
    "city":"Washington DC"
}

person_2 = {
    "first_name":"abby",
    "last_name":"donahue",
    "age":20,
    "city": "boston"
}

people = [person_0, person_1, person_2]
for person in people:
    print(person)
```

    {'first_name': 'zach', 'last_name': 'everett', 'age': 22, 'city': 'new york'}
    {'first_name': 'sam', 'last_name': 'markowitz', 'age': 22, 'city': 'Washington DC'}
    {'first_name': 'abby', 'last_name': 'donahue', 'age': 20, 'city': 'boston'}


## 6-8. Pets: 
Make several dictionaries, where the name of each dictionary is the name of a pet. In each dictionary, include the kind of animal and the owner’s name. Store these dictionaries in a list called pets. Next, loop through your list and as you do print everything you know about each pet.


```python
pet_0 = {
    "name": "scout",
    "kind": "dog",
    "owner": "zach",
}

pet_1 = {
    "name": "poopy",
    "kind": "cat",
    "owner": "alexa"
}

pet_2 = {
    "name": "boo",
    "kind": "dog",
    "owner": "tony"
}

pets = [pet_0, pet_1, pet_2]
for pet in pets:
    print(pet)
```

    {'name': 'scout', 'kind': 'dog', 'owner': 'zach'}
    {'name': 'poopy', 'kind': 'cat', 'owner': 'alexa'}
    {'name': 'boo', 'kind': 'dog', 'owner': 'tony'}


## 6-9. Favorite Places: 
Make a dictionary called favorite_places. Think of three names to use as keys in the dictionary, and store one to three favorite places for each person. To make this exercise a bit more interesting, ask some friends to name a few of their favorite places. Loop through the dictionary, and print each person’s name and their favorite places.


```python
favorite_places = {
    "zach":["granoff", "home", "beach"],
    "ray":["SEC", "lewis"],
    "magi":["eaton", "shoprite"]
}

for name, places in favorite_places.items():
    print(f"\n{name.title()}'s, favorite place(s) are: ")
    for place in places:
        print(place.title())
    


```

    
    Zach's, favorite place(s) are: 
    Granoff
    Home
    Beach
    
    Ray's, favorite place(s) are: 
    Sec
    Lewis
    
    Magi's, favorite place(s) are: 
    Eaton
    Shoprite


## 6-11. Cities: 
Make a dictionary called cities. Use the names of three cities as keys in your dictionary. Create a dictionary of information about each city and include the country that the city is in, its approximate population, and one fact about that city. The keys for each city’s dictionary should be something like country, population, and fact. Print the name of each city and all of the information you have stored about it.


```python
cities = {
    "new_york": {
        "country": "united states",
        "population": 8000000,
        "fact": "new york has the best pizza in the world!",
    },
    "boston": {
        "country": "united states",
        "population": 700000,
        "fact": "there are less bodegas in boston than in new york!",
    },
    "cuenca":{
        "country": "ecuador",
        "population": 436000,
        "fun fact": "cuenca is located in the mountains!",
    },
}

for city, city_info in cities.items():
    print(f"{city} {city_info}")
```

    new_york {'country': 'united states', 'population': 8000000, 'fact': 'new york has the best pizza in the world!'}
    boston {'country': 'united states', 'population': 700000, 'fact': 'there are less bodegas in boston than in new york!'}
    cuenca {'country': 'ecuador', 'population': 436000, 'fun fact': 'cuenca is located in the mountains!'}

