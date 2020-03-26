# Notes and files for Python Projects

### Chapter 1 - Reviewing Core Python

`dir(name)` tells you all the names in the `name` object.<br>
`help(name)` displays information about the `name` object.

There is only one `None` object in the environment and all references to `None` use the same instance. So equality tests for `None` are usually replaced with identity tests:<br>
`var is None` instead of `var == None`

https://docs.python.org/3/library/string.html<br>
https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range<br>
https://docs.python.org/3/tutorial/datastructures.html?highlight=dictionary

#### Structuring Your Program

```
if __name__ == "__main__":
    main()
```

#### Handling Exceptions

```
try:
    A block of application code
except <an error type> as <anExceptionObject>:
    A block of error handling code
else:
    Another block of application code
finally:
    A block of clean-up code
```

`else` is executed if `try` succeeds without errors.<br>
`finally` is always executed, even if the `try/except` is left via `break` or `return`.

#### Managing Context

A runtime context typically includes a temporary resource.

You use a context manager with the `with` statement:<br>
```
with open(filename, mode) as contextName:
    process file
```

The context manager closes the file after use. Context managers can remove the need for a `try/finally` construct.

#### Interacting with Users

`print()` send data to `stdout`. `input()` read data from users.<br>
`print()` can also be used to output to files with the `file=[filename]` option.

#### Using Text Files

Once you have an open file object:<br>
`read()` reads the entire contents as a single string.<br>
`readlines()` reads line-by-line into a list.<br>
`readline()` reads the next line in the file.

The file object is an iterable so it can be used directly in a loop:<br>
```
with open(filename, mode) as fileobject:
    for line in fileobject:
        # process line
```

You can write to a fileobject with `write()` or `writelines()` methods.<br>
There is no `writeline()` method for writing a single line.

`tell()` gives the current position in the file.<br>
`seek()` goes to a specific position in the file.

#### Generator Functions

Generator functions use the `yield` keyword to return a value. Generator functions preserve their state after each run and `yield` the next value on the next invocation.
```
def odds(start=1):
    '''return all odd numbers from start'''
    if int(start) % 2 == 0: start = int(start) + 1 # make sure start is an odd number
    while True:
        yield start
        start += 2
```

Generators become iterators so you can use them in `for` loops:
```
for n in odds():
    if n > 7: break
    else: print(n)
```

#### Lambda Functions

Anonymous function blocks. Limited to a single expression.<br>
`lambda <param1, param2, ...,paramN> : <expression>`

`straight_line = lambda m,x,c: m*x+c`<br>
`straight_line(2,4,-3)`

#### Defining and Using Classes and Objects

`__new()__`: Constructor<br>
`__init()__`: Initializer<br>
`__del()__`: Destructor

Constructors are rarely used in Python unless inheriting from a built-in class.

Method definitions have a reference to the calling instance as the first parameter. Typically called `self`.<br>
```
class MyClass(object):
    instance_count = 0
    def __init__(self, value):
        self.__value = value
        MyClass.instance_count += 1
        print(f"instance No {MyClass.instance_count} created")
    def aMethod(self, aValue):
        self.__value *= aValue
    def __str__(self):
        return f"A MyClass instance with value: {self.__value}"
    def __del__(self):
        MyClass.instance_count -= 1
```

Double underscores in `value` indicate that it's meant to be private and should not be accessed directly.

`__str__()` prints a formatted string when you pass the class to the `print()` method.

`testCircle.py` uses properties within the `Circle2` class.<br>
`radius = property(None, __setRadius)` creates a write-only attribute called `radius`. The `property()` function takes arguments for read, write, and delete. This code sets `None` as the read function but the (private) `__setRadius()` method as a write function.<br>
`area()` is set as a read-only property using the `@property` decorator.

#### Using and Creating Modules

Common forms of `import`:
```
import aModule
import aModule as anAlias
import firstModule, secondModule, thirdModule...
from aModule import anObject
from aModule import anObject as anAlias
from aModule import firstObject,secondObject, thirdObject...
from aModule import *
```

The `from...` forms are used to only import specified names and avoid naming conflicts.

Top-level code that runs every time it's imported should be avoided in modules, except for necessary variable initialization.<br>
Code to be re-used should be packaged as functions or classes.

To control visibility of module objects, prefix with `_` so the object won't be imported with any `from x import *` statements.<br>
Explicity listing the names of the objects to be visibile in the `__all__` variable is the preferred method.

#### Using and Creating Packages

A package is just a folder with a file named `__init__.py`. All other files in the folder are the modules of the package.<br>
`__init__.py` can be empty which will make all modules in the directory accessible. Or it can contain an `__all__` list to control which modules are visible.

`import os.path` makes the entire `os` package visible along with the `path` submodule.<br>
`import os.path as pth` only exposes `os.path`.

The `bitwise` directory contains a sample package.
