# [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pmRaul/DA-Python/blob/main/05_Python_Classes/05_Python_Classes.ipynb)

# Classes in Python 🚀🐍

In the last post, we talked about `functions` as a way to organize code for reusability and robustness. But sometimes, functions aren’t enough, and that’s where `classes` come in! 🎉 With classes, we can create our own objects, equipped with their own `methods` (functions attached to the object) and `attributes` (properties of the object). Plus, Python’s **inheritance** feature lets us build new objects by reusing and extending existing ones. Cool, right? Let’s dive in! 💡

## Defining a Class 🏗️

To define a class, we use the keyword `class` followed by the name of the class. Inside, we define attributes and methods. Here's an example:

```python
class MyClass:
    greeting = "Hello!"

    def say_greeting(self):
        print(self.greeting)
```

### Key Points:
1. `class`: Used to define a class.
2. `MyClass`: The class name (you can name it anything you want!).
3. `greeting`: An attribute of the class.
4. `say_greeting`: A method that prints the `greeting` attribute.

## Creating an Object 🤖

Once a class is defined, we can create an object (also called an **instance**) from it:

```python
x = MyClass()
```
Now, `x` is an instance of `MyClass`. It inherits all the methods and attributes of the class:

```python
x.say_greeting()  # Outputs: Hello!
```

> **Note**: We use `self` inside methods to access attributes and other methods of the class.

## Customizing Classes with a Constructor 🛠️

We use a special method, `__init__`, to initialize attributes when creating an object:

```python
class MyClass:
    def __init__(self, name):
        self.name = name

    def greet(self):
        print(f"Hi, {self.name}!")

x = MyClass("Alice")
x.greet()  # Outputs: Hi, Alice!
```

### Explanation:
- `__init__`: Automatically called when an object is created.
- `self.name`: Assigns the provided `name` to the object.

## Adding and Modifying Attributes Dynamically 🔄

Python allows us to modify objects on the fly:

```python
x.name = "Bob"
x.greet()  # Outputs: Hi, Bob!

x.age = 30  # Add a new attribute
print(x.age)  # Outputs: 30
```

> ⚠️ Changes to an instance do not affect the class or other instances.

## Inheritance 🌟

Inheritance allows us to create new classes based on existing ones, reusing their functionality:

```python
class BaseClass:
    def show(self):
        print("I’m the base class.")

class DerivedClass(BaseClass):
    def greet(self):
        print("I inherit from the base class!")

obj = DerivedClass()
obj.show()  # Outputs: I’m the base class.
obj.greet()  # Outputs: I inherit from the base class!
```

## Operator Overloading 🎭

We can redefine how operators work with our objects by implementing special methods like `__add__`:

```python
class Number:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return self.value + other.value

x = Number(10)
y = Number(20)
print(x + y)  # Outputs: 30
```

## Summary 📚

- Classes allow us to bundle data (attributes) and behaviors (methods) together.
- Use `__init__` to customize object creation.
- Extend functionality using inheritance.
- Overload operators to make objects behave like built-in types.

With these tools, you can create robust, reusable, and elegant code! 🌈✨