# Complex numbers

Python supports computation with complex numbers. The imaginary unit is written as `j` in Python, 
instead of `i` as in mathematics ([Mathematical functions for complex numbers](https://docs.python.org/3/library/cmath.html)). You can generate complex numbers by two following methods:
```python
a = 2j
print(a)
# 2j
b = complex(0,2)
print(b)
# 2j
c = 2+0.5j
print(c)
# 2+0.5j
d = complex(2,0.5)
print(d)
# 2+0.5j
```

To use mathematical functions for complex numbers we can use `cmath` module. For emaple:
```python
import cmath
cmath.sqrt(-1)
# 1j
cmath.sin(1j)
# 1.1752011936438014j
```
