[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/03-03%20Broadcasting%20and%20computation.ipynb) 

> Click above image to access the interactive version of this notebook


## Broadcasting and more Computation

### Broadcasting
[Broadcasting](https://docs.scipy.org/doc/numpy-1.13.0/reference/ufuncs.html#broadcasting) is a set of rules for performing arithmetic operations  (e.g., addition, subtraction, multiplication, etc.) on arrays of different shapes. It is an important functionality to leverage the power of NumPy.

If you recall, NumPy Arithmetic  operations are performed element-wise. Let’s take a look at adding a [scalar](https://docs.scipy.org/doc/numpy-1.13.0/reference/arrays.scalars.html). 


```python
from __future__ import print_function
import numpy as np
arr1 = np.random.randint(1, 40, 5)
num  = 5
print("Arr1: \n{}".format(arr1), end="\n\n")
print("num : \n{}".format(num), end="\n\n")
print("Sum : \n{}".format(arr1+num), end="\n\n")
```

    Arr1: 
    [ 8 23  1  9 26]
    
    num : 
    5
    
    Sum : 
    [13 28  6 14 31]
    


Broadcasting allows these types of binary operations to be performed on arrays of different sizes just as we added a scalar (think of a scalar as a zero-dimensional array) to the array.

We can think of this as an operation that *stretches* or *duplicates* the value `5` into the array `[5, 5, 5, 5, 5]`, and adds it to the array. This duplication does not actually take place during Broadcasting but it is a useful logic to remember when you talk about broadcasting.

Just like adding scalar, we can perform broadcasting on multi-dimensional arrays as well.. however there are rules to be followed for `broadcasting` to work.

- Rule 1: If the two arrays differ in their number of dimensions, the shape of the one with fewer dimensions is *padded* with ones on its leading (left) side.
- Rule 2: If the shape of the two arrays does not match in any dimension, the array with shape equal to 1 in that dimension is stretched to match the other shape.
- Rule 3: If in any dimension the sizes disagree and neither is equal to 1, an error is raised.

Let's add two arrays of different sizes


```python
arr1 = np.ones((3, 4))
arr2 = np.arange(4)
```

Lets match these arrays to our set of Rules.

Rule 1: Shape mismatch!
- arr1 is of shape `m1 x n1 = 3 x 4`
- arr2 is of shape `m2 x n2 = 1 x 4`

Rule 2: **Stretch** `m2` or the first dimension of arr2 to match `m1` or the first dimension of arr1. So now,
- arr1 is of shape `m1 x n1 = 3 x 4`
- arr2 is of shape `m2 x n2 = 3 x 4`

Rule 3: Doesnt apply since m1 x n1 = m2 x n2


```python
arr1 + arr2
```




    array([[1., 2., 3., 4.],
           [1., 2., 3., 4.],
           [1., 2., 3., 4.]])



Now lets look at an example where we add arr1 to the transpose of arr1 itself. Lets first print out the transpose and then we shall apply the rules as we did for previous example


```python
print("Arr1: \n{}".format(arr1))
print("arr1.shape: {}".format(arr1.shape), end="\n\n")
print("Arr1 Transpose: \n{}".format(arr1.T))
print("arr1.T.shape: {}".format(arr1.T.shape))
```

    Arr1: 
    [[1. 1. 1. 1.]
     [1. 1. 1. 1.]
     [1. 1. 1. 1.]]
    arr1.shape: (3, 4)
    
    Arr1 Transpose: 
    [[1. 1. 1.]
     [1. 1. 1.]
     [1. 1. 1.]
     [1. 1. 1.]]
    arr1.T.shape: (4, 3)


Lets apply our rules:

Rule 1: Shape mismatch!
- arr1 is of shape   `m1 x n1 = 3 x 4`
- arr1.T is of shape `m2 x n2 = 4 x 3`

Rule 2: **Stretch** `m1` or the first dimension of arr1 to match `m2` or the first dimension of arr1.T. So now,
- arr1 is of shape   `m1 x n1 = 4 x 4`
- arr1.T is of shape `m2 x n2 = 4 x 3`

Rule 3: `n1` and `n2` or the second dimension of both the arrays are definitely not `1` and they don't match! This will raise a `ValueError`


```python
arr1 + arr1.T
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-10-c545f5548cf5> in <module>
    ----> 1 arr1 + arr1.T
    

    ValueError: operands could not be broadcast together with shapes (3,4) (4,3) 




### Aggregation
When performing analysis on any dataset, most of the times the first thing that you would end up doing is finding the summary statistics of the datasets. Things like maximum, minimum, mean, variance etc. is the first thing you would look at (for the relevant columns). NumPy provides such fast-performing aggregation ufuncs. Let’s take a look at some.

#### sum
As the name suggests, this function will return the sum of all the values of an array


```python
arr = np.random.randint(1, 700, 10000)
print("Sum of 1D: {}".format(np.sum(arr)))
```

    Sum of 1D: 3496585



```python
arr2d = np.random.uniform(1, 700, (3, 4))
print("Sum of 2D: {}".format(np.sum(arr2d)))
```

    Sum of 2D: 4461.878924723045


#### max and min
This will find the maximum and minimum value in an array.


```python
print("Max of 1D arr: {}".format(np.max(arr)))
print("Min of 1D arr: {}".format(np.min(arr)))
print("Max of 2D arr: {}".format(np.max(arr2d)))
print("Min of 2D arr: {}".format(np.min(arr2d)))
```

    Max of 1D arr: 699
    Min of 1D arr: 1
    Max of 2D arr: 584.3120316508158
    Min of 2D arr: 108.07311142542031


We can also get minimum and maximum along a particular axis
> - axis 0 = along the column
> - axis 1 = along the row


```python
print("2D Array: \n{}".format(arr2d), end="\n\n")
print("Max of 2D arr along axis 0: {}".format(np.amax(arr2d, axis=0)))
print("Min of 2D arr along axis 0: {}".format(np.amin(arr2d, axis=0)))
```

    2D Array: 
    [[584.31203165 523.13245439 575.76317045 108.07311143]
     [280.62754588 395.38638114 318.85086995 444.20232451]
     [346.43051046 288.82455482 161.57584953 434.70012052]]
    
    Max of 2D arr along axis 0: [584.31203165 523.13245439 575.76317045 444.20232451]
    Min of 2D arr along axis 0: [280.62754588 288.82455482 161.57584953 108.07311143]


#### std
Compute standard deviation along a particular axis


```python
print("2D Array: \n{}".format(arr2d), end="\n\n")
print("Std along axis 0: \n{}".format(np.std(arr2d, axis=0)))
print("Std along axis 1: \n{}".format(np.std(arr2d, axis=1)))
```

    2D Array: 
    [[584.31203165 523.13245439 575.76317045 108.07311143]
     [280.62754588 395.38638114 318.85086995 444.20232451]
     [346.43051046 288.82455482 161.57584953 434.70012052]]
    
    Std along axis 0: 
    [130.44450296  95.78603114 170.71434848 156.26129927]
    Std along axis 1: 
    [197.54711062  63.90470882  99.16841638]


We will take a look at more of these in module on matplotlib so that while we will be printing the output, we will also be able to plot the results for a better understanding. If you are intersted to know about more such functions, you can check the link on official documentation here: [`Numpy Statistics Routines`](https://docs.scipy.org/doc/numpy/reference/routines.statistics.html)
