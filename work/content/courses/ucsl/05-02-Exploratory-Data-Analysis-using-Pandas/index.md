[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/05-02%20Exploratory%20Data%20Analysis%20using%20Pandas.ipynb) 

> Click above image to access the interactive version of this notebook


## 05 - 02 Exploratory Data Analysis using Pandas
Based on the concepts that we have built in the last couple of modules, we will explore the imdb dataset but before we do that, let's first look at ways of loading the datasets as pandas dataframe.

### Loading Data
You can read data from a CSV file using the read_csv function. By default, it assumes that the fields are comma-separated.
Pandas supports following file formats:

|Function| Description|
|:---|:---|
|read_csv | Load delimited data from a file, URL, or file-like object. Use comma as default delimiter|
|read_table | Load delimited data from a file, URL, or file-like object. Use tab ('\t') as default delimiter|
|read_fwf | Read data in fixed-width column format (that is, no delimiters)|
|read_clipboard | Version of read_table that reads data from the clipboard. Useful for converting tables from web pages.|

For most of the analysis work, you will be loading the csv, tsv or some delimited files. We will only look at `read_csv` function in this example.

First, let's import the dataset:



```python
import pandas as pd
import numpy as np
%matplotlib inline
import matplotlib.pyplot as plt
plt.style.use('seaborn-darkgrid')
```

Lets load the cast, release-dates and titles dataset. This might take sometime.


```python
%%time
cast = pd.read_csv('./sample_datasets/cast.csv', index_col=None)
release_dates = pd.read_csv('./sample_datasets/release_dates.csv', index_col=None,
                            parse_dates=['date'], infer_datetime_format=True)
titles = pd.read_csv('./sample_datasets/titles.csv', index_col=None)
```

    CPU times: user 4.75 s, sys: 398 ms, total: 5.14 s
    Wall time: 5.16 s


Lets look at some of the contents of these dataframes


```python
cast.head()
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
      <th>title</th>
      <th>year</th>
      <th>name</th>
      <th>type</th>
      <th>character</th>
      <th>n</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Closet Monster</td>
      <td>2015</td>
      <td>Buffy #1</td>
      <td>actor</td>
      <td>Buffy 4</td>
      <td>31.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Suuri illusioni</td>
      <td>1985</td>
      <td>Homo $</td>
      <td>actor</td>
      <td>Guests</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Battle of the Sexes</td>
      <td>2017</td>
      <td>$hutter</td>
      <td>actor</td>
      <td>Bobby Riggs Fan</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Secret in Their Eyes</td>
      <td>2015</td>
      <td>$hutter</td>
      <td>actor</td>
      <td>2002 Dodger Fan</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Steve Jobs</td>
      <td>2015</td>
      <td>$hutter</td>
      <td>actor</td>
      <td>1988 Opera House Patron</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



> The `n` in the cast dataframe tells us the rank or the order of the leading roles.


```python
release_dates.head()
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
      <th>title</th>
      <th>year</th>
      <th>country</th>
      <th>date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>#73, Shaanthi Nivaasa</td>
      <td>2007</td>
      <td>India</td>
      <td>2007-06-15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>#BKKY</td>
      <td>2016</td>
      <td>Cambodia</td>
      <td>2017-10-12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>#Beings</td>
      <td>2015</td>
      <td>Romania</td>
      <td>2015-01-29</td>
    </tr>
    <tr>
      <th>3</th>
      <td>#Captured</td>
      <td>2017</td>
      <td>USA</td>
      <td>2017-09-05</td>
    </tr>
    <tr>
      <th>4</th>
      <td>#Ewankosau saranghaeyo</td>
      <td>2015</td>
      <td>Philippines</td>
      <td>2015-01-21</td>
    </tr>
  </tbody>
</table>
</div>




```python
titles.head()
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
      <th>title</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Gypsy 83</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Challenge of Five Gauntlets</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Haunting Shadows</td>
      <td>1919</td>
    </tr>
    <tr>
      <th>3</th>
      <td>The Cake Eaters</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>4</th>
      <td>B Qu 32 Hao</td>
      <td>2011</td>
    </tr>
  </tbody>
</table>
</div>



Do you know how many movies released since you were born?


```python
my_birth_year = 1990
len(titles[(titles['year']>my_birth_year) & (titles['year']<2017)])
```




    115183



Lets plot how many movies released every year since you were born


```python
titles.groupby('year').size().loc[my_birth_year:2016].plot(title="Number of movies released every year")
```




    <AxesSubplot:title={'center':'Number of movies released every year'}, xlabel='year'>




    
![png](./05-02%20Exploratory%20Data%20Analysis%20using%20Pandas_12_1.png)
    


Pandas provides matplotlib based plotting as a part of dataframe. To plot any dataframe (with *plottable data*) you can simply use `.plot()`.

Ofcourse we can also do this manually using matplotlib's pyplot as well (which is actually what pandas uses under the cover)


```python
fig, ax = plt.subplots()
ax.plot(titles.groupby('year').size().loc[my_birth_year:2016])
ax.set_xlabel("Year")
ax.set_ylabel("# of Movies")
ax.set_title("Number of movies released every year")
ax.set_xlim(1990, 2016)
```




    (1990.0, 2016.0)




    
![png](./05-02%20Exploratory%20Data%20Analysis%20using%20Pandas_14_1.png)
    


Hmm.. How about the total number of movies released every decade?

This will involve a little math. We know that the `titles` dataframe has a `year` column which, obviously, has the year when a movie was released.

To count the occurence of something, we can use the `value_counts` method. 

So now, all we need to do is pass the *decade* as key to the `titles` dataframe and apply the `value_counts` method. 

Let's see how to do this


```python
(titles['year'] // 10 * 10).value_counts().sort_index().plot(kind='bar')
```




    <AxesSubplot:>




    
![png](./05-02%20Exploratory%20Data%20Analysis%20using%20Pandas_16_1.png)
    


How many movies did a *movie star* star in?


```python
movie_star = "Matt Damon"
len(cast[cast['name'] == movie_star])
```




    62



What are the 10 most common name of the roles played by characters?


```python
cast['character'].value_counts().head(10)
```




    Himself        20746
    Dancer         12477
    Extra          11948
    Reporter        8434
    Student         7773
    Doctor          7669
    Party Guest     7245
    Policeman       7029
    Nurse           6999
    Bartender       6802
    Name: character, dtype: int64



What are the 10 most common movie names?


```python
titles['title'].value_counts().head(10)
```




    Hamlet                  20
    Carmen                  17
    Macbeth                 16
    Maya                    12
    Temptation              12
    The Outsider            12
    The Three Musketeers    11
    Othello                 11
    Honeymoon               11
    Freedom                 11
    Name: title, dtype: int64



Similarly, you can find who has been the most in the movies


```python
cast['name'].value_counts().head(10)
```




    Bess Flowers       835
    Herman Hack        702
    Sam (II) Harris    667
    Harold Miller      624
    Lee Phelps         624
    Frank O'Connor     613
    Franklyn Farnum    570
    Tom London         565
    Larry Steers       559
    Frank Ellis        546
    Name: name, dtype: int64



Lets find the years when *The Bourne* series were released.


```python
titles[titles['title'].str.contains("Bourne")].sort_values('year')
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
      <th>title</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>169218</th>
      <td>The Bourne Identity</td>
      <td>2002</td>
    </tr>
    <tr>
      <th>244703</th>
      <td>The Bourne Supremacy</td>
      <td>2004</td>
    </tr>
    <tr>
      <th>74839</th>
      <td>The Bourne Ultimatum</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>197575</th>
      <td>The Mel Bourne Ultimatum</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>106112</th>
      <td>The Bourne Legacy</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>4707</th>
      <td>Jason Bourne</td>
      <td>2016</td>
    </tr>
  </tbody>
</table>
</div>



Lets find the movies when *Matt Damon* was *Jason Bourne*


```python
matt_jbourne = cast[(cast['title'].str.contains("Bourne")) & 
                    (cast['name'].str.contains("Matt Damon"))]
matt_jbourne
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
      <th>title</th>
      <th>year</th>
      <th>name</th>
      <th>type</th>
      <th>character</th>
      <th>n</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>522755</th>
      <td>Jason Bourne</td>
      <td>2016</td>
      <td>Matt Damon</td>
      <td>actor</td>
      <td>Jason Bourne</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>522774</th>
      <td>The Bourne Identity</td>
      <td>2002</td>
      <td>Matt Damon</td>
      <td>actor</td>
      <td>Bourne</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>522775</th>
      <td>The Bourne Supremacy</td>
      <td>2004</td>
      <td>Matt Damon</td>
      <td>actor</td>
      <td>Jason Bourne</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>522776</th>
      <td>The Bourne Ultimatum</td>
      <td>2007</td>
      <td>Matt Damon</td>
      <td>actor</td>
      <td>Jason Bourne</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



So, How many movies do you think is released every year starring Matt Damon?


```python
fig, ax = plt.subplots()
ax.plot(cast[cast['name'] == "Matt Damon"].groupby('year').size())
ax.set_xlabel("Year")
ax.set_ylabel("# of Movies")
ax.set_title("Matt Damon movies")
```




    Text(0.5, 1.0, 'Matt Damon movies')




    
![png](./05-02%20Exploratory%20Data%20Analysis%20using%20Pandas_30_1.png)
    


And how about the ranks at which *Matt Damon* stars in the movies?


```python
matt_movies = cast[cast.name == 'Matt Damon'].sort_values('year')
matt_movies = matt_movies[matt_movies['n'].notnull()]
# For scatter plots, you can simply pass the column
# names for the x and y argument
matt_movies.plot(x='year', y='n', kind='scatter')
```




    <AxesSubplot:xlabel='year', ylabel='n'>




    
![png](./05-02%20Exploratory%20Data%20Analysis%20using%20Pandas_32_1.png)
    


So how many leading roles?


```python
matt_movies = cast[cast.name == 'Matt Damon'].sort_values('year')
matt_movies[matt_movies['n'] == 1]['n'].value_counts()
```




    1.0    21
    Name: n, dtype: int64



Lets see how many people were casted in all these *Jason Bourne* movies


```python
%%time
cast[(cast['title'].str.contains("Bourne"))].groupby(['year', 'title']).size()
```

    CPU times: user 1.31 s, sys: 7.41 ms, total: 1.31 s
    Wall time: 1.32 s





    year  title                   
    2002  The Bourne Identity          56
    2004  The Bourne Supremacy         49
    2007  The Bourne Ultimatum         70
    2009  The Mel Bourne Ultimatum      8
    2012  The Bourne Legacy           122
    2016  Jason Bourne                259
    dtype: int64



Among these casts, how many were actors and actresses?


```python
%%time 
cast[(cast['title'].str.contains("Bourne"))].groupby(['year', 'title', 'type']).size()
```

    CPU times: user 1.34 s, sys: 8.34 ms, total: 1.35 s
    Wall time: 1.36 s





    year  title                     type   
    2002  The Bourne Identity       actor       50
                                    actress      6
    2004  The Bourne Supremacy      actor       38
                                    actress     11
    2007  The Bourne Ultimatum      actor       59
                                    actress     11
    2009  The Mel Bourne Ultimatum  actor        5
                                    actress      3
    2012  The Bourne Legacy         actor       86
                                    actress     36
    2016  Jason Bourne              actor      189
                                    actress     70
    dtype: int64



Lets plot the above and see the total number of roles based on gender


```python
jason_cast = cast[(cast['title'].str.contains("Bourne"))]
jason_cast_gender = jason_cast[['year', 'type']].groupby(['year', 'type']).size().unstack()
print(jason_cast_gender)
jason_cast_gender.plot()
```

    type  actor  actress
    year                
    2002     50        6
    2004     38       11
    2007     59       11
    2009      5        3
    2012     86       36
    2016    189       70





    <AxesSubplot:xlabel='year'>




    
![png](./05-02%20Exploratory%20Data%20Analysis%20using%20Pandas_40_2.png)
    


Lets find out the entire cast of the *The Bourne Ultimatum* and print just the top 10 leads


```python
cast[cast['title'] == "The Bourne Ultimatum"].sort_values(['n']).head(10)
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
      <th>title</th>
      <th>year</th>
      <th>name</th>
      <th>type</th>
      <th>character</th>
      <th>n</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>522776</th>
      <td>The Bourne Ultimatum</td>
      <td>2007</td>
      <td>Matt Damon</td>
      <td>actor</td>
      <td>Jason Bourne</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>3613634</th>
      <td>The Bourne Ultimatum</td>
      <td>2007</td>
      <td>Julia Stiles</td>
      <td>actress</td>
      <td>Nicky Parsons</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2195770</th>
      <td>The Bourne Ultimatum</td>
      <td>2007</td>
      <td>David Strathairn</td>
      <td>actor</td>
      <td>Noah Vosen</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>840581</th>
      <td>The Bourne Ultimatum</td>
      <td>2007</td>
      <td>Scott Glenn</td>
      <td>actor</td>
      <td>Ezra Kramer</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>459423</th>
      <td>The Bourne Ultimatum</td>
      <td>2007</td>
      <td>Paddy Considine</td>
      <td>actor</td>
      <td>Simon Ross</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1872404</th>
      <td>The Bourne Ultimatum</td>
      <td>2007</td>
      <td>Edgar (IV) Ram?rez</td>
      <td>actor</td>
      <td>Paz</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>728791</th>
      <td>The Bourne Ultimatum</td>
      <td>2007</td>
      <td>Albert Finney</td>
      <td>actor</td>
      <td>Dr. Albert Hirsch</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>2552022</th>
      <td>The Bourne Ultimatum</td>
      <td>2007</td>
      <td>Joan Allen</td>
      <td>actress</td>
      <td>Pam Landy</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>790556</th>
      <td>The Bourne Ultimatum</td>
      <td>2007</td>
      <td>Tom Gallop</td>
      <td>actor</td>
      <td>Tom Cronin</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>1112789</th>
      <td>The Bourne Ultimatum</td>
      <td>2007</td>
      <td>Corey Johnson</td>
      <td>actor</td>
      <td>Wills</td>
      <td>10.0</td>
    </tr>
  </tbody>
</table>
</div>



Lets see in what months Matt Damon's movies are most often released in the USA.

- First, find the year and the title of unique movies starring Matt Damon were released


```python
matt_movies = cast[cast['name'] == "Matt Damon"][['title', 'year']].drop_duplicates()
```

Now we have to re-index the `release_dates` dataframe with `title` and `year` keys


```python
rel_dts = release_dates.set_index(['title', 'year']).sort_index()
```

- Now, the 'month' part is present in `date` column present in `release_dates` dataframe so we have to combine the `cast` and `release_dates` dataframes for Matt Damon's movies by some common index (in our case, we will use the common index as `title` and `year` since it is present in both the dataframes)


```python
matt_movie_releases = matt_movies.join(rel_dts, on=['title', 'year'])
```

- We only want movies released in the USA


```python
matt_movie_releases = matt_movie_releases[matt_movie_releases['country'] == "USA"]
```

- Now lets plot the `month` part.


```python
matt_movie_releases['date'].dt.month.value_counts().sort_index().plot(kind='bar')
```




    <AxesSubplot:>




    
![png](./05-02%20Exploratory%20Data%20Analysis%20using%20Pandas_52_1.png)
    


Cool, Now lets see when the Bourne movie series were released in different countries.
> Since there are is a huge list of countries, lets just select "USA", "UK" and "India"


```python
countries = ["USA", "UK", "Australia"]
matt_movie_releases = matt_movies.join(rel_dts, on=['title', 'year'])
matt_movie_countries = matt_movie_releases[matt_movie_releases['country'].str.contains('|'.join(countries))]
matt_movie_countries.set_index(['title', 'country'])[['date']].unstack()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">date</th>
    </tr>
    <tr>
      <th>country</th>
      <th>Australia</th>
      <th>UK</th>
      <th>USA</th>
    </tr>
    <tr>
      <th>title</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>All the Pretty Horses</th>
      <td>2001-05-10</td>
      <td>2001-05-25</td>
      <td>2000-12-25</td>
    </tr>
    <tr>
      <th>Chasing Amy</th>
      <td>1997-07-03</td>
      <td>1997-11-14</td>
      <td>1997-04-18</td>
    </tr>
    <tr>
      <th>Che: Part Two</th>
      <td>2009-10-01</td>
      <td>2009-02-20</td>
      <td>2009-01-24</td>
    </tr>
    <tr>
      <th>Confessions of a Dangerous Mind</th>
      <td>2003-07-24</td>
      <td>2003-03-14</td>
      <td>2003-01-24</td>
    </tr>
    <tr>
      <th>Contagion</th>
      <td>2011-10-20</td>
      <td>2011-10-21</td>
      <td>2011-09-09</td>
    </tr>
    <tr>
      <th>Courage Under Fire</th>
      <td>1996-09-12</td>
      <td>1996-10-04</td>
      <td>1996-07-12</td>
    </tr>
    <tr>
      <th>Dogma</th>
      <td>2000-02-03</td>
      <td>1999-12-26</td>
      <td>1999-11-12</td>
    </tr>
    <tr>
      <th>Downsizing</th>
      <td>2017-12-26</td>
      <td>2018-01-24</td>
      <td>2017-12-22</td>
    </tr>
    <tr>
      <th>Elysium</th>
      <td>2013-08-15</td>
      <td>2013-08-21</td>
      <td>2013-08-09</td>
    </tr>
    <tr>
      <th>EuroTrip</th>
      <td>2004-08-12</td>
      <td>2004-06-25</td>
      <td>2004-02-20</td>
    </tr>
    <tr>
      <th>Field of Dreams</th>
      <td>1989-08-31</td>
      <td>1989-11-24</td>
      <td>1989-05-05</td>
    </tr>
    <tr>
      <th>Finding Forrester</th>
      <td>2001-03-29</td>
      <td>2001-02-23</td>
      <td>2001-01-12</td>
    </tr>
    <tr>
      <th>Gake no ue no Ponyo</th>
      <td>2009-08-27</td>
      <td>2010-02-12</td>
      <td>2009-08-14</td>
    </tr>
    <tr>
      <th>Geronimo: An American Legend</th>
      <td>1994-05-26</td>
      <td>1994-10-14</td>
      <td>1993-12-10</td>
    </tr>
    <tr>
      <th>Gerry</th>
      <td>NaT</td>
      <td>2003-08-22</td>
      <td>NaT</td>
    </tr>
    <tr>
      <th>Glory Daze</th>
      <td>NaT</td>
      <td>NaT</td>
      <td>1996-09-27</td>
    </tr>
    <tr>
      <th>Good Will Hunting</th>
      <td>1998-03-12</td>
      <td>1998-03-06</td>
      <td>1998-01-09</td>
    </tr>
    <tr>
      <th>Green Zone</th>
      <td>2010-03-11</td>
      <td>2010-03-12</td>
      <td>2010-03-12</td>
    </tr>
    <tr>
      <th>Happy Feet Two</th>
      <td>2011-12-26</td>
      <td>2011-12-02</td>
      <td>2011-11-18</td>
    </tr>
    <tr>
      <th>Hereafter</th>
      <td>NaT</td>
      <td>2011-01-28</td>
      <td>2010-10-22</td>
    </tr>
    <tr>
      <th>Interstellar</th>
      <td>2014-11-06</td>
      <td>2014-11-07</td>
      <td>2014-11-07</td>
    </tr>
    <tr>
      <th>Invictus</th>
      <td>2010-01-21</td>
      <td>2010-02-05</td>
      <td>2009-12-11</td>
    </tr>
    <tr>
      <th>Jason Bourne</th>
      <td>2016-07-28</td>
      <td>2016-07-27</td>
      <td>2016-07-29</td>
    </tr>
    <tr>
      <th>Jay and Silent Bob Strike Back</th>
      <td>2002-01-31</td>
      <td>2001-11-30</td>
      <td>2001-08-24</td>
    </tr>
    <tr>
      <th>Jersey Girl</th>
      <td>2004-08-12</td>
      <td>2004-06-18</td>
      <td>2004-03-26</td>
    </tr>
    <tr>
      <th>Margaret</th>
      <td>2012-06-14</td>
      <td>NaT</td>
      <td>NaT</td>
    </tr>
    <tr>
      <th>Mystic Pizza</th>
      <td>1989-08-03</td>
      <td>1990-01-05</td>
      <td>1988-10-21</td>
    </tr>
    <tr>
      <th>Ocean's Eleven</th>
      <td>2002-01-10</td>
      <td>2002-02-15</td>
      <td>2001-12-07</td>
    </tr>
    <tr>
      <th>Ocean's Thirteen</th>
      <td>2007-06-14</td>
      <td>2007-06-08</td>
      <td>2007-06-08</td>
    </tr>
    <tr>
      <th>Ocean's Twelve</th>
      <td>2004-12-09</td>
      <td>2005-02-04</td>
      <td>2004-12-10</td>
    </tr>
    <tr>
      <th>Promised Land</th>
      <td>2013-05-02</td>
      <td>2013-04-19</td>
      <td>2013-01-04</td>
    </tr>
    <tr>
      <th>Rounders</th>
      <td>1999-01-28</td>
      <td>1998-11-20</td>
      <td>1998-09-11</td>
    </tr>
    <tr>
      <th>Saving Private Ryan</th>
      <td>1998-11-19</td>
      <td>1998-09-11</td>
      <td>1998-07-24</td>
    </tr>
    <tr>
      <th>School Ties</th>
      <td>1993-06-10</td>
      <td>NaT</td>
      <td>1992-09-18</td>
    </tr>
    <tr>
      <th>Spirit: Stallion of the Cimarron</th>
      <td>2002-06-20</td>
      <td>2002-07-05</td>
      <td>2002-05-24</td>
    </tr>
    <tr>
      <th>Stuck on You</th>
      <td>2004-02-12</td>
      <td>2004-01-02</td>
      <td>2003-12-12</td>
    </tr>
    <tr>
      <th>Suburbicon</th>
      <td>2017-10-26</td>
      <td>2017-11-24</td>
      <td>2017-10-27</td>
    </tr>
    <tr>
      <th>Syriana</th>
      <td>2006-02-16</td>
      <td>2006-03-03</td>
      <td>2005-12-09</td>
    </tr>
    <tr>
      <th>The Adjustment Bureau</th>
      <td>NaT</td>
      <td>2011-03-04</td>
      <td>2011-03-04</td>
    </tr>
    <tr>
      <th>The Bourne Identity</th>
      <td>2002-08-22</td>
      <td>2002-09-06</td>
      <td>2002-06-14</td>
    </tr>
    <tr>
      <th>The Bourne Supremacy</th>
      <td>2004-08-26</td>
      <td>2004-08-13</td>
      <td>2004-07-23</td>
    </tr>
    <tr>
      <th>The Bourne Ultimatum</th>
      <td>2007-08-30</td>
      <td>2007-08-17</td>
      <td>2007-08-03</td>
    </tr>
    <tr>
      <th>The Brothers Grimm</th>
      <td>2005-11-24</td>
      <td>2005-11-04</td>
      <td>2005-08-26</td>
    </tr>
    <tr>
      <th>The Departed</th>
      <td>2006-10-12</td>
      <td>2006-10-06</td>
      <td>2006-10-06</td>
    </tr>
    <tr>
      <th>The Good Mother</th>
      <td>1989-05-04</td>
      <td>1989-02-17</td>
      <td>1988-11-04</td>
    </tr>
    <tr>
      <th>The Good Shepherd</th>
      <td>2007-02-15</td>
      <td>2007-02-23</td>
      <td>2006-12-22</td>
    </tr>
    <tr>
      <th>The Great Wall</th>
      <td>2017-02-16</td>
      <td>2017-02-17</td>
      <td>2017-02-17</td>
    </tr>
    <tr>
      <th>The Informant!</th>
      <td>2009-12-03</td>
      <td>2009-11-20</td>
      <td>2009-09-18</td>
    </tr>
    <tr>
      <th>The Legend of Bagger Vance</th>
      <td>2001-02-08</td>
      <td>2001-02-23</td>
      <td>2000-11-03</td>
    </tr>
    <tr>
      <th>The Majestic</th>
      <td>2002-05-16</td>
      <td>2002-05-24</td>
      <td>2001-12-21</td>
    </tr>
    <tr>
      <th>The Martian</th>
      <td>2015-09-30</td>
      <td>2015-09-30</td>
      <td>2015-10-02</td>
    </tr>
    <tr>
      <th>The Monuments Men</th>
      <td>2014-03-13</td>
      <td>2014-02-14</td>
      <td>2014-02-07</td>
    </tr>
    <tr>
      <th>The Rainmaker</th>
      <td>1998-01-22</td>
      <td>1998-04-03</td>
      <td>1997-11-21</td>
    </tr>
    <tr>
      <th>The Talented Mr. Ripley</th>
      <td>2000-02-24</td>
      <td>2000-02-25</td>
      <td>1999-12-25</td>
    </tr>
    <tr>
      <th>The Zero Theorem</th>
      <td>2014-05-15</td>
      <td>2014-03-14</td>
      <td>NaT</td>
    </tr>
    <tr>
      <th>Titan A.E.</th>
      <td>2001-01-04</td>
      <td>2000-07-28</td>
      <td>2000-06-16</td>
    </tr>
    <tr>
      <th>True Grit</th>
      <td>2011-01-26</td>
      <td>2011-02-11</td>
      <td>2010-12-22</td>
    </tr>
    <tr>
      <th>We Bought a Zoo</th>
      <td>2011-12-26</td>
      <td>2012-03-16</td>
      <td>2011-12-23</td>
    </tr>
    <tr>
      <th>Youth Without Youth</th>
      <td>2008-11-20</td>
      <td>2007-12-14</td>
      <td>NaT</td>
    </tr>
  </tbody>
</table>
</div>



> To match the `country` column against all the elements of the list, we use the `|` (OR) operator. It is considered as a Regular Expression.

We can also create a `Pivot` table to provide the above output.
> - The pivot table takes simple column-wise data as input, and groups the entries into a two-dimensional table that provides a multidimensional summarization of the data.
> - Think of it as a multi-dimensional GroupBy function


```python
countries = ["USA", "UK", "Australia"]
matt_movie_releases = matt_movies.join(rel_dts, on=['title', 'year'])
matt_movie_countries = matt_movie_releases[matt_movie_releases['country'].str.contains('|'.join(countries))]
matt_movie_countries.pivot(index='title', columns='country', values='date')
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
      <th>country</th>
      <th>Australia</th>
      <th>UK</th>
      <th>USA</th>
    </tr>
    <tr>
      <th>title</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>All the Pretty Horses</th>
      <td>2001-05-10</td>
      <td>2001-05-25</td>
      <td>2000-12-25</td>
    </tr>
    <tr>
      <th>Chasing Amy</th>
      <td>1997-07-03</td>
      <td>1997-11-14</td>
      <td>1997-04-18</td>
    </tr>
    <tr>
      <th>Che: Part Two</th>
      <td>2009-10-01</td>
      <td>2009-02-20</td>
      <td>2009-01-24</td>
    </tr>
    <tr>
      <th>Confessions of a Dangerous Mind</th>
      <td>2003-07-24</td>
      <td>2003-03-14</td>
      <td>2003-01-24</td>
    </tr>
    <tr>
      <th>Contagion</th>
      <td>2011-10-20</td>
      <td>2011-10-21</td>
      <td>2011-09-09</td>
    </tr>
    <tr>
      <th>Courage Under Fire</th>
      <td>1996-09-12</td>
      <td>1996-10-04</td>
      <td>1996-07-12</td>
    </tr>
    <tr>
      <th>Dogma</th>
      <td>2000-02-03</td>
      <td>1999-12-26</td>
      <td>1999-11-12</td>
    </tr>
    <tr>
      <th>Downsizing</th>
      <td>2017-12-26</td>
      <td>2018-01-24</td>
      <td>2017-12-22</td>
    </tr>
    <tr>
      <th>Elysium</th>
      <td>2013-08-15</td>
      <td>2013-08-21</td>
      <td>2013-08-09</td>
    </tr>
    <tr>
      <th>EuroTrip</th>
      <td>2004-08-12</td>
      <td>2004-06-25</td>
      <td>2004-02-20</td>
    </tr>
    <tr>
      <th>Field of Dreams</th>
      <td>1989-08-31</td>
      <td>1989-11-24</td>
      <td>1989-05-05</td>
    </tr>
    <tr>
      <th>Finding Forrester</th>
      <td>2001-03-29</td>
      <td>2001-02-23</td>
      <td>2001-01-12</td>
    </tr>
    <tr>
      <th>Gake no ue no Ponyo</th>
      <td>2009-08-27</td>
      <td>2010-02-12</td>
      <td>2009-08-14</td>
    </tr>
    <tr>
      <th>Geronimo: An American Legend</th>
      <td>1994-05-26</td>
      <td>1994-10-14</td>
      <td>1993-12-10</td>
    </tr>
    <tr>
      <th>Gerry</th>
      <td>NaT</td>
      <td>2003-08-22</td>
      <td>NaT</td>
    </tr>
    <tr>
      <th>Glory Daze</th>
      <td>NaT</td>
      <td>NaT</td>
      <td>1996-09-27</td>
    </tr>
    <tr>
      <th>Good Will Hunting</th>
      <td>1998-03-12</td>
      <td>1998-03-06</td>
      <td>1998-01-09</td>
    </tr>
    <tr>
      <th>Green Zone</th>
      <td>2010-03-11</td>
      <td>2010-03-12</td>
      <td>2010-03-12</td>
    </tr>
    <tr>
      <th>Happy Feet Two</th>
      <td>2011-12-26</td>
      <td>2011-12-02</td>
      <td>2011-11-18</td>
    </tr>
    <tr>
      <th>Hereafter</th>
      <td>NaT</td>
      <td>2011-01-28</td>
      <td>2010-10-22</td>
    </tr>
    <tr>
      <th>Interstellar</th>
      <td>2014-11-06</td>
      <td>2014-11-07</td>
      <td>2014-11-07</td>
    </tr>
    <tr>
      <th>Invictus</th>
      <td>2010-01-21</td>
      <td>2010-02-05</td>
      <td>2009-12-11</td>
    </tr>
    <tr>
      <th>Jason Bourne</th>
      <td>2016-07-28</td>
      <td>2016-07-27</td>
      <td>2016-07-29</td>
    </tr>
    <tr>
      <th>Jay and Silent Bob Strike Back</th>
      <td>2002-01-31</td>
      <td>2001-11-30</td>
      <td>2001-08-24</td>
    </tr>
    <tr>
      <th>Jersey Girl</th>
      <td>2004-08-12</td>
      <td>2004-06-18</td>
      <td>2004-03-26</td>
    </tr>
    <tr>
      <th>Margaret</th>
      <td>2012-06-14</td>
      <td>NaT</td>
      <td>NaT</td>
    </tr>
    <tr>
      <th>Mystic Pizza</th>
      <td>1989-08-03</td>
      <td>1990-01-05</td>
      <td>1988-10-21</td>
    </tr>
    <tr>
      <th>Ocean's Eleven</th>
      <td>2002-01-10</td>
      <td>2002-02-15</td>
      <td>2001-12-07</td>
    </tr>
    <tr>
      <th>Ocean's Thirteen</th>
      <td>2007-06-14</td>
      <td>2007-06-08</td>
      <td>2007-06-08</td>
    </tr>
    <tr>
      <th>Ocean's Twelve</th>
      <td>2004-12-09</td>
      <td>2005-02-04</td>
      <td>2004-12-10</td>
    </tr>
    <tr>
      <th>Promised Land</th>
      <td>2013-05-02</td>
      <td>2013-04-19</td>
      <td>2013-01-04</td>
    </tr>
    <tr>
      <th>Rounders</th>
      <td>1999-01-28</td>
      <td>1998-11-20</td>
      <td>1998-09-11</td>
    </tr>
    <tr>
      <th>Saving Private Ryan</th>
      <td>1998-11-19</td>
      <td>1998-09-11</td>
      <td>1998-07-24</td>
    </tr>
    <tr>
      <th>School Ties</th>
      <td>1993-06-10</td>
      <td>NaT</td>
      <td>1992-09-18</td>
    </tr>
    <tr>
      <th>Spirit: Stallion of the Cimarron</th>
      <td>2002-06-20</td>
      <td>2002-07-05</td>
      <td>2002-05-24</td>
    </tr>
    <tr>
      <th>Stuck on You</th>
      <td>2004-02-12</td>
      <td>2004-01-02</td>
      <td>2003-12-12</td>
    </tr>
    <tr>
      <th>Suburbicon</th>
      <td>2017-10-26</td>
      <td>2017-11-24</td>
      <td>2017-10-27</td>
    </tr>
    <tr>
      <th>Syriana</th>
      <td>2006-02-16</td>
      <td>2006-03-03</td>
      <td>2005-12-09</td>
    </tr>
    <tr>
      <th>The Adjustment Bureau</th>
      <td>NaT</td>
      <td>2011-03-04</td>
      <td>2011-03-04</td>
    </tr>
    <tr>
      <th>The Bourne Identity</th>
      <td>2002-08-22</td>
      <td>2002-09-06</td>
      <td>2002-06-14</td>
    </tr>
    <tr>
      <th>The Bourne Supremacy</th>
      <td>2004-08-26</td>
      <td>2004-08-13</td>
      <td>2004-07-23</td>
    </tr>
    <tr>
      <th>The Bourne Ultimatum</th>
      <td>2007-08-30</td>
      <td>2007-08-17</td>
      <td>2007-08-03</td>
    </tr>
    <tr>
      <th>The Brothers Grimm</th>
      <td>2005-11-24</td>
      <td>2005-11-04</td>
      <td>2005-08-26</td>
    </tr>
    <tr>
      <th>The Departed</th>
      <td>2006-10-12</td>
      <td>2006-10-06</td>
      <td>2006-10-06</td>
    </tr>
    <tr>
      <th>The Good Mother</th>
      <td>1989-05-04</td>
      <td>1989-02-17</td>
      <td>1988-11-04</td>
    </tr>
    <tr>
      <th>The Good Shepherd</th>
      <td>2007-02-15</td>
      <td>2007-02-23</td>
      <td>2006-12-22</td>
    </tr>
    <tr>
      <th>The Great Wall</th>
      <td>2017-02-16</td>
      <td>2017-02-17</td>
      <td>2017-02-17</td>
    </tr>
    <tr>
      <th>The Informant!</th>
      <td>2009-12-03</td>
      <td>2009-11-20</td>
      <td>2009-09-18</td>
    </tr>
    <tr>
      <th>The Legend of Bagger Vance</th>
      <td>2001-02-08</td>
      <td>2001-02-23</td>
      <td>2000-11-03</td>
    </tr>
    <tr>
      <th>The Majestic</th>
      <td>2002-05-16</td>
      <td>2002-05-24</td>
      <td>2001-12-21</td>
    </tr>
    <tr>
      <th>The Martian</th>
      <td>2015-09-30</td>
      <td>2015-09-30</td>
      <td>2015-10-02</td>
    </tr>
    <tr>
      <th>The Monuments Men</th>
      <td>2014-03-13</td>
      <td>2014-02-14</td>
      <td>2014-02-07</td>
    </tr>
    <tr>
      <th>The Rainmaker</th>
      <td>1998-01-22</td>
      <td>1998-04-03</td>
      <td>1997-11-21</td>
    </tr>
    <tr>
      <th>The Talented Mr. Ripley</th>
      <td>2000-02-24</td>
      <td>2000-02-25</td>
      <td>1999-12-25</td>
    </tr>
    <tr>
      <th>The Zero Theorem</th>
      <td>2014-05-15</td>
      <td>2014-03-14</td>
      <td>NaT</td>
    </tr>
    <tr>
      <th>Titan A.E.</th>
      <td>2001-01-04</td>
      <td>2000-07-28</td>
      <td>2000-06-16</td>
    </tr>
    <tr>
      <th>True Grit</th>
      <td>2011-01-26</td>
      <td>2011-02-11</td>
      <td>2010-12-22</td>
    </tr>
    <tr>
      <th>We Bought a Zoo</th>
      <td>2011-12-26</td>
      <td>2012-03-16</td>
      <td>2011-12-23</td>
    </tr>
    <tr>
      <th>Youth Without Youth</th>
      <td>2008-11-20</td>
      <td>2007-12-14</td>
      <td>NaT</td>
    </tr>
  </tbody>
</table>
</div>



Do you know when are the most *Action* movies released in the USA?


```python
action_usa = release_dates[(release_dates['title'].str.contains('Action')) & 
                           (release_dates['country'] == "USA")]
action_usa['date'].dt.dayofweek.value_counts().sort_index().plot(kind='bar')
```




    <AxesSubplot:>




    
![png](./05-02%20Exploratory%20Data%20Analysis%20using%20Pandas_58_1.png)
    


In which months are *Matt Damon*'s movies generally released in the USA?


```python
matt_movies = cast[cast['name'] == 'Matt Damon']
matt_movies_usa = matt_movies.merge(release_dates[release_dates.country == 'USA']).sort_values('date')
matt_movies_usa.date.dt.month.value_counts().sort_index().plot(kind='bar')
```




    <AxesSubplot:>




    
![png](./05-02%20Exploratory%20Data%20Analysis%20using%20Pandas_60_1.png)
    


The above examples should give you some idea about the importance of Pandas and how its high level functions mask the complex computation that is performed on the underlying Numpy arrays.

This is by no means an exhaustive list of all the functions. We have barely scratched the surface. 

> Remember --
> ### The only way to become a master of something is to be really With It! 
So keep practicing and whenever you are stuck:
- Go through the official documentation.
- Enter the object name and Press `<TAB>` or `.?` and Jupyter will show you the docstring.
- Don't trust the examples blindly. Run them, modify them, make mistakes and then rectify them.
- Don't simply copy the StackOverflow or StackExchange or answers from anywhere else. Understand the solution that you find on such sites and then and only then use it in your code.

>If you want more tutorials/ cookbooks, take a look at 

> - [`Pandas own 10 minute to Pandas`](http://pandas.pydata.org/pandas-docs/stable/10min.html#min '10 minutes to pandas')

> - [`Hernan Rojas's Learn Pandas`](https://bitbucket.org/hrojas/learn-pandas 'hrojas's Learn Pandas')

> - [`Pandas Cookbook`](http://pandas.pydata.org/pandas-docs/stable/cookbook.html#cookbook 'Pandas Cookbook')

> - [`Greg Reda's Blog`](http://www.gregreda.com/2013/10/26/intro-to-pandas-data-structures/ 'Greg Redas blog on Pandas')

