# Regular expression

Regular expressions (called REs, or regexes, or regex patterns) are essentially a tiny, highly specialized programming language embedded inside Python and made available through the re module. Using this little language, you specify the rules for the set of possible strings that you want to match; this set might contain English sentences, or e-mail addresses, or TeX commands, or anything you like. You can then ask questions such as “Does this string match the pattern?”, or “Is there a match for the pattern anywhere in this string?”. You can also use REs to modify a string or to split it apart in various ways. (from [Python HOWTOs](https://docs.python.org/3/howto/regex.html#regex-howto))

Sources
- [Python HOWTOs](https://docs.python.org/3/howto/regex.html#regex-howto)
- [Python *re* library](https://docs.python.org/3/library/re.html)

Examples
```python
import re

re.findall('begin', 'begin with this example for beginning') # find all 'begin's in text
# ['begin', 'begin']

re.findall('^begin', 'begin with this example for beginning') # find 'begin' only at the beginnig (^) of text
['begin']

re.findall('begin$', 'this is another begin') # search only last word ($)
# ['begin']

re.findall('.*begin', 'this is another begin') # search 'begin' and everything before (.*)
# ['this is another begin']

re.findall('goo?al','goal vs goooooal') # zero or one (?) 'o' character
# ['goal']

re.findall('goo*al','goal vs goooooal') # zero or more (*) 'o' character
# ['goal', 'goooooal']

re.findall('goo+al','goal vs goooooal') # one or more (*) 'o' character
# ['goooooal']

re.findall('\d', 'today is Oct 10') # Find digits (\d)
# ['1', '0']

re.findall('\d{2}', 'today is Oct 10') # Find two digits (\d{2})
# ['10']

re.findall('\w', 'today is Oct 10') # find any words (\w)
# ['t', 'o', 'd', 'a', 'y', 'i', 's', 'O', 'c', 't', '1', '0'] 

re.findall('\w+', 'yesterday was October 9') # find any word with one or more (+) characters
# ['yesterday', 'was', 'October', '9']

re.findall('\w{4}\w*', 'yesterday was October 9') # find any word with 4 letters or more
# ['yesterday', 'October']

re.findall('[A-Z]..', 'yesterday was October 9') # find any capital word ([A-Z]) and two characters after (..)
# ['Oct']

re.findall('([A-Z][a-z]* \d+)', 'yesterday was October 9') # find any capital letter ([A-Z]) followed by two small letters ([a-z]{2}) and a space ( ) and two digits (\d{2})
# ['October 9']

re.findall('(?<=; )[\w ]*', 'I want everything after; this part is important') # after (\w = [a-zA-Z0-9_])
# ['this part is important']

re.findall('[\w ]+(?=;)', 'I want everything before; this part is not important') # before
# ['I want everything before']

mm = re.match('[\w ]*(?=;)', 'I want everything before; this part is not important') # before
mm.group(0)
# 'I want everything before'
```

---
Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
