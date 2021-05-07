# String formatting or interpolation operator

## C-style (printf-style)

String objects have one unique built-in operation: the `%` operator (modulo). This is also known as the string formatting or interpolation operator. Given format `%` values (where format is a string), `%` conversion specifications in format are replaced with zero or more elements of values ([Python standard library](https://docs.python.org/3/library/stdtypes.html?highlight=string%20interpolation#printf-style-string-formatting)). 

Examples:

```python
num = [1,2,3]
for i in num:
  print("The number is: %d" % (i))

# The number is: 1
# The number is: 2
# The number is: 3
```

```python
num = [1,2,3]
for i in num:
  print("%d divided by %d is %f" % (i,i+1,i/(i+1)))
  
# 1 divided by 2 is 0.500000
# 2 divided by 3 is 0.666667
# 3 divided by 4 is 0.750000
```

```python
import os

file = [1,2,3]
for i in file:
  os.system("echo File number %s is available" % (i))

# File number 1 is available
# File number 2 is available
# File number 3 is available
```

The following is a list of some important string formatting specifications:

|Format|Meaning|
|---|---|
|`%s`|a string|
|`%d`|an integer|
|`%f`|a decimal with 6 decimals|
|`%e`|scientific notation (with `e`)|
|`%g`|compact decimal or scientific notation (with `e`)|
|`%.xy`|format y with x decimals, eg. `.12f`|


## F-string style

This method is avalable for Python 3.6 and higher. Review [here](https://docs.python.org/3/reference/lexical_analysis.html#formatted-string-literals) to learn more. 

```python
num = [1,2,3]
for i in num:
  print(f"The number is: {i}")

# The number is: 1
# The number is: 2
# The number is: 3
```
```python
num = [1,2,3]
for i in num:
  print(f"{i} divided by {i+1} is {i/(i+1)}")

# 1 divided by 2 is 0.500000
# 2 divided by 3 is 0.666667
# 3 divided by 4 is 0.750000
```

```python
import os

file = [1,2,3]
for i in file:
  os.system(f"echo File number {i} is available")

# File number 1 is available
# File number 2 is available
# File number 3 is available
```

---
Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
