# String formatting or interpolation operator
[Python standard library](https://docs.python.org/3/library/stdtypes.html?highlight=string%20interpolation#printf-style-string-formatting)

String objects have one unique built-in operation: the `%` operator (modulo). This is also known as the string formatting or interpolation operator. Given format `%` values (where format is a string), `%` conversion specifications in format are replaced with zero or more elements of values.

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

num = [1,2,3]
for i in num:
    print("===", i)
    f = open("file-%d.sh" % (i),'w')
    f.write("""                                                                                       
    #!/bin/bash                                                                                       
    echo file %d                                                                                   
    """ % i))
    f.close()

for i in num:
    os.system("bash file-%d.sh" % (i))

# === 1
# === 2
# === 3
# file 1
# file 2
# file 3
```
