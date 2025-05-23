# Conditionals

## Comparison

Lets first begin by being able to check objects, there are a couple of ways to do this

```py
#Equality is ==
print(1 == 1)  # => True
print(2 == 1)  # => False
```

```py
# Inequality is !=
print(1 != 1)  # => False
print(2 != 1)  # => True
```

```py
# More comparisons
print(1 < 10)  # => True
print(1 > 10)  # => False
print(2 <= 2)  # => True
print(2 >= 2)  # => True
```

```py
# Seeing whether a value is in a range
print(1 < 2 and 2 < 3)  # => True
print(2 < 3 and 3 < 2)  # => False
```

```py
# Chaining makes this look nicer
print(1 < 2 < 3)  # => True
print(2 < 3 < 2)  # => False
```

We can run this on variables as well

```py
a = 5
print(a == 5) # => True
print(a < 3)  # => False
print(2 < a)  # => True
```

since everything on both the right and left side are treated as independent expressions, 

 (`is` vs. `==`) is checks if two variables refer to the same object, but `==` checks
if the objects pointed to have the same values.

```py
a = [1, 2, 3, 4]  # Point a at a new list, [1, 2, 3, 4]
b = a             # Point b at what a is pointing to
print(b is a)     # => True, a and b refer to the same object
print(b == a)     # => True, a's and b's objects are equal
b = [1, 2, 3, 4]  # Point b at a new list, [1, 2, 3, 4]
print(b is a)     # => False, a and b do not refer to the same object
print(b == a)     # => True, a's and b's objects are equal
```

## the "If" statement

We can have code that changes behavior based on conditions being met, to put it simply, whether there is a `True` or a `False` value present

Try out the following example
```py
# Let's just make a variable
some_var = 5

# Here is an if statement. Indentation is significant in Python!
# Convention is to use four spaces, not tabs.
# This prints "some_var is smaller than 10"
if some_var > 10:
    print("some_var is totally bigger than 10.")
elif some_var < 10:    # This elif clause is optional.
    print("some_var is smaller than 10.")
else:                  # This is optional too.
    print("some_var is indeed 10.")
```

Inside this there are three distinct blocks, an `if` block, an `elif` and an `else`

You can read the above code with the following in english:
```py,norepl
if the value "some var" is greater than ten, then print "..."
otherwise,  if the value of "some var" is less than 10, then print "..."
otherwise, print "...."
```

heres another example that python executes code from top down in ifs
```py
some_var = 5
if some_var < 10:
	print("I am less than 10")
elif some_var < 20: # despite this statement being true, the below does not run
	print("I am also less than 20")
else:
	print("I shouldn't run")
print("I am outside of the if statement, I will print")
```

the `elif` and `else` statements are completely optional in a conditional, the following are examples showing that you can have an infinite number of `elif`s, but a maximum of 1 `else` 
```py
# example using a singular `if` and nothing more
print("Give a number")
user_number = int(input()) 
# we use int() to turn the string result of input into a number

if user_number < 10:
	print("I am less than 10!")
	
print("I will always print!")
```

```py
# example using multiple `elif`s but no `else`
print("Give a number")
user_number = int(input()) 

if user_number < 10:
	print("I am less than 10!")
elif user_number < 20:
	print("I am less than 20, but more than 10!")
elif user_number < 30:
	print("in between 20 and 30!")
	
print("I will always print!")
```

```py
# example showing that the if takes only a boolean
if True:
	print("I will always print!")
else:
	print("I will never print")
```

```py
# example showing a False will never run
if False:
	print("I will never print!")
else:
	print("I will always print")
```

