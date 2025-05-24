# Advanced functions

## args
 You can define functions that take a variable number of
 positional arguments, it will take it as a tuple, since you cannot modify the arguments you are passed
 
```py
def varargs(*args): # note the *
    return args

result = varargs(1, 2, 3)  # => (1, 2, 3)
print(result)
```

## kwargs
 You can define functions that take a variable number of
 keyword arguments, as well
 
```py
def keyword_args(**kwargs): # note the **
    return kwargs

# Let's call it to see what happens
result = keyword_args(big="foot", loch="ness")  # => {"big": "foot", "loch": "ness"}
print(result)
```

### You can do both at once, if you like

```py
def all_the_args(*args, **kwargs):
    print(args)
    print(kwargs)
"""
all_the_args(1, 2, a=3, b=4) prints:
    (1, 2)
    {"a": 3, "b": 4}
"""
all_the_args(1, 2, a=3, b=4)
```


When calling functions, you can do the opposite of `args` / `kwargs`, using `*` to expand tuples and `**` to expand dictionaries

```py
def all_the_args(*args, **kwargs):
    print(args)
    print(kwargs)
	
args = (1, 2, 3, 4)
kwargs = {"a": 3, "b": 4}
all_the_args(*args)            # equivalent: all_the_args(1, 2, 3, 4)
all_the_args(**kwargs)         # equivalent: all_the_args(a=3, b=4)
all_the_args(*args, **kwargs)  # equivalent: all_the_args(1, 2, 3, 4, a=3, b=4)
```


## first class functions

Python has first class functions. What this means is that we can actually create functions that return other functions

```py
def create_adder(x):
    def adder(y):    # we are making a function, inside of a function!
        return x + y # this will "take" the x variable from the scope above it
    return adder

add_10 = create_adder(10)
print(add_10(3))   # => 13
```

The act of "taking" a variable from an existing scope is called a closure function

## nonlocal

we can use the `nonlocal` keyword to work with variables in nested scope which shouldn't be declared in the inner functions
```py
def create_avg():
    total = 0
    count = 0
    def avg(n):
        nonlocal total, count
        total += n
        count += 1
        return total/count
    return avg
	
avg = create_avg()
print(avg(3))  # => 3.0
print(avg(5))  # (3+5)/2 => 4.0
print(avg(7))  # (8+7)/3 => 5.0
```

## anonymous functions

In python we can also create what are called anonymous functions. These are functions that have no name, but can be called. To make these we use the `lambda` keyword

Lambda functions will always return whatever is after them. They are good for short functions but once you get to longer operations, it is best to declare a standard function

```py
res = (lambda x: x > 2)(3)                  # => True
print(res)
```
```py
res = (lambda x, y: x ** 2 + y ** 2)(2, 1)  # => 5
print(res)
```

despite being anonymous functions, we can assign them to variables

```py
greater_two = lambda x: x > 2
print(greater_two(3)) # => True
```

Anonymous functions may seem useless, but have good properties relating to higher order actions. 

## Basic functional programming

```py
# there are built-in higher order functions like `map`
add_10 = lambda x: x + 10

comp = list(map(add_10, [1,2,3])) # apply a function to every value of an iterable
print(comp) # => [11, 12, 13]
```

```py
# the `max` function takes the greater of 2 variables

res = list(map(max, [1,2,3], [4,2,1])) 
print(res) # => [4, 2, 3]
```

since we can pass the anonymous functions directly in, we can replace one of the above examples with a single line!

```py
print(list(map((lambda x: x+10), [1,2,3]))) # => [11, 12, 13]
```

`filter` can take a list and trim it down based on a conditional function that takes each element and returns a boolean

```py
res = list(filter(lambda x: x > 5, [3, 4, 5, 6, 7]))  # => [6, 7]
print(res)                                            # 3,4 and 5 are not > 5
```

{{#authors lmaxwell24}}