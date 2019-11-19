# Python data structure
[The Python Tutorial](https://docs.python.org/3.7/tutorial/datastructures.html)

Different types of data in Python are:

- Strings `str`
- Numbers `int` `float`
- Booleans `bool`
- None `NoneType`
- Lists `[]`
- Tuples `()`
- Sets `{}`
- Dictionaries `{'key' : value}`

``` python
# All types
for element in ['a', True, None, 123, 0.777, [1,2], (1,2), {1,2}, {'key':1}]:
    print(type(element))
## <class 'str'>
## <class 'bool'>
## <class 'NoneType'>
## <class 'int'>
## <class 'float'>
## <class 'list'>
## <class 'tuple'>
## <class 'set'>
## <class 'dict'>

# Strings
single = 'this is a string'
type(single)
## <class 'str'>
double = "this is also a string"
type(double)
## <class 'str'>

multiline = '''
this is
also a string
in multiple lines
'''
type(multiline)
## <class 'str'>

'some text' + ' MORE TEXT'
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

### Converting between data types
We can use the following commands to convert data to other types:

- `str()` creates a string
- `int()` creates an integer
- `float()` creates a float
- `bool()` creates a boolean
- `list()` creates a list
- `tuple()` creates a tuple
- `set()` create a set
- `dict()` create a dictionary

``` python
str(5) + ' five'
## 5 five

int('5') + 5
## 10

float('5') + 5
## 10.0

list((2,4,6))
## [2,4,6]

tuple([1,3,5])
## (1,3,5)

set([1,3,5,1,3,5])
## {1,3,5}
```

## Data structures
There are four major data structures in Python:

-   Lists: `list()` `[]`
-   Tuples: `tuple()` `()`
-   Sets: `set()` `{}`
-   Dictionaries: `dict()` `{'key': value}`

### Lists
A list is a set of objects enclosed by a set of square brackets (`[]`). Lists are **mutable**, and their elements are usually 
**homogeneous** and are accessed by iterating over the list.

``` python
list_ = [1,3,5,7]
print(list_)
## [1, 3, 5, 7]
type(list_)
## <class 'list'>

list_[0] = 100 # Lists are mutable
print(list_)
## [100, 3, 5, 7]

# Lists can hold any type of item
example = [1,True,None,['word',123],'test', (0,1), {'name id': 7}]
```

We can use numeric index to find the elements.
``` python
names = ['turtle','polar bear','elephant','penguin']
print(names[0]) # First element
## 'turtle'

print(example[3]) # Fourth element
## 'penguin'
print(names[:]) # Everything
## ['turtle', 'polar bear', 'elephant', 'penguin']

print(names[:2]) # Everything before third element
## ['turtle', 'polar bear']

print(names[2:]) # Everything after third element
## ['elephant', 'penguin']
```

And if we use a negative index, it means get elements from the end, going backwards.
``` python
print(names[-1]) # Last element
## 'penguin'

print(names[:-2]) # Everything before the last two elements
## ['turtle', 'polar bear']
```

Note that we can use the index multiple times to retrieve information from nested objects.
``` python
print(example[3][1])
## 123
```
Here are some of the methods of list objects:
- `list.append(x)` append x
- `list.extend(x)` or `+=` extend/add x
- `list.insert(i,x)` insert x in position i
- `list.remove(x)` remove x
- `list.pop(i)` remove item at position i
- `list.sort()` sort
- `list.reverse()` reverse the order
- `list.count(x)` count number of times x repeated
- `list.index(x)` find index of item x
- `list.copy()` copy list
- `list.clear()` clear list

``` python
a = [1,4,5]
a += [2,3]
print(a)
## [1, 4, 5, 2, 3]

a.append([6,7])
print(a)
## [1, 4, 5, 2, 3, [6, 7]]

a.remove([6,7])
print(a)
## [1, 4, 5, 2, 3]

a.extend([6,7])
print(a)
## [1, 4, 5, 2, 3, 6, 7]

a.sort()
print(a)
## [1, 2, 3, 4, 5, 6, 7]

a.reverse()
print(a)
## [7, 6, 5, 4, 3, 2, 1]

a.count(5)
## 1
a.index(5)
## 2

a.clear()
print(a)
## []
```

Be cautious when you set a list is equal to another list. It might change list unintentionally, see the example in below:
```python
list1 = [1, 2, 3]
list2 = list1
list2 += [4, 5]
print(list1)
## [1, 2, 3, 4, 5]
print(list2)
## [1, 2, 3, 4, 5]
print(id(list1))
## 139724935851336
print(id(list2))
## 139724935851336
```

As you can see, by changing `list2`, `list1` is changing automatically since `list1 = list2` - they have a same ID as well. 
You can work on `list2` without changing `list1` by using `.copy()`, for instance:
```python
list1 = [1,2,3]
list2 = list1.copy()
list2 += [4,5] 
print(list1)
## [1, 2, 3]
print(list2)
## [1, 2, 3, 4, 5]
print(id(list1))
## 139724935851400
print(id(list2))
## 139724935851208
```

### Iterating through lists
``` python
print([x**2 for x in range(5)])
## [0, 1, 4, 9, 16]

nested = []
p = [1,2,3]
for i in p:
    nested.append([(x,i) for x in p])
print(nested)
## [[(1, 1), (2, 1), (3, 1)], 
##  [(1, 2), (2, 2), (3, 2)], 
##  [(1, 3), (2, 3), (3, 3)]]
```

## Tuples and sets
A **tuple** consists of a number of values separated by commas. Though tuples may seem similar to lists, they are often used 
in different situations and for different purposes. Tuples are **immutable**, and usually contain a **heterogeneous** sequence of 
elements that are accessed via unpacking or indexing. Tuples may be input with or without surrounding parentheses.

A **set** is an **unordered** collection with **no duplicate** elements. Basic uses include membership testing and eliminating duplicate 
entries. Set objects also support mathematical operations like union, intersection, difference, and symmetric difference.
```python
# Tuples
tp = 1399,'hello',1400 # It might include parentheses or not
type(tp)
## <class 'tuple'>
print(tp)
(1399, 'hello', 1400)
print(tp[0])
1399

tp[0] = 1390 # Tuples are immutable
## Traceback (most recent call last):
##   File "<stdin>", line 1, in <module>
## TypeError: 'tuple' object does not support item assignment

singleton = 'hello', # A tuple should include at leat one comma (,)
print(singleton)
## ('hello',)

# Sets
st = {12,13,13,15,12,15}
print(st)
## {12, 13, 15}

print(st[1])
## Traceback (most recent call last):
##   File "<stdin>", line 1, in <module>
## TypeError: 'set' object does not support indexing

si = {'singleton'}
print(si)
## {'singleton'}

sii = set('singleton')
print(sii)
## {'l', 'g', 'n', 's', 't', 'i', 'e', 'o'}
```

**Note**: to create empty sets use `set()` because `{}` considered as empty dictionary in python.
```python
for element in [[], (), {}]:
    print(type(element)) 
## <class 'list'>
## <class 'tuple'>
## <class 'dict'>
```

### Iterating through sets
```python
print({x**2 for x in [1,2,2,1,3]})
## {1, 4, 9}
```

## Dictionaries
Dictionaries (also called dicts) are another key data structure. Unlike sequences (lists, and tuples), which are indexed by a range of numbers, **dictionaries** are indexed by keys, which can 
be any immutable type (e.g. strings and numbers). The main operations on a dictionary are storing a value with some key and 
extracting the value given the key.
``` python
example = {}
type(example)
## <class 'dict'>

example['first key'] = 'value'
example[2] = 'two'
example['third key'] = 3
print(example)
## {'first key': 'value', 2: 'two', 'third key': 3}
print(example['first key'])
## 'value'

k = list(example.keys())
print(k)
## ['first key', 2, 'third key']

v = list(example.values())
print(v)
## ['value', 'two', 3]
```

Here are some of the methods of dict objects:
- `dict.update()` update/add element 
- `dict.popitem()` remove arbitrary element
- `dict.pop(k)` remove element k
- `dict.keys()` return keys
- `dict.items()` retun items  
- `dict.copy()` copy dict
- `dict.clear()` clear dict

### Iterating through dicts
``` python
color = ['blue', 'red', 'white', 'green', 'green', 'red', 'red', 'white', 'red', 'green']
c = {x:color.count(x) for x in color}
print(c)
## {'blue': 1, 'red': 4, 'white': 2, 'green': 3}
s = [{k:c[k]} for k in sorted(c,key = c.get,reverse = True)]
print(s)
## [{'red': 4}, {'green': 3}, {'white': 2}, {'blue': 1}]
```
