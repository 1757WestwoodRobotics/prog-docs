# Exception handling

We've already been introduced to the idea of exceptions in previous lessons, lets formalize them a little more

In programming, its typical that we have systems that may have certain ways they break. For instance, you may be trying to parse data from a user as an integer, but they didn't enter it in a way we can parse, in such instances we have encountered an error and instead of terminating the program would want to continue to function through it. 

lets look an an example program that we can modify to use exceptions

```py
shopping = ["Bananas", "Tomatoes", "Potatoes", "Carrots"]
print(f"Your current shopping list is {shopping}\nWhich one would you like to query")

index = int(input())   # This can error, they don't enter an int
print(shopping[index]) # This can error, the index they selected doesn't exist 
```

We can use a `try/catch` block in order to handle different exceptions. The syntax is as follows:

```py,norepl
try:
	# code that will error
except ExceptionType as exception_var:
	# what do to if it fails
except AnotherException:
	# what to do if that is encountered
else:
	# what to do if no errors are encountered
finally:
	# what to do after the end of everything, no matter what
```

here's an example in action
```py
try:
    # Use "raise" to raise an error
    raise IndexError("This is an index error")
except IndexError as e:
    pass                 # we can use the `pass` statement to have indentation with no action
except (TypeError, NameError):
    pass                 # Multiple exceptions can be processed jointly.
else:                    # Optional clause to the try/except block. Must follow
                         # all except blocks.
    print("All good!")   # Runs only if the code in try raises no exceptions
finally:                 # Execute under all circumstances
    print("We can clean up resources here")
```

lets rewrite our first example that won't error out

```py
shopping = ["Bananas", "Tomatoes", "Potatoes", "Carrots"]
print(f"Your current shopping list is {shopping}\nWhich one would you like to query")

validInput = False
while not validInput: # we want to keep retrying 
	try:
		index = int(input())   
		print(shopping[index])
		validInput = True
	except ValueError: # an invalid int cast results in a ValueError
		print("Could not parse your input")
	except IndexError: # an invalid indexing results in an IndexError
		print("Invalid index, please try again")
```

If we don't care about the specific error and want to just catch all errors, we can use the class that both inherit from (we'll learn about what that means), `Exception`

```py
shopping = ["Bananas", "Tomatoes", "Potatoes", "Carrots"]
print(f"Your current shopping list is {shopping}\nWhich one would you like to query")

validInput = False
while not validInput: # we want to keep retrying 
	try:
		index = int(input())   
		print(shopping[index])
		validInput = True
	except Exception as e: # we're taking the exception object returned here
		print(f"The following error occured: {e}\nPlease try again")
```

{{#authors lmaxwell24}}