# Solution

## While loops

- Create a program that allows the user to continuously enter a word, prints the last letter of the word, and the program only ends once they type the word “end”

```py
while True:
	print("Enter a word")
	word = input()
	print(word[-1])

	if word == "end":
		break
```

- Create a program that allows the user to enter a number. Then, a segment of code containing a print statement is repeated their number amount of times, using a while loop

```py
print("Enter a number!")
user_number = int(input())

while user_number > 0:
	print("Hello!")
	user_number -= 1
```

---

## For Loops


- Create a program that allows the user to enter a word, and prints each vowel in the world

```py
print("Enter a word:")
word = input()
for character in word:
	if character in ["a", "e", "i", "o", "u"]:
		print(character)
```
alt solution
```py
print("Enter a word:")
word = input()
for character in word:
	if character == "a" or character == "e" or character == "i" or character == "o" or character == "u":
		print(character)
```

- Then alter the program to print how many vowels are in the word

```py
print("Enter a word:")
word = input()
vowel_count = 0
for character in word:
	if character in ["a", "e", "i", "o", "u"]:
		vowel_count += 1

print(f"Total vowel count: {vowel_count}")
```

alt solution

```py
print("Enter a word:")
word = input()
vowel_count = 0
for character in word:
	if character == "a" or character == "e" or character == "i" or character == "o" or character == "u":
		vowel_count += 1

print(f"Total vowel count: {vowel_count}")
```

{{#authors lmaxwell24}}