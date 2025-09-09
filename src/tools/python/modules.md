# Modules and Imports

As your programs get larger, it's good practice to split your code into multiple files. In Python, each file is considered a "module". You can use the `import` statement to use functions, classes, and variables from one module in another.

### Basic Import

Let's say you have a file named `my_math.py`:
```python
# my_math.py
def add(a, b):
    return a + b

PI = 3.14159
```

You can import this module in another file, like `main.py`, to use its contents.

```python
# main.py
import my_math

result = my_math.add(5, 3)
print(result) # => 8

print(my_math.PI) # => 3.14159
```

### Specific Imports

You can also import specific functions or variables from a module using the `from` keyword.

```python
from my_math import add, PI

result = add(10, 20)
print(result) # => 30

print(PI) # => 3.14159
```

You can also use `*` to import everything, but this is generally discouraged as it can lead to naming conflicts.
```python
from my_math import *
```

### Aliasing

You can rename a module or an imported function using the `as` keyword. This is useful for shortening long names or avoiding conflicts.

```python
import my_math as mm
from my_math import add as addition

result = mm.add(2, 2)
print(result) # => 4

result2 = addition(1, 1)
print(result2) # => 2
```

### The `if __name__ == "__main__"` block

Sometimes you want to have code in a file that runs only when that file is executed directly, not when it's imported as a module. You can do this by placing that code inside an `if __name__ == "__main__"` block.

When you run a Python file directly, Python sets the special variable `__name__` for that file to `"__main__"`. When the file is imported, `__name__` is set to the module's name (the filename).

```python
# my_math.py
def add(a, b):
    return a + b

# This code will only run when my_math.py is executed directly
if __name__ == "__main__":
    print("Running my_math.py as a script!")
    print(add(10, 5))
```

If you run `python my_math.py`, it will print:
```
Running my_math.py as a script!
15
```

If you import it from `main.py`, that block will not run.

{{#authors lmaxwell24}}
