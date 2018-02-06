
__Shakespeare's Sonnets__

Using Lists and Dictionaries to find novel words in Shakespeare's sonnets.

I will start with the code below and as the coding exercise moves forward you'll notice how its being optimized.


```python
import time
import os

my_words = [elt.strip() for elt in open('sonnet_words.txt', 'r').readlines()]
word_list = [elt.strip() for elt in open('sowpods.txt', 'r').readlines()]

counter = 0

start = time.time()

for word in my_words:
    if word not in word_list:
        print(word)
        counter += 1
        
stop = time.time()
        
print('Total new words: %d' % counter)
print('Tiem elapsed: %.5f seconds' % (stop-start))
```

    ADDETH
    AMAZETH
    APRIL
    BEATED
    BURIEST
    CONVERTEST
    DEBATETH
    DECEIVEST
    DEPARTEST
    DIEST
    DISDAINETH
    FADETH
    GAZETH
    GLUTTONING
    GOEST
    HATETH
    JUNES
    MAKETH
    MATCHETH
    NURSETH
    POSSESSETH
    PRESENTETH
    PRIVILAGE
    RECEIVEST
    REELETH
    REFUSEST
    RENEWEST
    RESPOSE
    REVIEWEST
    SATURN
    SEETING
    STAINETH
    TEACHEST
    TEMPTETH
    USEST
    VIEWEST
    Total new words: 36
    Tiem elapsed: 7.48644 seconds


__Run time with Big 'O'__

Running the code took over seven seconds to complete?  Let's explore why?

The reason why is because we are iterating through the entire word list one word at a time.  In other words the for loop iterates our variable ```word_list``` for every single word found in our variable ```my_words```. 

Lists are big 'O' of 'n'.  Its run time is O(n).

__Optimizing with Dictionary__

Lets optimize the code by creating a ```word_dict```.  Dictionaries have hash functions that point directly to a key, if it exists.   It's the hash function that allows dictionaries to be extremely fast with a run time of O( i ).

Our new variable ```word_dict``` will store a key:value pair of the elements in our ```word_list```.  For the value in our key:value pair we will simply have a place holder. 


```python
my_words = [elt.strip() for elt in open('sonnet_words.txt', 'r').readlines()]
word_list = [elt.strip() for elt in open('sowpods.txt', 'r').readlines()]
word_dict = dict((elt, 1) for elt in word_list)

counter = 0

start = time.time()

for word in my_words:
    if word not in word_dict:
        print(word)
        counter += 1
        
stop = time.time()
        
print('Total new words: %d' % counter)
print('Tiem elapsed: %.5f seconds' % (stop-start))
```

    ADDETH
    AMAZETH
    APRIL
    BEATED
    BURIEST
    CONVERTEST
    DEBATETH
    DECEIVEST
    DEPARTEST
    DIEST
    DISDAINETH
    FADETH
    GAZETH
    GLUTTONING
    GOEST
    HATETH
    JUNES
    MAKETH
    MATCHETH
    NURSETH
    POSSESSETH
    PRESENTETH
    PRIVILAGE
    RECEIVEST
    REELETH
    REFUSEST
    RENEWEST
    RESPOSE
    REVIEWEST
    SATURN
    SEETING
    STAINETH
    TEACHEST
    TEMPTETH
    USEST
    VIEWEST
    Total new words: 36
    Tiem elapsed: 0.01049 seconds


We have optimized our code to run in __less than a second!!!__

__Set Data Structure__

The code above works well but we're creating a key:value pair where the key is a word form our ```word_list``` and the value is simple place holder.  We can optimize this code further by using a Python ```set()``` rather than a dictionary.

Sets in Python are very similar to Python dictionaries in that they are both hashed but sets do not have key:value pairs.  Sets are not allowed to have duplicated values and ordering does not matter. 


```python
my_words = [elt.strip() for elt in open('sonnet_words.txt', 'r').readlines()]
word_list = [elt.strip() for elt in open('sowpods.txt', 'r').readlines()]
word_set = set(word_list)

counter = 0

start = time.time()

for word in my_words:
    if word not in word_set:
        print(word)
        counter += 1
        
stop = time.time()
        
print('Total new words: %d' % counter)
print('Tiem elapsed: %.5f seconds' % (stop-start))
```

    ADDETH
    AMAZETH
    APRIL
    BEATED
    BURIEST
    CONVERTEST
    DEBATETH
    DECEIVEST
    DEPARTEST
    DIEST
    DISDAINETH
    FADETH
    GAZETH
    GLUTTONING
    GOEST
    HATETH
    JUNES
    MAKETH
    MATCHETH
    NURSETH
    POSSESSETH
    PRESENTETH
    PRIVILAGE
    RECEIVEST
    REELETH
    REFUSEST
    RENEWEST
    RESPOSE
    REVIEWEST
    SATURN
    SEETING
    STAINETH
    TEACHEST
    TEMPTETH
    USEST
    VIEWEST
    Total new words: 36
    Tiem elapsed: 0.00660 seconds


__Awesome!!!___  

With a set we have the exact same run time as a dictionary but without the burden of key:value pairs.
