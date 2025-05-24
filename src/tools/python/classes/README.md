# Classes

Classes are higher order data structures in which we can define our own `method`s and `variable`s on

Lets look at a basic class example:

```py
# We use the "class" statement to create a class
class Human:

    # A class attribute. It is shared by all instances of this class
    species = "H. sapiens"

    # Basic initializer, this is called when this class is instantiated.
    # Note that the double leading and trailing underscores denote objects
    # or attributes that are used by Python but that live in user-controlled
    # namespaces. Methods(or objects or attributes) like: __init__, __str__,
    # __repr__ etc. are called special methods (or sometimes called dunder
    # methods). You should not invent such names on your own.
    def __init__(self, name):
        # Assign the argument to the instance's name attribute
        self.name = name

        # Initialize property
        self._age = 0   # the leading underscore indicates the "age" property is
                        # intended to be used internally
                        # do not rely on this to be enforced: it's a hint to other devs

    # An instance method. All methods take "self" as the first argument
    def say(self, msg):
        print("{name}: {message}".format(name=self.name, message=msg))

    # Another instance method
    def sing(self):
        return "yo... yo... microphone check... one two... one two..."


bob = Human("Bob") # we can create classes by calling them like functions
                   # on initialization, classes call their __init__ method 
                   # as a template for how to "build" the class

bob.say("hi!")     # just like we've done on other classes, we can call methods
bob.sing()         # these are called instance methods, since they run on 
                   # the instance of the class
```

In the next couple of sub lessons we will look at each of these parts in more depth

{{#authors lmaxwell24}}