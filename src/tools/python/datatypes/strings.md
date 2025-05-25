# Strings

Strings are a sequence of alphanumeric and ascii characters.

```py
# Strings are created with " or '
print("This is a string.")
print('This is also a string.')
```
```py
# Strings can be added too
print("Hello " + "world!")  # => "Hello world!"
# String literals (but not variables) can be concatenated without using '+'
print("Hello " "world!")    # => "Hello world!"
```

We can find the length of a string with the `len` keyword

```py
print(len("This is a string")) # => 16
```
---
Once we talk more about variables the following becomes really useful
```py
# Since Python 3.6, you can use f-strings or formatted string literals.
name = "Reiko"
print(f"She said her name is {name}.")  # => "She said her name is Reiko"
```

```py
# Any valid Python expression inside these braces is returned to the string.
name = "Reiko"
print(f"{name} is {len(name)} characters long.")  # => "Reiko is 5 characters long."
```

if we want to include the literal character `"` in a string, we can use the escape character `\` like the following
```py
print("these are \"quotes\" and are cool!")
```

here is a list of different characters that would need to be escaped, try them out

- `\'` single quote, if you are using `'` to quote
- `\\` the backslash character
- `\n` new line
- `\r` carriage return
- `\t` tab
- `\b` backspace
- `\f` form feed

```py
print("edit me and try some of the escape characters!")
```

Methods of strings
---

We can call a couple functions on things of `string` type

```py
# str.index(n) returns the index of the first found substring `n` in a string,
# raises a ValueError if index does not exist. (We will talk more exceptions in a later section).
str = 'robor'
print(str.index('ro')) # => 0
print(str[0])       # => r

print(str.index('bor')) # => 2
print(str[2])       # => b
```

```py
# str.isalnum() returns 'True' if characters in the string are alphanumeric
# (i.e. is a number of letter) and there is at least one character.
str1 = 'robor123'
str2 = '""'
str3 = '' # strings can have no characters! (this is an empty string)

print(str1.isalnum()) # => True
print(str2.isalnum()) # => False
print(str3.isalnum()) # => False
```

```py
# str.upper() returns returns a copy of the string with all the cased characters converted to uppercase.
str1 = 'ww1757'
print(str1.upper())) # => 'WW1757'
print(str1) # => 'ww1757'
# note the original string is unaffected as str.upper() returns a copy!
```

```py
# str.lower() returns returns a copy of the string with all the cased characters converted to lowercase.
str1 = 'WestWood1757'
print(str1.lower())) # => 'westwood1757'
print(str1) # => 'WestWood1757'
# note the original string is unaffected as str.lower() returns a copy!
```

Python has powerful string manipulation methods already built into the language. You should take advantadge of these where possible. For an exhaustive list, check out the [official Python docs](https://docs.python.org/3/library/stdtypes.html#string-methods).


After this, try out [Challenge 1!](../challenges/1.md)

{{#authors lmaxwell24,stao5}}
