# Iterators, and list comprehension

## TODO: cleanup

```py
# We can use list comprehensions for nice maps and filters
# List comprehension stores the output as a list (which itself may be nested).
print([i + 10 for i in [1, 2, 3]])            # => [11, 12, 13]
print([x for x in [3, 4, 5, 6, 7] if x > 5])  # => [6, 7]

# You can construct set and dict comprehensions as well.
print({x for x in "abcddeef" if x not in "abc"})  # => {'d', 'e', 'f'}
print({x: x**2 for x in range(5)})                # => {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

we can use the `reversed` function to take a given `iterable` and reverse it

```py
print(list(range(5)))           # => [4,3,2,1,0]
print(list(reversed(range(5)))) # => [4,3,2,1,0]
```

{{#authors lmaxwell24}}