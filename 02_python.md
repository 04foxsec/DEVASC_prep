# Introduction to Python

The 200-901 DevNet Associate DEVASC exam is not a Python test per se. You will not be asked to answer esoteric questions about techniques and syntax that only a Python wizard would know. The exam ensures that you are competent enough with Python to know how to interact with Cisco hardware through APIs and to use Cisco software development kits and frameworks such as pyATS and Genie.

Many UNIX-based operating systems, such as Mac and Linux, already have Python installed, but with Windows, you need to install it yourself. This used to be a hassle, but now you can even install Python from the Windows Store. On a Mac, the default version of Python is 2.7, and you should update it to the more current 3.8 version. One of the easiest ways is to head over to python.org and download the latest variant from the source. The installation is fast, and there are many tutorials on the Internet that walk you through the process.

## Python Virtual environment

The use of Python 3 has changed dramatically as support for the 2.x version ended in January 2020. The 3.x version came out in 2008 and is the one that you should be using today. Of course, this version issue is still a problem even within the 3.x train of Python and the corresponding modules you may want to use. To address this compatibility conundrum across different versions and modules, Python virtual environments have been created. 
Such an environment allows you to install a specific version of Python and packages to a separate directory structure. This way, you can ensure that the right modules are loaded, and your applications don't break when you upgrade your base Python installation. 

To use virtual environments, you launch Python 3 with the **-m** argument to run the **venv** module. To activate the virtual environment by using the **source** command.

```
#MacOS or Linux
python3 -m venv myvenv
source myvenv/bin/activate
```

```
#Windows
C:\py -3 -m venv myvenv
C:\myvenv\Scripts\activate.bat
```
At this point, you will see your virtual environment name in parentheses at the beginning of your command prompt: ```(myvenv)$```

To turn off the virtual environment, just type **deactivate** at the command prompt, and your normal command prompt returns, indicating that you are using your local system Python setup.

To install new modules for Python, you use **pip**, which pulls modules down from the PyPI repository. ```(myvenv)$ pip install "packagename"``` 

The pip command also offers a search function that allows you to query the package index: ```(myvenv)$ pip search "search value"``` 

The output includes the name, version, and a brief description of what the package does. To install a specific version ```pip install package==1.1.1.``` 

Using a requirements.txt file included with your code is another essential good practice. If you have a requirements.txt file included with your code, it will give pip a set of packages that need to be installed, and you can issue this one command to get them loaded: ```pip install -r requirements.txt ```

Contents of requirements.txt
```ansible==2.6.3
black==19.3b0
flake8==3.7.7
genie==19.0.1
```
If want to save the current modules configured in your virtual environment, you can use the **freeze** command and have it automatically populate the requirements.txt file: ```pip freeze > requirements.txt```

## Python syntax

The word *syntax* is used to describe structure in a progaming language. **Python is a looser language than some, it does have rules that should be followed to keep your code not only readable but functional.**  Python is best understood through its core philosophy (The Zen of Python):

- Beautiful is better than ugly.
- Explicit is better than implicit.
- Simple is better than complex.
- Complex is better than complicated.
- Readability counts.

Python is a scripted language, which means that any text editor can become a Python programming environment. The easiest way to get started with some Python code is to just enter ```python3``` at the command prompt.

```
$ python3
>>> print("Savannah rules!")
Savannah rules!
```
For doing simple repetitive tasks, the interpreter is a quick interface to Python. For any program that you want to do a lot of editing, an editor is your best bet.

One aspect in which Python is different from other languages is that within Python code, **whitespace matters. Python uses indentation to separate blocks of code.
Python allows you to use spaces or tabs. The standard for Python from the PEP 8 style guide is to use four spaces of indentation before each block of code.**

## Commenting in python

```# comemnt``` is a single line comment
```
'''multi
line
comment'''
``` 
Triple (') quote is multi line commenting.

## Data Types and Variables

Python supports many data types natively. Python can also be expanded with modules to support even more variables. A variable is really just a label that maps to a Python object stored somewhere in memory. Without variables, your programs would not be able to easily identify these objects, and your code would be a mess of memory locations.

### Varialbles

Assigning a variable in Python is very straightforward. Python auto types a variable, and you can reassign that same variable to another value of a different type in the future. (Try doing that in C!) You just need to remember the rules for variable names:

- A variable name must start with a letter or the underscore character.
- A variable name cannot start with a number.
- A variable name can only consist of alphanumeric characters and underscores (A-Z, 0-9, and _).
- A variable name is case sensitive (so Value and value are two different variable names).

### Data types

**Everything in Python is an object, and depending on the type of object, there are certain characteristics that you must be aware of when trying to determine the correct action you can perform on them**. In Python, **whenever you create an object, you are assigning that object an ID that Python uses to recall what is being stored**. This mechanism is used to **point to the memory location of the object in question and allows you to perform actions on it, such as printing its value. When the object is created, it is assigned a type that does not change. This type is tied to the object and determines whether it is a string, an integer, or another class.**

Within these types, you are allowed to either change the object (mutable) or are not allowed to change the object (immutable) after it has been created. It means that most of the basic data types are not able to be modified but need to be replaced (or assigned) with another value. You can't just add a character at the end of a string value, for example. You have to instead reassign the whole string if you want to change it. This mutable/immutable concept will make more sense as you interact with various data types in programs. Python treats these two types of objects differently, and each has nuances that you must work around as you build your Python programs. To make it simple, think of immutable objects as ones that you want to stay the same, such as constants. Mutable objects, on the other hand, are objects that you will be adding elements to and subtracting from on a regular basis.

|Name|Type|Mutable|Description|
|----|----|-------|-----------|
|Integer|int|No|Whole numbers, such as 6, 600, and 1589|
|Boolean|bool|No|Comparison value, either True or False|
|String|str|No|Sequence of characters delimited by quotes, such as "Cisco", 'Piper', and "2000"|
|List|list|Yes|Ordered sequence of objects, such as [10, "DNA", 19.8]|
|Tuple|tup|No|Ordered sequence of immutable objects, such as (10, "DNA", 19.8)|
|Dictionary|dict|Yes|Unordered key:value pairs, such as {"key1":"value1","name":"Pip"}|
|Set|set|Yes|Unordered collection of unique objects, such as {"a","b"}|

#### Integers and Folating point

The integers and floating point numbers are the simplest of data types:

- Integers: Whole numbers without decimal points
- Floating point: Numbers with decimal points or exponents (such as 10e5, which indicates 10 to the fifth power)

##### Numerical Operators

Python can perform advanced calculations, so it is used heavily in data science, and many features are built into the language and can be easily added with modules.

|Operator|Description|Example|Evaluates to|
|--------|-----------|-------|------------|
|```+```|Adds two expressions together|5 + 5|10|
|```-```|Subtracts one expression from another|35 - 15|20|
|```*```|Multiplies two expressions|10 * 10|100|
|```/```|Divides one expression by another|20 / 5|4|
|```//```|Performs integer division (leaving off the remainder)|30 // 7|4|
|```%```|Performs modulus division (printing the remainder only)|30 % 7|2|
|```**```|Indicates an exponent|2 ** 8|256|

1. **Parentheses:** Parentheses are always evaluated first.
2. **Power:** The exponent is evaluated.
3. **Multiplication:** Any multiplication is performed.
4. **Division:** Division is evaluated.
5. **Addition:** Addition is performed.
6. **Subtraction:** Subtraction is performed.
7. **Left to right:** After PEMDAS, anything else (such as **sqrt()** or other math functions) is evaluated from left to right.

In most languages, the parentheses are preferred over anything else. Most Python programmers use them liberally in their math formulas to make them simpler to construct without being so strict with the rules. 

#### Numerical Data representation

You have the option to use other base systems instead of just the default base 10. You have three choices in addition to base 10: binary (base 2), octal (base 8), and hex (base 16). You need to use prefixes before integers in order for Python to understand that you are using a different base:

- 0b or 0B for binary
- 0o or 0O for octal
- 0x or 0X for hex

**From Pythonis perspective, these are still just integers**, and if you type any of them into the interpreter, it will return the decimal value by default, as shown in this example:
```
>>> 0xbadbeef
195935983
```
#### Booleans

**A Boolean has only two possible values, True and False.** You use comparison operators to evaluate between two Boolean objects in Python. This data type is the foundation for constructing conditional steps and decisions within programs. 


|Operator|What It Does|Example|Evaluates to|
|--------|------------|-------|------------|
|```<```|Less than|5 < 10|True|
|```>```|Greater than|6.5 > 3.5|True|
|```<=```|Less than or equal to|0 <= -5|False|
|```>=```|Greater than or equal to|6 >= 6|True|
|```==```|Equal to|5 = "5"|False|
|```!=```|Not equal to|5 != "5"|True|

#### Strings

The **string data type is a sequence of characters and uses quotes to determine which characters are included**. The string "Hello" is just a set of characters that Python stores in order from left to right. Even if a string contains a series of numbers, it can still be a string data type.

**A string is just a list of characters in a certain order that Python keeps track of.** In fact, this aspect of strings makes them easy to manipulate. If you use the string **'DevNet'**, you can pull out any individual characters of the string by knowing where it sits in the string index. **Indexes in Python always start with 0, so if you want the very first character in a string**

```
>>> a='DevNet'
>>> a[0]
'D'
```
##### Ranges
You can also specify ranges to print. The **colon operator gives you control over whole sections of a string. The first number is the beginning of the slice, and the second number determines the end. The second number may be confusing at first because it is intended to identify "up to but not including" the last character.**

|Range| Value|
|-----|------|
|a[0:6]|'DevNet'|
|a[:2]|'De'|
|a[2:]|'vNet'|
|a[-2:]|'et'|
|a[:-2]|'DevN'|

You **can perform math operations on strings as well.** The + is used to add or concatenate two strings together and Multiplication works as well.
```
>>> 'DevNet' + 'Rocks'
'DevNetRocks'
>>> 'DevNet Rocks ' * 5
'DevNet Rocks DevNet Rocks DevNet Rocks DevNet Rocks DevNet Rocks '
```

**There is a tremendous amount of string manipulation you can do with Python, and there are a number of built-in methods in the standard string library. These methods are called with a dot after the variable name for a string.**

|Method|What It Does|
|------|------------|
|str.capitalize()|Capitalize the string|
|str.center(width[, fillchar])|Center justify the string|
|str.endwith(suffix[, start[, end]])|Add an ending string to the string|
|str.find(sub[, start[, end]])|Find the index position of the characters in a string|
|str.lstrip([chars])|Remove whitespace characters from the end of the string|
|str.replace(old, new[, count])|Replace characters in the string|
|str.lower()|Make the string all lowercase|
|str.rstrip([chars])|Strip whitespace characters from the front of the string|
str.strip([chars])|Remove whitespace characters from the beginning and end of the string|
|str.upper()|Make the string all uppercase|


