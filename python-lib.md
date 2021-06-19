# Python standard library
*[Ashkan Mirzaee](https://ashki23.github.io/index.html)*

Python standard library includes about 220 modules and 89 built-in
functions (Python 3.9). Each of these modules designed for specific
purposes and includes several functions (methods) and most of the users
might never use many of them (use `help('modules')` to see list of the
modules). On the other hand, built-in functions are very limited and it
is not hard to learn and apply most of them.

In this tutorial we will learn more about Python built-in functions and
some useful modules for general Python users.

Sources:

  - [Python built-in
    functions](https://docs.python.org/3/library/functions.html)
  - [Python lexical
    analysis](https://docs.python.org/3/reference/lexical_analysis.html)
  - [The Python standard
    library](https://docs.python.org/3/library/index.html)

You might also like these related articles:

  - [Python data structures](python-str.html)
  - [Function programming in Python](python-fun.html)
  - [Virtual environments in Python](python-env.html)

-----

## Built-in functions and keywords

In general we can categorize built-in functions to:

  - Mathematical: `abs`, `divmod`, `max`, `min`, `pow`, `round`, `sum`
  - Logical/test: `all`, `any`, `isinstance`, `issubclass`
  - Structural: `bool`, `bytes`, `bytearray`, `complex`, `dict`,
    `float`, `frozenset`, `int`, `list`, `set`, `str`, `type`, `tuple`
  - Applicator: `exec`, `eval`, `filter`, `len`, `map`, `reversed`,
    `sorted`, `slice`, `zip`
  - Iteration:`enumerate`, `iter`, `next`, `range`
  - In/out: `input`, `open`, `print`
  - Character converter: `ascii`, `bin`, `chr`, `format`, `hex`, `oct`,
    `ord`, `repr`
  - Variable’s scope/location: `dir`, `globals`, `id`, `locals`, `vars`
  - Objects: `callable`, `delattr`, `getattr`, `hasattr`, `setattr`
  - Other: `breakpoint`, `classmethod`, `compile`, `memoryview`,
    `property`, `staticmethod`, `super`, …

Note that functions require parentheses, for instance `abs(-7)` or
`range(3)`. Some of the built-in functions are part of a module that can
add the module’s methods to the objects, for instance `open` function
from module io has `read`, `write`, `seek`, `close` and more methods
(see examples in the below).

The most common operators are:

  - Arithmetic `+`, `-`, `*`, `/`, `**`, `//`, `%`, `@`
  - Indexing: `[`
  - Sequence operator: `:`
  - Assignment: `=`, `+=`, `-=`, `*=`, `/=`, `**=`, `//=`, `%=`, `@=`
  - Ordering and comparison: `<`, `>`, `<=`, `>=`, `==`, `!=`

The following identifiers are used as reserved words, or keywords of the
language, and cannot be used as ordinary identifier:

    False      await      else       import     pass
    None       break      except     in         raise
    True       class      finally    is         return
    and        continue   for        lambda     try
    as         def        from       nonlocal   while
    assert     del        global     not        with
    async      elif       if         or         yield

Next are some examples for the above functions:

``` python
divmod(6,4)
## (1, 2) # (Quotient,Remainder)
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

# For example the following add x_0 = 0, x_1 = 1 and x_2 = 2 to the locals dictionary: 
for i in range(3):
  locals()['x_%s' % i] = i # or exec('x_%s = %s' % (i,i))
x_0,x_1,x_2
## (0, 1, 2)

hex(id(x)) # this is the address of the object x in memory
## '0x1048d7f10'

with open('new_file.txt', 'w') as fw:
    fw.write('The first line\nThe second line\n')

my_file = open('new_file.txt', 'r')
my_file.read() ## read the openned file from the begining to the end
## 'The first line\nThe second line\n'
my_file.read() ## since we read the file, the cursor is at the end
## ''
my_file.seek(0) ## move the cursor to the begining
my_file.read()
## 'The first line\nThe second line\n'

my_file.seek(0) ## move the cursor to the begining
my_file.readline() ## read line by line
## 'The first line\n'
my_file.readline()
## 'The second line\n'

my_file.seek(0) ## move the cursor to the begining
my_file.readlines() ## read all lines as a list
['The first line\n', 'The second line\n']

my_file.seek(0) ## move the cursor to the begining
for line in my_file:
    print(line, end = '')
## The first line
## The second line
my_file.close() ## we should close the file
```

## Library

Python includes a very extensive standard library that offering a wide
range of facilities. We can categorize the below modules as follows:

  - Numeric and mathematical: `math`, `cmath`, `statistics`, `random`,
    `decimal`
  - File formats: `csv`, `json`
  - Generic operating system services: `os`, `ctypes`, `argparse`,
    `time`
  - System-specific parameters and functions: `sys`
  - File and directory access: `glob`, `shutil`
  - Data persistence: `sqlite3`, `dbm`, `pickle`
  - Functional programming: `itertools`, `functools`, `operator`
  - Text processing services: `srting`, `re`, `readline`
  - Data types: `collections`, `datetime`
  - Software packaging and distribution: `venv`
  - Launching parallel tasks: `concurrent.futures`

The following are some of applications of the above modules.

### OS

Miscellaneous operating system interfaces (`os`) module provides a
portable way of using operating system dependent functionality.

``` python
import os

# Run OS commands
os.system("""
echo $(date) $(hostname) > date_hname.txt
""")

os.popen("""
echo $(date) $(hostname)
""").read().strip()
## 'Fri Feb 21 18:19:11 CST 2020 UserHost.local' 

os.popen("""
echo $(date) $(hostname)
echo $HOME
""").readlines()
## ['Fri Feb 21 18:19:11 CST 2020 UserHost.local\n', '/home/user\n']

os.popen("""
echo $(date) $(hostname)
echo $HOME
""").read().strip().split('\n')
## ['Fri Feb 21 18:19:11 CST 2020 UserHost.local', '/home/user']

# Make directory and navigation
os.getcwd()
## '/home/user'
os.mkdir('new_directory')
os.chdir('new_directory')
os.getcwd()
## '/home/user/new_directory'

# Rename and remove
os.rename('new_directory', 'dir_new')
os.removedirs('dir_new')
os.remove('<file_name>')

# Env variables
os.getenv('HOME')
## '/home/user'

os.environ ## returns all the envs as ENV:PATH 
```

### Glob

Unix style pathname pattern expansion (`glob`) module finds all the
pathnames matching a specified pattern according to the rules used by
the Unix shell, although results are returned in arbitrary order.

``` python
import glob

glob.glob('*.py')
## ['file1.py', 'file2.py']
```

### Sys

System-specific parameters and functions (`sys`) module help to pass
arguments and standard inputs. Let’s create the following Python script
called `test-sys.py`:

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
comes from the Shell pipe as standard input (`stdin`). Sys module has
many methods that you may find them in the Python docs.

### Argeparse

Parser for command-line options, arguments and sub-commands (`argparse`)
module makes it easy to write user-friendly command-line interfaces. The
program defines what arguments it requires, and `argparse` will figure
out how to parse those out of `sys.argv`. Lets create a script
(`reverse-file.py`) that read text files and print in reverse order
(bottom to top):

``` python
import argparse
import sys

parser = argparse.ArgumentParser(description = 'Read a file in reverse')
parser.add_argument('filename', help = 'the file to read')
parser.add_argument('-v', '--version', action = 'version', version = '%(prog)s 1.0', help = 'show program version and exit')
parser.add_argument('-l', '--limit', type = int, help = 'the number of lines to read')

args = parser.parse_args()

try:
    f = open(args.filename)
except FileNotFoundError as err:
    print("Error:", err)
    sys.exit(2)
else:
    with open(args.filename, 'r') as f:
        lines = f.readlines()
        lines.reverse()
        
    if args.limit:
        lines = lines[:args.limit]
            
    for line in lines:
        print(line.strip())
```

Now we can use the script to read files in reverse. We can use `-h` or
`-v` options to see help and version:

``` bash
python3 reverse-file.py -h
```

``` 
usage: reverse-file.py [-h] [-v] [-l LIMIT] filename
Read a file in reverse
positional arguments:
 filename                 the file to read
optional arguments:
 -h, --help               show this help message and exit
 -v, --version            show program version and exit
 -l LIMIT, --limit LIMIT  the number of lines to read                       
```

To read last 2 lines of a file and print in reverse order we can run:

``` bash
python3 reverse-file.py -l 2 new_file.txt
## The second line
## The first line
```

### JSON

JSON encoder and decoder (`json`) module read and write JSON files.

``` python
import json

# Read
with open('./input.json', 'r') as jsf:
  input_json = json.load(jsf)

# Write
list_dict = [{'title': 'Monty Python and the Holy Grail', 'year': [1975, 'March 14']}]
with open('output.json', 'w') as jso:
    json.dump(list_dict, jso)

# Serialize to a JSON formatted str 
js = json.dumps(list_dict)
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
## Monty Python and the Holy Grail
```

### Pickle

Python object serialization (`pickle`) module implements binary
protocols for serializing and de-serializing a Python object structure.
You might prefer JSON to pickle for many reasons such as security and
human readability. Learn more about pickle in
[here](https://docs.python.org/3/library/pickle.html).

``` python
import pickle

# Read
data = with open('input.pickle','rb') as pkl:
    input_pkl = pickle.load(pkl)

# Write
dict_data = {'title': 'Monty Python and the Holy Grail', 'year': [1975, 'March 14']}
with open('output.pickle', 'wb') as pkl:
    pickle.dump(dict_data, pkl)

# Serialize to a pickle formatted str 
pkl = pickle.dumps(dict_data)
print(pkl)
## b'\x80\x04\x95H\x00\x00\x00\x00\x00\x00\x00}\x94(\x8c\x05title\x94\x8c\x1fMonty Python and the Holy Grail\x94\x8c\x04year\x94]\x94(M\xb7\x07\x8c\x08March 14\x94eu.'
```

### CSV

CSV file reading and writing (`csv`) module read and write CSV files.

``` python
import csv

# Read to list
with open('./input.csv', 'r') as fl:
    csv_list = list(csv.reader(fl))

print(csv_list)
## [['a', 'b', 'c', 'd'], ['22', 'yes', '5', '0'], ['34', 'no', '7', '8']]

# Write from list
with open('output1.csv', 'w') as nfl:
    csv_writer = csv.writer(nfl)
    csv_writer.writerows(csv_list)

# Read to dict
with open('./input.csv', 'r') as fl:
    csv_dict = list(csv.DictReader(fl))

print(csv_dict)
## [{'a': '22', 'b': 'yes', 'c': '5', 'd': '0'}, {'a': '34', 'b': 'no', 'c': '7', 'd': '8'}]
    
# Write from dict
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

### SQLite3

Interface for SQLite (`sqlite3`) module provides a SQL interface
compliant. Example from [Python
documentation](https://docs.python.org/3/library/sqlite3.html).

``` python
import sqlite3

conn = sqlite3.connect('example.db')
c = conn.cursor()

# Create table
c.execute("""CREATE TABLE stocks
             (date text, trans text, symbol text, qty real, price real)""")

# Insert a row of data
c.execute("INSERT INTO stocks VALUES ('2006-01-05','BUY','RHAT',100,35.14)")

# Save (commit) the changes
conn.commit()

# We can also close the connection if we are done with it
# just be sure any changes have been committed or they will be lost
conn.close()
```

### Collections

Container datatypes (`collections`) module implements specialized
container datatypes providing alternatives to Python’s general purpose
built-in containers, `dict`, `list`, `set`, and `tuple`.

``` python
import collections

# Example 1
dict_list = collections.defaultdict(list)
for i in list(range(2))*3:
    dict_list[i].append(1)

dict(dict_list)
## {0: [1, 1, 1], 1: [1, 1, 1]}

for k in dict_list:
    dict_list[k] = sum(dict_list[k])

dict(dict_list)
## {0: 3, 1: 3}

# Example 2
s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
d = collections.defaultdict(list)
for k,v in s:
    d[k].append(v)

sorted(d.items())
## [('blue', [2, 4]), ('red', [1]), ('yellow', [1, 3])]

dict(sorted(d.items()))
## {'blue': [2, 4], 'red': [1], 'yellow': [1, 3]}
```

### Time

Time access and conversions (`time`) module provides various
time-related functions.

``` python
import time

local_time = time.localtime() # a time tuple expressing local time
local_time
## time.struct_time(tm_year=2021, tm_mon=5, tm_mday=6, tm_hour=22, tm_min=3, tm_sec=32, tm_wday=3, tm_yday=126, tm_isdst=1)

local_time.tm_year
## 2021

time.strftime("%X", local_time) # convert a time tuple to a string according to a format specification
## '22:03:32'

time.strftime("%Y-%m-%d %H:%M:%S") # the default tuple is localtime()
## '2021-05-06 22:10:03'

time.time() # return the current time in seconds since the Epoch
## 1620356510.8557692

time.mktime(local_time) # convert a time tuple in local time to seconds since the Epoch
## 1620356612.0

local_time2 = time.localtime()
difference = time.mktime(local_time2) - time.mktime(local_time) # time difference in sec
difference
## 452.0

time.gmtime(difference) # convert seconds since the Epoch to a time tuple
## time.struct_time(tm_year=1970, tm_mon=1, tm_mday=1, tm_hour=0, tm_min=7, tm_sec=32, tm_wday=3, tm_yday=1, tm_isdst=0)

time.strptime("30 Nov 20", "%d %b %y") # parse a string to a time tuple according to a format specification
## time.struct_time(tm_year=2020, tm_mon=11, tm_mday=30, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=0, tm_yday=335, tm_isdst=-1)
```

Commonly used time format codes:

  - `%Y` Year with century as a decimal number.
  - `%m` Month as a decimal number \[01,12\].
  - `%d` Day of the month as a decimal number \[01,31\].
  - `%H` Hour (24-hour clock) as a decimal number \[00,23\].
  - `%M` Minute as a decimal number \[00,59\].
  - `%S` Second as a decimal number \[00,61\].
  - `%z` Time zone offset from UTC.
  - `%a` Locale’s abbreviated weekday name.
  - `%A` Locale’s full weekday name.
  - `%b` Locale’s abbreviated month name.
  - `%B` Locale’s full month name.
  - `%c` Locale’s appropriate date and time representation.
  - `%x` Locale’s appropriate date representation.
  - `%X` Locale’s appropriate time representation.
  - `%p` Locale’s equivalent of either AM or PM.
  - `%I` Hour (12-hour clock) as a decimal number \[01,12\].

### Itertools

Functions creating iterators for efficient looping (`itertools`) module
implements a number of iterator building blocks.

``` python
import itertools

# Combinatoric iterators
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

# Accumulate
mylist = [1,3,5,7,9,11,13]
list(itertools.accumulate(mylist))
## [1, 4, 9, 16, 25, 36, 49]
```

### RE

In Regular expression operations (`re`) module, we specify the rules for
the set of possible strings that you want to match; this set might
contain English sentences, or e-mail addresses, or TeX commands, or
anything you like (from [Python
HOWTOs](https://docs.python.org/3/howto/regex.html#regex-howto)).

``` python
import re

re.findall('begin', 'begin with this example for beginning') # Find all 'begin's in text
## ['begin', 'begin']

re.findall('^begin', 'begin with this example for beginning') # Find 'begin' only at the beginnig (^) of text
['begin']

re.findall('begin$', 'this is another begin') # Search only last word ($)
## ['begin']

re.findall('.*begin', 'this is another begin') # Search 'begin' and everything before (.*)
## ['this is another begin']

re.findall('goo?al','goal vs goooooal') # Zero or one (?) 'o' character
## ['goal']

re.findall('goo*al','goal vs goooooal') # Zero or more (*) 'o' character
## ['goal', 'goooooal']

re.findall('goo+al','goal vs goooooal') # One or more (*) 'o' character
## ['goooooal']

re.findall('\d', 'today is Oct 10') # Find digits (\d)
## ['1', '0']

re.findall('\d{2}', 'today is Oct 10') # Find two digits (\d{2})
## ['10']

re.findall('\w', 'today is Oct 10') # Find any words (\w)
## ['t', 'o', 'd', 'a', 'y', 'i', 's', 'O', 'c', 't', '1', '0'] 

re.findall('\w+', 'yesterday was October 9') # Find any word with one or more (+) characters
## ['yesterday', 'was', 'October', '9']

re.findall('\w{4}\w*', 'yesterday was October 9') # Find any word with 4 letters or more
## ['yesterday', 'October']

re.findall('[A-Z]..', 'yesterday was October 9') # Find any capital word ([A-Z]) and two characters after (..)
## ['Oct']

re.findall('([A-Z][a-z]* \d+)', 'yesterday was October 9') # Find any capital letter ([A-Z]) followed by two small letters ([a-z]{2}) and a space ( ) and two digits (\d{2})
## ['October 9']

re.findall('(?<=; )[\w ]*', 'I want everything after; this part is important') # After (\w = [a-zA-Z0-9_])
## ['this part is important']

re.findall('[\w ]+(?=;)', 'I want everything before; this part is not important') # Before
## ['I want everything before']

pattern = re.compile('[\w ]*(?=;)') # We can keep the pattern in this way
mm = re.match(pattern, 'I want everything before; this part is not important') # Before
mm.group(0)
## 'I want everything before'
```

-----

## Other packages

Beside the standard library, we can add numerous packages to the Python
toolkit. The following are some of the most famous Python packages that
can empower your toolbox.

  - **SymPy:** a library for symbolic mathematics
  - **Matplotlib:** a comprehensive 2D plotting library
  - **IPython/Jupyter:** an enhanced interactive console
  - **Pandas:** a tool for working with tabular data (DataFrame), such
    as data stored in spreadsheets or databases
  - **NumPy:** a base N-dimensional array package - useful linear
    algebra
  - **SciPy:** a Python-based ecosystem of open-source software for
    mathematics, science, and engineering
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
  - **Redis:** is Python interface to the Redis key-value store
  - **PySpark:** is Python API for Apache Spark

**Hint:**
[Anaconda](https://ashki23.github.io/python-env.html#miniconda), a
package manager system for Python, can amazingly help you to add modules
to your Python environment.

---

Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
