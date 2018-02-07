

```python
import sqlite3
```

Connect sqlite with db via Python interpreter.
```python
connection = sqlite3.connect('jeopardy.db')```

Crate a cursor.
```python 
cursor = connection.cursor()```

Execute a query using hte cursor.
```python
cursor.execute('SELECT name FROM category LIMIT 10')```

*<font color='grey'>We are selecting the name column from the category table and limiting our results to 10.</font>*

Fetch the results from our executed query.
```python
results = cursor.fetchall()
results

[('DETECTIVE FICTION',), ('THE OLD TESTAMENT',), ('ASIAN HISTORY',), ('RIVER SOURCES',), ('WORLD RELIGION',), ('SEAN SONG',), ('ANIMATED MOVIES',), ('NEW YORK CITY',), ('AFRICAN WILDLIFE',), ('LITTLE RED RIDING HOOD',)]```
*<font color='grey'>The results are a list of tuples and inside them are 10 row entries from the ```name``` column.</font>*

We can query the list.
```python
results[0]
('DETECTIVE FICTION',)```

We can query just the string.
```python
results[0][0]
'DETECTIVE FICTION'

results[1][0]
'THE OLD TESTAMENT'```

Iterate through the list and print each.
```python
for category in results:
    print(category[0])

DETECTIVE FICTION
THE OLD TESTAMENT
ASIAN HISTORY
RIVER SOURCES
WORLD RELIGION
SEAN SONG
ANIMATED MOVIES
NEW YORK CITY
AFRICAN WILDLIFE
LITTLE RED RIDING HOOD```

Close the connection.
```python
connection.close()```

We can write a script to help us avoid the repetitiveness.
```python
# script.py
# Goal:
# Print the names of 10 Jeopardy categories.

# SQL:
# SELECT name FROM category LIMIT 10

import sqlite3

connection = sqlite3.connect("jeopardy.db")
cursor = connection.cursor()

cursor.execute("SELECT name FROM category LIMIT 10")
results = cursor.fetchall()

print("Example categories:\n")

connection.close()

```

Lets write a new script to query 3 columns from the clue table.
```python

connection = sqlite3.connect("jeopardy.db")
cursor = connection.cursor()

cursor.execute("SELECT value, text, answer FROM clue LIMIT 10")
results = cursor.fetchall()

print("Example categories:\n")
for clue in results:
    value = clue[0]
    text = clue[1]
    answer = clue[2]
    
    # format the value strint to output [$200]
    # format question as Question: .....
    # format answer as Answer: What is .....
    
    print("[$%s]" % (value,)) # string formating, prints $ sign before value
    print("Question: %s" % (text,))
    print("Answer: What is '%s'?" % (answer,))
    print("")```



__Tuple Unpacking__

We can run the same code above using tuple unpacking.  This produces a single two lines of code in our for loop.
```python
connection = sqlite3.connect("jeopardy.db")
cursor = connection.cursor()

cursor.execute("SELECT value, text, answer FROM clue LIMIT 3")
results = cursor.fetchall()

print("Example categories:\n")
for clue in results:
    value, text, answer = clue # <-- this is tuple unpacking
    
    # format the value strint to output [$200]
    # format question as Question: .....
    # format answer as Answer: What is .....
    
    print("[$%s]" % (value,)) # string formating, prints $ sign before value
    print("Question: %s" % (text,))
    print("Answer: What is '%s'?" % (answer,))
    print("")
    
[$200]
Question: As the Mayan god of merchants, Ek Chuah was responsible for this yummy bean, once the standard May
an currency
Answer: What is 'Cacao bean'?

[$600]
Question: Hagar, carrying this man's baby, fled into the desert after harsh treatment from his wife
Answer: What is 'Abraham'?

[$800]
Question: According to this Old Testament book, this "swords into plowshares" prophet walked naked for 3 yea
rs
Answer: What is 'Isaiah'?```
    




Next we will write a script to query the Jeopardy database for the full set of categories for a game.
```python
import sqlite3

connection = sqlite3.connect("jeopardy.db")
cursor = connection.cursor()

# Get a random game
cursor.execute("SELECT game FROM category ORDER BY random() LIMIT 1")
results = cursor.fetchall()
game_id = results[0][0]
print("Categories for game #%d:" % (game_id))

# Get the categories for that game.
query = """SELECT name, round FROM category
WHERE game=%d ORDER BY round""" % (game_id)
cursor.execute(query)
results = cursor.fetchall()

# TODO: process results
for result in results:
    # round 0 = Jeopardy round
    # round 1 = Double Jeopardy
    # round 2 = Final Jeopardy
    name, round = result
    print("Round %d: %s" % (round, name))
    
connection.close()

Categories for game #1062:
Round 0: PEOPLE IN HISTORY
Round 0: DAD TV
Round 0: GORILLA MY DREAMS
Round 0: ARCH-EOLOGY
Round 0: FOOD GLORIOUS FOOD
Round 0: FIX THE PROVERB
Round 1: LITERATURE
Round 1: DIRECTORS
Round 1: WORD ORIGINS
Round 1: HEIFETZ
Round 1: TUESDAY
Round 1: THIS MUST BE BELGIUM
Round 2: FAMOUS NICKNAMES```


```python

```
