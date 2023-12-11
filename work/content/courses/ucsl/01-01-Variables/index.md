[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/01-01%20Variables.ipynb) 

> Click above image to access the interactive version of this notebook 

## Variables
As the name implies, a variable is something that can change. A variable is just a way of referring to a memory location used by a Python program. Based on the datatype of the variable, the Python interpreter allocates the memory and decides what can be stored in the reserved memory. This makes Python a dynamically-typed language

If you are familiar with other programming languages like C, C++ or Java it might be tempting to consider variable as just a container to store data. However in Python, you can at best, think of variables as pointers. This is why you can dynamically change the type of data that a variable is pointing at. 

### Assigning values to variables

One of the main differences between Python and strongly typed languages like C++ or Java is the way it deals with the data types. In languages like C++ or Java, every variable must have a unique data type (i.e if a variable is of type string it cannot store integers or floats). Moreover, every variable has to be declared before it can be used, thus binding it to the data type that can be stored in it. Python variables do not need explicit declaration to reserve memory space. The declaration happens automatically when a value is assigned to a variable. This means that a variable that was used to store a string can now be used to store an integer. Try it out.

Do something like this


```python
var = 'I am in NYC'
print(var)
```

    I am in NYC


**var** is a string in the above case.

Well.. don't take our word for it. Let's confirm. If we run the next line,


```python
type(var)
```




    str



As we saw in the grid in the 01.00, Type is a built-in function that returns any datatype If we point our variable var to, lets say, an integer, it will return int 


```python
var = 123
type(var)
```




    int



**So what are the rules of naming a variable?**

Every language has some rules for naming the identifier of variables (aka the variable name). In Python, a valid identifier is a non-empty sequence of characters of any length with:

The start of the character can be an underscore _ or a capital or lowercase letter. However, it is generally recommended to use all uppercase for global variables and all lower case for local variables. The letters following the first letter can be a digit or a string. Python is a case-sensitive language. Therefore, **var** is not equal to **VAR** or **vAr**.

Apart from the above restrictions, Python keywords cannot be used as identifier names. These are:

||||||
|:-------|:--------|:---------|:--------|:----|
|and     |del      |from      |not      |while|
|as      | elif    |global    |or       |with |
|assert  | else    | if       |pass     |yield|
|break   | except  | import   |print
|class   | exec    | in       |raise
|continue| finally | is       |return 
|def     | for     | lambda   |try


###  Multiples
Python allows you to assign a single value to several variables simultaneously. For example:


```python
x = y = z = a = 1
```

or even assign different values to different variables:


```python
x, y, z, a = 'Hello', 'World', 1, 2
print (x,y,z,a)
```

    Hello World 1 2


Try printing the above variables. Hint: The key to printing lies above!
