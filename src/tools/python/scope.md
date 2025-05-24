# Variable Scope

Variables have a different given "scope" that they are valid in. Each function has their own scope. Python scopes things explicitly different in functions. Within conditionals and loops it has access to the parent scope.

```py
x = 5
def set_x(num):
	x = num # this x here is not the same as global var x
	print(x)

print(x)  # => 5
set_x(43) # prints 43, set in local scope
print(x)  # => still 5
```

If we want to control a variable in the global scope, we can use the `global` keyword

Note: please refrain from doing this. On 1757 we typically reject code with the `global` keyword

```py
x = 5
def set_global_x(num):
    # global indicates that particular var lives in the global scope
    global x
    print(x)   # => 5
    x = num    # global var x is now set to 6
    print(x)   # => 6

print(x)
set_global_x(43)
print(x) # retains its scope
```

{{#authors lmaxwell24}}