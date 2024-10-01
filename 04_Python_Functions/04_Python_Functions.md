
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pmRaul/DA-Python/blob/main/04_Python_Functions/04_Python_Functions.ipynb)

# Functions
`Functions` are the main tool that `Python` offers us to organize our code, allowing for its reuse. As a general rule, if you find yourself writing the same code or a similar functionality multiple times, it is very likely that you need a `function`. This `function` would include the code, and when we need to execute it, we invoke it, optionally passing different `arguments` and retrieving the result returned by the `function`.

In `Python`, we define a function with the keyword `def`.

```python
def func():
    pass
```

> ⚠️ We use the reserved word `pass` to tell `Python` to do nothing.

Once we have our function defined, we can invoke it using its name.

```python
func()
```

For now, our function does not perform any interesting task. Let’s see how we can make our function print a `string` to the console.

```python
def func():
    print('hello')
func()
```

As you can see, we include all the code we want to execute inside the function with the correct indentation. Inside a function, we can define new variables that will only be visible within the function itself.

```python
def func():
    s = 'hello'
    print(s)
func()
```


```python
# `s` only exists within the function
s
```

However, we can use variables defined outside the `function`.

```python
s = 'hello'

def func():
    print(s)
func()
```

```python
# `s` now exists both inside and outside the function

s
```

## Arguments
In most cases, we want our `function` to perform a certain action abstractly, allowing us to specify the data on which it should act. To do this, we can define `arguments` that the `function` will use during execution.

```python
def func(s):
    print(s)
func('hello')
func('hi')
```

Now our `function` is much more versatile and reusable. We can define different arguments separated by a comma.

```python
def func(a, b, c):
    print(a, b, c)
func('hello', 'how', 'are you')
```

We can also define optional arguments, so if no value is specified during the function call, the default value is used.

```python
def func(a, b, c='hello'):
    print(a, b, c)
func('hello', 'how')
```

> ⚠️ Always remember to define the required `arguments` first, and then the optional ones.

It’s possible to use the argument's name when calling a `function`.

```python
func(a=1, b=2)
```

## Returning Values
In addition to receiving `arguments`, a function can return results. To do this, we use the reserved word `return`.

```python
def func(a, b):
    return a + b
x = func(1, 2)
x
```

`Python` allows us to return multiple values at once.

```python
def func(a, b):
    return a + b, a - b
x1, x2 = func(1, 2)
x1, x2
```

## Anonymous Functions
An `anonymous function`, also known as a `lambda function`, is a way of defining functions that only contain one statement, the result of which is automatically returned.

```python
def func(x):
    return 2 * x
```

# Same function, but defined as a lambda function

```python
func = lambda x: 2 * x
func(2)
```

In data analysis, it is quite common to perform transformations that consist of a single statement, and being able to express this functionality concisely increases our productivity while reducing possible sources of error. We can define anonymous functions with multiple parameters.

```python
func = lambda x, y: x + y
func(1, 2)
```

## Generators
`Python` implements a consistent way to iterate over sequences, which we can use to our advantage to define our own iteration logic through a type of function called `generators`. We can define a `generator` the same way we define a normal `function`, changing the word `return` to `yield`. This tells `Python` that although the function has returned a value, the function's execution is not over and will continue to yield values in the future.

```python
def func(n=10):
    for i in range(n):
        if i % 2:
            yield i
gen = func()
for i in gen:
    print(i)
```

An alternative way to define a generator more compactly is as follows:

```python
gen = (i for i in range(10) if i % 2)
for i in gen:
    print(i)
```

In data analysis, it is very common to iterate over large datasets, applying transformations or processing, and depending on the algorithm we are using, we may want to iterate over our data in different ways. A `generator` will be very useful in these situations.
