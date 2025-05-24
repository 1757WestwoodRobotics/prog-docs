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
After this, try out [Challenge 1!](../challenges/1.md)

{{#authors lmaxwell24}}