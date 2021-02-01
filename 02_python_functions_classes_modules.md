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

### Arguments and parameters

An **argument is some value (or multiple values) that you pass to a function** when you call the function within code. Arguments allow a function to produce different results and make code reuse possible. You simply place arguments within the parentheses after a function name. Each function must define how it will use arguments, using parameters to identify what gets passed in and how it gets used. **A parameter is simply a variable that is used in a function definition** that allows code within the function to use the data passed to it. To get results back from the function, you use the keyword **return** and the object you want to pass back.

```
def sub(arg1, arg2):
  result = arg1 - arg2
  return result

print(sub(10, 15))
-5
```
The variable **result** is local, meaning that it is not accessible to the main Python script, and it is used only within the function itself. You can, however, access global variables from within the function; you might do this, to set certain constants or key variables that any function can use (for example, IP addresses). The difference in **accessibility between a local variable and global variable is important**, because they allow your code to maintain separation and can keep your functions self-contained.

The previous example uses **positional arguments, which must be passed to a function in a particular order**. Positional arguments work with a simple set of consistently applied arguments, but if a function needs more **flexible alignment to parameters within a function, you can use keyword arguments** instead. A **keyword argument is a name/value pair that you pass to a function**. Instead of using position, you specify the argument the function uses. It is a lot like assigning a variable to an argument. In the previous example, arg1 is subtracted from arg2, and if the positions of these arguments were switched, you would get a different result when subtracting the values. 
```
print((sub(arg2=15, arg1=10))
...
-5
```
### \*args and \*\*kwaargs
In Python, we can pass a variable number of arguments to a function using special symbols. There are two special symbols:
- \*args (Non Keyword Arguments)
- \*\*kwargs (Keyword Arguments)
If you don't know the total number of arguments that are being passed to a function Python allows you to use **\*** and **\*\*** (often referred to as **\*args and \*\*kwargs**) to define any number of arguments or keyword arguments. * and ** allow you to iterate through a list or other collection of data.

#### \*args
Python passes variable length non keyword(positional) argument to function using *args.
```
def hello(*args):
  for arg in args:
    print("Hello", arg, "!")

hello('Caleb', 'Sydney', 'Savannah')
Hello Caleb !
Hello Sydney !
Hello Savannah !
```
You’re no longer passing a list to hello(). Instead, you’re passing three **different positional arguments**. hello() takes all the parameters that are provided in the input and **packs them all into a single iterable object named *args***. ***Note that args is just a name. You’re not required to use the name args***. The function still works, even if you pass the iterable object as **names** instead of args. All that matters here is that you use the **unpacking operator (\*)**.
```
def hello(*names):
  for name in names:
    print("Hello", name, "!")

hello('Caleb', 'Sydney', 'Savannah')
Hello Caleb !
Hello Sydney !
Hello Savannah !
```
**The iterable object you’ll get using the unpacking operator \* is not a list but a tuple(lists are mutable, while tuples are not).**

#### \*\*kwaargs

\*\*kwargs works just like *args, but instead of accepting positional arguments **it accepts keyword (or named) arguments**. Like args, kwargs is just a name that can be changed to whatever you want. Again, what is important here is the use of the **unpacking operator (\*\*)**
```
def hello(**kwargs):
  for key, value in kwargs.items():
    print("Hello", value, "!")

hello(kwarg1='Caleb', kwarg2='Sydney', kwarg3='Savannah')
Hello Caleb !
Hello Sydney !
Hello Savannah !
```

You can also supply a default value argument in case you have an empty value to send to a function. By defining a function with an assigned key value, you can prevent an error. If the value in the function definition is not supplied, Python uses the default, and if it is supplied, Python uses what is supplied when the function is called and then ignores the default value. 
```
def greeting(name, message="Good morning!"):
  print("Hello", name + ', ' + message)
...
greeting('Caleb')
Hello Caleb, Good morning!
...
greeting('Sydney', "How are you?")
Hello Sydney, How are you?
```

## Classes

## Modules
