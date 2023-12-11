[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/01-04%20Operators.ipynb) 

> Click above image to access the interactive version of this notebook


## Operators

Operators in Python are the constructs which can manipulate the value of operands. Simply put when operators are used with one or more than one operand, they produce some result. Consider a basic mathematical addition `2` in this case, `1` and `2` are operands and `+` is the operator. Operands can also be variables. Python supports following types of operators:

- Arithmetic Operators
- Relational (Comparison) Operators
- Assignment Operators
- Logical Operators
- Bitwise Operators
- Membership Operators
- Identity Operators


### Arithmetic Operators

As the name suggests, Arithmetic Operators includes all the operators to perform basic arithmetic functions.

#### Addition (+)

Addition operator adds the value of the operands on its either side. 


```python
2 + 2
```




    4



#### Subtraction (-)

Subtracts right hand operand with the operand on the left hand.


```python
2 - 2
```




    0



#### Multiplication ( * )

Multiplies the operands on its either sides and outputs the product.


```python
2 * 2
```




    4



#### Division ( / )

Divides left hand operand with the right hand operand and outputs the quotient of the division.


```python
2 / 2
```




    1.0



#### Modulus ( % )

Divides left hand operand with the right hand operate and outputs the remainder of the division.


```python
7 % 2
```




    1



#### Exponential ( ** )

Performs exponential operation on the operands. The left hand operand is 'raised to' the right hand operand.


```python
4 ** 4
```




    256



#### Floor Division ( // )

Divides the left hand operand with the right hand operand and outputs the quotient of the division removing the digits after decimal point.


```python
3.0 // 2
```




    1.0



### Relational Operators

Relational Operators compare the operands on either side and identifies the relation between them. These are also known as Comparison Operators.

#### Equal to ( == )

If the value of the two operands are equal, the condition becomes true.


```python
a, b = 10, 10
```


```python
a == b
```




    True



#### Not Equal to ( != )

If the value of two operands are not equal, the condition becomes true.


```python
a != b
```




    False



#### Greater than ( > )

If the value of the operand on the left hand side of the operator is greater than the value of the operand on the right hand side, the condition becomes true.


```python
a > b
```




    False



#### Less than ( < )

If the value of the operand on the left hand side of the operator is less than the value of the operand on the right hand side, the condition becomes true.


```python
a < b
```




    False



#### Greater than OR Equal to ( >= )

If the value of the operand on the left hand side of the operator is greater than or equal to the operand on the right hand side, the condition becomes true.


```python
a >= b
```




    True



#### Less than OR Equal to ( <= )

If the value of the operand on the left hand side of the operator is less than or equal to the operand on the right hand side, the condition becomes true.


```python
a <= b
```




    True




###Assignment Operators

The assignment operator is responsible for assigning some value to a variable. Example a = 2 .We have been doing this for quite now, but the assignment operator can be used in many other ways.



#### Equals ( = )

Assigns the value from right hand side operand to the left hand side operand.


```python
a = 10
```


#### Add AND ( += )

It is logically a two-step process. In the first step, the side operand is added to the left-hand side operand. In the second step, the output of the first step is assigned to the operand on the side. This sort of shorthand can make code more readable.


```python
a += 10  # It is equivalent to a = a + 10
```

#### Subtract AND ( -= )

It is also a process where the right operand is subtracted from the left operand and the result is assigned to the left operand


```python
a -= 10  # It is equivalent to a = a - 10
```

#### Multiply AND ( *= )

The right operand is multiplied with the left operand and the result is assigned to the left operand.


```python
a *= 10  # It is equivalent to a = a * 10
```

#### Divide AND ( /= )

The left operand is divided by the right operand and the quotient is assigned to the left operand.


```python
a /= 10  # It is equivalent to a = a / 10
```

#### Modulus AND ( %= )

It takes the modulus of the two operands and assigns the result to the left operand


```python
a %= 10  # It is equivalent to a = a % 10
```

#### Exponent AND ( **= )

It performs the exponential operation on the two operands and assigns the value to the left operand


```python
a **= 10  # It is equivalent to a = a ** 10
```

#### Floor Division AND ( //= )

It performs floor division and assigns the quotient to the left operand.


```python
a //= 10 # It is equivalent to a = a // 10
```

### Bitwise Operator

Bitwise operator works on bits and performs operations bit by bit. Before we jump into the operator, let's revise the concept of Bits. At the smallest scale in computers, the information is stored in bits. Consider bit as the smallest unit of storage, just like an atom. A bit can only store binary values i.e 0's or 1's (but not both). n bits can store 2 to the power of n values (n 0's or 1's). Practically a bit is very small for storage purposes, thus we deal with bytes which is equal to 8 bits. Then comes KiloBytes and MegaBytes and so on... To understand the working of bitwise operators, we need to convert the operands to bits.

To understand the conversion between decimal and binary numbers, watch this video.

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/H4BstqvgBow/0.jpg)](https:/youtube.com/v/H4BstqvgBow)

For examples below, we will be using a, b = 6, 10. In python binary equivalent can be obtained by using a built-in function bin() which basically converts the integer to binary representation. If you followed the tutorial video above you must be writing full 8-bit representation for even a small integer. Python's bin() however only prints the bits that are necessary for representing the integer. For example,


```python
bin(6)   # To print the binary equivalent of integer 6
```




    '0b110'



The leading 0b is for python to understand that the string representation means a binary number and not a regular string. Let's dive into the bitwise operators.

Let's get going with our examples.


```python
a,b = 6, 10
```

#### Binary AND ( & )

Operator uses two operands comparing them bit by bit. It outputs 1 if and only if both the operands have 1 at same bit location


```python
bin(a & b)
```




    '0b10'



#### Binary OR ( | ) 
("|" is the key above Return/ Enter key)

Operator uses two operands comparing them bit by bit. It outputs 1 if both the operands do not have 0 at same bit location.


```python
bin(a | b)
```




    '0b1110'



#### Binary XOR ( ^ )

The operator uses two operands comparing them bit by bit. It outputs 1 if and only if both the operands do not have same bit value at the same location.




```python
bin(a ^ b)
```




    '0b1100'



#### Binary One's Complement ( ~ )

Operator uses single operand and toggles the bit value at every location. The operator would toggle between 0 and 1. So if the existing value is 0, it becomes 1 and vice-versa.


```python
bin(~ a)
```




    '-0b111'



#### Binary Left Shift ( << )

Operator shifts the bit location of the left operand towards left by the number of bits specified by the right operand.


```python
bin(a << 2)
```




    '0b11000'



#### Binary Right Shift ( >> )

Operator shifts the bit location of the left operand towards the right by the number of bits specified by the right operand.


```python
bin(a >> 2)
```




    '0b1'



### Logical Operators

Python supports three logical operators viz AND, OR and NOT.

#### AND ( and )

If both the operands are true, the condition becomes true.

#### OR ( or )

If any of the two operands are true, the condition becomes true.

#### NOT (not)



Reverses the logical state of the operand.

### Membership Operator

This operator basically tests if the two operands are pointing at the same object or not. There are two types of membership operators:

It evaluates to true if the operands on both the sides of the operator point to the same object.


```python
a = 10
b = 10
```


```python
a == b
```




    True




```python
a is b
```




    True



**So, does this mean that `==` is same as `is` operator? **


```python
id(a)
```




    4545799568




```python
id(b)
```




    4545799568



Python keeps an array of integer objects for all integers between -5 and 256, when you create an `int` in that range you actually just get back a reference to the existing object!

This means that if you check the `id()` for any integer between -5 and 256 (both included), they will turn out to be the same every time.


```python
id(100)
```




    4545802448




```python
id(100)
```




    4545802448



Now if I try to find the `id()` for any integer *except* between -5 and 256, I will get different id's everytime

*(try running the following two cells multiple times and see the different id's being returned everytime)*


```python
id(2500)
```




    4580880080




```python
id(2500)
```




    4580880240



For more information you can refer:
1. [Stackoverflow](http://stackoverflow.com/questions/306313/is-operator-behaves-unexpectedly-with-integers) question as pointed out by Ben Miller (*Student* NYU CUSP 2017 Cohort).
2. [Python C-API](https://docs.python.org/2/c-api/int.html#c.PyInt_FromLong)

#### Is Not

It evaluates to true if both the operands do not point to the same object.


```python
a is not b
```




    False



### Identity Operator 

It is same as the Python's Membership operator.

- Implement your own decimal to 8-bit binary converter. Convert decimal number 88 and see if the output is 01011000 .
