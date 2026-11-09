Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Composition vs inheritance are two ways to reuse code and model relationships.
# Inheritance ("is-a")
A class inherits behavior from another class.

Example:
```python
class Animal:
    def eat(self):
        pass

class Dog(Animal):
    def bark(self):
        pass
```

Relationship:
```
Dog is an Animal
```

Pros:
- Easy code reuse
- Supports polymorphism

Cons:
- Creates strong coupling
- Changes in parent can affect children
- Deep inheritance hierarchies become difficult to maintain
# Aggregation and composition
Both aggregation and composition are techniques where we create in a class an object of another class. So we can say that an object of one class "has" an object of another class, e.g. a car has an engine or a class has students.

There is no difference in code syntax or in how this code works for aggregation and composition.

The difference is only in the way how we work with those classes:
- Aggregation - We create and manage (modify) an object outside of a class and only use it inside of that class
- Composition - We create and manage (modify) an object inside of the class where we use it

For example:

Composition:
```python
class Room:
    def __init__(self, name):
        self.name = name


class House:
    def __init__(self):
        self.rooms = [
            Room("Kitchen"),
            Room("Bedroom")
        ]

    def add_room(self, name):
        self.rooms.append(Room(name))


house = House()
house.add_room("Bathroom")
```

Aggregation:
```python
class Student:
    def __init__(self, name):
        self.name = name


class University:
    def __init__(self, students):
        self.students = students


# Create students independently
john = Student("John")
mary = Student("Mary")

# Pass existing students to the university
university = University([john, mary])
```

Pros:
- More flexible
- Lower coupling
- Components can be swapped easily

Cons:
- Sometimes requires more code