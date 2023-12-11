[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/02-05%20Exception%20Handling.ipynb) 

> Click above image to access the interactive version of this notebook


## 02 - 05 Exception Handling
An exception is a python object that represents an error. It is an event, which occurs during the execution of a program that disrupts the normal flow of the program's instructions. When such a situation occurs and if python is not able to cope with it, it raises and exception. We have been seeing errors like TypeError and NameError or IndentationError throughout our tutorial which caused our application or that code to stop the execution. To prevent this from happening, we have to handle such exceptions.
Following is a hierarchy for built-in exceptions in python:

```
BaseException
 +-- SystemExit
 +-- KeyboardInterrupt
 +-- GeneratorExit
 +-- Exception
      +-- StopIteration
      +-- StandardError
      |    +-- BufferError
      |    +-- ArithmeticError
      |    |    +-- FloatingPointError
      |    |    +-- OverflowError
      |    |    +-- ZeroDivisionError
      |    +-- AssertionError
      |    +-- AttributeError
      |    +-- EnvironmentError
      |    |    +-- IOError
      |    |    +-- OSError
      |    |         +-- WindowsError (Windows)
      |    |         +-- VMSError (VMS)
      |    +-- EOFError
      |    +-- ImportError
      |    +-- LookupError
      |    |    +-- IndexError
      |    |    +-- KeyError
      |    +-- MemoryError
      |    +-- NameError
      |    |    +-- UnboundLocalError
      |    +-- ReferenceError
      |    +-- RuntimeError
      |    |    +-- NotImplementedError
      |    +-- SyntaxError
      |    |    +-- IndentationError
      |    |         +-- TabError
      |    +-- SystemError
      |    +-- TypeError
      |    +-- ValueError
      |         +-- UnicodeError
      |              +-- UnicodeDecodeError
      |              +-- UnicodeEncodeError
      |              +-- UnicodeTranslateError
      +-- Warning
           +-- DeprecationWarning
           +-- PendingDeprecationWarning
           +-- RuntimeWarning
           +-- SyntaxWarning
           +-- UserWarning
           +-- FutureWarning
       +-- ImportWarning
       +-- UnicodeWarning
       +-- BytesWarning
```

Let's take a look at an example


```python
1 / 0
```


    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-1-bc757c3fda29> in <module>
    ----> 1 1 / 0
    

    ZeroDivisionError: division by zero


Quite a straightforward example where we are trying to divide a number by 0. Python raises a `ZeroDivisionError` and the execution halts. There are basically two ways to handle this error. 

Check to make sure that the divisor is not zero.

Use `try-catch` block. Place the code to be executed inside the try block and place the exception to be handled in the except block.

Give this a try in your notebook if you’d like.


```python
for i in range(3, -3, -1):
    try:
        print(1.0 / i)
    except ZeroDivisionError:
        print("So, you're trying to divide by zero huh?")
```

    0.3333333333333333
    0.5
    1.0
    So, you're trying to divide by zero huh?
    -1.0
    -0.5


As observed from the above example, our execution continued even after we tried dividing 1.0 by zero.
> Python2 users.. Check the division that is being performed. To obtain floating point answer, you have to convert any one of the operand to float

> Python3 users.. you don't HAVE to do this. You can simply perform integer division and get floating point output

### Argument of an Exception

An exception can have an argument, which is a value that gives additional information about the problem that caused the exception. The contents of argument vary by exception.


```python
for i in range(3, -3, -1):
    try:
        print(1.0 / i)
    except ZeroDivisionError as err:
        print('Zero Division Error: ', str(err.args[0]))
```

    0.3333333333333333
    0.5
    1.0
    Zero Division Error:  float division by zero
    -1.0
    -0.5


### 02 - 05.02 Hierarchy of Exceptions

The exceptions are organized in an hierarchy as observed from above tree. This means that we can have multiple exceptions handled by the except block.


```python
# time module has a sleep method which will help slow down the execution of loop
import time 
i = -2
while i < 5:
    i = i + 1
    try:
        print(1.0 / i)
        # This will halt the code for 2 seconds
        time.sleep(2)
    except KeyboardInterrupt:
        # Lets raise the exception that we just caught!
        raise KeyboardInterrupt('Ctrl C pressed')
    except ZeroDivisionError:
        print("So, you're trying to divide by zero huh?")
```

    -1.0
    So, you're trying to divide by zero huh?
    1.0
    0.5
    0.3333333333333333
    0.25
    0.2


After starting the execution of the code, wait for few seconds and then press `i` key twice on your keyboard and you should get the above error (another way is to click on `Kernel -> Interrupt` ). The new thing that we can observe in this code is that we have used a keyword `raise`. This helps in raising a particular exception and as a parameter to the exception you can pass the string that you want to print. 

The raise statement does two things: it creates an exception object, and immediately leaves the expected program execution sequence to search the enclosing `try` statements for a matching `except` clause. The effect of `raise` statement is to either divert execution in a matching `except` suite, or to stop the program (if no proper exception handling was performed).

Now lets see the above example with hierarchy in action:


```python
import time
i = -2
while i < 5:
    i = i + 1
    try:
        print(1.0 / i)
        time.sleep(2)
    except BaseException:
        print('Some Exception occurred..')
```

    -1.0
    Some Exception occurred..
    1.0
    0.5
    0.3333333333333333
    0.25
    0.2


In the above example we can see that we did implement a handler (a very bad kind, I must say). If you check from the hierarchy list, you can observe that `KeyboardInterrupt` and `ArithmeticError`(which includes `ZeroDivideError`) are subclass of `BaseException` class. So since we implemented `BaseException` handler, all the errors under the base class are handled. 

Avoid raising a generic exception like we did in this example because you will not be able to understand what actually caused the exception and allows bugs to pass through. Instead use the most specific Exception constructor that semantically fits your issue.

### 02 - 05.03 Finally

`finally` keyword is a clause which contains the block of code that will always be executed regardless of whether there was any exception in the code or not. This is generally used to cleanup some resources in a program.. especially when using file I/O operations


```python
fhandler = None
try:
    # Open file in read-only mode. Try renaming file to test1.txt
    fhandler = open('./sample_datasets/test.txt', 'r')
    # Read all lines
    print(fhandler.readlines())
except IOError:
    print('Error Opening File')
finally:
    # If the file was opened
    if fhandler:
        # Close the file
        fhandler.close
```

    ['Alteration literature to or an sympathize mr imprudence. Of is ferrars subject as enjoyed or tedious cottage. Procuring as in resembled by in agreeable. Next long no gave mr eyes. Admiration advantages no he celebrated so pianoforte unreserved. Not its herself forming charmed amiable. Him why feebly expect future now. Preserved defective offending he daughters on or. Rejoiced prospect yet material servants out answered men admitted. Sportsmen certainty prevailed suspected am as. Add stairs admire all answer the nearer yet length. Advantages prosperous remarkably my inhabiting so reasonably be if. Too any appearance announcing impossible one. Out mrs means heart ham tears shall power every.']


In the above example we can observe that we are trying to open a file and read its contents. If the file doesn't exist, it will raise an IOError exception. We are handling that, no worries. However once the file has been read, we need to close the file so that other processes or other functions in our code can access it. (Remember: when accessing/ modifying a file, the file is locked to that process which is performing the I/O operation on it. Unless the lock is released, no other process will be able to modify it.. ) 

To make sure we release the resources, in the `finally` block we are checking if fhandler is not null and closing it. 
