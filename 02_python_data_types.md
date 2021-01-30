## 4. Data Types and Variables

Python supports many data types natively. Python can also be expanded with modules to support even more variables. A variable is really just a label that maps to a Python object stored somewhere in memory. Without variables, your programs would not be able to easily identify these objects, and your code would be a mess of memory locations.

### 4.1. Varialbles

Assigning a variable in Python is very straightforward. Python auto types a variable, and you can reassign that same variable to another value of a different type in the future. (Try doing that in C!) You just need to remember the rules for variable names:

- A variable name must start with a letter or the underscore character.
- A variable name cannot start with a number.
- A variable name can only consist of alphanumeric characters and underscores (A-Z, 0-9, and _).
- A variable name is case sensitive (so Value and value are two different variable names).

### 4.2. Data types

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

#### 4.2.1 Integers and Folating point

The integers and floating point numbers are the simplest of data types:

- Integers: Whole numbers without decimal points
- Floating point: Numbers with decimal points or exponents (such as 10e5, which indicates 10 to the fifth power)

##### 4.2.1.1 Numerical Operators

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

#### 4.2.1.2 Numerical Data representation

You have the option to use other base systems instead of just the default base 10. You have three choices in addition to base 10: binary (base 2), octal (base 8), and hex (base 16). You need to use prefixes before integers in order for Python to understand that you are using a different base:

- 0b or 0B for binary
- 0o or 0O for octal
- 0x or 0X for hex

**From Pythonis perspective, these are still just integers**, and if you type any of them into the interpreter, it will return the decimal value by default, as shown in this example:
```
>>> 0xbadbeef
195935983
```
#### 4.2.2 Booleans

**A Boolean has only two possible values, True and False.** You use comparison operators to evaluate between two Boolean objects in Python. This data type is the foundation for constructing conditional steps and decisions within programs. 


|Operator|What It Does|Example|Evaluates to|
|--------|------------|-------|------------|
|```<```|Less than|5 < 10|True|
|```>```|Greater than|6.5 > 3.5|True|
|```<=```|Less than or equal to|0 <= -5|False|
|```>=```|Greater than or equal to|6 >= 6|True|
|```==```|Equal to|5 = "5"|False|
|```!=```|Not equal to|5 != "5"|True|

#### 4.2.3 Strings

The **string data type is a sequence of characters and uses quotes to determine which characters are included**. The string "Hello" is just a set of characters that Python stores in order from left to right. Even if a string contains a series of numbers, it can still be a string data type.

**A string is just a list of characters in a certain order that Python keeps track of.** In fact, this aspect of strings makes them easy to manipulate. If you use the string **'DevNet'**, you can pull out any individual characters of the string by knowing where it sits in the string index. **Indexes in Python always start with 0, so if you want the very first character in a string**

```
>>> a='DevNet'
>>> a[0]
'D'
```
##### 4.2.3.1 String Ranges
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

##### 4.2.3.2 String Methods
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

#### 4.2.4 Lists

Python, unlike other programming languages, such as C++ and Java, doesn't have arrays. **If you want to store a bunch of values, you can use a list.** You can use a variable to store a collection of items in a list. 

```
>>> kids = ['Caleb', 'Sydney', 'Savannah']
>>> kids
['Caleb', 'Sydney', 'Savannah']
```

**A list can contain any Python object, such as integers, strings, and even other lists.** A list can also be empty and is often initialized in an empty state for programs that pull data from other sources. ``` mylist=[]``` or ```my2list=list()```

Lists are similar to strings in that each is a set of **items indexed by Python that you can interact with and slice and dice**. To pull out values, you just use the variable name with brackets and the index number, which starts at 0.
```
>>> kids[1]
Sydney
```
Unlike strings, **lists are mutable objects**, which means you can change parts of the list at will. With a string, you can't change parts of the string without creating a new string. This is not the case with lists, where you have a number of ways to make changes. 
```
>>> kids
['Caleb', 'Sidney', 'Savannah']
>>> kids[1]="Sydney"
>>> kids
['Caleb', 'Sydney', 'Savannah']
```
You **can concatenate lists as well** by using the + operator to join two lists together. **Slicing or ranges also apply here.** The elements in the list are the items in the bucket.
```
>>> a = [1, 2, 4, 5]
>>> b = [6, 7, 8, 9, 10]
>>> c = a + b
>>> print(c)
[1, 2, 4, 4, 5, 6, 7, 8, 9, 10]
>>> c[1:4]
[2, 3, 4]
>>> c[ :-4]
[1, 2, 3, 4, 5, 6]
>>> c[:]
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

##### 4.2.4.1 List Methods

|Method|What It Does|
|------|------------|
|list.append(element)|Adds an element to the end of the list|
|list.clear()|Removes everything from the list|
|list.copy(alist)|Returns a copy of the list|
|list.count(element)|Shows the number of elements with the specified value|
|list.extend(alist)|Adds the elements of a list to the end of the current list|
|list.index()|Returns the index number of the first element with a specified value|
|list.insert( index, element)|Adds an element at a specified index value|
|list.pop(index)|Removes an element at a specific index position, or if no index position is provided, removes the last item from the list|
|list.remove()|Removes a list item with a specified value|
|list.reverse()|Reverses the list order|
|list.sort()|Sorts the list alphabetically and/or numerically|

#### 4.2.5 Tuples

**Tuples and lists are very similar.** The biggest difference between the two comes down to mutability. As discussed earlier, Python data types are either mutable or immutable. **Lists are mutable, and tuples are immutable.** So why would you need these two types if they are so similar? It all comes down to how Python accesses objects and data in memory. **When you have a lot of changes occurring, a mutable data structure is preferred** because you don't have to create a new object every time you need to store different values. **When you have a value that is constant and referenced in multiple parts of a program, an immutable data type (such as a tuple), is more memory efficient and easier to debug.** 

To create a tuple, you use parentheses instead of brackets. You can use the ```type()``` function to identify a Python data type you have created.
```
>>> person = (2012, 'Mike', 'CCNA')
>>> person
(2012, 'Mike', 'CCNA')
>>> type(person)
<class 'tuple'>
```
You access data in a tuple the same way as in a list, by using brackets and the index value of the item in the tuple that you want to return:
```
>>> person[0]
2012
```
What **you can't do with a tuple is make an assignment to one of the values**:
```
>>> person[0]=15
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```
Tuples can, however, be used to assign a set of variables quickly:
```
>>> (a, b, c) = (12, 'Fred',18)
>>> c
18
```

#### 4.2.6 Dictionaries

A dictionary provides another way of creating a collection of items. Why do you need another way of storing data when you already have lists and tuples? A list is an ordered set of items tracked by an index. What if you need to access data that is tied to a certain value, such as a person�s name? This capability is exactly why you need dictionaries in Python. A dictionary saves a ton of effort by giving you a built-in system for storing data in a key:value pair. As when you use labels on files in a filing cabinet, you can assign data to a key and retrieve it by calling that key as if you are pulling a file from the cabinet. Dictionaries don�t have any defined order; all you need is the key�and not some index number�to get access to your data. There are some rules regarding dictionaries.

**Keys:** A dictionary's keys are limited to only using immutable values (int, float, bool, str, tuple, and so on). No, you can't use a list as a key, but you can use a tuple, which means you could use a tuple as a key (immutable) but you can't use a list as a key (mutable).
**Values:** A value can be any Python object or any combination of objects. To create a dictionary, you use braces and your key and value separated by a colon. You separate multiple items with commas.
```
>>> cabinet = { "scores":(98,76,95), "name":"Chris","company":"Pisco"}
>>> type(cabinet)
<class 'dict'>
```
Instead of using an index, you **use the key, to get the value.**
```
>>> cabinet["scores"]
(98, 76, 95)
>>> cabinet["company"]
'Pisco'
```

To add more items to a dictionary, you can assign them with a new key. You can even add another dictionary to your existing dictionary, as shown in this example:
```
>>> cabinet["address"] = {"street":"123 Anywhere Dr","city":"Franklin", "state":"TN"}
>>> cabinet["address"]
{'street': '123 Anywhere Dr', 'city': 'Franklin', 'state': 'TN'}
```

#### 4.2.7 Sets

A **set in Python consists of an unordered grouping of data and is defined by using the curly braces** of a dictionary, **without the key:value pairs**. **Sets are mutable**, and you can add and remove items from the set. **You can create a special case of sets called a frozen set that makes the set immutable.** A frozen set is often used as the source of keys in a dictionary (which have to be immutable); it basically creates a template for the dictionary structure. If you are familiar with how sets work in mathematics, the various operations you can perform on mutable sets in Python will make logical sense.
```
>>> numbs = {1, 2, 4, 5, 6, 8, 10}
>>> odds = {1, 3, 5, 7, 9}
```
To check that these are indeed sets, use the type() function:
```
>>> type(odds)
<class 'set'>
```
To join two sets (just as in a mathematical join), you can use the | operator to show a combined set with no duplicates:
```
>>> numbs | odds
{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
```
You can get an intersection of two sets and show what numbers are in both by using the & operator:
```
>>> numbs & odds
{1, 5}
```
There are many ways to evaluate sets, and the Python documentation can be used to explore them all. In addition, Python has library collections that give you even more options for ways to store data. Search the Python documentation for "collections" and take a look at ordered dictionaries, named tuples, and other variations that may suit your data collecting needs. For the purposes of the DEVASC exam, though, you do not need to know data structures beyond the basic types discussed here.

