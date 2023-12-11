[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/03-02%20Ufuncs.ipynb) 

> Click above image to access the interactive version of this notebook


## Ufuncs
Python's default implementation does some operations slowly. This is in part due to the dynamic and interpreted nature of the language. It is this feature that allows types to be flexible but since the type has to be checked at every operation, the sequences of operations cannot be compiled down to efficient machine code as in languages like C. Let’s take a look at Python native implementation of this:



```python
from __future__ import print_function
import numpy as np
def get_sin(arr):
    # Create an empty output array of same size as input
    output = np.empty_like(arr)
    for i in range(len(output)):
        output[i] = np.sin(arr[i])
    return output
```


```python
input_arr = np.random.uniform(-np.pi, np.pi, 10000000)
%time get_sin(input_arr)
```

    CPU times: user 13 s, sys: 53.9 ms, total: 13.1 s
    Wall time: 13.1 s





    array([-0.64745651, -0.99996545,  0.99756044, ..., -0.96197339,
            0.85711429,  0.99999453])



Even though the above implementation is correct and might look optimized for people who are familiar with languages like C and Java, the above loop takes significant amount of time (check the `total` CPU times) and is horribly inefficient due to the reasons we mentioned above. 

This is where NumPy's `ufuncs` come to save the day. NumPy provides a convenient interface into these kinds of statically-typed, compiled routine. This is known as a vectorized operation. This can be accomplished by simply performing an operation on the array, which will then be applied to each element.

The vectorized approach is designed to push the `loop` part of the code into the compiled layer that underlies NumPy, leading to much faster execution.

Let's take a look at the NumPy ufunc based solution for the same example


```python
input_arr = np.random.uniform(-np.pi, np.pi, 10000000)
%time np.sin(input_arr)
```

    CPU times: user 133 ms, sys: 450 µs, total: 133 ms
    Wall time: 134 ms





    array([-0.9657678 ,  0.79841143,  0.28326751, ..., -0.88320409,
           -0.79466346,  0.70549672])



Thats much faster, right?

You can also use these ufuncs on multi-dimensional array. 


```python
arr = np.random.randint(1, 100, (3, 4))
# take reciprocal
print("Original Array: \n{}".format(arr), end="\n\n")
print("Reciprocal: \n{}".format(1/arr), end="\n\n")
```

    Original Array: 
    [[96 45 96 63]
     [18 65 61 42]
     [31 21 65 19]]
    
    Reciprocal: 
    [[0.01041667 0.02222222 0.01041667 0.01587302]
     [0.05555556 0.01538462 0.01639344 0.02380952]
     [0.03225806 0.04761905 0.01538462 0.05263158]]
    


### Array Mathematics

#### Arithmetic Operations
Python's native operators can be directly used as a convenient wrapper for NumPy's ufuncs to `broadcast` the operation over all the elements of that array.


```python
x = np.arange(-5, 5)
print("x      =", x)
print("x + 10  =", x + 10) # wrapper for np.sum 
print("x - 10  =", x - 10) # wrapper for np.subtract
print("x * 4  =", x * 4)  # wrapper for np.multiply
print("x / 4  =", x / 4)  # wrapper for np.divide
print("x % 4  =", x % 4)  # wrapper for np.mod
print("x // 4 =", x // 4) # wrapper for np.floor_divide
print("x ** 2 =", x ** 2) # wrapper for np.power
print("abs(x) =", abs(x)) # wrapper for np.abs
```

    x      = [-5 -4 -3 -2 -1  0  1  2  3  4]
    x + 10  = [ 5  6  7  8  9 10 11 12 13 14]
    x - 10  = [-15 -14 -13 -12 -11 -10  -9  -8  -7  -6]
    x * 4  = [-20 -16 -12  -8  -4   0   4   8  12  16]
    x / 4  = [-1.25 -1.   -0.75 -0.5  -0.25  0.    0.25  0.5   0.75  1.  ]
    x % 4  = [3 0 1 2 3 0 1 2 3 0]
    x // 4 = [-2 -1 -1 -1 -1  0  0  0  0  1]
    x ** 2 = [25 16  9  4  1  0  1  4  9 16]
    abs(x) = [5 4 3 2 1 0 1 2 3 4]


The above operations have been performed on the array of a particular datatype and so the result will have the same datatype as the array that is being operated on. However when you perform any operation on an array that results in a different datatype or on multiple arrays of different datatypes, the type of the resulting array will correspond to the more precise one. This is also known as upcasting.

In the above example, check the output of division (/). Can you find the type of that array?

When standard mathematical operations are used with numpy arrays, they are applied on an element-by-element basis and a new array is created and filled with the result. This means that the arrays should be of same size when any mathematical operation is performed on them.


```python
arr1 = np.array([1., 2., 3., 4.])
arr2 = np.linspace(4, 16, num=4)
print("Array1: \n{}".format(arr1), end="\n\n")
print("Array2: \n{}".format(arr2), end="\n\n")
print("\n Array2 - Array1: \n {}".format(arr2-arr1), end="\n\n")
```

    Array1: 
    [1. 2. 3. 4.]
    
    Array2: 
    [ 4.  8. 12. 16.]
    
    
     Array2 - Array1: 
     [ 3.  6.  9. 12.]
    


However, if there was a size mismatch, then we would receive a `ValueError`


```python
arr2 = np.linspace(4, 16, num=3)
print("\n Array2 - Array1: \n {}".format(arr2-arr1), end="\n\n")
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-7-6db414b41f4e> in <module>
          1 arr2 = np.linspace(4, 16, num=3)
    ----> 2 print("\n Array2 - Array1: \n {}".format(arr2-arr1), end="\n\n")
    

    ValueError: operands could not be broadcast together with shapes (3,) (4,) 


Well you might wonder why was it that we did not get a broadcast error when we performed addition of a single number over an array. We shall look at this in the module on Broadcasting.

#### Trignometric Functions
Just like Arithmetic operations, NumPy provides a bunch of trigonometric `ufuncs`. Let’s take a look at some.


```python
input_arr = np.random.uniform(-1, 1, 5)
print("Input Array: \n{}".format(input_arr), end="\n\n")
print("sin: \n{}".format(np.sin(input_arr)), end="\n\n")
print("cos: \n{}".format(np.cos(input_arr)), end="\n\n")
print("tan: \n{}".format(np.tan(input_arr)), end="\n\n")
print("arcsin: \n{}".format(np.arcsin(input_arr)), end="\n\n")
print("arccos: \n{}".format(np.arccos(input_arr)), end="\n\n")
print("arctan: \n{}".format(np.arctan(input_arr)), end="\n\n")
```

    Input Array: 
    [-0.95633706 -0.49033535 -0.48827774  0.5121991   0.16100066]
    
    sin: 
    [-0.81708531 -0.47092175 -0.46910558  0.49009532  0.16030601]
    
    cos: 
    [0.57651678 0.88217498 0.88314209 0.87166885 0.98706737]
    
    tan: 
    [-1.4172793  -0.53381898 -0.53117792  0.56224943  0.16240635]
    
    arcsin: 
    [-1.27420085 -0.51247449 -0.51011515  0.53774331  0.16170446]
    
    arccos: 
    [2.84499718 2.08327082 2.08091147 1.03305302 1.40909187]
    
    arctan: 
    [-0.76308315 -0.45588604 -0.4542259   0.47335919  0.15963079]
    


#### Logarithmic Functions
Numpy provides logarithmic ufuncs for different `bases'


```python
input_arr = np.random.randint(1, 7, 5)
print("x        =", input_arr)
print("ln(x)    =", np.log(input_arr))
print("log2(x)  =", np.log2(input_arr))
print("log10(x) =", np.log10(input_arr))
```

    x        = [5 6 4 6 2]
    ln(x)    = [1.60943791 1.79175947 1.38629436 1.79175947 0.69314718]
    log2(x)  = [2.32192809 2.5849625  2.         2.5849625  1.        ]
    log10(x) = [0.69897    0.77815125 0.60205999 0.77815125 0.30103   ]


Counterpart of Logs, we also have exponential ufuncs


```python
input_arr = np.random.randint(1, 7, 5)
print("x     =", input_arr)
print("e^x   =", np.exp(input_arr))
print("2^x   =", np.exp2(input_arr))
print("10^x   =", np.power(10, input_arr))
```

    x     = [5 1 4 4 2]
    e^x   = [148.4131591    2.71828183  54.59815003  54.59815003   7.3890561 ]
    2^x   = [32.  2. 16. 16.  4.]
    10^x   = [100000     10  10000  10000    100]

