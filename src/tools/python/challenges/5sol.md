# Solution

## Basic challenges

- Create a function that takes in a number as a parameter, and returns double the number
	- Test the function by asking the user for a number, running that number through the function, then printing the result
```py
def double_num(num):
	return 2 * num

# testing the function
print("Enter a number")
user_number = int(input())

result = double_num(user_number)
print(result)
```
- Create a function that takes in two numbers and returns the sum of those two numbers
	- Test the function by asking the user for two numbers, running those numbers through the function, then printing the result
```py
def add_numbers(x,y):
	return x + y

print("enter a number")
x = int(input())
print("enter another number")
y = int(input())

print(add_numbers(x,y))
```

## More advanced
- Create a function titled vowelCount that takes in a word as a parameter, then returns how many vowels are in that word
	- Test that function by allowing the user to enter a word, passing that word into the vowelCount function, then
	
```py
def vowelCount(word):
	vowel_count = 0
	for character in word:
		if character in "aeiou":
			vowel_count += 1
	return vowel_count

print("Enter a word")
user_word = input()
print(f"The total number of vowels is {vowelCount(user_word)}")
```


{{#authors lmaxwell24}}