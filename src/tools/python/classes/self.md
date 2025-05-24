# the self keyword

What does `instance` really mean?

When python goes to create the `Human` class in the first class example, it allocates a new generic `object` that all classes inherit from. This defines some basic behavior by default, but now we don't have the `Human` class we are working with, we have this new `object` to work on. That is what `self` represents in each method

```py
class Brain:
	iq: int
	def __init__(self, iq: int) -> None:
		self.iq = iq

	def compareIq(self, other) -> None:
		print(f"Comparing to {other}")
		return self.iq - other.iq
		
class Human:
	name: str    # we can specify what type we expect instance variables to be
    def __init__(self, name, iq): # type decorators are optional, but encouraged
        self.name = name       # note that `self.name` and `name` are two diffirent objects
		self.brain = Brain(iq) # you can have instance variables of other classes

    def say(self, msg):
        print("{name}: {message}".format(name=self.name, message=msg))

    def sing(self):
        return "yo... yo... microphone check... one two... one two..."

	def smarterThan(self, other) -> bool:
		return self.brain.compareIq(other.brain) > 0

	def changeName(self, name):
		self.name = name


bob = Human("Bob", 100) 

bob.say("hi!")     
bob.sing()         

bob.changeName("Billy")
bob.say("I go by Billy now")

james = Human("James", 150)
james.say("Hi Billy")

print(james.smarterThan(bob)) # => True
```

{{#authors lmaxwell24}}