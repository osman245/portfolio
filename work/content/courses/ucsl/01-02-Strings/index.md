[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/01-02%20Strings.ipynb) 

> Click above image to access the interactive version of this notebook

## 01 - 02 Python Strings
A python string is usually a bit of text that you want to display or use or export out of the program that you are writing (to a file or over the network). Technically, strings are immutable `sequence` of characters.
> We will talk and learn more about sequences in Data Structures module.

Python has a built-in string class called `str` with many handy features. Python knows you want something to be a string when you enclose the text with either single quotes ( ' ) or double quotes ( " ). You must've seen this in our previous tutorials. If not, check a very basic example below:


```python
var = 'Hello World'
print("Contents of var: ", var)
print("Type of var: ", type(var))
```

    Contents of var:  Hello World
    Type of var:  <class 'str'>


A string literal can span multiple lines, to do that there must be a backslash ( `\` ) at the end of each line to escape the newline because by default the return key on the keyboard is considered as the end of line. However if you do not feel comfortable using backslashes, you can put your text between triple quotes ( `"""` ) or ( `'''` ). If you don't want characters prefaced by `\` to be interpreted as special characters, you can use raw strings by adding an alphabet`r` before the first quote. A very basic example would be something like this:


```python
print('C:\name\of\dir')  # even using triple quotes won't save you!
```

    C:
    ame\of\dir



```python
print(r'C:\name\of\dir')
```

    C:\name\of\dir


### 01 - 02.01 String Concatenation
Python strings are 'immutable'. What it means is that they cannot be changed after they are created. So if we concatenate the two strings, python will take the two strings and build a new, third string, with the concatenated value of the first and the second string.


```python
var1 = 'Hello'  # String 1
var2 = 'World'  # String 2
var3 = var1 + var2  # Concatenate two string as String 3
print(var3)
```

    HelloWorld


Concatenation of strings will also happen when the string literals are placed next to each other.


```python
var1 = 'Hello' 'World'
print(var1)
```

    HelloWorld


Concatenation can only be preformed on variables of same datatype. i.e a string concatenation can only be performed on two strings or two variables that have str as their datatype. If you try to perform string concatenation on a string and an integer, Python will trow a `TypeError`.


```python
var1 = 'Hello'
var2 = 1
print(var1+var2)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-6-974e56630dc5> in <module>
          1 var1 = 'Hello'
          2 var2 = 1
    ----> 3 print(var1+var2)
    

    TypeError: can only concatenate str (not "int") to str


### 01 - 02.02 String Indexing
Characters in a string can be accessed using the standard [ ] syntax. Python uses zero-based indexing which means that first character in a string will be indexed at `0th` location. So, for example if the string is '`Python`' then, its length can be obtained as


```python
var1 = 'Python'
len(var1)
```




    6



and its positional values can be obtained by


```python
var1[0]
```




    'P'




```python
var1[5]
```




    'n'



Now, if we try to change the positional value to something else, we will get a `TypeError` proving that strings are immutable


```python
var1[0] = 'J'
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-10-a207e949a80e> in <module>
    ----> 1 var1[0] = 'J'
    

    TypeError: 'str' object does not support item assignment


Apart from obtaining positional values of `var1` using (*positive*) index values between `0` to `5` (or between `0` and `len(var1)-1`), we can also index it by entering negative index values


```python
var1[-6]
```


```python
var1[-1]
```

This works because when you enter a non negative index value, it is considered as indexed from **left to right** and when you enter the negative index values (negative indexing starts from `-1`), python's interpreter is intelligent enough to understand that you meant to get the value indexed from right to left.
```
       +---+---+---+---+---+---+
       | P | y | t | h | o | n |
       +---+---+---+---+---+---+
         0   1   2   3   4   5 
        -6  -5  -4  -3  -2  -1
```

### 01 - 02.03 String Slicing
The 'Slice' syntax is a handy way to refer to sub-parts of strings. The slice `var1[start : end]` is the elements beginning at start and extending up to end (**not including end**). Look at the above Python string literals representation and work on following examples:


```python
var1[0:3]
```


```python
var1[:-3]
```


```python
var1[:2]+var1[-4:]
```

### 01 - 02.04 String Formatting
Everything that we have seen till now had a string that **cannot** be modified but what if we now want to modify a few words of the string and leave the remaining string unmodified?

For people familiar with C++, Python has a printf() - like facility to put together a string using `%` operator. Python uses `%d` operator to insert an integer, `%s` for string and `%f` for floating point. Example:


```python
text = '%s World. %s %d %d %f'
print(text)
```


```python
text %('Hello', 'Check', 1, 2, 3)
```

However, with the [PEP 3101](https://www.python.org/dev/peps/pep-3101/), the `%` operator has been replaced with a string method called `format` which can take arbitrary number of arguments.

According to this method, the "fields to be replaced" are surrounded by curly braces `{ }`. The curly braces and the "code" inside will be substituted with a formatted value from the arguments passed to the `format` method. Anything else, which is not contained in curly braces will be literally printed, i.e. without any changes.


```python
text = '{} World. {} {} {} {}'
# you can also do
# text = '{0} World. {1} {2} {3} {4}'
print(text)
```


```python
text.format('Hello', 'Check', 1, 2, 3)
```

Notice a minor difference in the output of `text` variable when we used `%`.. it is the datatype of value `3`. We want to pass the positional value as integer but want to make sure that it is formatted as a float in the final form. The way to do this is by specifying the type of value expected in the curly braces preceeded by a colon ( `:` )


```python
text = '{} World. {} {} {} {:.2f}'
# you can also do
#text = '{val1} World. {val2} {val3} {val4} {val5:.2f}'
print(text)
```


```python
text.format('Hello', 'Check', 1, 2, 3)
# if you uncomment the previous cell, then use this:
#text.format(val1='Hello', val2='Check', val3=1, val4=2, val5=3)
```

We will learn more neat tricks about `format` method as we proceed through the modules. Keep an eye out for such tricks.. 

### 01 - 02.05 Built-in String Methods
Now that we know about the string and some basic manipulation on strings, lets look at some more built-in methods that can be used. 

#### .. 02.05.01 capitalize
It returns a copy of the string with only its first character capitalized.
> Remember the same string is not modified because strings are immutable

Example:


```python
var1 = 'python'
var1.capitalize()
```

#### .. 02.05.02 center
Return the *input string* centered in a string of length width. Padding is done using the specified fill character (default is a space).

Example:


```python
var1.center(10, '!')
```

#### .. 02.05.03 count
The method count() returns the number of occurrences of a sub-string in the range [start, end].

Example:


```python
var1.count('t', 0, len(var1))
```

#### .. 02.05.04 endswith

TRUE if the string ends with the specified suffix, otherwise FALSE.


```python
var1 = "Hello World"
var1.endswith("World")
```

#### .. 02.05.05 find

It determines if the sub string occurs in string. Optionally between beg and end. If found, it returns the index value. Otherwise returns -1

Example:


```python
var2 = "This is a test string"
var2.find("is")
```




    2



#### .. 02.05.06 rfind

Same as find() but searches backwards in string

#### .. 02.05.07 index

Same as find but raises an exception if sub string is not found.

#### .. 02.05.08 isalnum

Returns true if the string has at least one character and all characters are alphanumeric and false otherwise.

Example:


```python
var3 = 'Welcome2015'
var3.isalnum()
```




    True



#### .. 02.05.09 join

Concatenates the string representations of elements in sequence into a string, with separator string.

Example:


```python
var1 = ''
var2 = ('p', 'y', 't', 'h', 'o', 'n')
var1.join(var2)
```




    'python'



#### .. 02.05.10 strip

Returns a copy of string in which all chars have been stripped from the beginning and the end of the string.

Example:


```python
var = '.......python'
var.lstrip('.')
```




    'python'



#### .. 02.05.11 rstrip

Removes all trailing whitespaces in a string.

#### .. 02.05.12 max

Returns the maximum alphabetical character from the string.

Example:


```python
var = 'python'
max(var)  # This is very helpful when used with integers
```




    'y'



#### .. 02.05.13 min

Returns the minimum alphabetical character from the string.

#### .. 02.05.14 replace

Returns a copy of the string with all occurrences of sub string old by new. If the optional argument max is given, only the first count occurrences are replaced.

Example:


```python
var = 'This is Python'
var.replace('is', 'was', 1)
```




    'Thwas is Python'



#### .. 02.05.15 rjust

Returns a space-padded string with the original string right-justified to a total width of width column

Example:


```python
var = 'Python'
var.rjust(10,'$')
```




    '$$$$Python'



#### .. 02.05.16 split

Returns a `list` of all the words in the string separated by a separator string.
> We will study about lists a little later.. for now, just remember that it is one of the data structure of python

Example:


```python
var = 'This is Python'
var.split(' ')
```




    ['This', 'is', 'Python']



These are the methods that you will end up using mostly. However, there are many more built in methods that you can access by pressing `tab` key on your keyboard after typing the variable name whose type is `str`. Go on.. try it.

For official documentation on Python Strings: 
- [for python3](https://docs.python.org/3.4/library/string.html)
- [for python2](https://docs.python.org/2/library/string.html)
