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

