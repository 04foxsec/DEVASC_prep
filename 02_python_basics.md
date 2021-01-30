# Introduction to Python

The 200-901 DevNet Associate DEVASC exam is not a Python test per se. You will not be asked to answer esoteric questions about techniques and syntax that only a Python wizard would know. The exam ensures that you are competent enough with Python to know how to interact with Cisco hardware through APIs and to use Cisco software development kits and frameworks such as pyATS and Genie.

Many UNIX-based operating systems, such as Mac and Linux, already have Python installed, but with Windows, you need to install it yourself. This used to be a hassle, but now you can even install Python from the Windows Store. On a Mac, the default version of Python is 2.7, and you should update it to the more current 3.8 version. One of the easiest ways is to head over to python.org and download the latest variant from the source. The installation is fast, and there are many tutorials on the Internet that walk you through the process.

## 1. Python Virtual environment

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

## 2. Python syntax

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

## 3. Commenting in python

```# comemnt``` is a single line comment
```
'''multi
line
comment'''
``` 
Triple (') quote is multi line commenting.

## 4 Input and output

### 4.1 Input

Input and output pretty much define what a computer does for you. In Python, the **input()** function and the **print()** function are two essential components that allow you to create interactive applications. 

Python has the **input()** function to get information from a user running your Python code. The user is asked a question, and the program waits until the user types a response. 
```
>>> inpt = input('Type your name: ')
Type your name: Chris Jackson
>>> inpt
'Chris Jackson'
```

You assign a variable **(in this case, inpt)** to the **input()** function with a text prompt so that the user knows what is expected. That variable now holds the string the user typed. **Python stores every input as a string**, you need to do a conversion on the data supplied. 

### 4.2 Output

The **print()** function provides output that can be displayed in the user's terminal. Just like every other function in Python, it is called with parentheses. 
```
>>> print('Hello World')
Hello World
```
**Every line printed with the print() function includes a newline character (\n) at the end**, which is a special character that tells the terminal to advance one line. 
There are numerous codes like this that can control how text is displayed in a string and how Python interprets the output. Without them, you would not be able to use, for example, a backslash in your text output. Here are a few of the most common ones:

- \\: Backslash
- \b: Backspace
- \' : Single quote
- \": Double quote
- \t: Tab
- \r: Carriage return

By default, **the print() function uses a separator between elements**. This is normally not an issue if you want spaces to appear between words or elements. You can **change the separator that the print() functions uses with the sep=''** attribute (using single quotes with nothing in between).

One capability added to Python 3.6 and up is the addition of f-string formatting. To create an f-string, you put an f at the beginning of a string, within the print() function, to let Python know what you are doing, and then you can use {} within your string to insert values or other functions. 
```
>>> name = 'Piper'
>>> name2 = 'Chris'
>>> print(f'{name2} says Hi to {name}!')
Chris says Hi to Piper!
```

### 5 Flow Control with Conditionals and Loops

So far you have been exposed to many of the building blocks of the Python language. The real power of a programming language is in the mechanisms you can use to embed logic and respond to different conditions by changing the flow of operation. **Python has three primary control statements**:

- **if**: An if statement is a conditional statement that can compare values and make branching decisions.
- **for**: A for loop is a counting loop that can iterate through data a specific number of times.
- **while**: The while loop can iterate forever when certain conditions are met.

#### 5.1 If Statements

**An if statement starts with an if and then sets up a comparison to determine the truth of the statement** it is evaluating and ending with a : to tell Python to expect the clause (the action if the condition is true) block of code next. As mentioned earlier in this chapter, whitespace indenting matters very much in Python. The clause of an if statement must be indented (four spaces is the standard) from the beginning of the if statement. 
```
>>> n = 20
>>> if n == 20:
...print('The number is 20')
...
The number is 20
```
The Python interpreter uses three dots to let you continue the clause for the if statement. Notice that there is space between the start of the dots and the print() statement. 

An if statement can have as many **elif** conditions as you want to add to the conditional check. Good coding practices recommend simplification, but there is no real limit to how many you add. Since each **if** and **elif** statement does something only if the condition identified is true, it may be helpful to have a default condition that handles situations where none of the if or elif statements are true. For this purpose, you can assign a single **else** statement at the end.

```
score = int(input('What was your test score?:'))
if score >= 90:
  print('Grade is A')
elif score >= 80:
  print('Grade is B')
elif score >= 70:
  print('Grade is C')
elif score >= 60:
  print('Grade is D')
else:
  print('Grade is F')

....

What was your test score?:53
Grade is F
>>> 
```
#### 5.2 For Loops

The **for** statement allows you to **create a loop that continues to iterate through the code a specific number of times**. It is also referred to as a counting loop and can work through a sequence of items, such as a list or other data objects. **The for loop is heavily used to parse through data and is likely to be your go-to tool for working with data sets**. A **for loop starts with the **for statement, followed by a variable name (which is a placeholder used to hold each sequence of data), the in keyword, some data set to iterate through, and then finally a closing colon.**
```
>>> dataset=(1,2,3,4,5)
>>> for variable in dataset:
... print(variable)
...

1
2
3
4
5
```
You can also use the **range()** function to iterate a specific number of times. The **range()** function can take arguments that let you choose what number it starts with or stops on and how it steps through each one. By default, if you just give range() a number, it starts at 0 and goes by 1s until it reaches the number you provided. You can change the increment from the default of 1, you can add a third attribute to the range() statement.
```
>>> for x in range(1,11,3): (1st attribute: begin from, 2nd attribute: ending with, 3rd attribute: inclement) 
... print(x)
...
1
4
7
10
```
Remember that these ranges are up to and not including the final number you specify.

#### 5.3 While Loops

Whereas the **for loop counts through data**, the **while loop is a conditional loop**, and the evaluation of the condition (as in if statements) being true is what determines how many times the loop executes. This difference is huge in that it means you can specify a loop that could conceivably go on forever, as long as the loop condition is still true. **You can use else with a while loop.** An else statement after a while loop executes when the condition for the while loop to continue is no longer met. 

```
count = 1
while (count < 5):
  print("Loop count is:", count)
  count = count + 1
else:
  print("loop is finished")
...  

Loop count is: 1
Loop count is: 2
Loop count is: 3
Loop count is: 4
loop is finished
```
You can use a **break** statement for exiting a loop and a **continue** statement for returning the control to the beginning of the while loop. 

