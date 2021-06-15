# Python data structures
*[Ashkan Mirzaee](https://ashki23.github.io/index.html)*

[Python](https://www.python.org/) is an easy to learn, powerful
programming language. It has efficient high-level data structures and a
simple approach to object-oriented programming. To learn Python, first
we need to learn how Python treats with data. In this article we will
learn about data types and structures in Python 3 through several
examples. You may find more about Python programming at:

  - [Programming with
    Python](http://swcarpentry.github.io/python-novice-inflammation/)
  - [Plotting and Programming in
    Python](http://swcarpentry.github.io/python-novice-gapminder/)
  - [Analysis pipelines with
    Python](https://hpc-carpentry.github.io/hpc-python/)
  - [The Python
    Tutorial](https://docs.python.org/3/tutorial/#the-python-tutorial)
  - [Function programming in Python](python-fun.html)

-----

## Python object types

Most common types in Python are:

  - Strings `str`
  - Numbers `int`, `float`, `complex`
  - Booleans `bool`
  - None `NoneType`
  - Lists `[]`
  - Tuples `()`
  - Sets `{}`
  - Dictionaries `{key:value}`

<!-- end list -->

``` python
for element in ['a', True, None, 123, 0.777, 8j, [1,2], (1,2), {1,2}, {'key':1}]:
    print(type(element))
## <class 'str'>
## <class 'bool'>
## <class 'NoneType'>
## <class 'int'>
## <class 'float'>
## <class 'complex'>
## <class 'list'>
## <class 'tuple'>
## <class 'set'>
## <class 'dict'>
```

To learn more about the built-in types, review Python standard types in
[here](https://docs.python.org/3.8/library/stdtypes.html).

### Characteristics

Strings, tuples and lists can be **concatenated**:

``` python
'some text ' + 'MORE TEXT'
## some text MORE TEXT

'repetition ' * 3
## repetition repetition repetition

# Lists
[1,3,'five'] + [7,9]
## [1, 3, 'five', 7, 9]

[1,3,'five'] * 2
## [1, 3, 'five', 1, 3, 'five']

# Tuples 
(2,4,'six') + (8,10)
## (2, 4, 'six', 8, 10)

(2,4,'six') * 2
## (2, 4, 'six', 2, 4, 'six')
```

Lists, dictionaries and sets are **mutable**. Mutable objects can change
their value but keep the same object (same `id()`):

``` python
a = [1,2,3]
id(a)
## 4504081480
a += [4,5]
a
## [1, 2, 3, 4, 5]
id(a)
## 4504081480
```

Numbers, strings and tuples are **immutable**. An object with a fixed
value:

``` python
a = 2
id(a)
## 4499865296
a += 3
a
## 5
id(a)
## 4499865392
```

Strings, tuples, lists and dictionaries are **subscriptable** objects:

``` python
sw = 'Python'
sw[0]
## 'P'

sw[0:1]
## 'Py'

sw[::2]
## 'Pto'

names = ['turtle','polar bear','elephant','penguin']
names[:2]
## ['turtle', 'polar bear']
```

In general, numbers in the indexing square brackets can be in one of the
following formats:

``` python
[element]
[begin:end]
[begin:end:step]
```

When negative numbers can be interpreted as inverse actions:

``` python
sw[-1] # last element
## 'n'

sw[::-1] # step 1 but in inverse order
## 'nohtyP'

names[:-2] # everything before the last two elements
## ['turtle', 'polar bear']

names[::-1]
## ['penguin', 'elephant', 'polar bear', 'turtle']
```

And empty clones could interpret as all:

``` python
sw[:]
## 'Python'

sw[::]
## 'Python'

names[:]
## ['turtle', 'polar bear', 'elephant', 'penguin']
```

As a summary review the following table:

<div style="margin-bottom: 1rem; overflow-x: auto;">

| Type   | Concatenate | Subscriptable | Mutable |
| ------ | ----------- | ------------- | ------- |
| Number | No          | No            | No      |
| String | Yes         | Yes           | No      |
| Tuple  | Yes         | Yes           | No      |
| List   | Yes         | Yes           | Yes     |
| Dict   | No          | Yes           | Yes     |
| Set    | No          | No            | Yes     |

</div>

### Conversion

We can use the following commands to convert objects to other types:

  - `str()` create a string
  - `int()` create an integer
  - `float()` create a float
  - `complex()` create a complex number
  - `bool()` create a boolean
  - `list()` create a list
  - `tuple()` create a tuple
  - `set()` create a set
  - `dict()` create a dictionary

<!-- end list -->

``` python
str(5) + ' five'
## 5 five

int('5') + 5
## 10

float('5') + 5
## 10.0

list((2,4,6))
## [2, 4, 6]

list({'a':1,'b':2})
## ['a', 'b']

list({'a':1,'b':2}.values())
## [1, 2]

tuple([1,3,5])
## (1,3,5)

set([1,3,5,1,3,5])
## {1, 3, 5}

dict([('a',1),('b',2),('c',3)])
## {'a': 1, 'b': 2, 'c': 3}
```

-----

## Data structures

There are five major [data
structures](https://docs.python.org/3.7/tutorial/datastructures.html) in
Python:

  - Strings: `srt()`, `' '`
  - Lists: `list()`, `[]`
  - Tuples: `tuple()`, `()`
  - Sets: `set()`, `{}`
  - Dictionaries: `dict()`, `{key:value}`

### Strings

One of the way that data can be stored in Python is strings and as we
discussed they are **immutable** and **subscriptable** objects that can
be **concatenated** together. In python, any thing inside single or
double quotes (`' '` or `" "`) considers as string. There are several
methods available for strings and the following are some of the main
methods for strings:

  - `str.capitalize()` capitalize
  - `str.lower()` lowercase
  - `str.upper()` uppercase
  - `str.find(x)` find index of character x
  - `str.index(x)` index of character x (similar to `.find(x)` if x is
    in the string)
  - `str.count(x)` count how many times x repeated
  - `str.replace(x,y)` replace character x with y
  - `str.split(x)` split an string to a list of strings based on the
    separator x (can be empty `''`)
  - `str.join(x)` join list of strings or string x to make an string by
    a separator - opposite of `.split()`
  - `str.startswith(x)` True if the string starts with x character
  - `str.endswith(x)` True if the string ends with x character
  - `str.strip()` removing whitespace from the beginning and ending
  - `str.center('chr', num)` see an example in the below

For example:

``` python
name = 'python'

name.startswith('p')
## True

name.capitalize()
## 'Python'

name.upper()
## 'PYTHON'

name.index('p')
## 0

name2 = name.replace('n', 'n3').replace('p', ',p')
name2
## ',python3'

nm = name + name2
nm
## 'python,python3'

nm_split = nm.split(',')
nm_split
## ['python', 'python3']

','.join(nm_split)
## 'python,python3'

' This is a test '.center(30,'=')
## '======= This is a test ======='
```

### Lists

A list is a set of objects enclosed by a set of square brackets (`[]`).
Lists are **mutable**, and their elements are usually **homogeneous**
and are accessed by iterating over the list.

``` python
ls = [1,3,5,7]
ls[0] = 100 # Lists are mutable
ls
## [100, 3, 5, 7]

# Lists can hold any type of item
example = [1,True,None,['word',123],'test',(0,1),{'name id': 7}]

# Indexing
ls[1:3]
## [3, 5]

example[3][1]
## 123
```

Here are main lists methods:

  - `list.append(x)` append x
  - `list.extend(x)` or `+=` extend/add x
  - `list.insert(i,x)` insert x to index i
  - `list.remove(x)` remove x
  - `list.pop(i)` pop out and remove item at index i (similar to
    `del(list[i])`)
  - `list.pop()` pop out and remove the last item
  - `list.sort()` sort
  - `list.reverse()` reverse the order
  - `list.count(x)` count number of times x is repeated
  - `list.index(x)` find index of item x
  - `list.copy()` copy list
  - `list.clear()` clear list

<!-- end list -->

``` python
a = [1,4,5]
a += [2,3]
a
## [1, 4, 5, 2, 3]

a.append([6,7])
a
## [1, 4, 5, 2, 3, [6, 7]]

a.remove([6,7])
a
## [1, 4, 5, 2, 3]

a.extend([6,7])
a
## [1, 4, 5, 2, 3, 6, 7]

a.sort()
a
## [1, 2, 3, 4, 5, 6, 7]

a.reverse()
a
## [7, 6, 5, 4, 3, 2, 1]

a.count(5)
## 1
a.index(5)
## 2

a.clear()
a
## []
```

Be cautious when set a list equal to another list. It might change list
unintentionally, see the example in below:

``` python
list1 = [1, 2, 3]
list2 = list1
list2 += [4, 5]
list1
## [1, 2, 3, 4, 5]
list2
## [1, 2, 3, 4, 5]
id(list1)
## 139724935851336
id(list2)
## 139724935851336
```

As we can see, by changing `list2`, `list1` is changing automatically
since `list1 = list2` - they have a same ID as well.

We can work on `list2` without changing `list1` by using `.copy()` or
clone `[:]`. For instance:

``` python
list1 = [1,2,3]
list2 = list1.copy() # or list2 = list1[:]
list2 += [4,5] 
list1
## [1, 2, 3]
list2
## [1, 2, 3, 4, 5]
id(list1)
## 139724935851400
id(list2)
## 139724935851208
```

Iterating through lists:

``` python
[x**2 for x in range(5)]
## [0, 1, 4, 9, 16]

[x**2 for x in range(5) if x**2 < 10]
## [0, 1, 4, 9]

nested = []
p = [1,2,3]
for i in p:
    nested.append([(x,i) for x in p])
nested
## [[(1, 1), (2, 1), (3, 1)], 
##  [(1, 2), (2, 2), (3, 2)], 
##  [(1, 3), (2, 3), (3, 3)]]
```

### Tuples

A **tuple** consists of a number of values separated by commas. Though
tuples may seem similar to lists, they are often used in different
situations and for different purposes. Tuples are **immutable**, and
usually contain a **heterogeneous** sequence of elements that are
accessed via unpacking or indexing. Tuples may be input with or without
surrounding parentheses.

``` python
tp = 1399,'hello',1400 # It might include parentheses or not
type(tp)
## <class 'tuple'>

tp
## (1399, 'hello', 1400)

tp[0]
## 1399

tp[0] = 1390 # Tuples are immutable
## Traceback (most recent call last):
##   File "<stdin>", line 1, in <module>
## TypeError: 'tuple' object does not support item assignment

singleton = 'hello', # A tuple should include at least a comma (,)
singleton
## ('hello',)
```

Since tuples are immutable, there are only two methods:

  - `tuple.count(x)` count number of times x repeated
  - `tuple.index(x)` find index of item x

By tuples we can change the variables at the same time. Let assume we
have two variables `a = 10` and `b = 20` and want `a = b = 20` and `b =
a + b = 30`. For example:

``` python
a = 10
b = 20
a = b 
b = a + b
(a,b)
## (20, 40) # we wanted (20, 30)

## Using tuple
a = 10
b = 20
a, b = (b, a + b) # or a, b = b, a + b
(a,b)
## (20, 30)
```

### Dictionaries

Dictionaries (also called dicts) are key data structure including a set
of *keys* and *values*. Unlike sequences (e.g. lists and tuples) which
are indexed by a range of numbers, dictionaries are indexed by
**unique** and **immutable** *keys*. At the same time, *values* of the
list could be **any type** (mutable or immutable) and duplicated. The
main operations on a dictionary are storing a *value* with some *key*
and extracting *value* by given *key*.

``` python
example = {}
type(example)
## <class 'dict'>

example['first key'] = 'value'
example[2] = 'two'
example['third key'] = 3
example
## {'first key': 'value', 2: 'two', 'third key': 3}

example['first key']
## 'value'
```

Here are some of dictionaries methods:

  - `dict.update()` update/add items
  - `dict.popitem()` remove the last item
  - `dict.pop(k)` remove item with key k
  - `dict.keys()` return keys
  - `dict.values()` return values
  - `dict.items()` return items
  - `dict.get(k)` return value for key k
  - `dict.copy()` copy dict
  - `dict.clear()` clear dict

For example:

``` python
state = {'new york': 'NY', 'missouri': 'MS', 'california': 'CA'}

list(state.items())
## [('new york', 'NY'), ('missouri', 'MS'), ('california', 'CA')]

list(state.keys())
## ['new york', 'missouri', 'california']

list(state.values())
## ['NY', 'MS', 'CA']

state.get('missouri')
## 'MS'

state.update({'missouri': 'MO', 'Texas': 'TX' })
state
## {'new york': 'NY', 'missouri': 'MO', 'california': 'CA', 'Texas': 'TX'}

state.get('missouri')
## 'MO'
```

Iterating through dicts:

``` python
## Example 1: counting and sorting
color = ['blue', 'red', 'white', 'green', 'green', 'red', 'red', 'white', 'red', 'green']
col = {x:color.count(x) for x in color}
col
## {'blue': 1, 'red': 4, 'white': 2, 'green': 3}

c = {k:col[k] for k in sorted(col,key = col.get,reverse = True)}
c
## {'red': 4, 'green': 3, 'white': 2, 'blue': 1}

## Example 2: make dict elements uppercase
{x.upper():y for x,y in c.items()}
## {'RED': 4, 'GREEN': 3, 'WHITE': 2, 'BLUE': 1}

## Example 3: filtering dicts by value
d = {'a': 10, 'b': 12, 'c': 20}
{x:y for x,y in d.items() if y >= 12}
## {'b': 12, 'c': 20}
```

For another example, let’s consider a list of dictionaries including
production rate of two products, id 23 and id 35, in years 2005 and
2010:

``` python
production = [{'id':23,'year':2005,'rate':2305},{'id':35,'year':2005,'rate':3505},{'id':23,'year':2010,'rate':2310},{'id':35,'year':2010,'rate':3510}]
```

We can make a dictionary of production rates for each `id_year`
combination such that:

``` python
annual_rates = {}
for i in production:
  annual_rates['%s_%s' % (i['id'],i['year'])] = i['rate']

annual_rates
## {'23_2005': 2305, '35_2005': 3505, '23_2010': 2310, '35_2010': 3510}
```

To make a dictionary of list of the production rates over years, we can
use `collections` module. `defaultdict(list)` makes a default dictionary
of lists such that:

``` python
import collections

annual_rates = collections.defaultdict(list)
for i in production:
  annual_rates[i['id']].append(i['rate'])

dict(annual_rates)
## {23: [2305, 2310], 35: [3505, 3510]}
```

Now let’s find total production over years:

``` python
annual_rates_total = {}
for i in annual_rates:
  annual_rates_total[i] = sum(annual_rates[i])

annual_rates_total
## {23: 4615, 35: 7015}
```

Also, the `dict()` constructor can accept an iterator that returns a
finite stream of `(key, value)` tuples:

``` python
L = [('Italy', 'Rome'), ('France', 'Paris'), ('US', 'Washington DC')]
dict(L)
## {'Italy': 'Rome', 'France': 'Paris', 'US': 'Washington DC'}
```

### Sets

A **set** is an **unordered** collection with **no duplicate** elements.
Basic uses include membership testing and eliminating duplicate entries.
Set objects also support mathematical operations like union,
intersection, difference, and symmetric difference.

``` python
st = {12,13,13,15,12,15}
st
## {12, 13, 15}

st[1]
## Traceback (most recent call last):
##   File "<stdin>", line 1, in <module>
## TypeError: 'set' object does not support indexing
```

**Note**: to create empty sets use `set()` because `{}` considered as
empty dictionary in python.

``` python
for element in [[], (), {}]:
    print(type(element)) 
## <class 'list'>
## <class 'tuple'>
## <class 'dict'>
```

Sets have several methods including set operations such as:

  - `set.add(x)`: add a member to the set
  - `set.update(x)`: add a set/list to a set
  - `set.remove(x)`: remove a member of the set
  - `set.pop()`: pop out and remove the first member
  - `set.union(x)`: union of a set/list to a set
  - `set.intersection(x)`: intersection of a set/list to a set
  - `set.difference(x)`: difference of a set/list to a set

<!-- end list -->

``` python
s = {1,2,3}
t = {3,4,5}

s.union(t)
## {1, 2, 3, 4, 5}

s.intersection(t)
## {3}

s.difference(t)
## {1,2}
```

Iterating through sets:

``` python
{x**2 for x in [1,2,2,1,3]}
## {1, 4, 9}
```

---

Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
