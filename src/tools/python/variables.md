# Variables

We've already gotten a taste of variables from previous lessons inside datatypes, because its difficult to have good examples without them.


You can think of a variable as a "storage box" that has some kind of "type" assigned to them. Each of these boxes has a value associated with it. 

 ##### *see the previous datatype section about the different types a variable can be*

Here is how you assign a variable, or fill that "box"
```py,norepl
a = 1
```

lets break it down character by charater:
- `a`: the variable name
- `=`: this keyword is how we assign to variables. Most notably, is that it is explicitly assignment. You will learn about `==` in the next section, conditionals, but it always **sets** the left side **equal to** the right side, never the other way
- `1` the value of which we are assigning the variable `a` to

note that python doesn't care about the spacing,  so all examples below yield equivelent results
```py
a=1
a =1
a= 1
a = 1
a          =                    1
a=                       1
```

Unlike other languages, python will dynamically infer the type for a given variable. Ever since python 3.6 you can also explicitly mark the type, but at runtime it won't listen, but for programming best practices it is reccomended that you when possible assign types

```py,norepl
a: int = 1
```

this will tell your IDE that it should expect the type of `a` to be an `int` or integer. Despite explicitly being told, python will not explicitly throw any error if you set a variable to a different type at runtime

```py
a: int = 1  # set the variable a to be an int with value 1
print(a)    # => 1
a = "hi"    # change the value and of `a` at runtime
print(a)    # => hi
```

It is good code practice to have types be static as it helps significantly with the debugging process

---

As mentioned before, the equals sign is explicitly assignment

```py
a = 2      # create variable a with value 2
a = a + 1  # lets set a to 1 + itself
print(a)   # => 3
```

for most basic arithmetic operations `+`, `-`, `*` and `/`, we can do the following substitution:

```py
a = 5
a = a + 2
a = a - 2
a = a * 5
a = a / 2.5
```
is the same as
```py
a = 5
a += 2
a -= 2
a *= 5
a /= 2.5
```

it even works for the modulo (`%`) operation!

```py
a = 49
b = 49
print(a,b)  # => 49 49
a %= 5
b %= 5
print(a,b)  # => 4 4
```

---

We can assign multiple variables at once

```py
a, b = 1, 2 # multi assignment
print(a)    # => a
print(b)    # => b
```

{{#authors lmaxwell24}}