[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/03-00%20Introduction%20to%20Numpy.ipynb) 

> Click above image to access the interactive version of this notebook


## 03 - 00 Introduction to Numpy
`Numpy` (Numerical Python) is an opensource library for performing scientific computation in python. Numpy lets you work with arrays and matrices in a natural way unlike lists where you have to loop through individual elements to perform any numerical operation. 
> This would probably be a good time to refresh your memory on what are arrays and matrices.. here is something that you need to know to get started
> - Arrays are simply a collection of values of *same type* indexed by integers.
> - Matrices are defined to be multi-dimensional array indexed by rows, columns and dimensions.

The methods in numpy are designed with high performance in mind. Numpy arrays are stored more efficiently than an equivalent data structure in python such as lists and arrays. This especially pays off when you are using really large arrays (i.e large data sets). The major portion of numpy is written in C and thus the computations are faster than the pure python code. Numpy is one of the part of the scientific stack in Python. It actually used to be a part of major scientific package called SciPy but was later separated and now scipy uses numpy for almost all of its major tasks.

Numpy is a very huge topic and we will barely scratch the surface in this bootcamp but it will be enough to get you all up to speed for starting with your Master's courseworks. 

In this module (and sub-modules) we will be looking at ways for effectively loading, storing, and manipulating in-memory. We will be dealing with some of the datasets comprising of wide range of sources such as images, sound clips, text data etc. but to reach that stage, lets first get a working understanding of `Numpy Arrays`.

Numpy is a third party module that has been installed for you here on UCSLHUB. Before we can begin using Numpy, we have to first `import` it in python. You must remember from the File IO module where we imported built-in csv module. Similarly, to import numpy module, you can type


```python
import numpy as np
print(np.__version__)
```

    1.19.2


We use `import numpy as np` so that we wont have to type `numpy` everytime we want to use the module, instead we can use `np`.

A gentle reminder to use tab-completion(`<TAB>`) and `?` to explore and access the documentation for anything that you are looking for.

Example:
```ipython
In [1]: np.<TAB>
```
or 
```ipython
In [2]: np.__version__?
```
