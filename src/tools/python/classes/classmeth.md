# Classmethods

Lets say we want to have a given method that will be shared among all instances. These methods are called `classmethods`, the are called with the class as the first argument instead of an instance of the class. 

Lets look at an example 

```py
class Human:
	# this class attribute is shared by all instances of the class
	species = "H. sapiens" 

	def __init__(self, name):
		self.name = name

	def say(self, msg):
		print(f"{self.name}: {msg}")

	@classmethod # this is called a decorator, it decorates a function or method
	def get_species(cls):
		return cls.species

i = Human(name="Ian") # just like with functions, you can have positional arguments for the __init__
i.say("Hi")            # Ian: hi
j = Human("Joel")
j.say("Hi")            # Joey: hi

i.say(i.get_species()) # Ian: H. sapiens
j.say(j.get_species()) # Joel: H. sapiens

# change the shared attribute for all classes
Human.species = "H. neanderthalensis"
i.say(i.get_species()) # Ian: H. neanderthalensis
j.say(j.get_species()) # Joel: H. neanderthalensis
```

{{#authors lmaxwell24}}