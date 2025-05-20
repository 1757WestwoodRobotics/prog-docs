# Strings

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

