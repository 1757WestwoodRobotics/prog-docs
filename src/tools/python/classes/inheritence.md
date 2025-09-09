# Inheritance

Inheritance is a way to form new classes using classes that have already been defined. The new class is
called a derived class (or child class), and the one from which it inherits is called the base class (or
parent class). This allows us to reuse code and create a class hierarchy.

Let's create a `Student` class that inherits from our `Human` class.
```python
class Human:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def say(self, msg):
        print(f"{self.name}: {msg}")

#To inherit, we pass the base class as an argument to the new class

class Student(Human):
    def __init__(self, name, age, student_id):
        # Use super() to call the __init__ method of the parent class (Human)
        super().__init__(name, age)
        self.student_id = student_id # Add a new attribute for the Student class

    #We can also add new methods
    def study(self, subject):
        print(f"{self.name} is studying {subject}.")

#Create an instance of the Student class
student_jane = Student("Jane", 20, "12345")

# student_jane can use methods from the Human class
student_jane.say("Hello!") # => Jane: Hello!

# And it can use its own methods
student_jane.study("Computer Science") # => Jane is studying Computer Science.
print(f"Student ID: {student_jane.student_id}") # => Student ID: 12345

### Overriding Methods

# You can also override methods from the parent class to provide a specific implementation for the child class.
class Student(Human):
    def __init__(self, name, age, student_id):
        super().__init__(name, age)
        self.student_id = student_id

    # Override the say method from the Human class
    def say(self, msg):
        print(f"Student {self.name} says: {msg}")

student_john = Student("John", 22, "67890")
student_john.say("I have an exam tomorrow.") # => Student John says: I have an exam tomorrow.
```
{{#authors lmaxwell24}}
