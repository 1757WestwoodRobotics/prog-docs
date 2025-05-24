# Methods vs functions

To put it simply, methods are functions that run on classes. For instance methods (which is what this section is covering) they call upon the instance of the class. In the next section we'll learn about what that means


```py
class Bird:
	def __init__(self, call: str) -> None: # I am specifying that call should be of type string, and that __init__ should return nothing, or type None
		print(f"Setting up bird with call {call}")
		self.call = call

	def tweet(self) -> None:
		print(self.call)

	def getCall(self) -> str: # specifying it should return a string
		return self.call
		
```




{{#authors lmaxwell24}}