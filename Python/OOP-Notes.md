# Object-Oriented Programming (OOP) in Python

These notes explain OOP using definitions, syntax, examples, and practice questions.

## 1. What Is OOP?

**Object-Oriented Programming (OOP)** organizes code around **classes** and **objects**. A class defines attributes (data) and methods (behavior); an object is an instance of a class.

The four commonly discussed pillars are:
- **Encapsulation:** bundling data and related methods and controlling access to internal state.
- **Inheritance:** creating a class based on another class.
- **Polymorphism:** allowing different objects to respond to a common interface in different ways.
- **Abstraction:** exposing essential behavior while hiding implementation details.

## 2. Classes and Objects

```python
class Student:
    def study(self):
        print("Student is studying")

student1 = Student()
student1.study()
```

A class is a blueprint; `student1` is an object created from that class.

## 3. Constructor: `__init__()`

`__init__()` is an initializer that Python calls when a new object is created. It is commonly used to set initial attributes.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

student = Student("Asha", 21)
print(student.name)  # Asha
print(student.age)   # 21
```

## 4. The `self` Parameter

`self` refers to the current instance. It allows instance methods to access that object's attributes and other methods. It is a conventional parameter name, not a Python keyword.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def introduce(self):
        print(f"My name is {self.name}")

Student("Ravi").introduce()
```

## 5. Instance Variables and Class Variables

- **Instance variables** belong to a particular object and are commonly assigned using `self`.
- **Class variables** are defined in the class body and are shared through the class unless shadowed by an instance.

```python
class Employee:
    company = "ABC Ltd"  # class variable

    def __init__(self, name, salary):
        self.name = name       # instance variable
        self.salary = salary   # instance variable

emp1 = Employee("Asha", 30000)
emp2 = Employee("Ravi", 35000)
print(Employee.company)
print(emp1.name, emp2.name)
```

## 6. Types of Methods

### Instance method
Works with an instance and takes `self`.

```python
class Demo:
    def show(self):
        return "Instance method"
```

### Class method
Receives the class as `cls` and uses `@classmethod`.

```python
class Employee:
    company = "ABC Ltd"

    @classmethod
    def change_company(cls, name):
        cls.company = name

Employee.change_company("XYZ Ltd")
```

### Static method
Does not receive an automatic instance or class argument. Use `@staticmethod` for a related utility function.

```python
class Calculator:
    @staticmethod
    def add(a, b):
        return a + b

print(Calculator.add(5, 3))
```

## 7. Inheritance

**Inheritance** lets a child class reuse or extend a parent class.

```python
class Animal:
    def eat(self):
        print("Eating")

class Dog(Animal):
    def bark(self):
        print("Barking")

dog = Dog()
dog.eat()   # inherited
dog.bark()
```

Common forms:
- **Single:** one child, one parent.
- **Multiple:** one child inherits from multiple parents.
- **Multilevel:** a class inherits from a derived class.
- **Hierarchical:** multiple children inherit from one parent.
- **Hybrid:** a combination of patterns.

## 8. `super()`

`super()` accesses methods in the next class in the method resolution order. It is commonly used to initialize parent-class state.

```python
class Person:
    def __init__(self, name):
        self.name = name

class Student(Person):
    def __init__(self, name, roll_no):
        super().__init__(name)
        self.roll_no = roll_no

s = Student("Mina", 101)
print(s.name, s.roll_no)
```

## 9. Polymorphism and Method Overriding

**Polymorphism** means different object types can be used through a common interface. **Method overriding** happens when a child class provides its own implementation of an inherited method.

```python
class Animal:
    def sound(self):
        print("Animal sound")

class Dog(Animal):
    def sound(self):
        print("Dog barks")

class Cat(Animal):
    def sound(self):
        print("Cat meows")

for animal in [Dog(), Cat()]:
    animal.sound()
```

Python also supports duck typing: code can work with different objects if they provide the expected methods or behavior.

## 10. Encapsulation

**Encapsulation** bundles data and methods and provides controlled ways to interact with an object's state.

Python naming conventions:
- `name`: public.
- `_name`: non-public by convention.
- `__name`: name-mangled to reduce accidental name clashes; not truly private or secure.

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def get_balance(self):
        return self.__balance

account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())  # 1500
```

## 11. Getters, Setters, and `@property`

A property allows controlled attribute access using attribute-style syntax.

```python
class Student:
    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        if value < 0:
            raise ValueError("Age cannot be negative")
        self._age = value

student = Student(20)
student.age = 21
print(student.age)
```

## 12. Abstraction

**Abstraction** exposes what an object can do while hiding implementation details. Python supports abstract base classes through the `abc` module.

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width

print(Rectangle(5, 3).area())  # 15
```

A class with unimplemented abstract methods cannot be instantiated until a concrete subclass implements them.

## 13. Special (Dunder) Methods

Special methods have names beginning and ending with double underscores. They define how objects interact with built-in operations.

```python
class Book:
    def __init__(self, title):
        self.title = title

    def __str__(self):
        return self.title

print(Book("Python Basics"))
```

Other examples include `__repr__()`, `__len__()`, and `__eq__()`.

## 14. Composition

**Composition** builds a class using objects of other classes. It models a "has-a" relationship and can be an alternative to inheritance.

```python
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()
        print("Car is ready")

Car().start()
```

## 15. Inheritance vs. Composition

| Inheritance | Composition |
|---|---|
| Models an "is-a" relationship. | Models a "has-a" relationship. |
| Child reuses or specializes parent behavior. | One object uses another object. |
| Can create tightly coupled hierarchies. | Often allows flexible components. |

## 16. Common OOP Interview Questions

1. What is the difference between a class and an object?
2. What is the purpose of `__init__()`?
3. What does `self` represent?
4. Compare class and instance variables.
5. Compare instance, class, and static methods.
6. What is inheritance? Name its common forms.
7. What does `super()` do?
8. What is method overriding?
9. Explain polymorphism with an example.
10. What is encapsulation? Is a double-underscore attribute truly private?
11. What is abstraction? What does `@abstractmethod` do?
12. Compare inheritance and composition.

## 17. Practice Problems

1. Create a `Student` class with name, roll number, and a display method.
2. Create a `BankAccount` class with deposit, withdraw, and balance methods.
3. Create a `Vehicle` parent class and `Car` and `Bike` child classes.
4. Count created employees using a class variable.
5. Demonstrate overriding with `Animal`, `Dog`, and `Cat`.
6. Write a class method that changes a shared class attribute.
7. Write a static method that checks whether a number is even.
8. Create an abstract `Shape` class with `Circle` and `Rectangle`.
9. Use `@property` to validate a person's age.
10. Create a `Car` containing an `Engine` object.

## 18. Quick Reference

| Concept | Syntax |
|---|---|
| Class | `class Student:` |
| Create object | `student = Student()` |
| Initializer | `def __init__(self, ...):` |
| Instance method | `def method(self):` |
| Class method | `@classmethod` |
| Static method | `@staticmethod` |
| Inheritance | `class Child(Parent):` |
| Parent behavior | `super()` |
| Property | `@property` |
| Abstract class | `class Shape(ABC):` |
| Abstract method | `@abstractmethod` |
| String representation | `def __str__(self):` |

## 19. Recommended Learning Order

1. Class and object
2. `__init__()` and `self`
3. Instance and class variables
4. Instance, class, and static methods
5. Inheritance and `super()`
6. Overriding and polymorphism
7. Encapsulation and properties
8. Abstraction
9. Dunder methods
10. Composition

Write each example yourself, change its values, and then solve the practice problems without looking at the notes.
