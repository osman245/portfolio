[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/02-04%20Functions.ipynb) 

> Click above image to access the interactive version of this notebook


## Functions
Imagine that you have to open a file, read the contents of the file and close it. Pretty trivial, right? Now imagine that you have to read ten files, print their output or perform some computation on the contents and then close them. Now you don't want to sit there and type file i/o operations for every file. What if there are over 500 files?

This is where the functions come in. A function is a block of organized and reusable code in a program that performs a specific task which can be incorporated into a larger program or reused by passing different sets of parameters.

The advantages of using functions are:
- Allowing code reuse.
- Reducing code duplication.
- Improving readability while reducing the complexity of the code.

There are two basic types of functions: 
- Built-in functions 
- User defined functions. 

We have been using [built-in](https://docs.python.org/3/library/functions.html) functions for quite some time without actually understanding how a function works. This is the beauty of Python. According to [Guido van Rossum](https://en.wikipedia.org/wiki/Guido_van_Rossum), all objects in Python are first class citizens. Meaning all the objects (like function, strings, integers, etc) can be assigned to variables, placed in lists, stored in dictionaries, passed as arguments and so forth. We have been doing this the whole time, right? Now let’s see how you can create your own functions and call them in your code.

### Defining Functions

A function is defined using the `def` keyword followed by the name of the function. The parameters or the arguments should be placed within the parentheses followed by the function name. The code block within every function starts with a colon and should be indented.



```python
def mul(a, b):
    return('{} * {} = {}'.format(a, b, a*b))
    
print(mul(4, 5))
```

    4 * 5 = 20


In the above code we have used a keyword return. A function may or may not have a return value. The job of return is just to return the expression/ object to the the calling function. 

### Function Arguments

A function can be called by using following types of formal arguments:

- Required arguments
- Keyword arguments
- Default arguments
- Variable-length arguments

####  Required Arguments:

Required arguments are passed to a function in correct positional order. The number of arguments being passed should be equal to the number or arguments expected by the function that is defined. Let's take a look at the example:


```python
# Dumb example
def info(name, sem):
    print('My name is: ',name)
    print('This is semester',int(sem))
```


```python
info('Mohit', 2)
```

    My name is:  Mohit
    This is semester 2



```python
# What if we change the order in which we are passing the arguments?
info(2, 'Mohit')
```

    My name is:  2



    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-4-49e350bc57ab> in <module>
          1 # What if we change the order in which we are passing the arguments?
    ----> 2 info(2, 'Mohit')
    

    <ipython-input-2-297a0559a08b> in info(name, sem)
          2 def info(name, sem):
          3     print('My name is: ',name)
    ----> 4     print('This is semester',int(sem))
    

    ValueError: invalid literal for int() with base 10: 'Mohit'


We'll learn about how to prevent such errors from breaking our code in our next module on Exception Handling

#### Keyword Arguments:

Keyword arguments are related to the function calls. When you use keyword arguments in a function call, the caller identifies the arguments by the parameter name. This allows you to skip the arguments or place them out of order because python's interpreter will be able to match the values with parameters. Let's modify the way we are calling the above function.


```python
def info(name, sem=2):
    print('My name is: ',name)
    print('This is semester',int(sem))
```


```python
# The order of the parameter does not matter.
info(sem=2, name='Mohit')
```

    My name is:  Mohit
    This is semester 2



```python
# Not providing second argument.
info('Jack')
```

    My name is:  Jack
    This is semester 2


#### Variable Length Arguments: 

At some point, you may need to process the function for more than the arguments that you specified when you defined the function. These arguments can be of variable length and are not named in the function definition, unlike required and default arguments. So how do you handle this?


```python
def names(course, *names):
    print('Name of course: ',course)
    print('Name of students in the course:')
    for name in names:
        print(name)
```


```python
names('Python', 'Jim', 'Jack', 'Mat')
```

    Name of course:  Python
    Name of students in the course:
    Jim
    Jack
    Mat


An asterisk (`*`) is placed before the variable name that holds the values of all non keyword variable arguments. This tuple remains empty if no additional arguments are specified during the function call. 

### 02 - 04.03 Anonymous Functions

Anonymous functions do not have a name! They are not declared in the standard manner (using the def keyword). To create an anonymous function you use `lambda` keyword. They are part of the functional paradigm incorporated in Python.

Lambda forms can take any number of arguments but they return just one value in the form of an expression. They cannot contain commands or multiple expressions.

Lambda functions have their own local namespace (just like regular functions) and cannot access variables other than those in their parameter list or those in the global namespace.

Lambda function cannot be a direct call to print function.


```python
mul = lambda a, b: a*b
```


```python
print(mul(4, 5))
```

    20


### Map function
**Syntax:** 

`map(function, iterable)`

As the name suggests, `map` applies the `function` to every element in the `iterable`. 


```python
numbers = range(1, 10)
#numbers = 0,1,2..9 
def square(num):
    return num**2
```


```python
list(map(square, numbers))
# The equivalent of this function is:
# result = []
# for i in range(1, 10):
#     result.append(i**2)
```




    [1, 4, 9, 16, 25, 36, 49, 64, 81]



Even better, we can write the whole thing in a single line


```python
list(map(lambda x: x**2, range(1, 10)))
```




    [1, 4, 9, 16, 25, 36, 49, 64, 81]



### Filter function
**Syntax:** 

`filter(function, iterable)`

Just like map, `filter` applies the function to every element of the `iterable` but instead of returning the output of function, it returns the `list` of elements for which the function returns `True`


```python
# Return all values for which %2 is non zero.. (List of all odd numbers, right?)
list(filter(lambda x: x%2, range(1, 10)))
```




    [1, 3, 5, 7, 9]


