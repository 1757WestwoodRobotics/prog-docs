# Loops


## For loop

There are instances in which we do not want to have long messy unreadable code. 
```py
# this is bad!
print("hi")
print("hi")
print("hi")
print("hi")
print("hi")
print("hi")
```

so instead, we have ways of repeating code over and over again

```py
for i in range(6):
	print("hi")
```

typically we want something to change a little bit in each part of the loop. the `i` in this for loop is specifying the name of a variable, so we can use it in the loop

```py
for i in range(5):
	print(i) # should print 0, 1, 2, 3, 4 all on seperate lines
```

just like in conditional statements, loops are indent sensitive, the following should produce an error

```py
for i in range(6):
print("hi") # indentation error!!!
```

---

Lets break down each part of the `for` loop
- `for` the keyword telling python we want to create a loop that iterates a fixed number of times
- `i` we are defining a variable with name `i` to run through this loop
- `in` just another part of the syntax in a `for` loop
- `range(6)` creates an iterator that goes from 0 through 5. We will talk about the difference between an iterator and a list in a future chapter. 
	- For the purposes of a loop, all lists are iterables, but not all iterables are lists. You can't call `range(6)[0]` like you can `[1,2,3,4][0]` If you wish to treat any iterable as a list, just wrap it in a `list` function like so:

```py
a = range(6)
print(a)      # => range(0,6)
print(list(a) # => [0,1,2,3,4,5]
```


since lists are iterables, we can also do the following:

```py
a = ["sheep", "dog", "cat", "mouse"]
for i in a:
	print(f"{i} is an animal")
```

note that while convention says that loop variables should be `i`, `j`, `k`, `l`, there is no reason that they can't be anything else

```py
for cool_var in range(7):
	print(f"This works! {cool_var}")
```

{{#authors lmaxwell24}}