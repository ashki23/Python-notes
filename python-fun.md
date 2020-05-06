# Function programming in Python

For efficiently programming with Python, we need to learn how to write functions. In this article we will be familiar with basic of function programming in Python 3 and learn about some Python's built-in functions through several examples. As a prerequisite for this tutorial, it is better to learn the following first:

- [Python data structure](https://ashki23.github.io/python-str.html)
- [Control flow tools in Python](https://docs.python.org/3/tutorial/controlflow.html)

The following is a good resource to learn more about function programming subject:

- [Functional Programming HOWTO](https://docs.python.org/3.8/howto/functional.html)

---

## Defining functions
We can use Python to define any function that we want. A function should include:

- **name**, to be able to refer it later
- **documentation**, to explain the function (optional)
- **parameters**, that could be zero or more
- **body**, that contains all computations that the function is doing

In general, we can use `def` command to define functions like:
```python
def name(par1, par2, par3, ...):
  "Documentation."
  body
  return result
``` 

For example:
```python
def mult(a, b):
  "Two numbers multiplication."
  m = a * b
  return m

mult(12, 13)
## 156
```

In general, we can define three types of functions:

- **computative**, find the results by substituting parameters and doing calculations
- **iterative**, find the results by iteration (control flow tools)
- **recursive**, find the results by recursion (function itself)

In above example, we used a **computative** function to find `a * b`. Now let's use **iterative** method:
```python
def mult_itr(a, b):
  """
  Two integers multiplication by iteration.
  Note that a * b is equal to a + a + ... + a; b times.
  """   
  result = 0
  while b > 0:
    result += a
    b -= 1
  return result
 
mult_itr(12, 13)
## 156
```

We can also use **recursive** method such that:
```python
def mult_rec(a, b):
  """
  Two integers multiplication by recursion.
  Note that a * b is equal to a + a(b-1).
  """
  if b == 1:
    return a
  else:
    return a + mult_rec(a,b-1)

mult_rec(12, 13)
## 156
```

At each iteration, both iterative and recursive functions follow this pattern to find `12 * 13`:
```python
12
12 + 12
12 + 12 + 12
...
12 + 12 + ... + 12 (13 times)
```

For another example let's compute an integer factorial with all mentioned methods:
```python
def fact(n):
  "Compute n factorial by using Python math library"
  import math
  return math.factorial(n)

fact(6)
## 720

def fact_itr(n):
  """
  Compute n factorial by iteration.
  Note that n! is equal to n(n-1)(n-2)...1.
  """
  result = 1
  while n > 1:
    result *= n
    n -= 1
  return result
 
fact_itr(6)
## 720

def fact_rec(n):
  """
  Compute n factorial by recursion.
  Note that n! is equal to n(n-1)!.
  """
  if n == 1:
    return n
  else:
    return n * fact_rec(n-1)
    
fact_rec(6)
## 720
```

Each of the above method has their pros and cons. For instance, let's try a function that returns numbers in Fibonacci series:
```python
def fib(n):
  """
  Function to return nth Fibonacci number.
  By using Binet's Fibonacci number formula.
  """
  phi = 5**0.5
  if n < 2:
    return n
  else:
    return ((1+phi)**n - (1-phi)**n)/(2**n * phi)

[fib(x) for x in range(12)]
## [0, 1, 1.0, 2.0, 3.0000000000000004, 5.000000000000001, 8.000000000000002, 13.000000000000002, 21.000000000000004, 34.00000000000001, 55.000000000000014, 89.00000000000003]
  
def fib_itr(n):
  """
  Iterative function to return nth Fibonacci number.
  Note that Fibonacci series is 0, 1, 0+1=1, 1+1=2, 1+2=3, 2+3=5, ... .
  """
  series = []
  a, b = 0, 1
  while len(series) < n:
    series.append(a)
    a, b = b, a + b
  return a
 
[fib_itr(x) for x in range(12)]
## [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]

def fib_rec(n):
  """
  Inefficient recursive function to return nth Fibonacci number.
  Note that Fibonacci series is f(n-2) + f(n-1).
  """
  if n < 2:
    return n
  else:
    return fib_rec(n-2) + fib_rec(n-1)

[fib_rec(x) for x in range(12)]
## [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
```

Here, computative method provides an estimation (which is actually a very good estimation) of the Fibonacci number and recursive method requires a lot of time as `n` gets bigger since at each iteration it needs to compute two `fib_rec` such that (for `n = 5`):
```python
              fib_rec(5)
           _______|________
          |                |
      fib_rec(4)       fib_rec(3)
       ___|___          ___|___
      |       |        |       |
   fib(3)  fib(2)   fib(2)     1
    __|__    __|__   __|__ 
   |     |  |     | |     |
 fib(2)  1  1     0 1     0
 __|__
|     |
1     0
```

Therefore, it is very important to always choose the right approach based on the function context.

Python provides another method that let us to write functions in a very compact way that called **lambda** function.

## Lambda function
Python includes a quick one-line construction of functions that is often convenient to make your code compact. In general we can write lambda function such that:
```python
name = lambda par1, par2, par3, ...: body
```

For example:
```python
cube = lambda x: x**3

cube(2)
## 8
```

Which is same as:
```python
def cube(x):
  return x**3

cube(2)
## 8
```

For another example, let's find Euclidean norm of a vector by a lambda function:
```python
pnorm = lambda v, p = 2: sum([abs(x)**p for x in v])**(1/p)
 
## Example
v = [2,3,4]
pnorm(v)
## 5.385164807134504

pnorm(v,1)
## 9.0
 ```
 
Or for instance, let's replace an string in a mathematical formula with a number and find the answer:
```python
re = lambda f, x, z: eval(f.replace(str(x), str(z)))

## Example
f = '2*x + 5'
re(f,'x',2)
## 9
```

For last example in here, let's **def**ine single limit formula to find the second derivative of **f(x) = x^3** for **x = 2** by using **lambda**:
```python
def deriv2nd(f, x, h = 1E-6):
  "Single limit formula."
  return (f(x-h) - 2*f(x) + f(x+h))/float(h**2) 

f = lambda x: x**3
deriv2nd(f, 2)
## 12.002843163827492
```
 
As we know, the second derivative of `f(x) = x^3` is equal to `3 * x^2` which is equal to **12** for `x = 2`.

## Map and filter
Map and filter are two Python built-in functions that let us to expand our function programming tools. In general, **map** function is:
```python
map(function, iterable, ...)
```

When a *function*, that could be another built-in function or a created function by **def** or **lambda**, applies on each element of an *iterable* (i.e. lists, tuples or dictionaries - see [here](https://docs.python.org/3.8/howto/functional.html#iterators) to learn more). For an example let's assume we have sales rate for each month during each season of a year and are interested to know what is the total seasonal sales:
```python
sale = [(1,3,4,5),(3,4,5,6),(7,6,5,5),(8,6,9,1)]
seasonal = list(map(sum, sale))
seasonal
## [13, 18, 23, 24]
```

We can answer the above question without using **map** by:
```python
sale = [(1,3,4,5),(3,4,5,6),(7,6,5,5),(8,6,9,1)]
seasonal = []
for i in sale:
  seasonal.append(sum(i))

seasonal
## [13, 18, 23, 24]
```

As you can see, without **map** we need a loop to address each element of the *iterable*. 

For another example, let's assume we have an *iterable* of strings (e.g. a list of names) and want them to be in lowercase:
```python
fruit = ['APPLE','ORANGE','PEACH','BANANA']
list(map(str.lower, fruit))
## ['apple', 'orange', 'peach', 'banana']
```

Or we can use **map** to round a list of float numbers:
```python
flt = [2.0678,3.9870,4.7869,5.3459]
list(map(round, flt, [2]*len(flt)))
## [2.07, 3.99, 4.79, 5.35]
```

In the above function we have two *iterable*s, one a list of numbers (`flt`) and one a list of floating numbers (`[2,2,2,2]`).

We can also use **map** to create new functions. For instance, let's define `zip_diy` function that do same operation as Python `zip` function:
```python
def zip_diy(x,y):
  return map(lambda a, b: (a,b), x, y)

## Example
list_1 = [1,2,3]
list_2 = [3,2,1]
list(zip_diy(list_1, list_2))
## [(1, 3), (2, 2), (3, 1)]

list(zip(list_1, list_2))
## [(1, 3), (2, 2), (3, 1)]
```  

As you noticed, **map** in `zip_diy` includes a **lambda** function that generates `(a,b)` tuple for each element in given *iterables*, `x` and `y`.   

**Filter** is another important tool in function programming. As you probably guessed, **filter** lets us to filter an *iterable*. In general, **filter** function is:
```python
filter(function, iterable)
```

When the *function* is required to return a boolean type (`True/False`) by testing each element of the *iterable*. For an example let's select numbers greater than **22** in `number` list in below:
```python
number = [88,22,11,33,2,99]
list(filter(lambda x: x > 22, number))
## [88, 33, 99]
```

Traditionally we can use the following loop to filter `number` list:
```python
number = [88,22,11,33,2,99]
select = []
for i in number:
  if i > 22:
    select.append(i)

select
## [88, 33, 99]
```

Now let's define a function to return numbers (integer, float and complex) from a list of numbers and strings:
```python
def return_num(lis):
  return filter(lambda x: isinstance(x, (int,float,complex)), lis) 

## Example
test = [2.05, 3, 'aaa', 4.23, 'bbb', 7j]
list(return_num(test))
## [2.05, 3, 4.23, 7j]
```

---
Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
