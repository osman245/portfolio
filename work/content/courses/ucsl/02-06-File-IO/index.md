[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/02-06%20File%20IO.ipynb) 

> Click above image to access the interactive version of this notebook


## File I/O
Before we jump in to file I/O functions, lets first look at some basic I/O functions that are available to use in Python. 
In Python, there are three basic I/O connections, Standard Input, Standard Output and Standard Error. As the name suggests, Standard Input is the data that goes to the program through the keyboard. keyboard being the standard input. Standard output is the terminal console, unless redirected..(guess where?!!) and Standard error is the stream where the programs write their error messages which is again to the terminal unless redirected.

### Standard Input, Output and Error:

The `input( )` function reads one line from the standard input and returns it as a string.


```python
name = input("Enter your name: ")
print("Hello {name}".format(name=name))
```

    Enter your name: Mohit
    Hello Mohit



```python
# Lets use list comprehension in the input
some_val = input("Enter something: ")
print("You entered: {}".format(some_val))
```

    Enter something: Foo
    You entered: Foo


Python2 users would have observed the output as `You entered: [0, 2, 4, 6, 8]`
and Python3 users would have observed the output as `[x for x in range(10) if x%2 == 0]`

Until Python3.2 there used to be two methods for accepting input -- `raw_input` and `input` the behavior that python3 users are seeing is the actual behavior of `raw_input`. However after Python3.2, it was decided to drop the `input` method.
> For the sake of staying on topic, we cannot discuss more on this.. but for the curious souls.. head here: https://www.python.org/dev/peps/pep-3111/

We saw the Standard Error in the Exception Handling module. 

We've also been using Standard Output since `module 1`, I guess.. using the `print` function (for python3) or `print` statement (for python2), right?

### File I/O
Until now you have been reading and writing to the standard input. Lets now perform the same function to the files. Now we will see how we can read and write to the files.

#### Opening Files: 
Files can be opened using python's built-in `open()` function. This function creates a file object which is used for performing different operations on the file. It will become much clear when we look at a complete example. For now, just remember that we need to create a file object before performing any file I/O and try to remember the syntax.
`fhandler = open(file_name, access mode, encoding)`

- `file_name`: The file name that you would like to perform your I/O operations on.
- `encoding`: Encoding tells python what encoding scheme to use to convert the stream of bytes to text. 
- `access_mode`: This is the mode which determines if the file is to opened as read only,read-write, write only etc modes. The ways in which a file can be opened are mentioned below:

|access_mode | Its Function|
|:------|------------:|
|r	|Opens a file as read only|
|rb	|Opens a file as read only in binary format|
|r+	|Opens a file for reading and writing|
|rb+	|Opens a file for reading and writing in binary format|
|w	|Opens a file for writing only|
|wb	|Opens a file for writing only in binary format|
|w+	|Opens a file for both reading and writing|
|wb+	|Opens a file for writing and reading in binary format|
|a	|Opens a file for appending|
|ab	|Opens a file for appending in binary|
|a+	|Opens a file for appending and reading|
|ab+	|Opens a file for appending and reading in binary format|

#### Reading and Writing
Once we have created a file object we can perform many operations on the file object which, like all objects, has methods to take care of nitty gritty details and perform the operations on the file. Before we jump into the functions, lets take a look at a complete File I/O example.



```python
try:
    fhandler = open('test.txt', 'w') 
    fhandler.write('Hello World')
except IOError as ex:
    print("Error performing I/O operations on the file: ",ex)
finally:
    if fhandler:
        fhandler.close()
```

If the above code ran without any exception, then it should have created a file test.txt (and if it existed before, it will overwrite it because of access_mode as `w`)

Now before we proceed ahead, don't you think the total number of lines that we wrote to achieve just a small objective (of writing a string to file) is too much effort?

Let's look at an alternative way of writing to a file


```python
try:
    with open('test.txt', 'w') as fhandler:
        fhandler.write('Hello World')
except IOError as ex:
    print("Error performing I/O operations on the file: ",ex)
```

Much better, eh?

In fact, It is good practice to use the `with` keyword when dealing with file objects. This has the advantage that the file is properly closed (`fhandler.close()`) after its suite finishes, even if an exception is raised on the way. It is also much shorter than writing equivalent `try-except-finally` blocks.

Want another reason for using `with` statement? Ok, if you want to open multiple files together, you can do that using with statement by simply separating the different file handlers by a comma.. 
something like this
```
with open('test0.txt', 'w') as fh0, open('test1.txt', 'w') as fh1 ...
```

So what is `with` statement? Putting it very very simply.. `with` has `__enter__()` and `__exit__()` functions where stuff like opening and closing the file handler can take place. The `with` statement guarantees that if the `__enter__()` method returns without an error, then `__exit__()` will always be called.

> We cannot discuss more about `with` statement here--it can take up a whole module--but again for curious minds out there, read this `pep`: https://www.python.org/dev/peps/pep-0343/

Alright, coming back to our discussion on File I/O,  lets now look at some of the functions that you may end up using.

##### file_object.close()

This method will close the file that we have currently open. You should always call this method once you are done performing I/O operations on the file using the file object unless you are using `with` statement. `with` statement already does that for you.

#####  file_object.mode

This is a read-only attribute that is the value of the mode string used in the open call that created the file_object

##### file_object.readline([size])

This method reads strings from the file till it reaches new line character ( `\n` ) if the `size` parameter is empty. If an integer is provided as size parameter, then this method returns string of length size.

##### file_object.readlines([size])

This method basically calls the `readline()` method till it reaches the end of file.

##### file_object.seek(pos, how=0)

Sets the file_object's current position to the signed integer byte offset by pos from the reference point. The how parameter, which is 0 by default, indicates the reference point. `how`=1 is the reference of current position and `how`=2 is the reference of the end of the file.

##### file_object.tell()

This method tells the current file position when you are reading from or writing to a file.

##### file_object.truncate([size])

This method truncates the file to be at most of size size.  If you don't mention the size it takes the size from `tell()` method as the new size.

##### file_object.write(str)

Writes the bytes of string str to the file.

##### file_object.writelines(lst)

Writes sequence of strings to file. No new line is added automatically.


```python
try:
    with open('test.txt', 'r+') as fhandler:
        print(fhandler.readline())
        fhandler.writelines(['.', 'This is', ' Python'])
        # Go to the starting of file
        fhandler.seek(0)
        # Print the content of file
        print(fhandler.readlines())
        fhandler.truncate(20)
        fhandler.seek(0)
        print('After truncate: ',fhandler.readlines())
except IOError as ex:
    print("Error performing I/O operations on the file: ",ex)
```

    Hello World
    ['Hello World.This is Python']
    After truncate:  ['Hello World.This is ']


Great! So now we opened the file, read its contents, added multiple strings, truncated and closed it! This covers pretty much everything that you will need when you are working with almost any kind of file that has some text.

### 02 - 06.03 CSV File I/O
In the above examples, we saw how to perform read-write operations on a file. This is generally used for files that have multiple lines of strings. However if you have data like this:

||||
|:--|:--|:--|
|Data1	|Data2	|Data3|
|Example1	|Example2	|Example3|

It is stored in a file with this format:
```
Data1, Data2, Data3
Example01, Example02, Example03
Example11, Example12, Example13
```

As can be seen in the above example, each row is a new line, and each column is separated with a comma. Many online services allow its users to export tabular data from the website into a CSV file. These files can then be opened and viewed offline using a Spreadsheet program such as Google Sheets, Numbers or Microsoft Excel.

>Disclaimer: The data generated is completely random using a third party website [`https://www.fakenamegenerator.com`](https://www.fakenamegenerator.com 'FakeName Generator')


#### So why do we need such CSV files? 
There are two primary reasons for the existence of this format:

- CSV are plain-text files which makes them easy to store and read from
- CSV files are stored as sequence of human readable characters, thus making it easy for humans to interpret the data without requiring any format conversion.
- CSV is a delimited text file that uses a comma to separate values (many implementations of CSV import/export tools allow other separators to be used). Simple CSV implementations may prohibit field values that contain a comma or other special characters such as newlines. More sophisticated CSV implementations permit them, often by requiring " (double quote) characters around values that contain reserved characters (such as commas, double quotes, or less commonly, newlines). Embedded double quote characters may then be represented by a pair of consecutive double quotes, or by prefixing an escape character such as a backslash (for example in Sybase Central). The name "CSV" indicates the use of the comma to separate data fields. Nevertheless, the term "CSV" is widely used to refer a large family of formats, which differ in many ways. Some implementations allow or require single or double quotation marks around some or all fields; and some reserve the very first record as a header containing a list of field names. An official standard for the CSV file format does not exist.

Download a Sample\* CSV file from [`HERE`](./sample_datasets/sample_names.csv 'Sample CSV') and save it in your current folder location. 


#### Reading CSV files

`reader()` can be used to create an object that is used to read the data from a csv file. The reader can be used as an iterator to process the rows of the file in order. Lets take a look at an example:


```python
import csv
row = []
try:
    with open('./sample_datasets/sample_names.csv', 'r') as fh:
        reader = csv.reader(fh)
        for info in reader:
            row.append(info)
except IOError as ex:
    print("Error performing I/O operations on the file: ",ex)

print(row[0:10])
```

    [['\ufeffGivenName', 'Gender', 'Title', 'Occupation', 'City'], ['Nicholas', 'male', 'Mr.', 'Speech writer', 'Plantation'], ['Jeanette', 'female', 'Mrs.', 'Surfacing equipment operator', 'Chicago'], ['David', 'male', 'Mr.', 'Engineering geologist', 'Worthington'], ['Susan', 'female', 'Ms.', 'Cutting, punching, and press machine tender', 'Fulton'], ['Dennis', 'male', 'Mr.', 'Construction millwright', 'Fargo'], ['Susan', 'female', 'Mrs.', 'Private investigator', 'Blackwood'], ['John', 'male', 'Mr.', 'Chemical engineering technician', 'Marietta'], ['Damon', 'male', 'Mr.', 'Loan closer', 'Mansfield'], ['George', 'male', 'Mr.', 'Public defender', 'Minneapolis']]


`reader()` is a method available in csv package so the first line basically imports the csv package. The `reader()` method takes sequence or an iterable file object, and returns an iterator. As the csv file is being read, each row of the input data is converted to a list of strings. The parser handles the line breaks embedded within the strings which is why using row is not always the output that you might get when taking a line input from file. 

#### Writing CSV files

Writing csv files is just as easy as reading them. To write to a csv file, we can use `writer()` method to create an object for writing and then iterate over the rows using csv's `writerow()` method to write it.


```python
import csv
try:
    with open('test.csv', 'w') as fh:
        writer = csv.writer(fh)
        for num in range(10):
            writer.writerow((num, num**1, num**2))
except IOError as ex:
    print("Error performing I/O operations on the file: ",ex)
```

Now try opening the file just like we did before and see the contents

#### DictReader

In addition to working with sequences or data, the `csv` module includes classes for working with rows as dictionaries so that the fields can be named. The `DictReader` and `DictWriter` classes translate rows to dictionaries instead of lists. Keys for the dictionary can be passed in, or inferred from the first row in the input.


```python
import csv
row = []
try:
    with open('./sample_datasets/sample_names.csv', 'r') as fh:
        reader = csv.DictReader(fh)
        for info in reader:
            row.append(info)
except IOError as ex:
    print("Error performing I/O operations on the file: ",ex)

print(row[0:10])
```

    [OrderedDict([('\ufeffGivenName', 'Nicholas'), ('Gender', 'male'), ('Title', 'Mr.'), ('Occupation', 'Speech writer'), ('City', 'Plantation')]), OrderedDict([('\ufeffGivenName', 'Jeanette'), ('Gender', 'female'), ('Title', 'Mrs.'), ('Occupation', 'Surfacing equipment operator'), ('City', 'Chicago')]), OrderedDict([('\ufeffGivenName', 'David'), ('Gender', 'male'), ('Title', 'Mr.'), ('Occupation', 'Engineering geologist'), ('City', 'Worthington')]), OrderedDict([('\ufeffGivenName', 'Susan'), ('Gender', 'female'), ('Title', 'Ms.'), ('Occupation', 'Cutting, punching, and press machine tender'), ('City', 'Fulton')]), OrderedDict([('\ufeffGivenName', 'Dennis'), ('Gender', 'male'), ('Title', 'Mr.'), ('Occupation', 'Construction millwright'), ('City', 'Fargo')]), OrderedDict([('\ufeffGivenName', 'Susan'), ('Gender', 'female'), ('Title', 'Mrs.'), ('Occupation', 'Private investigator'), ('City', 'Blackwood')]), OrderedDict([('\ufeffGivenName', 'John'), ('Gender', 'male'), ('Title', 'Mr.'), ('Occupation', 'Chemical engineering technician'), ('City', 'Marietta')]), OrderedDict([('\ufeffGivenName', 'Damon'), ('Gender', 'male'), ('Title', 'Mr.'), ('Occupation', 'Loan closer'), ('City', 'Mansfield')]), OrderedDict([('\ufeffGivenName', 'George'), ('Gender', 'male'), ('Title', 'Mr.'), ('Occupation', 'Public defender'), ('City', 'Minneapolis')]), OrderedDict([('\ufeffGivenName', 'Elizabeth'), ('Gender', 'female'), ('Title', 'Dr.'), ('Occupation', 'Professional athlete'), ('City', 'Boston')])]


> Python 2 users should see a `list of dictionaries` and Python3 users should see a list of `OrderedDict`. The `OrderedDict`, as the name suggests, will preserve the order in which the entries were inserted. (You can guess why!)

#### DictWriter

Similar to DictReader, we also have DictWriter which needs to be given a list of field names so it knows how to order the columns in the output file. 


```python
import csv
try:
    fieldnm = ('Title1', 'Title2', 'Title3')
    with open('test_dict.csv', 'w') as fh:
        writer = csv.DictWriter(fh, fieldnames=fieldnm)
        headers = dict((hdr, hdr) for hdr in fieldnm)
        for num in range(10):
            writer.writerow({'Title1':num, 'Title2':num+1, 'Title3':num+2})
except IOError as ex:
    print("Error performing I/O operations on the file: ",ex)
```

The above DictReader and DictWriter techniques are good when the filesize (or the number of columns) is not very big. When the row numbers start scaling up, the list that is created by the reader() method starts growing in memory and makes the process very very slow. 

We will generally be dealing with the files that have over a million row entries and this method is not the most efficient way of dealing with such files. To handle such 'Big Data', we will study python packages like `Numpy` and `Pandas` in next few modules.
