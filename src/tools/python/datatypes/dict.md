## Dictionaries
# TODO: CLEANUP

```py
# Dictionaries store mappings from keys to values
empty_dict = {}
# Here is a prefilled dictionary
filled_dict = {"one": 1, "two": 2, "three": 3}
print(filled_dict)
```

> **Note:** keys for dictionaries have to be immutable types. This is to ensure that
 the key can be converted to a constant hash value for quick look-ups.
> 
> Immutable types include `int`s, `float`s, `string`s, `tuple`s.
```py
invalid_dict = {[1,2,3]: "123"}  # => Yield a TypeError: unhashable type: 'list'
valid_dict = {(1,2,3):[1,2,3]}   # Values can be of any type, however.
```

```py
filled_dict = {"one": 1, "two": 2, "three": 3}
# Look up values with []
print(filled_dict["one"])  # => 1
```

 Get all keys as an iterable with `keys()`. We need to wrap the call in `list()`
 to turn it into a list. We'll talk about those later.  
 
 > **Note:**  for Python
 versions <3.7, dictionary key ordering is not guaranteed. Your results might
 not match the example below exactly. However, as of Python 3.7, dictionary
 items maintain the order at which they are inserted into the dictionary.
```py
filled_dict = {"one": 1, "two": 2, "three": 3}
print(list(filled_dict.keys()))  # => ["three", "two", "one"] in Python <3.7
                                 # => ["one", "two", "three"] in Python 3.7+
```


Get all values as an iterable with `values()`. Once again we need to wrap it
 in `list()` to get it out of the iterable. 
 > **Note:** Same as above regarding key
 ordering.
```py
filled_dict = {"one": 1, "two": 2, "three": 3}
print(list(filled_dict.values()))  # => [3, 2, 1]  in Python <3.7
                                   # => [1, 2, 3] in Python 3.7+

```

 Check for existence of keys in a dictionary with `in`
 
```py
filled_dict = {"one": 1, "two": 2, "three": 3}
print("one" in filled_dict)  # => True
print(1 in filled_dict)      # => False
```

Looking up a non-existing key is a `KeyError`

```py
filled_dict = {"one": 1, "two": 2, "three": 3}
print(filled_dict["four"])  # KeyError
```

Use `get()` method to avoid the `KeyError`

```py
filled_dict = {"one": 1, "two": 2, "three": 3}
print(filled_dict.get("one"))      # => 1
print(filled_dict.get("four"))     # => None

# The get method supports a default argument when the value is missing
print(filled_dict.get("one", 4))   # => 1
print(filled_dict.get("four", 4))  # => 4
```

`setdefault()` inserts into a dictionary only if the given key isn't present
```py
filled_dict = {"one": 1, "two": 2, "three": 3}

filled_dict.setdefault("five", 5)  # filled_dict["five"] is set to 5
print(filled_dict["five"])

filled_dict.setdefault("five", 6)  # filled_dict["five"] is still 5
print(filled_dict["five"])
```

Adding to a dictionary
```py
filled_dict = {"one": 1, "two": 2, "three": 3, "five": 5}
print(filled_dict)

filled_dict.update({"four":4})  # => {"one": 1, "two": 2, "three": 3, "four": 4}
print(filled_dict)

filled_dict["four"] = 4         # another way to add to dict
print(filled_dict)
```

```py
filled_dict = {"one": 1, "two": 2, "three": 3}

# Remove keys from a dictionary with del
del filled_dict["one"]  # Removes the key "one" from filled dict
print(filled_dict)

# From Python 3.5 you can also use the additional unpacking options
print({"a": 1, **{"b": 2}})  # => {'a': 1, 'b': 2}
print({"a": 1, **{"a": 2}})  # => {'a': 2}

```


{{#authors lmaxwell24}}