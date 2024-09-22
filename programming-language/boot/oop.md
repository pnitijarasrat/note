# Object Oriented Programming

## Class

- A class is a special type of value in an object-oriented programming language like Python. It's similar to a dictionary in that it usually stores other types inside itself.
- instance aka object

```python
# Defines a new class called "Soldier"
class Soldier:
    health = 5
    armor = 3
    damage = 2

# An object is just an instance of a class type. For example:

health = 50
# health is an instance of an integer type
aragorn = Soldier()
# aragorn is an instance of the Soldier type (class)
```

### Class Method

- One thing that makes classes cool is that we can define methods on them. A method is a function that's tied directly to a class and has access to all its properties.

```python
class Soldier:
    health = 5

    def take_damage(self, damage):
        self.health -= damage

soldier_one = Soldier()
soldier_one.take_damage(2)
print(soldier_one.health)
# prints "3"

# A method automatically receives the object it was called on as its first parameter.
class Soldier:
    health = 5

    def take_damage(self, damage, multiplier):
        damage = damage * multiplier
        self.health -= damage

dalinar = Soldier()
damage, multiplier = 30, 3

# Only "damage" and "multiplier" are passed as arguments
# "dalinar" is passed implicitly as the first argument, "self"
dalinar.take_damage(damage, multiplier)
```

### Class Constructor

```python
class Soldier:
    def __init__(self, name, armor, num_weapons):
        self.name = name
        self.armor = armor
        self.num_weapons = num_weapons

soldier = Soldier("Legolas", 5, 10)
print(soldier.name)
# prints "Legolas"
print(soldier.armor)
# prints "5"
print(soldier.num_weapons)
# prints "10"
```

### Class Variable Instance Variable

```python
# Class Variable
class Wall:
    height = 10

south_wall = Wall()
print(south_wall.height)
# prints "10"

Wall.height = 20 # updates all instances of a Wall

print(south_wall.height)
# prints "20"

# Instance Variable
class Wall:
    def __init__(self):
        self.height = 10

south_wall = Wall()
south_wall.height = 20 # only updates this instance of a wall
print(south_wall.height)
# prints "20"

north_wall = Wall()
print(north_wall.height)
# prints "10"
```

## Encapsulation

- Encapsulation is the practice of hiding complexity inside a "black box" so that it's easier to focus on the problem at hand.
- The most basic example of encapsulation is a function. The caller of a function doesn't need to worry too much about what happens inside, they just need to understand the inputs and outputs.
- not security purpose

```python
acceleration = calc_acceleration(initial_speed, final_speed, time)
```

### Public and Private

- By default, all properties and methods in a class are public. That means that you can access them with the . operator:

```python
wall.height = 10
print(wall.height)
# 10
```

- Private data members are how we encapsulate logic and data within a class. To make a property or method private, you just need to prefix it with two underscores.

```python
class Wall:
    def __init__(self, armor, magic_resistance):
        self.__armor = armor
        self.__magic_resistance = magic_resistance

    def get_defense(self):
        return self.__armor + self.__magic_resistance

front_wall = Wall(10, 20)

# This results in an error
print(front_wall.__armor)

# This works
print(front_wall.get_defense())
# 30
```

## Abstraction

- Abstraction is about creating a simple interface for complex behavior. It focuses on what's exposed.
- Encapsulation is about hiding internal state. It focuses on tucking implementation details away so no one depends on them.

## Inheritance

- Inheritance allows one class, the "child" class, to inherit the properties and methods of another class, the "parent" class.
- This powerful language feature helps us avoid writing a lot of the same code twice. It allows us to DRY (don't repeat yourself) up our code.

```python
class Animal:
    def __init__(self, num_legs):
        self.num_legs = num_legs

# The Cow class can reuse the Animal class's constructor with the super() method:
# any parent method can be called using super() method
class Cow(Animal):
    def __init__(self):
        # call the parent constructor to
        # give the cow some legs
        super().__init__(4)
```

## Polymorphism

- While inheritance is the most unique trait of object-oriented languages, polymorphism is probably the most powerful. Polymorphism is the ability of a variable, function or object to take on multiple forms.

> "poly"="many"
> "morph"="form".

- For example, classes in the same hierarchical tree may have methods with the same name but different behaviors.

```python
class Creature():
    def move(self):
        print("the creature moves")

class Dragon(Creature):
    def move(self):
        print("the dragon flies")

class Kraken(Creature):
    def move(self):
        print("the kraken swims")

for creature in [Creature(), Dragon(), Kraken()]:
    creature.move()
# prints:
# the creature moves
# the dragon flies
# the kraken swims

# The Dragon and Kraken child classes are overriding the behavior of their parent class's move() method.
```

### Operator Overloading

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, point):
        x = self.x + point.x
        y = self.y + point.y
        return Point(x, y)

p1 = Point(4, 5)
p2 = Point(2, 3)
p3 = p1 + p2
# p3 is (6, 8)
```

| Operation           | Operator | Method   |
| ------------------- | -------- | -------- | --- |
| Addition            | +        | add      |
| Subtraction         | -        | sub      |
| Multiplication      | \*       | mul      |
| Power               | \*\*     | pow      |
| Division            | /        | truediv  |
| Floor Division      | //       | floordiv |
| Remainder (modulo)  | %        | mod      |
| Bitwise Left Shift  | <<       | lshift   |
| Bitwise Right Shift | >>       | rshift   |
| Bitwise AND         | &        | and      |
| Bitwise OR          |          |          | or  |
| Bitwise XOR         | ^        | xor      |
| Bitwise NOT         | ~        | invert   |

## end
