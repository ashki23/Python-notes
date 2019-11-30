# Lambda function

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
def deriv2nd(f, x, h = 1E-6):
  r = (f(x-h) - 2*f(x) + f(x+h))/float(h**2) 
  return r
 
 deriv2nd(lambda x: x**3, x = 2, h = 1E-6)
 # 12.002843163827492
 ```
 
 Which we know for f(x) = x^3 the second derivative f(x)'' = 6x is equal to 12 for x = 2.
 
 For another example let's replace an string in a mathematical formula with a number and find the answer:
 ```python
 re = lambda f,x,z: eval(f.replace(str(x),str(z)))
 
 # Example
 f = '2*x + 5'
 re(f,'x',2)
 # 9
 ```
