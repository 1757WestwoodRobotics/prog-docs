# Solution

## Problem 1
Using higher order functions list `map` and `filter`, create a function called `getDesc` that takes a `controlScheme` and returns all of its descriptions in a list. You are given sample dataset below , but are encouraged to expand and try other customized datasets.
```py
controlScheme1 = [
 {"id": 2, "button": 1, "description": "fire"}, 
 {"id": 2, "button": 2, "description": "intake"},
 {"id": 1, "button": 4, "description": "climb"},
 {"id": 3, "button": 2, "description": "fudge up"},
 {"id": 3, "button": 3, "description": "fudge down"},
]
controlScheme2 = [
 {"id": 0, "button": 1, "description": "up"},
 {"id": 0, "button": 2, "description": "left"},
 {"id": 0, "button": 3, "description": "down"},
 {"id": 0, "button": 4, "description": "right"},
 {"id": 1, "button": 1, "description": "jump"},
 {"id": 1, "button": 2, "description": "shoot"},
 {"id": 1, "button": 3, "description": "duck"},
 {"id": 1, "button": 4, "description": "run"}
]

def getDesc(controls) -> list[str]:
	return list(map((lambda x: x["description"]), controls))

print(getDesc(controlScheme1)) # test and prove it works
print(getDesc(controlScheme2))
```

## Problem 2
Like above, except expand on to return a `set` of `id`s. Note that a set enforces that there are no duplicates to the `id`. Also write a function that returns a sorted list of all the buttons. If there are duplicate buttons, keep them.

```py
controlScheme1 = [
 {"id": 2, "button": 1, "description": "fire"}, 
 {"id": 2, "button": 2, "description": "intake"},
 {"id": 1, "button": 4, "description": "climb"},
 {"id": 3, "button": 2, "description": "fudge up"},
 {"id": 3, "button": 3, "description": "fudge down"},
]
controlScheme2 = [
 {"id": 0, "button": 1, "description": "up"},
 {"id": 0, "button": 2, "description": "left"},
 {"id": 0, "button": 3, "description": "down"},
 {"id": 0, "button": 4, "description": "right"},
 {"id": 1, "button": 1, "description": "jump"},
 {"id": 1, "button": 2, "description": "shoot"},
 {"id": 1, "button": 3, "description": "duck"},
 {"id": 1, "button": 4, "description": "run"}
]

def getIds(controls) -> set[int]:
	return set(map((lambda x: x["id"]), controls))

def getButtons(controls) -> list[int]:
	mapping_function = lambda x: x["button"]
	result_list = list(map(mapping_function, controls))
	result_list.sort()
	return result_list

print(getIds(controlScheme1)) # testing
print(getIds(controlScheme2)) # testing
print(getButtons(controlScheme1)) 
print(getButtons(controlScheme2)) 
```


## Problem 3

implement a moving weighted moving average generator function. The function has type signature: `(terms: float) => ((term: float) => float)`

This means that the function should take as input a number of terms to average at most, and then that returned function should take an argument to add to the moving average, and return the moving average.


```py
def movingGenerator(terms: float):
	moving_list = []
	def average(term: float):
		nonlocal moving_list
		moving_list.append(term)
		if len(moving_list) > terms:
			moving_list.remove(0)
		total = 0
		for i in moving_list:
			total += i
			
		return total / len(moving_list)
		
	return average

avg5 = movingGenerator(5)
print(avg5(1)) # => 1
print(avg5(3)) # => 2
for i in range(7):
	print(avg5(i)) # should print out 1.33, 1.25, 1.4, 1.8, 2.0, 3.0, 4.0
```

using [`collections.deque`](https://docs.python.org/3/library/collections.html#collections.deque) which is a datastructure that is beyond the scope of this course we can actually simplify this problem

```py
from collections import deque # we'll learn about module imports later

def movingGenerator(terms: float):
	moving_list = deque(maxlen=terms)
	def average(term: float):
		nonlocal moving_list
		moving_list.append(term)
		total = 0
		for i in moving_list:
			total += i
			
		return total / len(moving_list)
		
	return average

avg5 = movingGenerator(5)
print(avg5(1)) # => 1
print(avg5(3)) # => 2
for i in range(7):
	print(avg5(i)) # should print out 1.33, 1.25, 1.4, 1.8, 2.0, 3.0, 4.0
```


{{#authors lmaxwell24}}