# Functions

Functions are the same as they were in math. They take some input and return some output. 

There are two types of functions:
- "Pure" functions: they take input and then return output, they have no side effects
- "Impure" functions: they can take input, but also change the variables passed to input

Lets look at function syntax in python:
```py
# we use the `def` keyword to specify and create functions
def add(x,y):
    print("x is {} and y is {}".format(x, y)) # .format is another way of doing f-strings
    return x + y  # Return values with a return statement

print(add(5,6)) # note that this both runs the function and prints its result
```

lets break down each part of the statement:
- `def` tells python that we want to create a new function
- `add` is the name of this function we are creating
- `x` and `y` are arguments in this function
	- arguments are things the function can take as input and work with. They are their own variables that get passed from whatever calls the function
- `return` tells python to stop executing code, and instead *return* the following value to whatever called the function

when we do `add(5, 6)` python will take `5` and assign it to `x` and then `6` and assign it to `y` 

```py
# we can also call functions with keyword arguments
def add(x, y):
    print("x is {} and y is {}".format(x, y))
    return x + y  

result = add(y=6, x=5) # keyword arguments can arrive in any order
print(result)
```

functions can also include no arguments

```py
def say_hi():
	print("Hi!")

say_hi()
```

## Returning multiple values (with tuple assignments)
```py
def swap(x, y):
    return y, x  # Return multiple values as a tuple without the parenthesis.
                 # (Note: parenthesis have been excluded but can be included)

x = 1
y = 2
x, y = swap(x, y)     # => x = 2, y = 1
# (x, y) = swap(x,y)  # Again the use of parenthesis is optional.
print(x,y)
```

{{#authors lmaxwell24}}