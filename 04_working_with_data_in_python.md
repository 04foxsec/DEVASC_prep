# Working with Data in Python

There are numerous ways to ingest data into a Python program. You can get input from the user, pull data from a website or an API, or read data from a file. The trick is being able to convert data from a data source into native Python structures and objects so that you can use it to automate your infrastructure. This chapter discusses a number of ways to use built-in and third-party modules to transform different types of data into Python dictionaries, lists, and other data collection objects. 

## File Input and Output

Pulling data from a file in Python is very straightforward. To extract data from a text file, you can use native Python capabilities. Binary files, on the other hand, need to be processed by some module or another external program before it is possible to extract the data from them. 

From Python's perspective, a text file can be thought of as a sequence of lines. Each line, as it is read in to Python, is typically 79 characters long [(per PEP 8 convention)] (https://www.python.org/dev/peps/pep-0008/), with a newline character at the end (\n for Python). There are just two functions that you need to know when working with a text file: **open()** and **close()**.

### Open

To open a file and read in its contents, you have tell the name of the file you want to work with. You do this by using the **open()** function and assigning the output to a Python object (the variable readdata in this case). The function returns a file handle, which Python uses to perform various operations on the file.

```
readdate = open("textfile.txt","r")
```
The **open()** function **requires two arguments**: the **name of the file as a string** and the **mode that you want to open the file**.

|mode|desc|
|----|----|
|r|Open for reading (default)|
|w|Open for writing, truncating the file first|
|x|Open for exclusive creation, failing if the file already exists|
|a|Open for writing, appending to the end of the file if it exists|
|b|Open in binary mode|
|t|Open in text mode (default)|
|+|Open for updating (reading and writing)|

### Close

When using the open() function, **you have to remember to close the file when you are finished reading from it**. If you don't, the file will stay open, and you might run in to file lock issues with the operating system while the Python app is running. To close the file, you simply use the close() method on the readdata object:
```
readdata.close()
```
Keeping track of the state of the file lock and whether you opened and closed it can be a bit of a chore. Python provides another way you can use to more easily work with files as well as other Python objects. **The with statement (also called a context manager in Python) uses the open() function but doesn't require direct assignment to a variable**. It also has **better exception handling and automatically closes the file** for you when you have finished reading in or writing to the file. 
```
with open("textfile.txt", "r") as data:
  print(data.read())
```
### File methods

Python has a set of methods available for the file object. Here are some of the common ones.

|Method|Description|
|------|-----------|
|close()|	Closes the file|
|read()|	Returns the file content|
|readline()|	Returns one line from the file|
|readlines()|	Returns a list of lines from the file|
|write()| Writes the specified string to the file|
|writelines()|	Writes a list of strings to the file|


## Parsing data
Imagine a world where all the data is in nice, neatly formatted cells, completely structured, and always consistent. Unfortunately, data is not so easily accessible, as there are a multitude of types, structures, and formats. This is why it is essential that you learn how to parse data in some of the more common forms within your Python programs.

### [CSV (comma-separated values)](https://en.wikipedia.org/wiki/Comma-separated_values)
**A CSV file is just a plaintext spreadsheet or database file.** All of those spreadsheets or databases that you have with infrastructure information can be easily exported as CSV files so that you can use them as source data in Python. Each line in a CSV file represents a row, and commas are used to separate the individual data fields to make it easier to parse the data. Python has a built-in CSV module that you can import that understands the CSV format and simplifies your code.
```
"router1","192.168.10.1","Nashville"
"router2","192.168.20.1","Tampa"
"router3","192.168.30.1","San Jose"
```
To start working with this data, you have to **import the CSV module**, and then you need to **create a reader object** to read your CSV file into. **You first have to read the file into a file handle, and then you run the CSV read function on it and pass the results on to a reader object.** From there, you can begin to use the CSV data as you wish.
```
import csv
csvfile=open("data.csv") #open csv
csvreader = csv.reader(csvfile) #read the csv data
csvdata = list(csvreader) #make a list from the data
print(csvdata)
...
[['router1', '192.168.10.1', 'Nashville'],['router2','192.168.20.1', 'Tampa'], ['router3', '192.168.30.1', 'San Jose ']]

print(csvdata[0])
...
['router1', '192.168.10.1', 'Nashville']
```


### JSON
### XML
### YAML
## Error handling
## Test-Driven Development
## Unit test
