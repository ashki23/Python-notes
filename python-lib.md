# Python standard library
*[Ashkan Mirzaee](https://ashki23.github.io/index.html)*

Python standard library includes about 220 modules and 54 built-in
functions. Each of these modules designed for specific purposes and
includes several functions (beside the built-in functions) and most of
the users might never use many of them (use `help('modules')` to see
list of the modules). On the other hand, built-in functions are very
limited and it is not hard to learn and apply most of them.

In this tutorial we will learn more about Python built-in functions and
some useful modules for general Python users.

Sources:

  - [Python built-in
    functions](https://docs.python.org/3/library/functions.html)
  - [The Python standard
    library](https://docs.python.org/3/library/index.html)

You might also like these related articles:

  - [Python data structures](https://ashki23.github.io/python-str.html)
  - [Function programming in
    Python](https://ashki23.github.io/python-fun.html)
  - [Virtual environments in
    Python](https://ashki23.github.io/python-env.html)

-----

## Built-in functions

In general we can categorize built-in functions to:

  - Mathematical: `abs`, `divmod`, `max`, `min`, `pow`, `round`,`sum`
  - Logical/test: `all`, `any`, `isinstance`, `issubclass`
  - Structural: `dict`, `bool`, `complex`, `list`, `tuple`, `int`,
    `float`, `str`, `set`, `type`
  - Applicator: `map`, `filter`, `eval`, `exec`,`slice`, `zip`, `len`,
    `reversed`, `sorted`
  - Iteration: `iter`, `enumerate`, `next`, `range`
  - In/out: `input`, `open`, `print`
  - Character converter: `bin`, `chr`, `ord`, `hex`, `oct`, `repr`,
    `ascii`, `format`
  - Variable’s scope/location: `locals`, `globals`, `dir`,`id`
  - Objects: `callable`, `delattr`, `getattr`, `hasattr`, `setattr`

Python operators also are:

  - Arithmetic `+`, `-`, `*`, `/`, `**`, `//`, `%`
  - Indexing: `[`
  - Sequence operator: `:`
  - Identity: `is`, `is not`
  - Logical: `and`, `or`, `not`
  - Membership: `in`, `not in`
  - Assignment: `=`, `+=`, `-=`, `*=`, `/=`, `**=`, `%=`, `//=`
  - Ordering and comparison: `<`, `>`, `<=`, `>=`, `==`, `!=`

The following are some examples for the above functions:

``` python
divmod(6,4)
## (1, 2) ## (quotient,remainder)
(6 // 4, 6 % 4)
## (1, 2)

all([i < 5 for i in [1,2,3]])
## True

all([i < 5 for i in [1,2,10]])
## False

[isinstance(i,str) for i in ['a','b',3]] 
## [True, True, False]

list(map(pow, a, [2]*len(a))) # or
list(map(lambda x: x**2, a)) # or
[x**2 for x in a]
## [1, 9, 25]

list(filter(lambda x: x < 5, a)) # or
[x for x in a if x < 5]
## [1, 3]

a = [1,3,5]
b = [2,4,6]
list(zip(a,b)) # or
list(map(lambda x,y: (x,y), a, b)) 
## [(1, 2), (3, 4), (5, 6)]

[x for x in enumerate(b)]
## [(0, 2), (1, 4), (2, 6)]

[i for i,j in enumerate(b)]
## [0, 1, 2]

[j for i,j in enumerate(b)]
## [2, 4, 6]

x = 4
eval('2 * x**2 + 6')
## 38

exec('z = 40')
z
## 40

locals()/globals()
## Return a dictionary containing the current scope's local/global variables

## For example the following add x_0 = 0, x_1 = 1 and x_2 = 2 to the locals dictionary: 
for i in range(3):
  locals()['x_%s' % i] = i # or exec('x_%s = %s' % (i,i))
x_0,x_1,x_2
## (0, 1, 2)

hex(id(x)) # this is the address of the object x in memory
# '0x1048d7f10'
```

## Library

Python includes a very extensive standard library that offering a wide
range of facilities. We can categorize the below modules as follows:

  - Numeric and mathematical: `math`, `cmath`, `statistics`, `random`
  - File formats: `csv`, `json`
  - Generic operating system services: `os`, `ctypes`, `argparse`,
    `time`
  - System-specific parameters and functions: `sys`
  - File and directory access: `glob`
  - Data persistence: `sqlite3`, `dbm`, `pickle`
  - Functional programming: `itertools`, `functools`, `operator`
  - Text processing services: `srting`, `re`, `readline`
  - Data types: `collections`, `datetime`
  - Software packaging and distribution: `venv`
  - Launching parallel tasks: `concurrent.futures`

The following are some of applications of the above modules.

### Miscellaneous operating system interfaces (`os`)

This module provides a portable way of using operating system dependent
functionality.

``` python
import os

os.system("""
echo $(date) $(hostname) > date_hname.txt
""")
## It will generate date_hname.txt file

os.popen("""
echo $(date) $(hostname)
""").read()
## 'Fri Feb 21 18:19:11 CST 2020 UserHost.local\n' 

lst = os.popen("""
echo $(date) $(hostname)
""").read()[:-1].split(' ')
lst
## ['Fri', 'Feb', '21', '18:19:11', 'CST', '2020', 'UserHost.local']
```

### Unix style pathname pattern expansion (`glob`)

The glob module finds all the pathnames matching a specified pattern
according to the rules used by the Unix shell, although results are
returned in arbitrary order.

``` python
import glob

glob.glob('*.py')
# ['file1.py', 'file2.py']
```

### System-specific parameters and functions (`sys`)

Let’s create the following Python code called `test-sys.py`:

``` python
import sys

filename = sys.argv[0]
usr = sys.argv[1]
host = sys.stdin

print('File name is "%s"' % filename)
print('User "%s" is in %s' % (usr,host.read()))
```

Now, open a Unix Shell and run:

``` python
hostname | python3 test-sys.py buzz
## File name is "test-sys.py"
## User "buzz" is in hostname.local
```

When `argv[0]` is file name, `argv[1]` is user name (buzz) and host name
comes from the Shell pipe as standard input (`stdin`).

### JSON encoder and decoder (`json`)

This module read and write JSON files.

``` python
import json

## read
with open('./input.json', 'r') as jsf:
  input_json = json.load(jsf)

## write
list_dict = [{'title': 'Monty Python and the Holy Grail', 'year': [1975, 'March 14']}]
with open('output.json', 'w') as jso:
    json.dump(list_dict, jso)
```

Note that we read files by system arguments (`sys.argv`) by using `with
open(sys.argv[1], 'r') as jsf`. Also, we can read use standard inputs
(`sys.stdin`) to read the files. For instance the following script,
`jread.py`, read the `output.json` (from the above example) and print
titles:

``` python
import json 
import sys

data = json.load(sys.stdin)

for i in data:
    print(i['title'])
```

Now, open a Unix Shell and run:

``` bash
cat output.json | python jread.py
# Monty Python and the Holy Grail
```

### CSV file reading and writing (`csv`)

This module read and write CSV files.

``` python
import csv

## read to list
with open('./input.csv', 'r') as fl:
    csv_list = list(csv.reader(fl))

print(csv_list)
# [['a', 'b', 'c', 'd'], ['22', 'yes', '5', '0'], ['34', 'no', '7', '8']]

## write from list
with open('output1.csv', 'w') as nfl:
    csv_writer = csv.writer(nfl)
    csv_writer.writerows(csv_list)

## read to dict
with open('./input.csv', 'r') as fl:
    csv_dict = list(csv.DictReader(fl))

print(csv_dict)
# [{'a': '22', 'b': 'yes', 'c': '5', 'd': '0'}, {'a': '34', 'b': 'no', 'c': '7', 'd': '8'}]
    
## write from dict
with open('output2.csv', 'w') as nfl:
    csv_fl = csv.DictWriter(nfl, fieldnames = csv_dict[0].keys())
    csv_fl.writeheader()
    csv_fl.writerows(csv_dict)
```

We can also read CSV files as standard inputs (`sys.stdin`) or as system
arguments (`sys.argv`). For instance the following script, `csvread.py`,
read the `output1.csv` (from the above example) by `sys.stdin`:

``` python
import csv
import sys

data = list(csv.reader(sys.stdin))

for row in data:
    print(row)
```

Now, open a Unix Shell and run:

``` bash
cat output1.csv | python csvread.py
```

### Interface for SQLite (`sqlite3`)

This module provides a SQL interface compliant. Example from [Python
documentation](https://docs.python.org/3/library/sqlite3.html).

``` python
import sqlite3

conn = sqlite3.connect('example.db')
c = conn.cursor()

## create table
c.execute("""CREATE TABLE stocks
             (date text, trans text, symbol text, qty real, price real)""")

## insert a row of data
c.execute("INSERT INTO stocks VALUES ('2006-01-05','BUY','RHAT',100,35.14)")

## save (commit) the changes
conn.commit()

## we can also close the connection if we are done with it
## just be sure any changes have been committed or they will be lost
conn.close()
```

### Container datatypes (`collections`)

This module implements specialized container datatypes providing
alternatives to Python’s general purpose built-in containers, `dict`,
`list`, `set`, and `tuple`.

``` python
import collections

s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
d = collections.defaultdict(list)
for k, v in s:
    d[k].append(v)

sorted(d.items())
# [('blue', [2, 4]), ('red', [1]), ('yellow', [1, 3])]

dict(iter(sorted(d.items())))
# {'blue': [2, 4], 'red': [1], 'yellow': [1, 3]}
```

### Time access and conversions (`time`)

This module provides various time-related functions.

``` python
import time

time.strftime("%Y-%m-%d %H:%M:%S")
# '2020-08-11 18:17:52'

time.strptime("30 Nov 20", "%d %b %y")
# time.struct_time(tm_year=2020, tm_mon=11, tm_mday=30, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=0, tm_yday=335, tm_isdst=-1)
```

### Functions creating iterators for efficient looping (`itertools`)

This module implements a number of iterator building blocks.

``` python
import itertools

## Combinatoric iterators
list(itertools.combinations('ABC', 2))
## [('A', 'B'), ('A', 'C'), ('B', 'C')]

list(itertools.combinations_with_replacement('ABC', 2))
## [('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'B'), ('B', 'C'), ('C', 'C')]

list(itertools.permutations('ABC', 2))
## [('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]

list(itertools.product('ABC', repeat = 2))
## [('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'B'), ('B', 'C'), ('C', 'A'), ('C', 'B'), ('C', 'C')]

a = [1,3]
b = [2,4]

list(zip(a,b))
## [(1, 2), (3, 4)]

list(itertools.permutations(a+b,2))
## [(1, 3), (1, 2), (1, 4), (3, 1), (3, 2), (3, 4), (2, 1), (2, 3), (2, 4), (4, 1), (4, 3), (4, 2)]

## Accumulate
mylist = [1,3,5,7,9,11,13]
list(itertools.accumulate(mylist))
## [1, 4, 9, 16, 25, 36, 49]
```

### Regular expression operations (`re`)

In this module, you specify the rules for the set of possible strings
that you want to match; this set might contain English sentences, or
e-mail addresses, or TeX commands, or anything you like (from [Python
HOWTOs](https://docs.python.org/3/howto/regex.html#regex-howto)).

``` python
import re

re.findall('begin', 'begin with this example for beginning') # find all 'begin's in text
# ['begin', 'begin']

re.findall('^begin', 'begin with this example for beginning') # find 'begin' only at the beginnig (^) of text
['begin']

re.findall('begin$', 'this is another begin') # search only last word ($)
# ['begin']

re.findall('.*begin', 'this is another begin') # search 'begin' and everything before (.*)
# ['this is another begin']

re.findall('goo?al','goal vs goooooal') # zero or one (?) 'o' character
# ['goal']

re.findall('goo*al','goal vs goooooal') # zero or more (*) 'o' character
# ['goal', 'goooooal']

re.findall('goo+al','goal vs goooooal') # one or more (*) 'o' character
# ['goooooal']

re.findall('\d', 'today is Oct 10') # Find digits (\d)
# ['1', '0']

re.findall('\d{2}', 'today is Oct 10') # Find two digits (\d{2})
# ['10']

re.findall('\w', 'today is Oct 10') # find any words (\w)
# ['t', 'o', 'd', 'a', 'y', 'i', 's', 'O', 'c', 't', '1', '0'] 

re.findall('\w+', 'yesterday was October 9') # find any word with one or more (+) characters
# ['yesterday', 'was', 'October', '9']

re.findall('\w{4}\w*', 'yesterday was October 9') # find any word with 4 letters or more
# ['yesterday', 'October']

re.findall('[A-Z]..', 'yesterday was October 9') # find any capital word ([A-Z]) and two characters after (..)
# ['Oct']

re.findall('([A-Z][a-z]* \d+)', 'yesterday was October 9') # find any capital letter ([A-Z]) followed by two small letters ([a-z]{2}) and a space ( ) and two digits (\d{2})
# ['October 9']

re.findall('(?<=; )[\w ]*', 'I want everything after; this part is important') # after (\w = [a-zA-Z0-9_])
# ['this part is important']

re.findall('[\w ]+(?=;)', 'I want everything before; this part is not important') # before
# ['I want everything before']

pattern = re.compile('[\w ]*(?=;)') # we can keep the pattern in this way
mm = re.match(pattern, 'I want everything before; this part is not important') # before
mm.group(0)
# 'I want everything before'
```

-----

## Other packages

Beside the standard library, we can add numerous packages to the Python
toolkit. The following are some of the most famous Python packages that
can empower your toolbox.

  - **SymPy:** a library for symbolic mathematics
  - **Matplotlib:** a comprehensive 2D plotting library
  - **IPython/Jupyter:** an enhanced interactive console
  - **Pandas:** when working with tabular data (DataFrame), such as data
    stored in spreadsheets or databases, Pandas is a useful tool for you
  - **NumPy:** a base N-dimensional array package - useful linear
    algebra
  - **SciPy:** a Python-based ecosystem of open-source software for
    mathematics, science, and engineering such as SymPy, NumPy,
    Matplotlib, IPython and pandas
  - **Numba:** an open source JIT compiler that translates a subset of
    Python and NumPy code into fast machine code
  - **Cython:** a library for writing C extensions for Python as easy as
    Python itself
  - **mpi4py:** it provides Python bindings for the Message Passing
    Interface (MPI) standard
  - **SciKit-Learn:** a library for machine learning
  - **TensorFlow:** a library for fast numerical computing and deep
    learning
  - **Dask:** it natively scales Python and provides advanced
    parallelism for analytics

**Hint:**
[Anaconda](https://ashki23.github.io/python-env.html#miniconda), a
package manager system for Python, can amazingly help you to add modules
to your Python environment.

---

Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
