---
layout: page
title: From HTML to List of Words (part 1 and 2)
description: In this two-part lesson, we will build on what you’ve learned about Downloading Web Pages with Python, learning how to remove the HTML markup from the webpage of Benjamin Bowsey’s 1780 criminal trial transcript. We will achieve this by using a variety of string operators, string methods, and close reading skills. We introduce looping and branching so that programs can repeat tasks and test for certain conditions, making it possible to separate the content from the HTML tags. Finally, we convert content from a long string to a list of words that can later be sorted, indexed, and counted.

---

## Source
William J. Turkel and Adam Crymble, "From HTML to List of Words (part 1)," Programming Historian 1 (2012), https://doi.org/10.46430/phen0006.

William J. Turkel and Adam Crymble, "From HTML to List of Words (part 2)," Programming Historian 1 (2012), https://doi.org/10.46430/phen0007.

## From HTML to List of Words (part 1)

William J. Turkel and Adam Crymble, "From HTML to List of Words (part 1)," Programming Historian 1 (2012), https://doi.org/10.46430/phen0006.


## Isolating Desired Content
### obo.py


```python
def stripTags(pageContents):
    pageContents = str(pageContents)
    startLoc = pageContents.find("<p>")
    endLoc = pageContents.rfind("<br/>")

    pageContents = pageContents[startLoc:endLoc]
    return pageContents
```

### greet.py


```python
import urllib

url = 'http://www.oldbaileyonline.org/browse.jsp?id=t17800628-33&div=t17800628-33'

response = urllib.request.urlopen(url)
HTML = response.read().decode('UTF-8')

print(stripTags(HTML))
```

    <p>324.                                  <a class="invisible" name="t17800628-33-defend448"> </a>                     BENJAMIN                      BOWSEY                                                                                                          (a blackmoor                  ) was indicted for                                                          that he together with five hundred other persons and more, did, unlawfully, riotously, and tumultuously assemble on the 6th of June                      to the disturbance of the public peace and did begin to demolish and pull down the dwelling house of                                              <a class="invisible" name="t17800628-33-victim450"> </a>                           Richard                            Akerman                                                                                                                                                            , against the form of the statute, &amp;c.                           </p>               <p>                              <a class="invisible" name="t17800628-33-person451"> </a>                  ROSE                   JENNINGS                                                                                       , Esq. sworn.</p>               <p>Had you any occasion to be in this part of the town, on the 6th of June in the evening? - I dined with my brother who lives opposite Mr. Akerman's house. They attacked Mr. Akerman's house precisely at seven o'clock; they were preceded by a man better dressed than the rest, who went up to Mr. Akerman's door; he rapped three times, and I believe pulled the bell as often. Mr. Akerman had barrocadoed his house. When the man found that no one came, he went down the steps, made his obeisance to the mob, and pointed to the door, and then retired.</p>               <p>Have you any recollection how that man who you say had a better appearance than the rest was dressed? - I think he had on a dark brown coat and a round ha, but I cannot be particular as to that; the mob immediately following in that formidable manner made such an impression upon me, that I did not take notice. The mob approached about thirty in number, three a-breast, some with paving mattocks, others with iron crows and chissels; and then followed an innumerable company with bludgeons; they seemed to be the spokes of coach-wheels; they divided, some went to Mr. Akerman's door with the mattocks, some to the felons door, and some to the debtor's door. I was struck with the formidable appearance and order in which they divided and proceeded to destroy the place, the men threw their sticks up at the windows, which they broke and demolished, yet notwith standing these sticks were coming down in showers, two men with a bar, such as brewers servants carry on their shoulders,<div class="facsimile-link-wrapper"><div class="facsimile-link"><span class="facsimile-text"><a href="images.jsp?doc=178006280087">See original</a></span><span class="facsimile-image"><a href="images.jsp?doc=178006280087"><img class="facsimile-image-img" src="i/genericThumb.jpg" alt="Click to see original"/></a></span></div></div> attacked the parlour window to force it open. The window-shutters were exceedingly tough; they at last forced them partly open, but not quite. I then saw a man in a sailor's jacket helped up, he forced himself neck and heels into the window. They found the house-door still difficult to get open; before it was got open the other parlour window was opened and the mob were throwing the goods out at the window; at last the house-door gave way; about the same time some of the goods and furniture having been thrown out into the street, a fire was kindled.</p>               <p>They proceeded immediately to throw the goods out of the house? - Immediately. An equal degree of activity seemed to exhibit itself on the outside as within, one party to burn, the other to throw out the goods of Mr. Akerman. When the conflagration took place I applied my mind to the mob.</p>               <p>Was Mr. Akerman's house on fire then? - No. I was situated in the one-pair-of-stairs room, and could see what happened. I endeavoured to form a distinction between the active and inactive people. I thought I did so; the inactive people seemed to form a circle. I observed a person better dressed than the rest among those within the circle, who did not meddle, but seemed to be exciting and encouraging others. I saw several genteel looking men, and amongst them a black; there was one genteel man in particular, whose conduct I confess excited my indignation, and I took particular notice of him. I went down amongst the mob; I spoke to him; I made myself master of his voice; I believe if I was out of his sight I could swear to his voice; I have never seen that man since. When I first saw the black I turned to a lady and said, this is a motley crew, and of every colour. Mr. Akerman's house had then catched fire; the house in which I was was in extreme danger; my self with some others went down to desire the mob to prevent the houses of innocent people catching fire; and the mob were as active in saving those as in destroying Mr. Akerman's. I had no opportunity of making any remarks till I went to my station again, then I believe it was near nine o'clock; I heard a cry and a gingling of keys in the hands of some person; there were three or four genteel persons, but who had the keys I cannot say. Amongst them was the prisoner at the bar; he was without his hat, and his hands were down. I thought he might have his hat in his hand. The house I think was at that time destroyed; the roof was fallen in. Then those persons of the genteeler description moved off towards Smithfield, and amongst them was the prisoner.</p>               <p>You had observed the black in the mob before you went down? - I had.</p>               <p>Are you able to say who that black was? - No. Seeing this man afterwards I took it for granted it was him; I was certain to him the second time; he had his hat off in the middle of the mob.</p>               <p>Jury. You said his hands were down, did you see any thing in his hands? - No, I did not; I took it for granted he had his hat in his hand, not having it on his head.</p>               <p>Cross Examination.</p>               <p>There were I believe other blacks in the mob? - I never saw but one; I saw a black at first, but did not remark him so as to swear to him.</p>               <p>You could not swear to him I suppose from the difficulty every man has in his mind to swear to any black? - Yes.</p>               <p>There is more difficulty to swear to a black than to a white man? - No. The second time I made my remark too judiciously to err.</p>               <p>When was it you first saw the black? - After the goods were first set on fire, which was about a quarter after seven o'clock.</p>               <p>What dress had the black on? - Something of a dark colour, but my remark was on his face.</p>               <p>What w as remarkable in that man's face more than another black? - The make of his hair was one thing; the curls were out if he had had any; and his hair smooth on his head. His face was so exposed to my view the second time, that I could not be better situated to make any remark on his face.</p>               <p>                  <div class="facsimile-link-wrapper"><div class="facsimile-link"><span class="facsimile-text"><a href="images.jsp?doc=178006280088">See original</a></span><span class="facsimile-image"><a href="images.jsp?doc=178006280088"><img class="facsimile-image-img" src="i/genericThumb.jpg" alt="Click to see original"/></a></span></div></div>His hair was the thing by which you knew him? - His hair and his face.</p>               <p>What was particular in his face? - I cannot distinguish it any other than from the weight of the impression it made on me.</p>               <p>Counsel for the Crown. Have you any doubt about him? - No.</p>               <p>                              <a class="invisible" name="t17800628-33-person452"> </a>                  ANN                   WOOD                                                                                        sworn.</p>               <p>I live at Mr. Jennings's, opposite Mr. Akerman's house.</p>               <p>Was you at home on the Tuesday evening when Mr. Akerman's house was attacked? - I was.</p>               <p>Did you in the course of that evening see the prisoner? - I did. It was a little after seven o'clock; I saw him in Mr. Akerman's two-pair-of-stairs room, he stood against the window with something in his hand and looked at me for some time before I observed particularly what he was doing. I looked at him then, and he took up something off the ground and held it up to me; when he held it up, I went down from the window into the dining-room; I came up again, and he was there still. He seemed to be looking in a drawer upon the floor, and seemed to be doing some thing up into a bundle.</p>               <p>You was in the two-pair-of-stairs room opposite him? - No, I was in the three-pair-of-stairs room.</p>               <p>Did you afterwards see him do any thing else? - He got up and looked at me and nodded his head at me; then I went down stairs.</p>               <p>You saw him again in the course of the evening? - Yes, I saw him an hour or two afterwards in the mob.</p>               <p>From the observation you made of his person are you sure that is the man? - That is the man.</p>               <p>Have you any doubt about it? - No, none at all.</p>               <p>Cross Examination.</p>               <p>What makes you so positive that this is the man? - I know his face perfectly again by his standing and looking at me so long.</p>               <p>You recollect him only by his face? - His face and his hair.</p>               <p>Did you see any other black there? - Yes, I did; not in the house but in the mob.</p>               <p>Could you swear to him? - I do not know that I could. I took more notice of this man than I did of any other.</p>               <p>Court. What were the other people doing when the prisoner was in the two-pair-of-stairs room? - Some of the mob were pulling the house down, and some were running in with the fire to set the parlour on fire.</p>               <p>Jury. How many times did you see this prisoner? - Two or three times.</p>               <p>Had he his hat on when you saw him? - Yes.</p>               <p>                              <a class="invisible" name="t17800628-33-person453"> </a>                  ANN                   LESSAR                                                                                        sworn.</p>               <p>Do you know the prisoner? - Yes.</p>               <p>Where do you live? - I lodge in the same lodging, in which the prisoner lodged; I took the lodging of him and the landlady.</p>               <p>Do you remember his coming to you and bringing you any stockings? - He gave me three pair of stockings to mark.</p>               <p>What mark did he bid you put upon them? - Any kind of mark to distinguish them at the washerwoman's. I put BB, the initials of his name upon them.</p>               <p>Had he left a trunk in the room? - Yes, the trunk was found there by the constable when he came; it was locked, he had the key of it.</p>               <p>Who had the key of the room? - I had; nobody could get at the box without my knowledge.</p>               <p>                              <a class="invisible" name="t17800628-33-person454"> </a>                  PERCIVAL                   PHILLIPS                                                                                        sworn.</p>               <p>I am a constable. I searched the lodging of the prisoner last Tuesday-week.</p>               <p>Did you find a trunk there? - I did.</p>               <p>Did you find any thing in that trunk? - Yes; these stockings, this pocket book, and a handkerchief. (producing them.)</p>               <p>Any thing else? - This key (producing it) was upon the shelf in the lodging.</p>               <p>Mr.                <a class="invisible" name="t17800628-33-person455"> </a>                  RICHARD                   AKERMAN                                                                                        sworn.</p>               <p>This pocket-book, I believe, has been in my possession thirty years; it was, I believe, in one of the drawers belonging to my wife; here are several of my banker's cheques which had my name to them.</p>               <p>Look at the stockings? - Here is a very remarkable pair which I had made for me, and the maker wove the initials of my<div class="facsimile-link-wrapper"><div class="facsimile-link"><span class="facsimile-text"><a href="images.jsp?doc=178006280089">See original</a></span><span class="facsimile-image"><a href="images.jsp?doc=178006280089"><img class="facsimile-image-img" src="i/genericThumb.jpg" alt="Click to see original"/></a></span></div></div> name in them in open work; the prisoner has put the initials of his name (B B) over it; they were in the drawers in a one-pair of stairs room. Here are several others that were marked by my sister, they are mine; I believe the handkerchiefs to be mine, but there are no particular marks on them; there are a pair of stockings that were taken off the prisoner's legs, which has the name cut out.</p>               <p>To Phillips. Did you take them off the prisoner's legs? - I did.</p>               <p>To Mr. Akerman. Is the place that is cut out the place where the name was wove? - Yes. This is a remarkable key; it is a key of the Park, it has a crown and my name at length upon it.</p>               <p>To Lessar. Do you know any thing of the key that was found in the lodging? - No, it was on the shelf when he had the lodging?</p>               <p>Was it there when he left the lodging? - I believe it was there; I saw it once or twice; I never knew the meaning of the key.</p>               <p>Prisoner. My Lord, please to ask that woman if she did not wash the handkerchief the things were tied up in? - I washed a blue-and-white silk handkerchief, I cannot swear it was this, it was all over mud. I washed it on the Thursday, the first week that I was in the house.</p>               <p>Was that after the burning of Newgate? - Yes. I was not in town till it was burnt.</p>               <p>Prisoner. I leave my defence to my counsel and my witnesses.</p>               <p>For the prisoner.</p>               <p>Dr. SANDIMAN sworn.</p>               <p>Do you know the prisoner? - Yes, I knew him five years ago, he lived with a relation of mine; he bore an exceeding good character; he used to come backwards and forwards to my house.</p>               <p>                              <a class="invisible" name="t17800628-33-person456"> </a>                  ROBERT                   GATES                                                                                        sworn.</p>               <p>I am footman to Mr. Goodhousen in Golden Square.</p>               <p>Do you know the prisoner? - I do; I have known him perfectly well from the second day after he came to England, which is six years ago; he lived with a person I knew in America, that person gave him an excellent character, and he has always borne a good character since I knew him.</p>               <p>                              <a class="invisible" name="t17800628-33-person457"> </a>                  GRACE                   ROBERTS                                                                                        sworn.</p>               <p>The prisoner lay at our house the night that the prison was burnt.</p>               <p>What time did you see him that night? - I am not positive to the hour he came in, it was from nine to eleven o'clock.</p>               <p>What time did he come home? - I am not positive to the hour, it was a little after nine.</p>               <p>Are you positive of that? - Yes.</p>               <p>Where do you live? - At No. 3, in Berner's-street.</p>               <p>He came home a little after nine? - Yes, I am certain of it; he continued there all that night till six in the morning, and was never out of the house.</p>               <p>What day was that? - The 6th of June.</p>               <p>What day of the week? - I am not certain.</p>               <p>Are you sure it was the night the prison was burnt? - I am.</p>               <p>What prison? - I am not certain what prison, I heard it mentioned in the family that the prison was burnt down.</p>               <p>Cross Examination.</p>               <p>Who bid you to remember the 6th of June? - I remember it by the people being taken up.</p>               <p>When did you talk of its being the 6th of June? - I know he lay at our house on the 6th of June.</p>               <p>Did you take notice of any other night when he lay there? - No.</p>               <p>Did not he lie there on the 7th and 8th of June? - No, only that night.</p>               <p>You are an acquaintance of his? - Yes.</p>               <p>Is he a married man? - I cannot say.</p>               <p>Did he bring any body with him? - No.</p>               <p>Did he lie by himself? - Yes, I gave him a candle to light him to bed.</p>               <p>Did you know he was to lie there that night? - Yes, he told my fellow servant so.</p>               <p>You are a servant, are you? - Yes.</p>               <p>Did your master know that this man was to lie in the house? - I cannot tell.</p>               <p>Do you let such persons lie in the house without your master's knowledge? - He was an old servant, he lay in the servants hall.</p>               <p>Other servants lie there? - Yes, there was a black lay there.</p>               <p>                  <div class="facsimile-link-wrapper"><div class="facsimile-link"><span class="facsimile-text"><a href="images.jsp?doc=178006280090">See original</a></span><span class="facsimile-image"><a href="images.jsp?doc=178006280090"><img class="facsimile-image-img" src="i/genericThumb.jpg" alt="Click to see original"/></a></span></div></div>                              <a class="invisible" name="t17800628-33-person458"> </a>                  JOHN                   NORTHINGTON                                                                                        (a Black) sworn.</p>               <p>I am servant to Mr. Wood.</p>               <p>Did the prisoner lie at your house? - Yes, on the night that Holbourn was on fire.</p>               <p>When the house of Mr. Langdale was on fire? - Yes, the man that lives in Holbourn.</p>               <p>Counsel for the Crown. That was on Wednesday night, the 7th?</p>               <p>To Roberts. Where did the prisoner use to sleep at other times? - In the same bed.</p>               <p>That was when he was a servant there? - Yes.</p>               <p>When he was not a servant there where did he sleep? - He never lay at our house when he was not a servant but that night; I cannot be positive to the night nor the day of the week; I say nothing but the truth.</p>               <p>Prisoner to                <a class="invisible" name="t17800628-33-person459"> </a>                  Ann                   Wood                                                                                       . What dress had I on that night? - A light brownish coat, a round hat, and a red waistcoat.</p>               <p>                                                      GUILTY             (                                                         Death            .)</p>               <p>Tried by the Second London Jury before Mr. Justice NARES.</p>            </div>
    					


## From HTML to List of Words (part 2)

## The stripTags Routine


```python
# obo.py
def stripTags(pageContents):
    pageContents = str(pageContents)
    startLoc = pageContents.find("<p>")
    endLoc = pageContents.rfind("<br/>")

    pageContents = pageContents[startLoc:endLoc]

    inside = 0
    text = ''

    for char in pageContents:
        if char == '<':
            inside = 1
        elif (inside == 1 and char == '>'):
            inside = 0
        elif inside == 1:
            continue
        else:
            text += char

    return text
```


```python
myText = "This is my <h1>HTML</h1> message"

theResult = stripTags(myText)
```

### string-to-list.py


```python
# some strings
s1 = 'hello world'
s2 = 'howdy world'

# list of characters
charlist = []
for char in s1:
    charlist.append(char)
print(charlist)

# list of 'words'
wordlist = s2.split()
print(wordlist)
```

    ['h', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd']
    ['howdy', 'world']


### #html-to-list1.py


```python
import urllib.request, urllib.error, urllib.parse

url = 'http://www.oldbaileyonline.org/print.jsp?div=t17800628-33'

response = urllib.request.urlopen(url)
html = response.read().decode('UTF-8')
text = stripTags(html)
wordlist = text.split()

print((wordlist[0:120]))
```

    ['324.', 'BENJAMIN', 'BOWSEY', '(a', 'blackmoor', ')', 'was', 'indicted', 'for', 'that', 'he', 'together', 'with', 'five', 'hundred', 'other', 'persons', 'and', 'more,', 'did,', 'unlawfully,', 'riotously,', 'and', 'tumultuously', 'assemble', 'on', 'the', '6th', 'of', 'June', 'to', 'the', 'disturbance', 'of', 'the', 'public', 'peace', 'and', 'did', 'begin', 'to', 'demolish', 'and', 'pull', 'down', 'the', 'dwelling', 'house', 'of', 'Richard', 'Akerman', ',', 'against', 'the', 'form', 'of', 'the', 'statute,', '&amp;c.', 'ROSE', 'JENNINGS', ',', 'Esq.', 'sworn.', 'Had', 'you', 'any', 'occasion', 'to', 'be', 'in', 'this', 'part', 'of', 'the', 'town,', 'on', 'the', '6th', 'of', 'June', 'in', 'the', 'evening?', '-', 'I', 'dined', 'with', 'my', 'brother', 'who', 'lives', 'opposite', 'Mr.', "Akerman's", 'house.', 'They', 'attacked', 'Mr.', "Akerman's", 'house', 'precisely', 'at', 'seven', "o'clock;", 'they', 'were', 'preceded', 'by', 'a', 'man', 'better', 'dressed', 'than', 'the', 'rest,', 'who', 'went', 'up', 'to']


## Reflection

Despite my initial dissapointment with the the 2nd lesson that I did, these final ones certainly made up for it. Using a fairly small amount of code, this program is fully able to convert the web pages contents from oldbailyonline and convert it into a list of words which is now clean data. This is data that we could apply a number of techniques from class to like topic modeling or natural language processing. It's all pretty impressive. 

I will say that of the three lessons, my favorite is still the first on Bokeh and Pandas. I really liked the data visualization aspect of the lesson and thought that it was more interactive than the following two. In that lesson, it was really cool creating something then being able to play with it in a way that the following two lessons did not. That being said, I continue to be impressed with the work that Programing Historian does and the relative information accessability that their lessons have provided. 