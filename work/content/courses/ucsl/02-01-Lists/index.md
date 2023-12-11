[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/02-01%20Lists.ipynb) 

> Click above image to access the interactive version of this notebook


## Lists
The `list` is one of the most versatile datatypes available in Python. It can be written as a group of comma-separated values between square brackets. Creating a list is as simple as separating items by comma between square brackets.

For example:


```python
# Notice the mix data types
my_list = ['Python', 'Julia', 1, 3.1415]
print("Contents of my_list: {}.\nType: {}".format(my_list, type(my_list)))
```

    Contents of my_list: ['Python', 'Julia', 1, 3.1415].
    Type: <class 'list'>


 `\n` is the escape character for line break

Note: Python is a zero-index based, thus to get the first item we simply ask for the item/ element on the 0th index. 

To get the item in the list, we simply pass the index of the required item to the list:


```python
my_list[0]
```




    'Python'



We will now look at some list manipulations techniques (which are similar to strings) and then look at some more methods that makes lists unique.

#### Slicing the List

When a list is sliced, a shallow copy (we’ll discuss shallow and deep copies in a moment) of the list is performed and a new list is created containing the requested elements.

For example:


```python
my_list = ['Python', 'Julia', 1, 3.1415]
# Performs shallow copy and returns a **new** list with first two elements
my_list[:2] # [:2] means between start=0 and stop=2 index values (excluding stop)
```




    ['Python', 'Julia']



The slicing can also  be done to get the **n-th** value from a list by passing n as the third argument.


```python
my_list[1::2]
```




    ['Julia', 3.1415]




```python
# Remember, it doesn't include the nth index value when traversing a list.
my_list[-3:-2:1]  # Take every element between index value -3 and -2
```




    ['Julia']



#### Updating the List

Unlike strings and tuples which are immutable, elements in list can be changed without having to create a new list, thus making it mutable.

For example:


```python
my_list = ['Python', 'Julia', 1, 3.1415]
my_list[2] = 'Java'
print('Original Contents: \n', my_list)
print('Original Length of array: \n', len(my_list))
# Remove some elements/ changing the size
my_list[2:4] = []
print('Modified Contents: \n', my_list)
print('Modified Length of array: \n', len(my_list))
```

    Original Contents: 
     ['Python', 'Julia', 'Java', 3.1415]
    Original Length of array: 
     4
    Modified Contents: 
     ['Python', 'Julia']
    Modified Length of array: 
     2


#### Appending to the List

New items can be easily added to the list by using the `append()` method.

Example:


```python
my_list = ['Python', 'Julia', 1, 3.1415]
my_list.append('C++') # It will append the item to the end of the list
print(my_list)
```

    ['Python', 'Julia', 1, 3.1415, 'C++']


#### Copying Lists

There are many ways to create a copy of the lists in python. Lets take a look at few techniques:

##### using copy package

A copy package is included in Python so you don't have to install it externally to use it. So why create a separate package? 

From our module on variables, we know that it is very easy to create a copy of objects. We also know that assignment statements ( '=' ) in Python do not copy the objects, they merely create bindings between targets and objects. But for collections that are mutable or contain mutable items, a copy is sometimes needed so that one can change the content of the mutable item without changing the other. 

There are actually two ways of creating a copy of an object: shallow copies and deep copies. In a shallow copy, Python constructs a new object and then inserts references to into it that are found in the original list. A deep copy, however, creates a new object and copies everything.

(If you are curious to know more about it, head over to the [`official documentation`](https://docs.python.org/3.4/library/copy.html) )


```python
import copy
my_list  = ['Python', 'Julia', 1, 3.1415]
my_list1 = copy.copy(my_list)  # Shallow copy.. Fast
my_list2 = copy.deepcopy(my_list)  # Deep copy.. Slower
```

##### using slice


```python
my_list = ['Python', 'Julia', 1, 3.1415]
my_list1 = my_list[:2]
print(my_list1)
```

    ['Python', 'Julia']


##### using list constructor


```python
my_list = ['Python', 'Julia', 1, 3.1415]
# when list method takes a list as a parameter, it creates a copy of that list
my_list1 = list(my_list)
print(my_list1)
```

    ['Python', 'Julia', 1, 3.1415]


#### Delete List Elements
To remove list elements, one has two options: either use the del statement or lists’ remove method (we will discuss this last one a bit more later). Here's an example:


```python
my_list = [1, 2, 3, 4, 5]
del(my_list[4])
my_list
```




    [1, 2, 3, 4]



#### Nested Lists
As the name suggests, nested lists are a list of elements where the element itself is another list. 

For example:


```python
my_list1 = [1, 2, 3, 4, 5]
my_list2 = ['a', 'b', 'c', 'd', 'e']
my_list3 = [my_list1, my_list2]
my_list3
```




    [[1, 2, 3, 4, 5], ['a', 'b', 'c', 'd', 'e']]



#### List Concatenation, Repetition, Membership:

These are simple list manipulation methods similar to strings. Take a look at following examples:


```python
my_list1 = [1, 2, 3, 4, 5]
my_list2 = ['a', 'b', 'c', 'd', 'e']
my_list1 + my_list2  # List Concatenation
```




    [1, 2, 3, 4, 5, 'a', 'b', 'c', 'd', 'e']




```python
# List Repetition
my_list1 * 2
```




    [1, 2, 3, 4, 5, 1, 2, 3, 4, 5]




```python
# Membership operator, returns true if member of list
3 in my_list1
```




    True



#### Traversing a list:

The most straightforward way to traverse a list is using loops. We will look at loops in more detail later, but for now let’s just deal with two important elements, the for loop and while loop.

##### for loop:
Example:


```python
my_list = [1, 2, 3, 4, 5]
for element in my_list:
    print(element)
```

    1
    2
    3
    4
    5


Now lets traverse using the index numbers

Example:


```python
for index in range(len(my_list)): # start from 0 and go till the length of the list.
    print("my_list[{}] : {}".format(index, my_list[index]))
```

    my_list[0] : 1
    my_list[1] : 2
    my_list[2] : 3
    my_list[3] : 4
    my_list[4] : 5


##### While loop:
Just like for loop, we can traverse the list based on its index numbers:

For example:


```python
index = 0
# till index is less than length of list
while index < len(my_list):
    print("my_list[{}] : {}".format(index, my_list[index]))
    # increment index by 1 at every iteration
    index += 1
```

    my_list[0] : 1
    my_list[1] : 2
    my_list[2] : 3
    my_list[3] : 4
    my_list[4] : 5


#### Enumerating:
Python has a built-in method called enumerate which returns both index value and value of list ( or any other iterable object).

Example:


```python
for ind, val in enumerate(my_list):
    print("my_list[{}] : {}".format(ind, val))
```

    my_list[0] : 1
    my_list[1] : 2
    my_list[2] : 3
    my_list[3] : 4
    my_list[4] : 5


#### List Comprehension
List comprehension is a syntactic way of creating a list based on the existing list, just like we did when copying the lists above. The basic structure of the syntax includes a for loop that traverses the list and evaluates a condition using the if.. else condition. It then stores the output of the condition as a new list. Let's take a look at a quick example:



```python
my_list1 = [elem for elem in my_list if elem % 2 == 0]
print(my_list1)
```

    [2, 4]


We simply create a list `my_list1` from the elements in `my_list` that are completely divisible by 2.

There are many ways in which the list comprehension can be used. It is just a shorthand of writing better readable code.

#### Built- in List Functions and Methods:

Python provides following methods for lists:

##### max:

This method returns the elements from the list with maximum value.

For example:


```python
my_list1 = [1, 2, 3]
max(my_list1)
```




    3



##### min:

This method returns the element from the list with minimum value.


```python
min(my_list)
```




    1



##### list:

This method takes sequence types and converts them to lists. This is also used to convert a tuple into a list.

For example:


```python
my_list = list(('Python', 'Julia', 1, 3.1415))  # iterable as a tuple
my_list
```




    ['Python', 'Julia', 1, 3.1415]



The above line might be a little confusing. `list` is a built-in function which can either create an empty list if it is called with no parameters, or create a new list of the iterable/ sequence that it is given as an input. That means that list can at most 1 argument. Thus we have to put our elements in a circular bracket (which makes it a `tuple`, btw) and then pass it as an argument to list method. 

##### list.count(obj):
This method returns the number of times the object, that is passed as a parameter, occurs in the list.

For example:


```python
my_list = ['Python', 'Julia', 1, 3.1415]
my_list.count('Python')
```




    1



##### list.extend(seq):
This method appends the contents of a sequence to a list. Here is an equivalent operation using slicing -- `my_list1[len(my_list1):] = my_list2` and print `my_list1`.


```python
my_list1 = ['Python', 'Julia', 1, 3.1415]
my_list2 = ['C++', 'Java', 2, 2.7182]
my_list1.extend(my_list2)
print(my_list1)
```

    ['Python', 'Julia', 1, 3.1415, 'C++', 'Java', 2, 2.7182]


##### list.index(obj):

This method returns the lowest index in the list that object appears.


```python
my_list = ['Python', 'Julia', 1, 3.1415]
my_list.index('Julia')
```




    1



##### list.insert(index, obj):

This method is used to insert the object at the offset index.


```python
my_list = ['Python', 'Julia', 1, 3.1415]
my_list.insert(3, 2.7182)
print(my_list)
```

    ['Python', 'Julia', 1, 2.7182, 3.1415]


##### list.pop(obj = list[-1]):

This method removes and returns the removed object from the list. If you don't pass the argument to the function, it will by default `pop` the last element from the list


```python
my_list = ['Python', 'Julia', 1, 3.1415]
# pop the last element
my_list.pop(1)
```




    'Julia'



##### list.remove(obj):

This method is used to remove the object from the list. The `object` to be removed should be passed as an argument to the function. Unlike pop, this does not return anything.


```python
my_list = ['Python', 'Julia', 1, 3.1415]
my_list.remove('Julia')
print(my_list)
```

    ['Python', 1, 3.1415]


##### list.reverse():

This method reverses the objects of list in place


```python
my_list = ['Python', 'Julia', 1, 3.1415]
my_list.reverse()
print(my_list)
```

    [3.1415, 1, 'Julia', 'Python']


##### list.sort([func]):

This method sorts objects of list by using the compare function passed as optional parameter. You can also sort the string in reverse by passing the optional parameter `reverse=True`


```python
my_list = [7, 6, 1, 9, 2]
my_list.sort()
print("Sorted:         ", my_list)
my_list.sort(reverse=True)
print("Reverse Sorted: ", my_list)
```

    Sorted:          [1, 2, 6, 7, 9]
    Reverse Sorted:  [9, 7, 6, 2, 1]

