[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/02-02%20Tuples.ipynb) 

> Click above image to access the interactive version of this notebook

## 01 - 06 Tuples
Python tuple is much like a list except that it is immutable or unchangeable once created. Tuples use parentheses and creating them is as easy as putting different items separated by a comma between parentheses.


```python
my_tup = ('Python', 'Julia', 1, 3.1415)
type(my_tup)
```




    tuple



Pretty easy. So the next question is why do we need a new datatype? The answer can be summed up in three points:

- Tuples are faster than lists. If you ever defined a set of constant values and all you ever want to do is read those values, you should use tuples instead of lists.
- Tuples are like 'write-protected' lists so that the data cannot be changed by accident.
- Tuples are using in string formatting (we will see this in some examples below)


### Creating a Tuple
We already saw one example above on how to create tuples with multiple items. But to create a tuple with a single item, you need to include a comma after the first item.

See what happens when you don't enter comma. What is the type of such object?


```python
my_tup = ('test',)
```

### Slicing the Tuple

Slicing a tuple is similar to slicing a list.


```python
my_tup = ('Python', 'Julia', 1, 3.1415)
print(my_tup[:-3])
# -ve sign indicates -ve indexing. So start from right and skip 2 elements
print(my_tup[::-2])
```

    ('Python',)
    (3.1415, 'Julia')


From above example we can observe that just like lists, slicing a tuple returns a new shallow copied tuple containing the requested items.

### Tuple Concatentation, Repetition, Membership

Tuples are immutable objects which means that you cannot update, append, remove, and/or modify the items in the tuple. However what you can do is take items from different tuples and create new tuples with those. Let's take a look at some examples below.


```python
tuple1 = (1, 2, 3, 4, 5)
tuple2 = ('a', 'b' , 'c' ,'d' , 'e')
# Tuple Concatentation
tuple1 + tuple2
```




    (1, 2, 3, 4, 5, 'a', 'b', 'c', 'd', 'e')




```python
# Tuple Repetition
tuple1 * 2
```




    (1, 2, 3, 4, 5, 1, 2, 3, 4, 5)




```python
# Membership operator, returns true if member of tuple
'a' in tuple2
```




    True



### Nested Tuples

It is also possible to create a tuple of tuples or tuple of lists. 


```python
list1 = ['Python', 'Julia', 1, 3.1415]
 # List of tuples is possible too!
list2 = [('a', 'b'), ('c', 'd')]
tuple1 = (1, 2, 3, 4, 5)
# Concatenating the list and converting to tuple. 
# Then adding two tuples and storing it in another tuple
tuple2 = tuple(list1 + list2)+ tuple1
tuple2
```




    ('Python', 'Julia', 1, 3.1415, ('a', 'b'), ('c', 'd'), 1, 2, 3, 4, 5)



NOTE: Remember, we cannot concatenate a `list` and a `tuple` so we concatenate two lists and convert the new list into tuple by using the tuple built-in function. Then we concatenate that to tuple1 and store the new tuple as tuple2.

### Traversing a Tuple

Tuples can be traversed using the index value of the items. The most straightforward way of traversing a tuple is by using loops. Below is an example that extends the above example and using the items of tuple2.


```python
for ind in enumerate(tuple2):
    print('tuple2[{0[0]}]: {0[1]}'.format(ind))
```

    tuple2[0]: Python
    tuple2[1]: Julia
    tuple2[2]: 1
    tuple2[3]: 3.1415
    tuple2[4]: ('a', 'b')
    tuple2[5]: ('c', 'd')
    tuple2[6]: 1
    tuple2[7]: 2
    tuple2[8]: 3
    tuple2[9]: 4
    tuple2[10]: 5


Almost everything that we did in lists apply over here. Of course, except for the fact that we can modify the lists items but not the tuples. Remember, tuples are immutable.

#### Tuple Comprehension
We know that list comprehension is performed using a for loop that traverses the list and evaluates a condition using if.. else condition and creates a new list with the output. So for tuples it should be same as the list, right? Let's see below:


```python
tuple1 = (1, 2, 3, 4, 5)
# Same example as in list comprehension
tuple2 = (elem for elem in tuple1 if elem%2 == 0)
type(tuple2)
```




    generator




```python
next(tuple2)
```




    2



Remember when we talked about list comprehension and got all happy looking at such an easier way to create new lists? It so happens that the 'comprehension' for lists and dictionaries is just a syntactic sugar to use a generator expression that outputs a specific type. 

We learned the basics about generators when we saw `range` function. List comprehension, under the covers, creates a generator expression that outputs a list (just like we did above using next() method). Now that you know the truth behind the comprehension you might feel that you don't need list comprehension but believe me, it is awfully handy for lists when you start writing your codes in python using lists. So if you want  to use comprehension in tuples, you will get a generator expression and you can obtain your results using the next method. This also doesn't require the invention of another brace or bracket.

How do you obtain all the elements of generator without using loops? 

### Built-in Tuple Functions and Methods

Python provides following methods for tuples:

##### tuple.count()
This method returns the number of times the object, that is passed as a parameter, occurs in the tuple.


```python
tuple1.count(3)
```




    1



##### tuple.index()
This method returns the lowest index in the tuple that object appears at.


```python
tuple1.index(3)
```




    2


