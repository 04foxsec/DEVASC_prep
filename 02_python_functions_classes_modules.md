## Functions
In Python, a **function is a named block of code** that can take a wide variety of input parameters (or none at all) and return some form of output back to the code that called the function to begin with. It represents a key concept in programming sometimes referred to as **DRY**, which stands for **Don't Repeat Yourself**. The idea behind DRY is that if you perform some particular operations in your code multiple times, you can simply create a function to reuse that block of code anywhere you need it instead of duplicating effort by typing it each time.

**Python offers two types of functions: built-in functions that are part of the standard library and functions you create yourself.** The standard library includes a huge number of functions you can use in your program, like print(). Building your own functions is how you construct capabilities that are not already present within the Python language.

**To define a function in Python, you use the keyword def, a name for the function, a set of parentheses enclosing any arguments you want to pass to the function, and a colon at the end.** The name of a function must follow these rules:

- Must not start with a number
- Must not be a reserved Python word, a built-in function (for example, print(), input(), type()), or a name that has already been used as a function or variable
- Can be any combination of the A-Z, a-z, 0-9 and the underscore (_) and dash (-)

```
def devnet():
  '''prints simple function'''
  print('Simple function')
```
Call it with ``` devnet()``` and the output will be  ```Simpe function```. Python expects an **indented portion to contain all the code that makes up the function**. Keep in mind that whitespace matters in Python. The **three single quotation marks that appear on the first line of the indented text of the function are called a docstring and can be used to describe what the function does.** You can use the built-in Python function **help()** to learn what a function does and any methods that can be used:
```
>>> help(devnet)
Help on function devnet in module __main__:

devnet()
   prints simple function
```




## Classes

## Modules
