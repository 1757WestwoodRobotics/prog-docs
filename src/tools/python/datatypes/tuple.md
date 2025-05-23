# Tuple

List a list, but immutable
This means that once a tuple is created, you cannot change the values of tuples.

```py
tup = (1,2,3) # tuples are made with () instead of []
print(tup[0]) # => 1
```
```py
tup = (1,2,3)
tup[0] = 3 # Raises a TypeError
```

Tuples of length one must be made with a comma

```py
print(type((1))  )  # => <class 'int'>
print(type((1,)) )  # => <class 'tuple'>
print(type(())   )  # => <class 'tuple'>
```

You can do most of the list operations on tuples as well

```py
tup = (1,2,3)
print(len(tup))         # => 3
print(tup + (4, 5, 6))  # => (1, 2, 3, 4, 5, 6)
print(tup[:2])          # => (1, 2)
print(2 in tup)         # => True
```

```py
# You can unpack tuples (or lists) into variables
a, b, c = (1, 2, 3)  # a is now 1, b is now 2 and c is now 3

# You can also do extended unpacking
a, *b, c = (1, 2, 3, 4)  # a is now 1, b is now [2, 3] and c is now 4

# Tuples are created by default if you leave out the parentheses
d, e, f = 4, 5, 6  # tuple 4, 5, 6 is unpacked into variables d, e and f

# respectively such that d = 4, e = 5 and f = 6
# Now look how easy it is to swap two values
e, d = d, e  # d is now 5 and e is now 4
```

## So why would you want to use a tuple?
To put it shortly, tuples are really good when you are using static typing, as they have specified length and types of each parameter that doesn't change, which means that

{{#authors lmaxwell24}}