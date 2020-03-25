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

