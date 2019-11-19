# Regular expression
"Regular expressions (called REs, or regexes, or regex patterns) are essentially a tiny, highly specialized programming language 
embedded inside Python and made available through the re module. Using this little language, you specify the rules for the set 
of possible strings that you want to match; this set might contain English sentences, or e-mail addresses, or TeX commands, 
or anything you like. You can then ask questions such as “Does this string match the pattern?”, or “Is there a match for 
the pattern anywhere in this string?”. You can also use REs to modify a string or to split it apart in various ways." - from [Python HOWTOs](https://docs.python.org/3/howto/regex.html#regex-howto)

Sources
- [Python HOWTOs](https://docs.python.org/3/howto/regex.html#regex-howto)
- [Python *re* library](https://docs.python.org/3/howto/regex.html#regex-howto)

Examples
```python
import re

re.findall('begin', 'begin with this example for beginning') # find all 'begin's in text
# ['begin', 'begin']

re.findall('^begin', 'begin with this example for beginning') # find 'begin' only at the beginnig (^) of text
['begin']

re.findall('^begin', 'this is another begin') # no begin at the beginning
# []

re.findall('begin$', 'this is another begin') # search only last word ($)
# ['begin']

re.findall('.*begin', 'this is another begin') # search 'begin' and everything before (.*)
# ['this is another begin']

re.findall('goo?al','goal vs goooooal') # zero or one (?) of charcter 'o'
# ['goal']

re.findall('goo*al','goal vs goooooal') # zero or more (*) of character 'o'
# ['goal', 'goooooal']

re.findall('goo+al','goal vs goooooal') # one or more (*) of character 'o'
# ['goooooal']

re.findall('\d', 'today is Oct 10') # Find digits (\d)
# ['1', '0']

re.findall('\d{2}', 'today is Oct 10') # Find two digits (\d{})
# ['10']

re.findall('\w', 'today is Oct 10') # find any words (\w)
# ['t', 'o', 'd', 'a', 'y', 'i', 's', 'O', 'c', 't', '1', '0'] 

re.findall('\w+', 'today is Oct 10') # find any words with one or more (+) characters
# ['today', 'is', 'Oct', '10']

re.findall('\w{3}', 'today is Oct 10') # find any word with 3 or more letters
# ['tod', 'Oct']

re.findall('[A-Z]..', 'today is Oct 10') # find any capital word ([A-Z]) and two characters after (..)
# ['Oct']

re.findall('([A-Z][a-z]*)', 'today is Oct 10') # find any capital word ([A-Z]) and zero or more (*) latters right after ([a-z])
# ['Oct']

re.findall('[A-Z][a-z]{2} \d{2}', 'today is Oct 10') # find any capital letter ([A-Z]) followed by two small letters ([a-z]{2}) and a space ( ) and two digits (\d{2})
# ['Oct 10']

```