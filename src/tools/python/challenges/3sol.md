# Solution

- Create a program that allows the user to enter a number. If the number is between 10 and 20, output “Congratulations” and if not, output “That’s too bad”
```py
number = int(input())
if number > 10 and number < 20:
	print("Congratulations")
else:
	print("That's too bad")
```
- Create a program that asks the user for a number, and prints 5 different messages depending on the number
```py
# this is just an example solution, yours may differ
number = int(input())

if number < 13:
	print("Small")
elif number < 16:
	print("smallish")
elif number < 18:
	print("old kiddo")
elif number < 21:
	print("approaching unc status")
else:
	print("Achievement unlocked: unc status")
```
- Create a program that asks the user for their name. Have at least 3 different output messages depending on what the name is
```py
# this is just an example solution, yours may differ
print("What is your name?")
name = input()

if name == "Landon Bayer":
	print("ur a pretty cool guy")
elif name == "Luke Maxwell":
	print("Ur cool... i guess")
else:
	print("No idea who you are, try again")
```


{{#authors lmaxwell24}}