---
layout: page
title: Week 9 Homework
description: Chronicling America API 
---

## Chronicling America API Assignment
In this assignment, you are tasked with:
* searching Chronicling America's API for a key word of your choice
* parsing your results from a dictionary to a `DataFrame` with headings "title", "city", 'date", and "raw_text"
* processing the raw text by removing "\n" characters, stopwords, and then lemmatizing the raw text before adding it to a new column called "lemmas."
* saving your `DataFrame` to a csv file

If you need any help with this assignment please email micah.saxton@tufts.edu


## imports


```python
import requests
import json
import math
import pandas as pd
import spacy
```

## initial search


```python
url = 'https://chroniclingamerica.loc.gov/search/pages/results/?state=&date1=1945&date2=1963&proxtext=socialism&x=16&y=8&dateFilterType=yearRange&rows=20&searchType=basic&format=json'
response = requests.get(url)  # returns a 'object' representing the webpage
raw = response.text  # the text attribute contains the text from the web page as a string
results = json.loads(raw)  # the loads method from the json library transforms the string into a dict
```


```python
results.keys()
```




    dict_keys(['totalItems', 'endIndex', 'startIndex', 'itemsPerPage', 'items'])




```python
print('totalItems:', results['totalItems'])
print('endIndex:', results['endIndex'])
print('startIndex:', results['startIndex'])
print('itemsPerPage:', results['itemsPerPage'])
print('Length and type of items:', len(results['items']), type(results['items']))
```

    totalItems: 209609
    endIndex: 20
    startIndex: 1
    itemsPerPage: 20
    Length and type of items: 20 <class 'list'>


## find total amount of pages


```python
# find total amount of pages
total_pages = math.ceil(results['totalItems'] / results['itemsPerPage'])
print(total_pages)
```

    10481


## query the api and save to dict 


```python
# query the api and save to dict 
data = []
start_date = '1945'
end_date = '1963'
search_term = 'socialism'
for i in range(1, 11):  # for sake of time I'm doing only 10, you will want to put total_pages+1
    url = (f'https://chroniclingamerica.loc.gov/search/pages/results/?state=&date1={start_date}'
           f'&date2={end_date}&proxtext={search_term}&x=16&y=8&dateFilterType=yearRange&rows=20'
           f'&searchType=basic&format=json&page={i}')  # f-string
    response = requests.get(url)
    raw = response.text
    print(response.status_code)  # checking for errors
    results = json.loads(raw)
    items_ = results['items']
    for item_ in items_:
        temp_dict = {}
        temp_dict['title'] = item_['title_normal']
        temp_dict['city'] = item_['city']
        temp_dict['date'] = item_['date']
        temp_dict['raw_text'] = item_['ocr_eng']
        data.append(temp_dict)
```

    200
    200
    200
    200
    200
    200
    200
    200
    200
    200


## convert dict to dataframe



```python
df = pd.DataFrame.from_dict(data)
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
      <th>title</th>
      <th>city</th>
      <th>date</th>
      <th>raw_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>evening star.</td>
      <td>[Washington]</td>
      <td>19580921</td>
      <td>&gt;; sy '\n■ •■ / ;, • .\nWill you leave these f...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>valley settler.</td>
      <td>[Palmer]</td>
      <td>19460801</td>
      <td>Storage\nCACHE YOUR\nFOOD\nTHE\nMODERN WAY\n' ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>automotive news.</td>
      <td>[Detroit]</td>
      <td>19451022</td>
      <td>Itai/ck section\nWash. Idaho\nAgreement\nOn Re...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>valley settler.</td>
      <td>[Palmer]</td>
      <td>19460228</td>
      <td>PALMER, ALASKA Dorothy Boll Editor St Publishe...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>chicago star.</td>
      <td>[Chicago]</td>
      <td>19480724</td>
      <td>* — 1\nThe Chicago\nVol. 3. No. 30\nPublished\...</td>
    </tr>
  </tbody>
</table>
</div>



## convert date column from string to date-time object



```python
df['date'] = pd.to_datetime(df['date'])
sorted_df = df.sort_values(by='date')
```

## write fuction to process text



```python
nlp = spacy.load("en_core_web_sm")
nlp.disable_pipes('ner', 'parser')  # these are unnecessary for the task at hand

junk_words = ['hesse']  # you can add any words you want removed here

def process_text(text):
    """Remove new line characters and lemmatize text. Returns string of lemmas"""
    text = text.replace('\n', ' ')
    doc = nlp(text)
    tokens = [token for token in doc]
    no_stops = [token for token in tokens if not token.is_stop]
    no_punct = [token for token in no_stops if token.is_alpha]
    lemmas = [token.lemma_ for token in no_punct]
    lemmas_lower = [lemma.lower() for lemma in lemmas]
    lemmas_string = ' '.join(lemmas_lower)
    return lemmas_string
```

## apply process_text function to raw_text column



```python
sorted_df['lemmas'] = sorted_df['raw_text'].apply(process_text)
sorted_df.head()
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
      <th>title</th>
      <th>city</th>
      <th>date</th>
      <th>raw_text</th>
      <th>lemmas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>117</th>
      <td>coolidge examiner.</td>
      <td>[Coolidge]</td>
      <td>1945-03-30</td>
      <td>Page Six\nCooli\nPUBLISHED EVERY FRIDAY MORNIN...</td>
      <td>page cooli published friday morning enter seco...</td>
    </tr>
    <tr>
      <th>40</th>
      <td>proletarec.</td>
      <td>[Chicago]</td>
      <td>1945-05-30</td>
      <td>A Yugoslav Weekly Devoted to the\nInterest of ...</td>
      <td>yugoslav weekly devoted interest workers offic...</td>
    </tr>
    <tr>
      <th>195</th>
      <td>detroit evening times.</td>
      <td>[Detroit]</td>
      <td>1945-06-12</td>
      <td>End the Pacific War VICTORIOUSLY. Make the Pea...</td>
      <td>end pacific war victoriously peace permanently...</td>
    </tr>
    <tr>
      <th>49</th>
      <td>detroit evening times.</td>
      <td>[Detroit]</td>
      <td>1945-07-04</td>
      <td>End the Pacific War VICTORIOUSLY. Make the Pea...</td>
      <td>end pacific war victoriously peace permanently...</td>
    </tr>
    <tr>
      <th>76</th>
      <td>detroit evening times.</td>
      <td>[Detroit]</td>
      <td>1945-07-06</td>
      <td>End the Pacific War VICTORIOUSLY. Make the Pea...</td>
      <td>end pacific war victoriously peace permanently...</td>
    </tr>
  </tbody>
</table>
</div>



## save to csv



```python
sorted_df.to_csv(f'../data/{search_term}{start_date}-{end_date}.csv', index=False)
`````