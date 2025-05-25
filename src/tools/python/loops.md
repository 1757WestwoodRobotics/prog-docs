# Loops


## For loop

There are instances in which we do not want to have long messy unreadable code that can result from wanting to repeat an action. 
```py
# this is bad!
print("hi")
print("hi")
print("hi")
print("hi")
print("hi")
print("hi")
```

so instead, we have ways of repeating code over and over again, we can use a loop.

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
- `range(6)` creates an iterator that goes from 0 through 5 (6 is exclusive). We will talk about the difference between an iterator and a list in a future chapter. 
	- For the purposes of a loop, all lists are iterables, but not all iterables are lists. You can't call `range(6)[0]` like you can `[1,2,3,4][0]` If you wish to treat any iterable as a list, just wrap it in a `list` function like so:

```py
a = range(6)
print(a)      # => range(0,6)
print(list(a)) # => [0,1,2,3,4,5]
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

sometimes, we may need to keep track of the index of some iterable. We can take advantage of `len()` from before to help us solve these problems:

```py
a = ["sheep", "dog", "cat", "mouse"]
# what if we wanted only the even indices?
for i in range(len(a)):
    if i % 2 == 0: # check if even
        print(a[i])
```

While Loops
---

In control flow, we may want to have something run continuously until a certain condition is met. The basic syntax of a while loop is the following:

```py, norepl
while condition:
	action
```

Just like with `for` loops and `if` statements, indentation matters for python to correctly parse it

Here is an example while loop
```py
user = ""
while user != "q":
	print("I will keep printing until you enter 'q'")
	user = input()
```
When possible, you should use `for` loops as opposed to `while` loops as Python is more optimized for the former. In cases however in which you need to check a certain condition (above) or are modifying the list/string/iterable that you are attempting to iterate through, you must use a while loop.

## Breaking loops

Some times we want to break out of a loop conditionally, we can use the `break` keyword to exit a loop halfway
```py
for i in range(5):
	print(i)
	if i == 2:
		break # prevents us from printing 3 or 4
# this code should print 0, 1, 2 on seperate lines
```

rewriting the example from the while loop section to instead use a break
```py
while True: # while true will loop forever!! 
	print("I will keep printing until you enter 'q'")
	if input() == "q":
		break
```

heres perhaps a more practical example
```py
password = "super secure"
for i in reversed(range(3)):
	if password == input():
		print("Correct!")
		break
	else:
		print("incorrect!")
		print(f"You have {i} tries left for your password")
```

in this instance, since `break` is called, the `else` statement is actually optional, because when python hits `break` it will immediately cease the loop and not let it clean up

using this knowledge we can rewrite it as the following
```py
password = "super secure"
for i in reversed(range(3)):
	if password == input():
		print("Correct!")
		break
	print("incorrect!") # note no else statement needed
	print(f"You have {i} tries left for your password")
```


### continue

we can also use the `continue` statement in order to skip execution of anything after the statement if reached

```py
for i in range(5):
	print(f"I will be reached: {i}")
	continue # will stop execution of everything after, but continue the loop
	print("I will never be reached")
```

```py
for i in range(20):
	print(i)
	if i % 2 == 0: # simple check if the number is even
		print("I'm even")
		continue
	print("I'm an odd number!")
```

## After this, try out [Challenge 4](./challenges/4.md)

{{#authors lmaxwell24,stao5}}
