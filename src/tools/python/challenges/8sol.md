# Solution

## Problem 1: Custom Module

```python
# greetings.py
def say_hello(name):
    return f"Hello, {name}!"
```

```python
# main.py (or the editor)
import greetings

user_name = input("What is your name? ")
message = greetings.say_hello(user_name)
print(message)
```

## Problem 2: Using the `math` module

```python
import math

radius_str = input("Enter the radius of the circle: ")
radius = float(radius_str)

area = math.pi * (radius ** 2)

print(f"The area of the circle is: {area}")
```

## Problem 3: Number Guessing Game

```python
import random

secret_number = random.randint(1, 100)

while True:
    guess_str = input("Guess a number between 1 and 100: ")
    guess = int(guess_str)

    if guess < secret_number:
        print("Too low!")
    elif guess > secret_number:
        print("Too high!")
    else:
        print("You got it! The number was", secret_number)
        break
```

{{#authors lmaxwell24}}
