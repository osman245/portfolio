[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/05-01%20Series%20and%20Dataframe.ipynb) 

> Click above image to access the interactive version of this notebook


## Pandas Series and Dataframes

**Pandas** is a Python package providing fast, flexible, and expressive data structures designed to make working with “relational” or “labeled” data both easy and intuitive. It aims to be the fundamental high-level building block for doing practical, real world data analysis in Python.
Pandas provides high-performance, easy-to-use data structures and data analysis tools for the Python programming language. To get started with pandas, you will need to get comfortable with its two workhorse data structures: Series and DataFrame. 

## Series
Pandas Series is a one-dimensional array-like object that has index and value just like NumPy. In fact if you view the type of the values of series object, you will see that it indeed is `numpy.ndarray`.

You can assign name to pandas Series.



```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
plt.style.use('seaborn-darkgrid')
```


```python
ob = pd.Series([8,7,6,5], name='test_data')
print('Name: ',ob.name)
print('Data:\n',ob)
print('Type of Object: ',type(ob))
print('Type of elements:',type(ob.values))
```

    Name:  test_data
    Data:
     0    8
    1    7
    2    6
    3    5
    Name: test_data, dtype: int64
    Type of Object:  <class 'pandas.core.series.Series'>
    Type of elements: <class 'numpy.ndarray'>


You can also use your numpy array and convert them to Series.


```python
# integers between 5 to 8 (reversed)
ob = pd.Series(np.linspace(5, 8, num=4, dtype=int)[::-1])
print(ob)
print(type(ob))
```

    0    8
    1    7
    2    6
    3    5
    dtype: int64
    <class 'pandas.core.series.Series'>


You can also provide custom index to the values and just like in Numpy, access them with the index.


```python
ob = pd.Series([8,7,6,5], index=['a','b','c','d'])
print(ob['b'])
```

    7


Pandas Series is more like a fixed size dictionary whose mapping of index-value is preserved when array operations are applied to them. For example,


```python
# select all the values greater than 4 and less than 8
print(ob[(ob>4) & (ob<8)])
```

    b    7
    c    6
    d    5
    dtype: int64


This also means that if you have a dictionary, you can easily convert that into pandas series.


```python
states_dict = {'State1': 'Alabama', 
               'State2': 'California', 
               'State3': 'New Jersey', 
               'State4': 'New York'}
ob = pd.Series(states_dict)
print(ob)
print(type(ob))
```

    State1       Alabama
    State2    California
    State3    New Jersey
    State4      New York
    dtype: object
    <class 'pandas.core.series.Series'>


Just like dictionaries, you can also change the index using the following method. 


```python
ob.index = ['AL','CA','NJ','NY']
print(ob)
```

    AL       Alabama
    CA    California
    NJ    New Jersey
    NY      New York
    dtype: object


or use dictionary's method to get the label..


```python
ob.get('CA', np.nan)
```




    'California'



## Dataframe
Dataframe is something like spreadsheet or a sql table. It is basically a 2 dimensional labelled data structure with columns of potentially different datatype. Like Series, DataFrame accepts many different kinds of input:
* Dict of 1D ndarrays, lists, dicts, or Series
* 2-D numpy.ndarray
* [`Structured or record ndarray`](http://docs.scipy.org/doc/numpy/user/basics.rec.html 'Structured or record ndarray')
* A Series
* Another DataFrame

Compared with other such DataFrame-like structures you may have used before (like `R’s` `data.frame`), row- oriented and column-oriented operations in DataFrame are treated roughly symmetrically. Under the hood, the data is stored as one or more two-dimensional blocks rather than a list, dict, or some other collection of one-dimensional arrays.


### Creating Dataframes from dictionaries


```python
data = {'one' : pd.Series([1., 2., 3.], index=['a', 'b', 'c']),
    'two' : pd.Series([1., 2., 3., 4.], index=['a', 'b', 'c', 'd'])}
```


```python
df = pd.DataFrame(data)
print('Dataframe:\n',df)
print('Type of Object:',type(df))
print('Type of elements:',type(df.values))
```

    Dataframe:
        one  two
    a  1.0  1.0
    b  2.0  2.0
    c  3.0  3.0
    d  NaN  4.0
    Type of Object: <class 'pandas.core.frame.DataFrame'>
    Type of elements: <class 'numpy.ndarray'>


Another way to construct dataframe from dictionaries is by using DataFrame.from_dict function. DataFrame.from_dict takes a dict of dicts or a dict of array-like sequences and returns a DataFrame. It operates like the DataFrame constructor except for the orient parameter which is 'columns' by default, but which can be set to 'index' in order to use the dict keys as row labels.

Just like Series, you can access index, values and also columns.


```python
print('Index: ',df.index)
print('Columns: ',df.columns)
print('Values of Column one: ',df['one'].values)
print('Values of Column two: ',df['two'].values)
```

    Index:  Index(['a', 'b', 'c', 'd'], dtype='object')
    Columns:  Index(['one', 'two'], dtype='object')
    Values of Column one:  [ 1.  2.  3. nan]
    Values of Column two:  [1. 2. 3. 4.]


### Creating dataframe from list of dictionaries

As with Series, if you pass a column that isn’t contained in data, it will appear with NaN values in the result


```python
df2 = pd.DataFrame([{'a': 1, 'b': 2, 'c':3, 'd':None}, 
                    {'a': 2, 'b': 2, 'c': 3, 'd': 4}],
                   index=['one', 'two'])
print('Dataframe: \n',df2)

# Ofcourse you can also transpose the result:
print('Transposed Dataframe: \n',df2.T)
```

    Dataframe: 
          a  b  c    d
    one  1  2  3  NaN
    two  2  2  3  4.0
    Transposed Dataframe: 
        one  two
    a  1.0  2.0
    b  2.0  2.0
    c  3.0  3.0
    d  NaN  4.0


Assigning a column that doesn’t exist will create a new column. 


```python
df['three'] = None
print('Added third column: \n',df)

# The del keyword can be used delete columns:
del df['three']
print('\nDeleted third column: \n',df)
# You can also use df.drop(). We shall see that later
```

    Added third column: 
        one  two three
    a  1.0  1.0  None
    b  2.0  2.0  None
    c  3.0  3.0  None
    d  NaN  4.0  None
    
    Deleted third column: 
        one  two
    a  1.0  1.0
    b  2.0  2.0
    c  3.0  3.0
    d  NaN  4.0


Each Index has a number of methods and properties for set logic and answering other common questions about the data it contains.


|Method | Description|
|:---|:---|
|`append` | Concatenate with additional Index objects, producing a new Index|
|`diff` | Compute set difference as an Index|
|`intersection` | Compute set intersection|
|`union` | Compute set union|
|`isin` | Compute boolean array indicating whether each value is contained in the passed collection|
|`delete` | Compute new Index with element at index i deleted|
|`drop` | Compute new index by deleting passed values|
|`insert` | Compute new Index by inserting element at index i|
|`is_monotonic` | Returns True if each element is greater than or equal to the previous element| 
|`is_unique` | Returns True if the Index has no duplicate values|
|`unique` | Compute the array of unique values in the Index|

for example:


```python
print(1 in df.one.values)
print('one' in df.columns)
```

    True
    True


## Reindexing
A critical method on Pandas objects is reindex, which means to create a new object with the data conformed to a new index.

The following is how you might reindex.


```python
data = {'one' : pd.Series([1., 2., 3.], index=['a', 'b', 'c']),
    'two' : pd.Series([1., 2., 3., 4.], index=['a', 'b', 'c', 'd'])}
df = pd.DataFrame(data)
print(df)
```

       one  two
    a  1.0  1.0
    b  2.0  2.0
    c  3.0  3.0
    d  NaN  4.0



```python
# Reindex in descending order.
print(df.reindex(['d','c','b','a']))
```

       one  two
    d  NaN  4.0
    c  3.0  3.0
    b  2.0  2.0
    a  1.0  1.0


If you `reindex` with more number of rows than in the dataframe, it will return the dataframe with new row whose values are `NaN`.


```python
print(df.reindex(['a','b','c','d','e']))
```

       one  two
    a  1.0  1.0
    b  2.0  2.0
    c  3.0  3.0
    d  NaN  4.0
    e  NaN  NaN


Reindexing is also useful when you want to introduce any missing values. For example in our case, look at column `one` and row `d`


```python
df.reindex(['a','b','c','d','e'], fill_value=0)
# Guess why the df['one']['d'] was not filled with 0 ?
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>one</th>
      <th>two</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>e</th>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



For ordered data like time series, it may be desirable to do some interpolation or filling of values when `reindex`ing. The method option allows us to do this, using a `method` such as `ffill` which forward fills the values:


```python
df.reindex(['a','b','c','d','e'], method='ffill')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>one</th>
      <th>two</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>e</th>
      <td>NaN</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>



There are basically two different types of method (interpolation) options:

|Method | Description|
|:---|:---|
|`ffill` or `pad` | Fill (or carry) values forward |
|`bfill` or `backfill` | Fill (or carry) values backward|

Reindexing has following arguments:

|Argument | Description|
|:---|:---|
|`index` | New sequence to use as index. Can be Index instance or any other sequence-like Python data structure. An Index will be used exactly as is without any copying|
|`method` | Interpolation (fill) method, see above table for options.|
|`fill_value` | Substitute value to use when introducing missing data by reindexing.|
|`limit` | When forward- or backfilling, maximum size gap to fill|
|`level` | Match simple Index on level of MultiIndex, otherwise select subset of|
|`copy` | Do not copy underlying data if new index is equivalent to old index. True by default (i.e. always copy data)|

## Dropping Entries
Dropping one or more entries from an axis is easy if you have an index array or list without those entries.


```python
# Drop row c and row a
df.drop(['c', 'a'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>one</th>
      <th>two</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>b</th>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# And to drop column two try this
df.drop(['two'], axis=1)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>one</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2.0</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3.0</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



## Indexing, selection, Sorting and filtering
Series indexing works analogously to NumPy array indexing, except you can use the Series’s index values instead of only integers.

To slice and select only column one for rows 0 and 4 use the following.


```python
print("Dataframe: \n",df)
# Slicing and selecting only column `one` for row 0 and row 4
df['one'][['a', 'd']]
```

    Dataframe: 
        one  two
    a  1.0  1.0
    b  2.0  2.0
    c  3.0  3.0
    d  NaN  4.0





    a    1.0
    d    NaN
    Name: one, dtype: float64




```python
# Slicing df from row b to row 4 for column `one`
df['one']['b':'d']
```




    b    2.0
    c    3.0
    d    NaN
    Name: one, dtype: float64



If you observe the above command (and the one above it), you will see that slicing with labels behaves differently than normal Python slicing in that the endpoint is inclusive.

For DataFrame label-indexing on the rows, there is a special indexing field `ix` (or `loc`). It enables you to select a subset of the rows and columns from a DataFrame with NumPy- like notation plus axis labels. It is a less verbose way to do the reindexing.


```python
df.loc[['a','c'],['one']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>one</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3.0</td>
    </tr>
  </tbody>
</table>
</div>



There are many ways to select and rearrange the data contained in a pandas object. Some indexing options can be seen in below table:

|Indexing Type| Description|
|:---|:---|
|df[val] | Select single column or sequence of columns from the DataFrame. Special case con- veniences: boolean array (filter rows), slice (slice rows), or boolean DataFrame (set values based on some criterion).|
|df.ix[val] | (Deprecated)Selects single row of subset of rows from the DataFrame.|
|df.ix[:, val] | (Deprecated)Selects single column of subset of columns.|
|df.ix[val1, val2] | (Deprecated)Select both rows and columns.|
|reindex method | Conform one or more axes to new indexes.|
|xs method | Select single row or column as a Series by label.|
|icol, irowmethods | Select single column or row, respectively, as a Series by integer location.|
|get_value, set_value methods | Select single value by row and column label.|

You can sort a data frame or series (by some criteria) using the built-in functions. To sort lexicographically by row or column index, use the sort_index method, which returns a new, sorted object:


```python
dt = pd.Series(np.random.randint(3, 10, size=7), 
               index=['g','c','a','b','e','d','f'])
print('Original Data: \n', dt, end="\n\n")
print('Sorted by Index: \n',dt.sort_index())
```

    Original Data: 
     g    6
    c    7
    a    5
    b    8
    e    9
    d    4
    f    6
    dtype: int64
    
    Sorted by Index: 
     a    5
    b    8
    c    7
    d    4
    e    9
    f    6
    g    6
    dtype: int64


## Data alignment and arithmetic
Data alignment between DataFrame objects automatically align on both the columns and the index (row labels). The resulting object will have the union of the column and row labels.


```python
df1 = pd.DataFrame(np.random.randn(10, 4), columns=['A', 'B', 'C', 'D'])
df2 = pd.DataFrame(np.random.randn(7, 3), columns=['A', 'B', 'C'])
print('df1:\n',df1, end="\n\n")
print('df2:\n',df2, end="\n\n")
print('Sum:\n',df1.add(df2))
```

    df1:
               A         B         C         D
    0 -0.051041  1.435317  1.040367 -1.386706
    1 -0.695859  0.657432 -0.219758 -0.439142
    2 -2.134614 -0.769775 -1.062250  0.341384
    3  0.012058 -1.187045  1.259480  1.272664
    4  1.222599 -1.156810  0.129261  1.227567
    5 -1.903387  0.862699 -1.726118 -0.219394
    6 -1.161552 -0.005517  1.171261 -0.405814
    7 -1.675452  0.447608 -0.216641 -0.193666
    8 -0.657099  1.472844 -0.263241 -3.446278
    9  1.012759 -0.365675 -0.715288  0.377585
    
    df2:
               A         B         C
    0 -0.960266 -0.594496  0.739223
    1 -1.199692  0.863185  0.592592
    2  1.936042  0.675810  0.740688
    3  0.194588 -0.335408 -3.104826
    4 -0.259973 -1.860402  0.757029
    5  0.858095  1.355071 -0.587613
    6  0.051702 -1.551271 -0.232850
    
    Sum:
               A         B         C   D
    0 -1.011307  0.840822  1.779590 NaN
    1 -1.895552  1.520617  0.372834 NaN
    2 -0.198572 -0.093965 -0.321562 NaN
    3  0.206646 -1.522453 -1.845345 NaN
    4  0.962626 -3.017212  0.886290 NaN
    5 -1.045291  2.217770 -2.313732 NaN
    6 -1.109850 -1.556788  0.938411 NaN
    7       NaN       NaN       NaN NaN
    8       NaN       NaN       NaN NaN
    9       NaN       NaN       NaN NaN


Note that in arithmetic operations between differently-indexed objects, you might want to fill with a special value, like 0, when an axis label is found in one object but not the other:


```python
print('Sum:\n',df1.add(df2, fill_value=0))
```

    Sum:
               A         B         C         D
    0 -1.011307  0.840822  1.779590 -1.386706
    1 -1.895552  1.520617  0.372834 -0.439142
    2 -0.198572 -0.093965 -0.321562  0.341384
    3  0.206646 -1.522453 -1.845345  1.272664
    4  0.962626 -3.017212  0.886290  1.227567
    5 -1.045291  2.217770 -2.313732 -0.219394
    6 -1.109850 -1.556788  0.938411 -0.405814
    7 -1.675452  0.447608 -0.216641 -0.193666
    8 -0.657099  1.472844 -0.263241 -3.446278
    9  1.012759 -0.365675 -0.715288  0.377585


Similarly you can perform subtracion, multiplication and division. 

When doing an operation between DataFrame and Series, the default behavior is to align the Series index on the DataFrame columns, thus broadcasting (just like in numpy) row-wise.


```python
print("Dataframe: \n", df1, end="\n\n")
print("Operand (0th row): \n", df1.loc[0], end="\n\n")
print('Subtraction: \n',df1.sub(df1.loc[0]))
```

    Dataframe: 
               A         B         C         D
    0 -0.051041  1.435317  1.040367 -1.386706
    1 -0.695859  0.657432 -0.219758 -0.439142
    2 -2.134614 -0.769775 -1.062250  0.341384
    3  0.012058 -1.187045  1.259480  1.272664
    4  1.222599 -1.156810  0.129261  1.227567
    5 -1.903387  0.862699 -1.726118 -0.219394
    6 -1.161552 -0.005517  1.171261 -0.405814
    7 -1.675452  0.447608 -0.216641 -0.193666
    8 -0.657099  1.472844 -0.263241 -3.446278
    9  1.012759 -0.365675 -0.715288  0.377585
    
    Operand (0th row): 
     A   -0.051041
    B    1.435317
    C    1.040367
    D   -1.386706
    Name: 0, dtype: float64
    
    Subtraction: 
               A         B         C         D
    0  0.000000  0.000000  0.000000  0.000000
    1 -0.644818 -0.777885 -1.260125  0.947564
    2 -2.083572 -2.205093 -2.102617  1.728090
    3  0.063099 -2.622363  0.219114  2.659369
    4  1.273640 -2.592127 -0.911106  2.614273
    5 -1.852345 -0.572618 -2.766485  1.167312
    6 -1.110511 -1.440834  0.130894  0.980892
    7 -1.624411 -0.987710 -1.257008  1.193040
    8 -0.606057  0.037527 -1.303608 -2.059572
    9  1.063800 -1.800993 -1.755655  1.764291


In the special case of working with time series data, and the DataFrame index also contains dates, the broadcasting will be column-wise:


```python
ind1 = pd.date_range('06/1/2017', periods=10)
df1.set_index(ind1)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017-06-01</th>
      <td>-0.051041</td>
      <td>1.435317</td>
      <td>1.040367</td>
      <td>-1.386706</td>
    </tr>
    <tr>
      <th>2017-06-02</th>
      <td>-0.695859</td>
      <td>0.657432</td>
      <td>-0.219758</td>
      <td>-0.439142</td>
    </tr>
    <tr>
      <th>2017-06-03</th>
      <td>-2.134614</td>
      <td>-0.769775</td>
      <td>-1.062250</td>
      <td>0.341384</td>
    </tr>
    <tr>
      <th>2017-06-04</th>
      <td>0.012058</td>
      <td>-1.187045</td>
      <td>1.259480</td>
      <td>1.272664</td>
    </tr>
    <tr>
      <th>2017-06-05</th>
      <td>1.222599</td>
      <td>-1.156810</td>
      <td>0.129261</td>
      <td>1.227567</td>
    </tr>
    <tr>
      <th>2017-06-06</th>
      <td>-1.903387</td>
      <td>0.862699</td>
      <td>-1.726118</td>
      <td>-0.219394</td>
    </tr>
    <tr>
      <th>2017-06-07</th>
      <td>-1.161552</td>
      <td>-0.005517</td>
      <td>1.171261</td>
      <td>-0.405814</td>
    </tr>
    <tr>
      <th>2017-06-08</th>
      <td>-1.675452</td>
      <td>0.447608</td>
      <td>-0.216641</td>
      <td>-0.193666</td>
    </tr>
    <tr>
      <th>2017-06-09</th>
      <td>-0.657099</td>
      <td>1.472844</td>
      <td>-0.263241</td>
      <td>-3.446278</td>
    </tr>
    <tr>
      <th>2017-06-10</th>
      <td>1.012759</td>
      <td>-0.365675</td>
      <td>-0.715288</td>
      <td>0.377585</td>
    </tr>
  </tbody>
</table>
</div>



## Using Numpy functions on DataFrame
Elementwise NumPy `ufuncs` like `log`, `exp`, `sqrt`, ... and various other NumPy functions can be used on DataFrame


```python
np.abs(df1)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.051041</td>
      <td>1.435317</td>
      <td>1.040367</td>
      <td>1.386706</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.695859</td>
      <td>0.657432</td>
      <td>0.219758</td>
      <td>0.439142</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.134614</td>
      <td>0.769775</td>
      <td>1.062250</td>
      <td>0.341384</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.012058</td>
      <td>1.187045</td>
      <td>1.259480</td>
      <td>1.272664</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.222599</td>
      <td>1.156810</td>
      <td>0.129261</td>
      <td>1.227567</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.903387</td>
      <td>0.862699</td>
      <td>1.726118</td>
      <td>0.219394</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1.161552</td>
      <td>0.005517</td>
      <td>1.171261</td>
      <td>0.405814</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1.675452</td>
      <td>0.447608</td>
      <td>0.216641</td>
      <td>0.193666</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.657099</td>
      <td>1.472844</td>
      <td>0.263241</td>
      <td>3.446278</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1.012759</td>
      <td>0.365675</td>
      <td>0.715288</td>
      <td>0.377585</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Convert to numpy array
np.asarray(df1)
```




    array([[-0.05104128,  1.43531747,  1.04036687, -1.38670585],
           [-0.69585942,  0.65743225, -0.21975805, -0.43914213],
           [-2.13461366, -0.76977509, -1.06225   ,  0.34138446],
           [ 0.01205761, -1.18704538,  1.2594805 ,  1.27266359],
           [ 1.22259879, -1.15680983,  0.12926136,  1.2275674 ],
           [-1.90338674,  0.86269946, -1.72611846, -0.21939369],
           [-1.16155224, -0.00551654,  1.17126116, -0.40581426],
           [-1.67545226,  0.44760794, -0.2166412 , -0.19366562],
           [-0.65709867,  1.47284432, -0.26324095, -3.44627833],
           [ 1.01275903, -0.36567521, -0.71528779,  0.3775854 ]])



Below you will see another frequent operation is applying a function on 1D arrays to each column or row. DataFrame’s apply method does exactly this:


```python
def fn(x):
    """
    Get max and min of the columns
    """
    return pd.Series([x.min(), x.max()], index=['min', 'max'])

df1.apply(fn)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>min</th>
      <td>-2.134614</td>
      <td>-1.187045</td>
      <td>-1.726118</td>
      <td>-3.446278</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.222599</td>
      <td>1.472844</td>
      <td>1.259480</td>
      <td>1.272664</td>
    </tr>
  </tbody>
</table>
</div>



Element-wise Python functions can be used, too. Suppose you wanted to format the dataframe elements in floating point format with accuracy of only 3 decimal places. You can do this with applymap:


```python
fmt = lambda x: "{:.3f}".format(x)
df1.applymap(fmt)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.051</td>
      <td>1.435</td>
      <td>1.040</td>
      <td>-1.387</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.696</td>
      <td>0.657</td>
      <td>-0.220</td>
      <td>-0.439</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-2.135</td>
      <td>-0.770</td>
      <td>-1.062</td>
      <td>0.341</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.012</td>
      <td>-1.187</td>
      <td>1.259</td>
      <td>1.273</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.223</td>
      <td>-1.157</td>
      <td>0.129</td>
      <td>1.228</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-1.903</td>
      <td>0.863</td>
      <td>-1.726</td>
      <td>-0.219</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-1.162</td>
      <td>-0.006</td>
      <td>1.171</td>
      <td>-0.406</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-1.675</td>
      <td>0.448</td>
      <td>-0.217</td>
      <td>-0.194</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-0.657</td>
      <td>1.473</td>
      <td>-0.263</td>
      <td>-3.446</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1.013</td>
      <td>-0.366</td>
      <td>-0.715</td>
      <td>0.378</td>
    </tr>
  </tbody>
</table>
</div>



The reason for the name `applymap` for dataframe (instead of simply using `map`)is that pandas Series already has a `map` method for applying an element-wise operation
