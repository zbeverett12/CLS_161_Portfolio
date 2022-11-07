---
layout: page
title: Downloading Web Pages with Python
description: This lesson introduces Uniform Resource Locators (URLs) and explains how to use Python to download and save the contents of a web page to your local hard drive.


---

## Source 
William J. Turkel and Adam Crymble, "Downloading Web Pages with Python," Programming Historian 1 (2012), https://doi.org/10.46430/phen0021.


## Opening URLs with Python: open-webpage.py


```python
#Opens file from URL, reads it into a Python string called webContent, prints the first 300 Characters 
import urllib.request, urllib.error, urllib.parse

url = 'http://www.oldbaileyonline.org/browse.jsp?id=t17800628-33&div=t17800628-33'

response = urllib.request.urlopen(url)
webContent = response.read().decode('UTF-8')

print(webContent[0:300])
```

    
    
    
    
    
    
    
    
    
    
    
    
    
    
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
    <head>
    	<title>Browse - Central Criminal Court</title>
    	<meta http-equiv="content-type" content=


## Saving a Local Copy of a Web Page: save-webpage.py


```python
# save-webpage.py

import urllib.request, urllib.error, urllib.parse

url = 'http://www.oldbaileyonline.org/browse.jsp?id=t17800628-33&div=t17800628-33'

response = urllib.request.urlopen(url)
webContent = response.read().decode('UTF-8')

f = open('obo-t17800628-33.html', 'w')
f.write(webContent)
f.close
```




    <_io.TextIOWrapper name='obo-t17800628-33.html' mode='w' encoding='UTF-8'>




```python

```


## Reflection 

In a lot of my student life, I have struggled with how to save a webpage: the exact concept that this Programming Historian lesson tackles. I have basically tried everything: saving something as an HTML document, taking single screenshots, and recently, settling on a chrome attachment “GoFullPage” which is able to create a PDF/JPEG file of what is listed in a website which I then upload to Notability to annotate on my iPad. I had hoped that the programming historian lesson may be able to provide an alternate solution. 

Despite its alluring name, the lesson actually just provides somewhat basic code which simply reads HTML code into a new file and saves it. While I could be wrong, it seems to just be what happens on the back end if a user were to do “File > Save Page As…” What is saved is still data that requires cleaning as it has all the HTML tags. It’s definitely helpful as I continue my search to find an accessible way to download content from web pages and be able to navigate them in an accessible way, but unfortunately, the lesson did not necessarily provide that. 