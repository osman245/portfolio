[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/01-03%20Numeric%20Types.ipynb) 

> Click above image to access the interactive version of this notebook

## Numeric Types
As we mentioned in the opening to this section, in Python there are basically 3 built-in Numeric Data-Types

- int
- float
- complex

This sectino will illustrate a bit more about each.

### int
Integers are the most basic numeric type in Python. Any number that does not contain a decimal point is considered as an integer and is of type int.

An interesting difference between the int type in Python and other languages is that they are variable precision. This means that the integer computation on other languages will overflow at either  2^31 or 2^63 (based on whether you have 32-bit or 64-bit CPU architecture). However, in Python, you can perform computation on numbers that are larger than these. (Actually, the precision of a number can increase till your computer runs out of memory)


```python
# this will crash on C
2 ** 120
```




    1329227995784915872903807060280344576



### float
Floating point numbers contain the numbers with decimal point, that is they can hold the result of fractions or exponential numbers.

Any integer can be converted to float by passing it to the float constructor:


```python
float(2)
```




    2.0




```python
2e4
```




    20000.0



### complex 
Complex numbers are the numbers with real and imaginary parts. Just like int or float, we can construct a complex number by passing the arguments to the complex constructor:



```python
c_val = complex(2, 3)
print(c_val)
```

    (2+3j)



```python
c_val.real
```




    2.0




```python
c_val.imag
```




    3.0




```python
c_val.conjugate() # complex conjugate of c_val
```




    (2-3j)



Magnitude of a complex number:

i.e. $\sqrt{(c.real^2 + c.imag^2)}$

can be obtained by using `abs` function


```python
abs(c_val)
```




    3.605551275463989



We shall take a deeper look at these datatypes and the operations that can be performed on them in the Operators module.
