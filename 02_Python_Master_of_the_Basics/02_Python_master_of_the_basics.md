[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pmRaul/DA-Python/blob/main/02_Python_Master_of_the_Basics/02_Python_master_of_the_basics.ipynb)


# Master the Basics: Key Programming Concepts with Python
# Introduction to Python

In the previous post, we explored `Python` and its applications in the field of data analysis. We covered how to install it and looked at various tools you can use to work with Python, ranging from *scripts* in text editors like `VSCode` to *notebooks* in `Jupyter` or `Google Colab`.

This post will introduce you to the fundamental syntax of `Python` to help you grasp essential programming concepts and understand the mechanics of the language. `Python` is designed to be simple and explicit, closely resembling the idea of *pseudocode*.

## Objects in Python

In `Python`, everything whether a number, a string, a function, a class, a module, etc. is considered an `object`. This means that all data structures are treated uniformly, regardless of their type. This characteristic is one of the reasons why `Python` is so flexible.

## Comments

To include text that won’t be executed, we use the `#` symbol. This is particularly useful for adding `comments` to your code, explaining functionality, or providing any relevant details that another person reading the program should take into account.

```python
# This is a comment; Python will ignore this line.
```

###### Variables & References

When you assign a `variable` in `Python`, you're creating a `reference` to the object on the right side of the `=` sign. This implies that any changes made to the original object will be reflected in the new variable, unlike if a copy were created.


```python
a = [1, 2, 3]
a
```




    [1, 2, 3]


💡 In this example, the variable `a` is a `list`, a data structure provided by `Python` for storing objects sequentially. We will discuss lists (and other data structures) in more detail later.

```python
b = a
b
```




    [1, 2, 3]




```python
a.append(4)
a
```




    [1, 2, 3, 4]




```python
b
```




    [1, 2, 3, 4]



Understanding when, how, and why data are copied or referenced is crucial, especially when working with large *datasets*.

###### Dynamic References

Unlike other languages, a variable in `Python` (as a reference to another object) does not have a fixed type. All type information is stored within the object itself.


```python
a = 1
a
```




    1




```python
a = "hola"
a
```




    'hola'


You can change the object a variable references at any time. To determine the type of an object that a variable refers to, you can use the `isinstance` function.


```python
### a is an integer (int)

a = 1
isinstance(a, int)
```




    True




```python
### a is not a string (str)

a = 1
isinstance(a, str)
```




    False




```python
### a is now a string (str)


a = "hola"
isinstance(a, str)
```




    True



###### Methods & Attributes

Most `objects` in `Python` have `methods` (functions associated with the object) and `attributes` (other objects stored within it). For instance, a `str` object has methods for converting to uppercase, splitting into characters, and more.

```python
a = "hola"
a.capitalize()
```




    'Hola'




```python
a.upper()
```




    'HOLA'



This provides substantial default functionality that we can leverage, saving us from having to implement these features ourselves.

###### Binary Operators & Comparison

`Python` provides virtually all the binary operators you would expect from a programming language.

```python
### Addition

1 + 1
```




    2




```python
### Subtraction

2 - 1
```




    1




```python
### Multiplication

2 * 3
```




    6




```python
### Division

1 / 2
```




    0.5




```python
### Floor division

3 // 2
```




    1




```python
### Exponentiation

2**3
```




    8




```python
### AND operator (True if both are True)

True & False
```




    False




```python
### OR operator (True if at least one is True)

True | False
```




    True


The same goes for comparison operators.

```python
### Equality

1 == 2
```




    False




```python
### Inequality

1 != 2
```




    True




```python
### Less than

1 < 1
```




    False




```python
### Less than or equal to

1 <= 1
```




    True




```python
### Greater than 

3 > 2
```




    True




```python
### Greater than or equal to

2 >= 3
```




    False



###### Basic Data Types

`Python` provides several built-in data types


```python
### Decimal number

float
```




    float




```python
### Integer

int
```




    int




```python
### Decimal number

a = 1.34

### Integer

b = 2
```


```python
### string

str
```




    str


One of the features that `Python` shines for is its power when it comes to working with *strings*.


```python
a = 'this is a string'
b = "we can use single or double quotes"
c = """
    We can also create multi-line strings
    using triple quotes (single or double)
"""
```

The `print` function is helpful for displaying strings in the console.


```python
print(c)
```

    
        We can also create multi-line strings
        using triple quotes (single or double)
    


You can also convert other data types to a string using the `str` function.

```python
a = 1.3
b = str(a)
b
```




    '1.3'



However, the most flexible approach is using *string templates*.


```python
c = f"The value of 'a' is {a}"
print(c)
```

    The value of 'a' is 1.3



```python
### boolean

bool
```




    bool



There are only two boolean values: `True` and `False`.


```python
### Byte String

bytes
```




    bytes




```python
### None value (representing the absence of value)

None
```

###### Control flow

In `Python`, several reserved keywords exist for conditional logic, loops, and other flow control mechanisms.


```python
### if, elif, else

x = 1

if x < 0:
    print("negativo")
elif x == 0:
    print("cero")
else:
    print("positivo")
```

    positivo


> ⚠️ In `Python`, code is structured using indentation rather than curly braces, as in some other languages.

We use `for` loops to iterate over an `iterator`.


```python
### for loop

for i in range(3):
    print(i)
```

    0
    1
    2


> 💡 The `range` function returns an iterator over a sequence of consecutive integers.

We can skip to the next step in a loop using `continue`.


```python
for i in range(5):
    # skip the odd numbers
    if i % 2:
        continue
    print(i)
```

    0
    2
    4


We can also terminate the loop early with `break`.


```python
for i in range(5):
    # terminate when reaching 3
    if i >= 3:
        break
    print(i)
```

    0
    1
    2


Similarly, we can use a `while` loop to execute code while a condition holds true.


```python
i = 0
while i < 3:
    print(i)
    i = i + 1
```

    0
    1
    2


Python offers a ternary operator for concise conditional expressions.


```python
x = 1
if x > 0:
    a = x
else:
    a = 0
a
```




    1




```python
### Equivalent to the previous expression

a = x if x > 0 else 0
a
```




    1



###### Modules

In `Python`, any file ending in `.py` is considered a `module` and can be imported to access its code.


```python
# Importing the module `module` containing this code:
#
# def f(x):
#     return 2*x

import module

module.f(1)

```




    2


> ⚠️ We will discuss functions in more depth in future posts, but for now, it is essential to understand that the function `f` takes a variable `x` and returns it multiplied by 2.

There are several ways to import modules in Python. Here are a few examples:

```python
### We can assign a new name to the module

import module as m

m.f(2)

```




    4




```python
### We can use the function directly without the module's name

from module import f

f(3)
```




    6




```python
### We can assign a new name to the function

from module import f as mf

mf(4)
```




    8




```python
### We can import everything from the module (not recommended)

from module import *

f(5)
```




    10



###### Next Steps

This concludes our exploration of `Python`’s basic concepts. Those already familiar with programming will find `Python`'s syntax intuitive, with functionality similar to that of any modern language. Over time, they will realize that `Python`'s simplicity, its extensive default functionality, and the vast range of modules available in its ecosystem will make them more productive, allowing them to express more with less code. For those new to programming, `Python` will prove to be an easy-to-learn language, enabling them to develop interesting programs without the need for hundreds of hours of practice.

In the next post of this series, we will cover `Python`'s data structures, which will enable us to tackle more complex and engaging tasks.

## Exercises for Masters of the Basics

Below are some practical exercises to help reinforce the concepts discussed.

### Exercise 1: Create a function that calculates the factorial of a number

Write a function that takes an integer as an argument and returns the factorial of that number.

<details>
<summary>Hint</summary>

To solve this problem, you might want to use recursion. Recursion is when a function calls itself to break the problem down into smaller, more manageable parts. 

In this case, think of the factorial as `n * (n-1)!` and so on, until you reach the base case where `n == 0`.
</details>

<details>
<summary>Solution</summary>

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)
```
</details>

### Exercise 2: Filter a list to obtain only even numbers

Write a code snippet that filters a list of numbers and returns only the even ones.

<details> 
<summary>Hint</summary> 

You can use a `lambda` function to make the solution concise. A `lambda` function is an anonymous function that you can define in a single line. 

In this case, you can create a `lambda` function that returns `True` if a number is even and use it with the `filter()` function. 

For example:
```python
lambda x: x * 2
```
This creates a function that takes an argument `x` and returns `x` multiplied by 2. In your case, you can use a `lambda` to return `True` if a number is even and apply it with the `filter()` function.
</details>

<details>
<summary>Solution</summary>

```python
numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
pares = list(filter(lambda x: x % 2 == 0, numeros))
print(pares)
```
</details>

### Exercise 3: Sort a list of strings alphabetically

Create a code snippet that sorts a list of strings in alphabetical order.

<details>
<summary>Hint</summary> 

You can use the `sorted()` function, which is a built-in function in Python. However, if you want to use a more advanced sorting function from a library, consider using `sort` from the `operator` module for a customized sorting method.
</details>

<details>
<summary>Solution</summary>

```python
cadenas = ['manzana', 'naranja', 'banana', 'pera']
cadenas_ordenadas = sorted(cadenas)
print(cadenas_ordenadas)
```
</details>