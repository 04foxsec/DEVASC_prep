# Working with Data in Python

There are numerous ways to ingest data into a Python program. You can get input from the user, pull data from a website or an API, or read data from a file. The trick is being able to convert data from a data source into native Python structures and objects so that you can use it to automate your infrastructure. This chapter discusses a number of ways to use built-in and third-party modules to transform different types of data into Python dictionaries, lists, and other data collection objects. 

## File Input and Output

Pulling data from a file in Python is very straightforward. To extract data from a text file, you can use native Python capabilities. Binary files, on the other hand, need to be processed by some module or another external program before it is possible to extract the data from them. 

From Python's perspective, a text file can be thought of as a sequence of lines. Each line, as it is read in to Python, is typically 79 characters long [(per PEP 8 convention)](https://www.python.org/dev/peps/pep-0008/), with a newline character at the end (\n for Python). There are just two functions that you need to know when working with a text file: **open()** and **close()**.

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

TBC

### JavaScript Object Notation (JSON)
JavaScript Object Notation (JSON) is a data structure that is derived from the Java programming language, but it can be used as a portable data structure for any programming language. **It was built to be an easily readable and standard way for transporting data back and forth between applications**. JSON is heavily used in web services and is one of the core data formats you need to know how to use in order to interact with Cisco infrastructure. The data structure is built around key/value pairs that simplify mapping of data and its retrieval.
```
{
  "interface": {
     "name": "GigabitEthernet1",
     "description": "Router Uplink",
     "enabled": true,
     "ipv4": {
       "address": [
           {"ip": "192.168.1.1",
            "netmask": "255.255.255.0"}
            ]
      }
    }
}
```
You can see the structure that JSON provides. **interface** is the main data object, and you can see that its value is multiple key/value pairs. This nesting capability allows you to structure very sophisticated data models. Notice how similar to a Python dictionary the data looks. **You can easily convert JSON to lists (for a JSON array) and dictionaries (for JSON objects) with the built-in JSON module.** There are four functions that you work with to perform the conversion of JSON data into Python objects and back.

|Function| Description|
|--------|------------|
|load():| This allows you to import native JSON and convert it to a Python dictionary from a file.|
|loads():| This will import JSON data from a string for parsing and manipulating within your program.|
|dump():| This is used to write JSON data from Python objects to a file.|
|dumps():| This allows you to take JSON dictionary data and convert it into a serialized string for parsing and manipulating within Python.|

The **s at the end of dump and load refers to a string**, as in dump string. To see this in action, you load the JSON file and map the file handle to a Python object (data)
```
import json
with open("json_sample.json") as data:
  json_data = data.read()
json_dict = json.loads(json_data)
```
The object json_dict has taken the output of json.loads(json_data) and now holds the json object as a Python dictionary:
```
print(type(json_dict))
...
<class 'dict'>
...
print(json_dict)
...
{'interface': {'name': 'GigabitEthernet1', 'description':'Router Uplink', 'enabled': True, 'ipv4': {'address':[{'ip': '192.168.0.2', 'netmask': '255.255.255.0'}]}}}
```
You can now modify any of the key/value pairs, as in this example, where the description is changed:
```
json_dict["interface"]["description"] = "Backup Link"
print(json_dict)
...
{'interface': {'name': 'GigabitEthernet1', 'description': 'Backup Link', 'enabled': True, 'ipv4': {'address': [{'ip': '192.168.0.2','netmask': '255.255.255.0'}]}}}
```

In order **to save the new json object back to a file, you have to use the dump() function (without the s)** to convert the Python dictionary back into a JSON file object. To make it easier to read you can add the **indent** keyword with a number for the indentation.
```
with open("json_sample.json", "w") as filehandler:
  json.dump(json_dict, filehandler, indent = 4)
```
Loading the JSON File and Printing the Output to the Screen
``` 
with open ("json_sample.json") as data:
  json_data = data.read()
  print(json_data)
...
{
  "interface": {
    "name": "GigabitEthernet1",
      "description": "Backup Link",
      "enabled": true,
      "ipv4": {
        "address": [
            {
             "ip": "192.168.0.2",
             "netmask": "255.255.255.0"
             }
          ]
        }
    }
}
```

### Extensible Markup Language (XML)
Extensible Markup Language (XML) is a very common data format that is used heavily in configuration automation. Parsing XML is similar to using other data formats, in that Python natively understands and can support XML encoding and decoding. 
```
<device>
  <Hostname>Rtr01</Hostname>
  <IPv4>192.168.1.5</IP4>
  <IPv6> </IPv6>
</device>
```
It should come as no surprise that **XML looks a bit like HTML syntax;** it was designed to work hand-in-hand with HTML for data transport and storage between web services and APIs. **XML has a tree structure, with the root element being at the very top**. There is a parent/child relationship between elements. In the preceding example, device is the root element that has Hostname, IPv4, and IPv6 as child elements. **Just like with HTML, a tag has meaning and is used to enclose the relationships of the elements with a start tag (<>)and a closing tag (</>).** 

```
 <?xml version="1.0" encoding="UTF-8" ?>
<interface xmlns="ietf-interfaces">
  <name>GigabitEthernet2</name>
  <description>Wide Area Network</description>
  <enabled>true</enabled>
  <ipv4>
    <address>
      <ip>192.168.1.5</ip>
      <netmask>255.255.255.0</netmask>
    </address>
  </ipv4>
</interface>
```
**To work with this, you can use the native XML library, but it has a bit of a learning curve and can be a little hard to use** if you just want to convert XML into something you can work with in Python. **To make it easier, you can use a module called xmltodict to convert XML into an ordered dictionary in Python.** This is a special class of dictionary that does not allow elements to change order. Since dictionaries use key/value pairs, where the key/value pairs are stored is normally not a problem, but in the case of XML, order matters.
```
import xmltodict
with open("xml_sample.xml") as data:
  xml_example = data.read()
xml_dict = xmltodict.parse(xml_example)
print(xml_dict)
...
OrderedDict([('interface', OrderedDict([('@xmlns', 'ietf-interfaces'), ('name','GigabitEthernet2'), ('description', 'Wide Area Network'), ('enabled', 'true'), ('ipv4', OrderedDict([('address', OrderedDict([('ip', '192.168.0.2'), ('netmask','255.255.255.0')]))]))]))])
```
Now that you have the XML in a Python dictionary, you can modify an element:
```
xml_dict["interface"]["ipv4"]["address"]["ip"] = "192.168.55.3"
```
You can see your changes in XML format by using the unparse function. You can use **the pretty=True argument to format the XML to make it a bit easier to read**. XML doesnt care about whitespace, but humans do for readability.
```
print(xmltodict.unparse(xml_dict, pretty=True))
...
<?xml version="1.0" encoding="utf-8"?>
<interface xmlns="ietf-interfaces">
  <name>GigabitEthernet2</name>
  <description>Wide Area Network</description>
  <enabled>true</enabled>
    <ipv4>
      <address>
        <ip>192.168.55.3</ip>
        <netmask>255.255.255.0</netmask>
      </address>
    </ipv4>
</interface>
```
To write these changes back to your original file, you can use the following code:
```
with open("xml_sample.xml", "w") as data:
  data.write(xmltodict.unparse(xml_dict, pretty=True))
```
### YAML Ain't Markup Language (YAML)
YAML is an extremely **popular human-readable format for constructing configuration files and storing data.** It was built for the **same use cases as XML but has a much simpler syntax and structure**. It uses **Python-like indentation to differentiate blocks of information** and was actually built based on JSON syntax but with a whole host of features that are unavailable in JSON (such as comments). If you have ever used Docker or Kubernetes, you have undoubtably run into YAML files. 

```
---
interface:
  name: GigabitEthernet2
  description: Wide Area Network
  enabled: true
  ipv4:
    address:
    - ip: 172.16.0.2
       netmask: 255.255.255.0
```
YAML object has minimal syntax, all data that is related has the same indentation level, and key/value pairs are used to store data. YAML can also represent a list by using the - character to identify elements.

To work with **YAML in Python, you need to install and import the PyYaml module.** Once you import it into your code, you can convert YAML to Python objects and back again. YAML objects are converted to dictionaries, and YAML lists automatically become Python lists. The two functions that perform this magic are **yaml.load** to convert from YAML objects into Python and **yaml.dump** to convert Python objects back to YAML. Just as in the other data examples, you can load a YAML file and then pass it to yaml.load to work its magic. The latest PyYaml module requires that you add an argument to tell it which loader you want to use. This is a security precaution so that your code will not be vulnerable to arbitrary code execution from a bad YAML file.
```
import yaml
with open("yaml_sample.yaml") as data:
  yaml_sample = data.read()
yaml_dict = yaml.load(yaml_sample, Loader=yaml.FullLoader)
```
The variable yaml_dict is now a dictionary object containing your YAML file. Had this key/value been a YAML list.
```
print(yaml_dict)
...
{'interface': {'name': 'GigabitEthernet2', 'description': 'Wide Area Network', 'enabled': True, 'ipv4': {'address': [{'ip': '192.168.0.2', 'netmask': '255.255.255.0'}]}}}
```
As before, you can modify this object to your liking.
```
yaml_dict["interface"]["name"] = "GigabitEthernet1"

print(yaml.dump(yaml_dict, default_flow_style=False))
...
interface:
  description: Wide Area Network
  enabled: true
  ipv4:
    address:
    - ip: 192.168.0.2
       netmask: 255.255.255.0
  name: GigabitEthernet1
```
To write these changes back to your file, use the following code.
```
with open("yaml_sample.yaml", "w") as data:
  data.write(yaml.dump(yaml_dict, default_flow_style=False))
```
## Error handling
## Test-Driven Development
## Unit test
