[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/03-01%20Numpy%20Array%20Basics.ipynb) 

> Click above image to access the interactive version of this notebook


## Numpy Array Basics

Numpy’s main object is the homogenous multi-dimensional array, generally of fixed size. The number of dimensions in a numpy array is defined by its shape which is a tuple of positive integers that specifies the size of each dimension.

Numpy arrays are similar to Python lists with few differences such as: 
 - All the elements in a numpy array must be of same datatype. 
 - You can't change the size of a numpy array (at least not without making a full copy.. we'll see this a little later)
 - Numpy arrays are easy to construct and to manipulate.
 - Numpy arrays support “vectorized” operations like elementwise addition and multiplication without having to run a `for` loop explicitly in python.
 
We'll cover basic array manipulations here:
- *Attributes of arrays*: Determining the size, shape, memory consumption, and data types of arrays
- *Creating arrays*: Different ways of creating the Arrays
- *Indexing of arrays*: Getting and setting the value of individual array elements
- *Slicing of arrays*: Getting and setting smaller subarrays within a larger array
- *Reshaping of arrays*: Changing the shape of a given array
- *Joining and splitting of arrays*: Combining multiple arrays into one, and splitting one array into many

### Attributes of Arrays


```python
from __future__ import print_function
import numpy as np
# Single dimensional Array from a list
arr = np.array([1, 2, 3, 4], dtype=float)
print('Type: ',type(arr))
print('Shape: ',arr.shape)
print('Dimension: ',arr.ndim)
print('Itemsize: ',arr.itemsize)
print('Size: ',arr.size)
```

    Type:  <class 'numpy.ndarray'>
    Shape:  (4,)
    Dimension:  1
    Itemsize:  8
    Size:  4


There are many different attributes of `ndarray` class and by now you should be able to understand how to access those attributes and get help for them (Hint: completion). 

Let's understand at some of the attributes that we printed above.

##### ndarray.ndim
It is the number of axes or dimensions of the array.

##### ndarray.shape
It is the dimension of the array. This is a tuple of integers indicating the size of the array in each dimension. For a matrix with n rows and m columns, the shape will be (m, n). The shape attribute is thus a tuple. For single dimensional arrays, the second element of the tuple will be None (as it is on our case).

##### ndarray.dtype
It is an object describing the type of the elements in the array. Remember that all the elements need to be of same datatype in a numpy array. Additionally numpy provides its own int16, int32, float64 and so on.

##### ndarray.itemsize
The size in bytes of each element of the array. For example an array of elements of type float64 has itemsize of $\frac{64}{8} = 8$ and one complex32 has item size of $\frac{32}{8} = 4$.

##### ndarray.data
This is the buffer containing the actual elements of the array. Normally this attribute is not used as numpy offers many fancy indexing facilities.

Let's take a look at another example:


```python
# Elements have to be of same datatype
arr = np.array([1, 2.0, "ucsl"])
print("Datatype: ", arr.dtype)
```

    Datatype:  <U32


Since we did not pass the `dtype` parameter, Numpy saw that there are mixed types and it converts the datatype of all the elements to type `U`nicode`32` (or `S`tring`32` if you are using Python2). 

> To know all the datatypes supported by Numpy, you can type
```ipython
In [2]: np.typeDict
```
and check the output

If we would've passed the `dtype` as `float` or anything other than a type of `string` or `unicode`, we would've recevied a value error. (Try it!)

### Creating Arrays
There are many different ways in which a numpy array can be created. We saw one in the above example. Lets look at some other ways of creating arrays


```python
arr1 = np.arange(5, dtype=float)
print('arange() with float dtype: \n',arr1)
# Divide the range between start and stop in equal `num` intervals
arr2 = np.linspace(0, 8, num=5)
print('\n linspace(): \n', arr2)
arr3 = np.ones((2, 3), dtype=float)
print ('\n ones(): \n',arr3)
arr4 = np.zeros((2,3), dtype=float)
print ('\n zeros(): \n',arr4)
arr5 = np.empty((2, 4))
print('\n Empty: \n',arr5)  # Your output may be different..
arr6 = np.ones_like(arr1)
print('\n Ones_like(): \n',arr6)
arr7 = np.diag(arr1)
print('\n Diagonal array: \n',arr7)

```

    arange() with float dtype: 
     [0. 1. 2. 3. 4.]
    
     linspace(): 
     [0. 2. 4. 6. 8.]
    
     ones(): 
     [[1. 1. 1.]
     [1. 1. 1.]]
    
     zeros(): 
     [[0. 0. 0.]
     [0. 0. 0.]]
    
     Empty: 
     [[1.28822975e-231 2.68679301e+154 6.94538753e-310 2.17223877e-314]
     [7.90782398e-312 6.94539006e-310 2.12199582e-314 5.56270637e-309]]
    
     Ones_like(): 
     [1. 1. 1. 1. 1.]
    
     Diagonal array: 
     [[0. 0. 0. 0. 0.]
     [0. 1. 0. 0. 0.]
     [0. 0. 2. 0. 0.]
     [0. 0. 0. 3. 0.]
     [0. 0. 0. 0. 4.]]


#### np.arange()

is the same as the range function that we used previously. This method will however return a numpy array.

#### np.zeros() and np.ones()

as the name suggests, generate new arrays of specified dimensions filled with these values. These are most commonly used functions to create new arrays.


```python
arr3 = np.ones((2, 3), dtype=float)
print ('\n ones(): \n',arr3)
arr4 = np.zeros((2,3), dtype=float)
print ('\n zeros(): \n',arr4)
```

    
     ones(): 
     [[1. 1. 1.]
     [1. 1. 1.]]
    
     zeros(): 
     [[0. 0. 0.]
     [0. 0. 0.]]


#### np.empty()

This function creates an array whose initial content is random and depends on the state of the memory. If not specified, the data type of the created array is float64


```python
arr5 = np.empty((2, 4))
print('\n Empty: \n',arr5)  # Your output may be different..
```

    
     Empty: 
     [[1.28822975e-231 2.68679301e+154 6.94538753e-310 2.17223877e-314]
     [7.90782398e-312 6.94539006e-310 2.12199582e-314 5.56270637e-309]]


#### np.ones_like()  , np.zeros_like() and np.empty_like()

These functions create a new array with the same dimensions and type as the existing one but with the values as either ones or zeros or random value.


```python
arr6 = np.ones_like(arr1)
print('\n Ones_like(): \n',arr6)
```

    
     Ones_like(): 
     [1. 1. 1. 1. 1.]


#### np.diag()

As the name suggests, this will construct a diagonal array



```python
arr7 = np.diag(arr1)
print('\n Diagonal array: \n',arr7)
```

    
     Diagonal array: 
     [[0. 0. 0. 0. 0.]
     [0. 1. 0. 0. 0.]
     [0. 0. 2. 0. 0.]
     [0. 0. 0. 3. 0.]
     [0. 0. 0. 0. 4.]]


Let's take a look at an example for creating multi-dimensional array


```python
arr2d = np.arange(27).reshape(3, 9)
print("2D array: \n{}\n".format(arr2d))
arr3d = np.arange(27).reshape(3,3,3)
print("3D array: \n{}\n".format(arr3d))
```

    2D array: 
    [[ 0  1  2  3  4  5  6  7  8]
     [ 9 10 11 12 13 14 15 16 17]
     [18 19 20 21 22 23 24 25 26]]
    
    3D array: 
    [[[ 0  1  2]
      [ 3  4  5]
      [ 6  7  8]]
    
     [[ 9 10 11]
      [12 13 14]
      [15 16 17]]
    
     [[18 19 20]
      [21 22 23]
      [24 25 26]]]
    


Numpy displays the arrays in a similar way to nested lists but with the following layout:
- the last axis is printed from left to right
- the second to last axis is printed from top to bottom.
- the rest rest are also printed from top to bottom with each slice separated from the next by an empty line. Simply put, single dimensional arrays are printed as rows, bi-dimensional and multi-dimensional are printed as matrices and as lists of matrices respectively.

We will look at reshaping of arrays later in this module.

### Array Indexing
Numpy arrays are indexed in the same way as lists, so accessing the elements for single dimensional array is equivalent to accessing elements in a list


```python
arr = np.arange(3, 10)
print(arr[4])
          
```

    7


You can also use negative indexing like we did for lists. For example:


```python
print(arr[-3])
```

    7


Multi-dimensional array items can be accessed using comma-separated tuple of indexes, as here: 


```python
arr3d = np.arange(27).reshape(3,3,3)
dim, row, col = 2, 1, 0
print("3D array: \n", arr3d, end="\n\n")
print("Element at {dim}, {row}, {col} is: {val}".format(dim=dim, 
                                                        row=row, 
                                                        col=col, 
                                                        val=arr3d[dim, row, col]))
```

    3D array: 
     [[[ 0  1  2]
      [ 3  4  5]
      [ 6  7  8]]
    
     [[ 9 10 11]
      [12 13 14]
      [15 16 17]]
    
     [[18 19 20]
      [21 22 23]
      [24 25 26]]]
    
    Element at 2, 1, 0 is: 21


### Array Slicing
Slicing extracts the portion of a sequence by specifying a lower and upper bound. The lower bound element is included, but the upper-bound element is not included in slicing. Just like lists, there is a third parameter step which means the strides to be taken between the elements. If any of these are unspecified, they default to the values `start=0, stop=size of dimension, step=1`. Each of these parameters are separated by colons (`:`) as you can see in the example here: 


```python
arr = np.linspace(0, 8, num=5)
print("Original Array: \n", arr, end="\n\n")
# let the slicings begin
print("arr[:3]: ", arr[:3])
print("arr[-5:5:2]: ", arr[-5:5:2])
print("arr[::2]: ", arr[::2])
# Reverse the elements
print("arr[::-1]: ", arr[::-1])
# Reverse every other array from index 2
print("arr[2::-2]: ", arr[2::-2])
```

    Original Array: 
     [0. 2. 4. 6. 8.]
    
    arr[:3]:  [0. 2. 4.]
    arr[-5:5:2]:  [0. 4. 8.]
    arr[::2]:  [0. 4. 8.]
    arr[::-1]:  [8. 6. 4. 2. 0.]
    arr[2::-2]:  [4. 0.]


For multi-dimensional array, we specify in rows, columns format, as in the example below. 


```python
# Array of random integers between low and high of fixed size(mxn)
arr = np.random.randint(low=0, high=100, size=(3,4))
print("2D array: \n", arr, end="\n\n")
# first row, three columns
print("first row, three columns: \n", arr[:1, :3], end="\n\n")
# all rows, third column
print("all rows, third column: \n", arr[:, 3], end="\n\n")
# changing dimensions 
print("reversing rows and columns together: \n",
     arr[::-1, ::-1], end="\n\n")
```

    2D array: 
     [[33 18 10 56]
     [12 28 88 18]
     [24 73 51 43]]
    
    first row, three columns: 
     [[33 18 10]]
    
    all rows, third column: 
     [56 18 43]
    
    reversing rows and columns together: 
     [[43 51 73 24]
     [18 88 28 12]
     [56 10 18 33]]
    


Slices are references to the original array in memory. Changing the values in a slice also changes the original array. We can see that in this example: 


```python
arr1 = np.arange(5)
# slice arr1
arr2 = arr1[3:5]
print("arr1: \n", arr1, end="\n\n")
print("Sliced array: \n", arr2)
print('\nBefore changing, arr2[0]: \n',arr2[0])
# change value for 0th element of the slice
arr2[0] = 99
print('\nAfter changing arr2[0], arr1: \n',arr1)
```

    arr1: 
     [0 1 2 3 4]
    
    Sliced array: 
     [3 4]
    
    Before changing, arr2[0]: 
     3
    
    After changing arr2[0], arr1: 
     [ 0  1  2 99  4]


### Reshaping Arrays
We have been using the`reshape` function to view a one dimensional array as a multi-dimensional array. This nifty method only works if your new array shape matches the size of the original array i.e `size = m x n`

One can also row and column elements using `newaxis` method, demonstrated below: 


```python
arr = np.random.randint(low=0, high=100, size=12)
print("Original Array: \n", arr, end="\n\n")
print("Reshaped to 3 x 4: \n", arr.reshape(3,4), end="\n\n")
print("Row vector : \n", arr[np.newaxis, :], end="\n\n")
print("Column vector : \n", arr[:, np.newaxis], end="\n\n")
```

    Original Array: 
     [81 13 40  1  6 31 40 86 89  5 53 76]
    
    Reshaped to 3 x 4: 
     [[81 13 40  1]
     [ 6 31 40 86]
     [89  5 53 76]]
    
    Row vector : 
     [[81 13 40  1  6 31 40 86 89  5 53 76]]
    
    Column vector : 
     [[81]
     [13]
     [40]
     [ 1]
     [ 6]
     [31]
     [40]
     [86]
     [89]
     [ 5]
     [53]
     [76]]
    


### Concatenating Arrays
Just like Python Lists, you can concatenate two arrays using Numpy's `concatenate()`, `hstack()` and `vstack()` functions. 

However, you must remember that just like lists, when you combine a Numpy array, an actual copy of both the arrays is made. If you created the two arrays separately, they are randomly scattered in memory, and there is no way to represent them as a `view` Know the size of the array you need beforehand so that you can start with one big array, and have each of the small arrays be a `view` to the big array. (You can leverage the power of slicing!)

Follow the example below. 


```python
# Creating two 1D arrays separately
arr1 = np.arange(10)
arr2 = np.arange(10, 20)
arr3 = np.concatenate((arr1, arr2))
print("Arr1: \n{}".format(arr1), end="\n\n")
print("Arr2: \n{}".format(arr2), end="\n\n")
print("Concatenated Array: \n{}".format(arr3))
```

    Arr1: 
    [0 1 2 3 4 5 6 7 8 9]
    
    Arr2: 
    [10 11 12 13 14 15 16 17 18 19]
    
    Concatenated Array: 
    [ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19]


For concatenation of two multi-dimensional arrays, it is better to use the `hstack()` -- for stacking horizontally and `vstack()` -- for stacking against vertical axis, as demonstrated in example below.


```python
arr1 = np.random.randint(1, 10, 8).reshape(2, 4)
arr2 = np.random.randint(90, 100, 8).reshape(2, 4)
# stacking horizontally
hs_arr = np.hstack((arr1, arr2))
# stacking vertically
vs_arr = np.vstack((arr1, arr2))
print("Arr1: \n{}".format(arr1), end="\n\n")
print("Arr2: \n{}".format(arr2), end="\n\n")
print("Horizontally Stacked Array: \n{}".format(hs_arr), end="\n\n")
print("Vertically Stacked Array: \n{}".format(vs_arr), end="\n\n")
```

    Arr1: 
    [[4 5 2 2]
     [3 4 3 9]]
    
    Arr2: 
    [[94 90 92 91]
     [92 98 92 94]]
    
    Horizontally Stacked Array: 
    [[ 4  5  2  2 94 90 92 91]
     [ 3  4  3  9 92 98 92 94]]
    
    Vertically Stacked Array: 
    [[ 4  5  2  2]
     [ 3  4  3  9]
     [94 90 92 91]
     [92 98 92 94]]
    


### Splitting Arrays
Just like concatenating multiple arrays into one, Numpy's `split()`, `hsplit()` and `vsplit()` allows splitting of one array into multiple smaller ones.


```python
arr1 = np.arange(20)
np.split(arr1, (2, 8, 10, 14))
```




    [array([0, 1]),
     array([2, 3, 4, 5, 6, 7]),
     array([8, 9]),
     array([10, 11, 12, 13]),
     array([14, 15, 16, 17, 18, 19])]



`np.split()` takes the array that we want to split as the first argument and as a second argument, it requires a list or tuple of the index of the elements at which we want to split the array. More the number of split-points, there will be one more subarray i.e `N` split-points, leads to `N + 1` subarrays.

Similarly for multi-dimensional arrays, we can use `hsplit()` and `vsplit()`


```python
arr2d = np.random.randint(0, 9, (3,3))
print("Original Array: \n{}".format(arr2d), end="\n\n")
# split along horizontal axis
arr1, arr2 = np.hsplit(arr2d, [2])
print("First Split: \n{}".format(arr1), end="\n\n")
print("Remaining Split: \n{}".format(arr2), end="\n\n")
```

    Original Array: 
    [[1 7 7]
     [7 3 7]
     [3 1 4]]
    
    First Split: 
    [[1 7]
     [7 3]
     [3 1]]
    
    Remaining Split: 
    [[7]
     [7]
     [4]]
    

