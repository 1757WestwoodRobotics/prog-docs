# Values and Expressions

Here is some basic Python terminology regarding data in the language.

### Values
---

In Python, we represent data using *values*. These are encodings that Python recgonizes as representing some type of data. Here are some examples of different values in python:

`5, 3.7, 'a', 'Hello World!, True, [1,2,3,4]`

### Expressions
---

We can chain values together with *operators* (functions that can be performed on values) to create *expressions*. Here are a few examples:

```py
1 + 1 # evaluates to 2

2 - 3 + 7 + (8 // 2) # evaluates to 10

4 ** 3 # evaluates to 256

True or False # evaluates to True

True and False # evaluates to False

not True # evaluates to False

'Hello' + ' ' + 'World!' # evaluates to 'Hello World!'

'Hello' # evaluates to 'Hello'
```

When given an expression, Python will evaluate it (i.e. perform operatorations according to their order/precdence) into a value. An expression that evaluates to itself is what is known as a *literal*. 

```py
5 # evaluates to 5. This expression *literally* means exactly what is written: 5

'robot' # evaluates to 'robot'. Again, this expression is literally what it means

2 + 2 # evaluates to 4. This is NOT a literal as it isn't *literally* what is written.
```
{{#authors stao5}}