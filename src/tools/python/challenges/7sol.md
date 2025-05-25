# Solution

## Problem 1: The `Dog` Class

```python
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed

    def bark(self):
        print("Woof!")

# Create an instance
my_dog = Dog("Fido", "Golden Retriever")
my_dog.bark()
```

## Problem 2: The `Car` Class

```python
class Car:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year

    @property
    def description(self):
        return f"{self.year} {self.make} {self.model}"

# Create an instance
my_car = Car("Honda", "Civic", 2023)
print(my_car.description)
```

## Problem 3: Inheritance

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

class Student(Person):
    def __init__(self, name, age, student_id):
        super().__init__(name, age)
        self.student_id = student_id

# Create an instance
student = Student("Alice", 20, "s12345")
print(f"Name: {student.name}, Age: {student.age}, ID: {student.student_id}")
```

{{#authors lmaxwell24}}
