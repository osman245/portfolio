[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/01-05%20Control%20Flow.ipynb) 

> Click above image to access the interactive version of this notebook


## Control Flow
Generally, a program is executed sequentially and once executed it is not repeated again. There may be a situation when you need to execute a piece of code n number of times, or maybe even execute certain piece of code based on a particular condition.. this is where the control flow statements come in.

In this section, we will be covering:

- Conditional statements -- if, else, and elif
- Loop statements -- for, while
- Loop control statements -- break, continue, pass

### Conditional Statements
Conditionals statements are used to change the flow of execution. You can use the relational operators, logical operators and membership operators for performing condition checks


```python
result = 1
if result == 1:
    print("Best Match")
elif result <= 3:
    print("Close Enough")
else:
    print("This is Blasphemy!")
```

    Best Match


The logic is very simple.. *`if`* < `condition_is_met` >, *`then`* do something; *`else`* do something else. 

Python adopts the `if`-`else` clause as it is used in many languages.. However the `elif` part is unique to python. `elif` simply is a contraction for `else if`.

### Loop Statements
These statements are used when we want to execute a piece of code multiple times. Python has two types of loops -- `for` loop and `while` loop.


```python
for i in [0,1,2]:
    print("{}".format(i))
```

    0
    1
    2


In `for` loop, we specify the variable we want to use, the `iterator` we want to loop over, and use the `in` (membership) operator to link them together.


```python
i = 2
while i >= 0:
    print("{}".format(i))
    i -= 1
```

    2
    1
    0


As you can see, they both serve different purposes. For loop is used when you want to run something for fixed amount of times, whereas while loop can theoretically run forever (if you use something like `while True:` .. *dont!* ). 

One of the most commonly used `iterator` with for loop is the `range` object which is used to generate the sequence of numbers


```python
list(range(10))
```




    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]



The `range` requires the *stop* argument. It can also accept *start* (at first position) and *step* (at third position) as arguments but if not passed, it creates a sequence of numbers from `0` till `stop - 1`. Remember, the *stop* is not included in the output


```python
# With start and stop
list(range(2, 20))
```




    [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]




```python
# With start, stop and step
list(range(2, 20, 2))
```




    [2, 4, 6, 8, 10, 12, 14, 16, 18]



When you have an iterator of iterators .. for example a list of lists .. then you can use what is known as nested loops to flatten the list.


```python
# This is not the best way.. but for the sake of completion of
# topic, this example is included.
arr = [range(3), range(3, 6)]
for lists in arr:
    for elem in lists:
        print(elem)
```

    0
    1
    2
    3
    4
    5


### Loop Control Statements
Loop control statements change the executing of loop from its normal sequence.

#### Break

It terminates the current loop and resumes the execution at the next statement. The most common use for break is when some external condition is triggered requiring a hasty exit from a loop. The break statement can be used in both while and for loops.


```python
for i in range(1, 10):
    if i == 5:
        print('Condition satisfied')
        break
    print(i)  # What would happen if this is placed before if condition?
```

    1
    2
    3
    4
    Condition satisfied


#### Continue
Continue statement returns the control to the beginning of the loop. The continue statement rejects all the remaining statements in the current iteration of the loop and moves the control back to the top of the loop.


```python
for i in range(1, 10):
    if i == 5:
        print('Condition satisfied')
        continue
        print("whatever.. I won't get printed anyways.")
    print(i)
```

    1
    2
    3
    4
    Condition satisfied
    6
    7
    8
    9


#### Pass
Pass is used when a statement is required syntactically but performs a null operation i.e. nothing happens when the statement is executed.


```python
for i in range(1, 10):
    if i == 5:
        print('Condition satisfied')
        pass
    print(i)
```

    1
    2
    3
    4
    Condition satisfied
    5
    6
    7
    8
    9


As you can see execution of pass statement had no effect on the flow of the code. It wouldn't have mattered if it was not there. 

It is generally used as a temporary placeholder for an unimplemented logic. For example lets say you have written a function (we'll learn about functions a little later) and want to test the remaining part of code without actually running your function.. You can use pass statement in such cases. Python interpreter will read that and skip that part and get on with further execution.

### Loops with else
Python's Loop statements can be accompanies with an else block in cases where a certain block of code needs to be executed after the loop has successfully completed its execution i.e. iff the loop didn't `break` out in the middle of execution



```python
best = 11
for i in range(10):
    if i >= best:
        print("Excellent")
        break
    else:
        continue
else:
    print("Couldn't find the best match")
```

    Couldn't find the best match


Now if we change the `best` to something less than `10`


```python
best = 9
for i in range(10):
    if i >= best:
        print("Excellent")
        break
    else:
        continue
else:
    print("Couldn't find the best match")
```

    Excellent


You can implement similar functionality using the `while` loop.
