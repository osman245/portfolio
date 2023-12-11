[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/02-03%20Dictionaries.ipynb) 

> Click above image to access the interactive version of this notebook


##  Dictionaries
Python dictionary is an interesting and useful data structure in python. It is a container of [key-value pairs](https://en.wikipedia.org/wiki/Attribute%E2%80%93value_pair_). Just like lists, python dictionaries are mutable and can contain mixed types, however the key **must** be immutable (i.e the object being used as a key must be [hashable](https://docs.python.org/3/glossary.html#term-hashable)) -- e.g. like strings or numbers or even Tuples and must be unique within a dictionary. 

Python dictionaries are also known as hash tables in other programming languages. Each key is separated from its value by a colon ( `:` ) and just like lists the items are separated by commas and the whole thing is enclosed in curly braces (`{}`).

An important thing to remember is that, by design, python dictionaries do not maintain any ordering (i.e the sequence in which the objects were entered). This lack of ordering allows random elements to be accessed quickly, regardless of the size of the dictionary.

> For curious minds who wants to know more about `hash`ing (it is not *required*), [wikipedia](https://en.wikipedia.org/wiki/Hash_table) has a good writeup and then maybe this [StackOverflow](http://stackoverflow.com/questions/2061222/what-is-the-true-difference-between-a-dictionary-and-a-hash-table) link.

### Creating Dictionaries


```python
student = {'Name': 'John', 'Class': 'Urban Skills', 'Course': 'Python'}
print(student)
print(type(student))
```

    {'Name': 'John', 'Class': 'Urban Skills', 'Course': 'Python'}
    <class 'dict'>



```python
# Creating empty dictionary
states = {}
# Keys are inside square brackets and values on the right side of assignment
states['AL'] = 'Alabama'
states['NY'] = 'New York'
print(states)
```

    {'AL': 'Alabama', 'NY': 'New York'}


You can convert other data structures like lists and tuples to dictionaries too.. Lets look at some of the ways to achieve that:

#### fromkeys()


```python
states_key_list   = ['AL', 'NY']
# Instead of 0 you can leave the field empty
states_dict       = {}.fromkeys(states_key_list, 0)
print("Just added keys with default values as 0: ", states_dict)
states_dict['AL'] = 'Alabama'
states_dict['NY'] = 'New York'
print(states_dict)
```

    Just added keys with default values as 0:  {'AL': 0, 'NY': 0}
    {'AL': 'Alabama', 'NY': 'New York'}


#### zip()
This is a python built-in method to group every element from each iterable passed as an argument.
`zip` will return the group of size equal to the smallest iterable.


```python
states_key_list = ['AL', 'NY']
states_val_list = ['Alabama', 'New York']
states_dict     = dict(zip(states_key_list, states_val_list))
print(states_dict)
```

    {'AL': 'Alabama', 'NY': 'New York'}



```python
# what happens if we have more keys than values
states_key_tup  = ('AL', 'NY', 'TX', 'NJ')
states_val_list = ['Alabama', 'New York', 'Texas']
states_dict     = dict(zip(states_key_tup, states_val_list))
print(states_dict)
```

    {'AL': 'Alabama', 'NY': 'New York', 'TX': 'Texas'}


### Accessing Dictionary Items

#### Passing key as index to the dictionary


```python
student = {'Name': 'John', 'Class': 'Urban Skills', 'Course': 'Python'}
student['Name']
```




    'John'



#### get(key [, default])


```python
# If key is in Dictionary, it will return the value else return the 
# default.. in this case default = "Not Found"
print("Course:   ", student.get('Course'  , 'Not Found'))
# This will print Not Found since there is not key 'Location'
print("Location: ", student.get('Location', 'Not Found'))
```

    Course:    Python
    Location:  Not Found


### Updating Dictionary:

The dictionary can be updated by adding a new entry or a new key-value pair, modifying existing entry and/ or deleting an entry.

#### Passing key as index and assigning value


```python
student = {'Name': 'John', 'Class': 'Urban Skills', 'Course': 'Python'}
student['Degree']   = 'Masters'
student['Location'] = 'NYU CUSP'
student
```




    {'Name': 'John',
     'Class': 'Urban Skills',
     'Course': 'Python',
     'Degree': 'Masters',
     'Location': 'NYU CUSP'}



#### setdefault( )

In python, the value (of a key-value pair) is mutable. However at times you might not want to overwrite the key-value pair if it already exists. 
You can achieve this by using `setdefault()` method. The setdefault method returns a value if a key is present. Otherwise it inserts a key with the specified value and returns the value


```python
student = {'Name': 'John', 'Class': 'Urban Skills', 'Course': 'Python'}
# This will add the 'Degree:Masters' key value pair since it doesn't exist
# and return the value added
student.setdefault('Degree', 'Masters')
```




    'Masters'




```python
# This will return the existing value for key = "Class"
student.setdefault('Class','Urban Sensing')
```




    'Urban Skills'




```python
print(student)
```

    {'Name': 'John', 'Class': 'Urban Skills', 'Course': 'Python', 'Degree': 'Masters'}


#### update( )

The update method adds (joins) the two dictionary together.


```python
states_dict = {'AL': 'Alabama', 'NY': 'New York'}
states_dict2 = {'NJ': 'New Jersey', 'CA': 'California'}
states_dict.update(states_dict2)
states_dict
```




    {'AL': 'Alabama', 'NY': 'New York', 'NJ': 'New Jersey', 'CA': 'California'}



###  Removing elements from Dictionary

#### pop( )

Pop() method removes the key-value pair based on the key passed as an argument. It returns the value that is being 'popped' from the dictionary


```python
states_dict = {'AL': 'Alabama', 'CA': 'California', 'NJ': 'New Jersey', 'NY': 'New York'}
states_dict.pop('AL')
```




    'Alabama'




```python
states_dict
```




    {'CA': 'California', 'NJ': 'New Jersey', 'NY': 'New York'}



#### del()
del() method can be used to perform the above operation and also can be used to remove an entire dictionary. It does not return anything.


```python
states_dict = {'AL': 'Alabama', 'CA': 'California', 'NJ': 'New Jersey', 'NY': 'New York'}
del states_dict['AL']
states_dict
```




    {'CA': 'California', 'NJ': 'New Jersey', 'NY': 'New York'}




```python
# delete the whole dictionary
del states_dict
print(states_dict)
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-16-33158d208970> in <module>
          1 # delete the whole dictionary
          2 del states_dict
    ----> 3 print(states_dict)
    

    NameError: name 'states_dict' is not defined


#### clear( )

The clear method clears all items from the dictionary but does not delete the dictionary


```python
states_dict = {'CA': 'California', 'NJ': 'New Jersey', 'NY': 'New York'}
states_dict.clear()
states_dict
```




    {}



### Traversing a Dictionary

#### 07.06.01 for loop:

A dictionary can be traversed using for loops.


```python
states_dict = {'AL': 'Alabama', 'CA': 'California', 'NJ': 'New Jersey', 'NY': 'New York'}
for k in states_dict:
    print("{key}: {val}".format(key=k, val=states_dict[k]))
```

    AL: Alabama
    CA: California
    NJ: New Jersey
    NY: New York



```python
 # We will see items() method in next sub- topic
for k, v in states_dict.items():
    print(': '.join((k, v)))
```

    AL: Alabama
    CA: California
    NJ: New Jersey
    NY: New York


> Check the print statements in above two examples.

#### .. 07.06.02 keys( ) , values( ) and items( )

The keys() method returns a list of keys in dictionary. The values() method returns a list of all the values and items() returns a list of all key-value tuples.

> - For python2 users: The above methods will directly return a list (note: a `list`!). 
- For python3 users: The above methods return dict_keys, dict_values and dict_items respectively which are basically `view` objects (note: `view`!). 
    - view objects are faster and require small and fixed amount of memory and processor time. (python2 equivalent of these are `viewkeys()`, `viewvalues()` and `viewitems()`).
    - `views` are *dynamic view* of the dictionary which shows the contents of the dictionary even after it changes. They offer features that differ from those of lists: a list of keys contain a copy of the dictionary keys at a given point in time, while a view is dynamic and is much faster to obtain, as it does not have to copy any data (keys or values) in order to be created.
    - These `views` can be converted to lists by passing them to list constructor. e.g. `list(dict_keys)`. This technique will also work for python2 users.
- Python2 users: wherever you see `.keys()` or `.items()` or `.values()` you can also use `.viewkeys()`, `.viewitems()` and `.viewvalues()` respectively. These will return the `dict_keys`, `dict_items` and `dict_values`.


```python
states_dict = {'AL': 'Alabama', 'CA': 'California', 
               'NJ': 'New Jersey', 'NY': 'New York'}
list(states_dict.keys())
```




    ['AL', 'CA', 'NJ', 'NY']




```python
list(states_dict.values())
```




    ['Alabama', 'California', 'New Jersey', 'New York']




```python
list(states_dict.items())
```




    [('AL', 'Alabama'),
     ('CA', 'California'),
     ('NJ', 'New Jersey'),
     ('NY', 'New York')]



### Sorting

Dictionaries in Python can be sorted using keys or values in ascending or descending order. First let us look as the built-in function sorted() and then the method specific to collections class.

#### sorted( )

Sorted method returns a new list containing sorted items from iterable (in our case it is a dictionary). It can also take a boolean value for reverse, which, if set as True, will sort the iterable in descending order.

In this example, we will sort the dictionary by keys.


```python
states_dict = {'AL': 'Alabama', 'CA': 'California', 
               'NJ': 'New Jersey', 'NY': 'New York'}
sorted_keys = sorted(list(states_dict.keys()), reverse=False)
for key in sorted_keys:
    print('{} : {}'.format(key, states_dict[key]))
```

    AL : Alabama
    CA : California
    NJ : New Jersey
    NY : New York


#### sort()
This method sorts the list inplace!

Remember: Creating a copy of lists is memory expensive. (Any operation you perform on a list creates a copy of the list, making computations slower.) You should always try to reduce the copies that you create


```python
states_dict = {'AL': 'Alabama', 'CA': 'California', 
               'NJ': 'New Jersey', 'NY': 'New York'}
k = list(states_dict.keys())
k.sort(reverse=False)
for key in k:
    print('{key} : {val}'.format(key=key, val=states_dict[key]))
```

    AL : Alabama
    CA : California
    NJ : New Jersey
    NY : New York


*Remember, If you have any difficulty using any function or method in Jupyter notebook, type the function or method name followed by a '?' or `shift + Tab` and it will print the docstring/ help manual for you.*
