# Boolean
Its literally, `True` or `False`, note the capitalization in python has a capital first letter, unlike other languages

Booleans are really important in cs, once we get to conditionals this becomes more apparent

```py
# negate with not
print(not True)   # => False
print(not False)  # => True
```

Woah if a boolean is `not` one thing, its the other thing!!!

```py
# Boolean Operators
# Note "and" and "or" are case-sensitive
print(True and False)  # => False
print(False or True)   # => True
```

Coming from other languages, `||` is `or` and `&&` is `and`,  it reads more like english

```py
# True and False are actually 1 and 0 but with different keywords, you can do really cursed things with this info
print(True + True)  # => 2
print(True * 8)     # => 8
print(False - 5)    # => -5
```

We'll get into comparison operations in a second, but abusing the `True is 1` and `False is 0` principle we can do some more funny things
```py
# Comparison operators look at the numerical value of True and False
print(0 == False)   # => True
print(2 > True)     # => True
print(2 == True)    # => False
print(-5 != False)  # => True
```



{{#authors lmaxwell24}}