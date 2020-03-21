# Lambda function
*[Ashkan Mirzaee](https://ashki23.github.io/index.html) - November 2019*

Python includes a quick one-line construction of functions that is often convenient to make your code compact. For example:
```python
f = lambda x: x**3 + 6
f(2)
# 14
```

Which is same as:
```python
def f(x):
  return x**3 + 6
f(2)
# 14
```

For another example:
```python
g = lambda x,y,z: x*y/z
g(2,3,4)
# 1.5
```

which is same as:
```python
def g(x,y,z):
  return x*y/z
g(2,3,4)
# 1.5
```

In general,
```python
def fun(arg1,arg2,arg3,...):
  return expression
```

Can be written as
```python
fun = lambda arg1,arg2,arg3,...: expression
```

For example It is possible to write a single limit for the second derivative:
```python
def deriv2nd(f,x,h=1E-6):
  r = (f(x-h) - 2*f(x) + f(x+h))/float(h**2) 
  return r
 
# Example
f = lambda x: x**3
deriv2nd(f,2)
# 12.002843163827492
```
 
We know that the second derivative of `f(x) = x^3` is equal to `6*x` and is equal to 12 for `x = 2`.

Also, we can replace an string in a mathematical formula with a number to find the answer. For example, lets find the answer for `6*x` at `x = 2`:
```python
re = lambda f,x,z: eval(f.replace(str(x),str(z)))
 
# Example
f = '3*x'
re(f,'x',2)
# 12
```

Note that we can find the derivative of functions by using **SymPy** package.

And for another example let's find Euclidean norm of a vector by:
```python
pnorm = lambda v,p=2: sum([abs(x)**p for x in v])**(1/p)
 
# Example
v = [2,3,4]
pnorm(v)
# 5.385164807134504
pnorm(v,1)
# 9.0
```
 
Another fun example is finding palindrome words:
```python
def pal(x):
  return x == x[::-1]
## Or
pal = lambda x: x == x[::-1]

pal('pop')
## True
pal('pub'):
## False
pal('madam')
## True
```
---
Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
