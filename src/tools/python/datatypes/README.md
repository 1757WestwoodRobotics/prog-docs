# Datatypes

Python has a couple of primitive datatypes, or general structures, that you can use. A datatype or type is a set of values AND the operations that can be called upon them. The function of operators (i.e. `+`, `=`, `-`) may change depending on the type or may not be defined.

There are two categories of types:
- "Immutable" types: Types whose internal data cannot be changed. Includes int, bool, floats, strings, and tuples.
- "Mutable" types: Type whose internal data can be changed. Inclues lists, dictionaries, and sets.

The built-in `type()` function returns the type of a given input. 

```py
w = True
x = 5
y = 5.0
z = [5]

print(type(w)) # => <class 'bool'>
print(type(x)) # => <class 'int'>
print(type(y)) # => <class 'float'>
print(type(z)) # => <class 'list'>

```
{{#authors lmaxwell24, stao5}}