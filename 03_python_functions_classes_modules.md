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

## Object-Oriented Programming and Python
Python was developed as a modern object-oriented programming (OOP) language. **Object-oriented programming is a computer programming paradigm that makes it possible to describe real-world things and their relationships to each other**. Unlike procedure oriented programming, where the main emphasis is on functions, object oriented programming stresses on objects. **An object is simply a collection of data (variables) and methods (functions) that act on those data.** Similarly, **a class is a blueprint for that object.**


Objects are central to Python; in fact, Python really is just a collection of objects interacting with each other. **An object is self-contained code or data** and the idea of OOP is to break up a program into smaller, easier-to-understand components. Up until now, you have mainly seen procedural programming techniques, which take a top-down approach and follow predefined sets of instructions. While this approach works well for simple programs, to write more sophisticated applications with better scalability, OOP is often the preferred method used by professional programmers. However, Python is very flexible in that you can mix and match these two approaches as you build applications.

Functions are an important part of the OOP principles of reusability and object-oriented structure. For the 200-901 DevNet Associate DEVASC exam, you need to be able to describe the benefits and techniques used in Python to build modular programs. Therefore, you need to know how to use Python classes and methods, which are covered next.

## Classes

In Python, you use classes to describe objects. Think of a **class as a tool you use to create your own data structures that contain information about something;** you can then use functions (methods) to perform operations on the data you describe. 

We can think of class as a sketch (prototype) of a house. It contains all the details about the floors, doors, windows etc. Based on these descriptions we build the house. House is the object. As many houses can be made from a house's blueprint, we can create many objects from a class. An object is also called an instance of a class and the process of creating this object is called instantiation.

Say that you want to create a class to describe a router. The first thing you have to do is define it. In Python, you define a class by using the class keyword, giving the class a name, and then closing with a colon. **Pep8 recommends capitalizing a class name to differentiate it from a variable**. 
```
class Router:
  '''Router Class'''
  def __init__(self, model, swversion, ip_add):
    '''initialize values'''
    self.model = model
    self.swversion = swversion
    self.ip_add = ip_add

rtr1 = Router('iosV', '15.6.7', '10.10.10.1')
```

After defining the class, you add a docstring to document what the class is for and then you **create a function that calls __init__, which is a special case that is used for the setup of the class.** (In __init__, the double underscores are called dunder or magic methods.) **Class functions that begin with double underscore __ are called special functions as they have special meaning.** **Functions that are within the class are called methods and become actions that you can perform on the object you are creating.**

To store attributes, you map the name **self** and the values you pass to it become variables inside the object, which then store those values as attributes. This is because, whenever an object calls its method, the object itself is passed as the first argument. In general, calling a method with a list of n arguments is equivalent to calling the corresponding function with an argument list that is created by inserting the method's object before the first argument. For these reasons, the first argument of the function in class must be the object itself. This is conventionally called self. It can be named otherwise but we highly recommend to follow the convention.
The last bit of code instantiates the object itself. Up until now, you have been creating a template, and by assigning data to the variables within the class, you have been telling Python to build the object. Now you can access any of the stored attributes of the class by using dot notation, as shown here:
```
print(rtr1.model)
'iosV'
```
**When you call rtr1.model, the interpreter displays the value assigned to the variable model within the object.**

You can also create more attributes that aren�t defined during initialization and that shows how flexible objects are, but you typically want to define any attributes as part of a class to automate object creation instead of manually assigning values. When building a class, you can instantiate as many objects as you want by just providing a new variable and passing over some data.
```
rtr1.desc = 'virtual router'

print(rtr1.desc)
'virtual router'
```

## Methods

## Modules
