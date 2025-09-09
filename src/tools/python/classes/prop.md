# The @property Decorator

Python has a built-in `@property` decorator that allows you to define methods that can be accessed like
attributes. This is useful for creating "getter" methods that don't require parentheses to be called. It's a
more "Pythonic" way to handle getting and setting attributes, especially when you want to add logic to these
actions.

Let's look at an example where we want to control access to an `_age` attribute.
```python
class Human:
    def __init__(self, name, age):
        self.name = name
        # We use a leading underscore to indicate this is a "private" attribute
        self._age = age

    @property
    def age(self):
        # This is our "getter" method for the age
        print("Getting age...")
        return self._age

# Create an instance
person = Human("Alice", 30)

# Access the age property just like an attribute
print(person.age)
```
```python
#Output:
Getting age...
30
```



### Setters

The `@property` decorator also allows us to define a "setter" method. This lets us add validation or other logic whenever an attribute's value is changed.
```python 
class Human:
    def __init__(self, name, age):
        self.name = name
        self._age = age

    @property
    def age(self):
        return self._age

    # The setter decorator is named after the property
    @age.setter
    def age(self, new_age):
        print("Setting age...")
        if new_age > 0:
            self._age = new_age
        else:
            print("Age must be positive!")

person = Human("Bob", 25)

# Use the setter by assigning a new value
person.age = 26 # => Setting age...
print(person.age) # => 26

person.age = -5 # => Setting age...
# => Age must be positive!
print(person.age) # => 26 (the age was not changed)
```


Using properties allows you to start with simple public attributes and then add getters and setters later
without changing the way the attribute is accessed from outside the class.

{{#authors lmaxwell24}}
