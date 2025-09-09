# Static Methods

Static methods are methods that are part of a class but do not have access to the instance (`self`) or the
class (`cls`) as their first argument. They are defined using the `@staticmethod` decorator.

Think of them as regular functions that are namespaced within the class. They are used for utility functions
that are related to the class, but don't need to operate on an instance of it.

### Example

Let's say we have a `Calculator` class. We can define a static method to add two numbers. This `add` method
     doesn't need to know about any specific calculator instance.
```python
class Calculator:
    def __init__(self, brand):
        self.brand = brand

    # This is an instance method, it needs self
    def get_brand(self):
        return self.brand

    @staticmethod
    def add(x, y):
        # This is a static method, it does not receive self or cls
        return x + y

# You can call the static method directly on the class
result = Calculator.add(5, 3)
print(f"The result is: {result}") # => The result is: 8

# You can also call it on an instance, but it doesn't use the instance at all
my_calc = Calculator("Casio")
result2 = my_calc.add(10, 20)
print(f"The result is: {result2}") # => The result is: 30
```


### Classmethod vs. Staticmethod

-   A `@classmethod` receives the class (`cls`) as the first argument. It can be used to work with the class
itself, like creating instances from a different kind of input.
-   A `@staticmethod` does not receive any special first argument. It's essentially a function placed inside 
the class for organizational purposes.

{{#authors lmaxwell24}}
