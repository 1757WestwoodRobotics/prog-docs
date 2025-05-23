# Set

## TODO: write more than just learnxinyminutes
```py
# Sets store ... well sets
empty_set = set()
# Initialize a set with a bunch of values.
some_set = {1, 1, 2, 2, 3, 4}  # some_set is now {1, 2, 3, 4}
print(some_set) # {1,2,3,4}
```

```py
# Similar to keys of a dictionary, elements of a set have to be immutable.
invalid_set = {[1], 1}  # => Raises a TypeError: unhashable type: 'list'
valid_set = {(1,), 1}
```

```py
# Add one more item to the set
filled_set = {1,2,3,4}
filled_set.add(5)  # filled_set is now {1, 2, 3, 4, 5}
print(filled_set)
# Sets do not have duplicate elements
filled_set.add(5)  # it remains as before {1, 2, 3, 4, 5}
print(filled_set)
```

```py
filled_set = {1,2,3,4,5}
# Do set intersection with &
other_set = {3, 4, 5, 6}
print(filled_set & other_set)  # => {3, 4, 5}
```

```py
filled_set = {1, 2, 3, 4, 5}
other_set = {3, 4, 5, 6}
# Do set union with |
print(filled_set | other_set)  # => {1, 2, 3, 4, 5, 6}
```

```py
# Do set difference with -
print({1, 2, 3, 4} - {2, 3, 5})  # => {1, 4}
```

```py
# Do set symmetric difference with ^
print({1, 2, 3, 4} ^ {2, 3, 5})  # => {1, 4, 5}
```

```py
# Check if set on the left is a superset of set on the right
print({1, 2} >= {1, 2, 3})  # => False
```

```py
# Check if set on the left is a subset of set on the right
print({1, 2} <= {1, 2, 3})  # => True
```

```py
some_set = {1, 2, 3, 4}
filled_set = some_set
# Check for existence in a set with in
print(2 in filled_set)   # => True
print(10 in filled_set)  # => False

# Make a one layer deep copy
print(filled_set = some_set.copy())  # filled_set is {1, 2, 3, 4, 5}
print(filled_set is some_set)        # => False
```

{{#authors lmaxwell24}}