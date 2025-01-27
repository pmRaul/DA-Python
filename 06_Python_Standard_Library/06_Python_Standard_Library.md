
# [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pmRaul/DA-Python/blob/main/06_Python_Standard_Library/06_Python_Standard_Library.ipynb)

# Python's Standard Library 🚀🐍

In previous posts, we explored Python's basic syntax, from creating variables and control flow to advanced concepts like `classes`, `functions`, and data structures. These are the core of the language. However, Python also includes many built-in features and tools that we can use for data analysis without external libraries. Examples include file handling, system interaction, math operations, and more. All these features are part of Python's **Standard Library** (STL). In this post, we'll explore some of the most useful modules for data analysis. You can find a full list of available modules [here](https://docs.python.org/3/library/index.html). 📚✨

## Mathematical Modules 🧮

### The `math` Module

The `math` module provides access to a wide range of mathematical functions. Here are a few examples:

```python
import math
```

> ⚠️ To use a module, we import it using `import` followed by the module name (e.g., `math`).

```python
# Absolute value
math.fabs(-1)  # Output: 1.0

# Ceiling (round up)
math.ceil(2.1)  # Output: 3

# Floor (round down)
math.floor(2.1)  # Output: 2

# Exponential
math.exp(1)  # Output: 2.718281828459045

# Logarithm
math.log(1)  # Output: 0.0

# Power
math.pow(2, 2)  # Output: 4.0

# Square root
math.sqrt(4)  # Output: 2.0

# Trigonometric functions
math.cos(45)  # Output: 0.5253219888177297

# Constants
math.pi  # Output: 3.141592653589793
math.e   # Output: 2.718281828459045
```

For more functions, check the [documentation](https://docs.python.org/3/library/math.html). 📖

### The `random` Module 🎲

This module provides functionality to work with (pseudo)random numbers:

```python
import random

# Random number between 0 and 1
random.random()  # Example output: 0.8499521141392985

# Random number between two values
random.uniform(3, 5)  # Example output: 4.69170673249722

# Gaussian distribution (mean = 2, std = 0.3)
random.gauss(2, 0.3)  # Example output: 2.12423100921994
```

> ⚠️ Random results vary with every execution. To ensure reproducibility, set a seed:

```python
random.seed(42)
random.random()  # Example output: 0.6394267984578837
```

Find more features in the [documentation](https://docs.python.org/3/library/random.html). 📖

## The `os` Module 🌐

This module provides tools to interact with the operating system. It works on Windows, macOS, and Linux in a unified way.

```python
import os

# Access environment variables
os.environ

# Get current working directory
os.getcwd()

# List files in a directory
os.listdir('.')

# Create a directory
os.mkdir('test')

# Remove a directory
os.rmdir('test')
```

For more, visit the [documentation](https://docs.python.org/3/library/os.html). 📖

## The `io` Module 📝

The `io` module provides Python's main facilities for dealing with various types of I/O (input/output). While you can perform basic file operations using the built-in `open()` function without explicitly importing `io`, the `io` module offers more advanced functionalities and fine-grained control over I/O operations.

### Basic File Operations

You can read and write files using the `open()` function, which is part of the built-in namespace and doesn't require importing `io` directly.

```python
# Open a file for reading
with open('example.txt', 'r') as f:
    for line in f:
        print(line)
```

### Writing to a File

To write data to a file, you can open it in write (`'w'`) or append (`'a'`) mode.

```python
# Open a file for writing
with open('example.txt', 'w') as f:
    f.write('Hello, World!\n')

# Open a file for appending
with open('example.txt', 'a') as f:
    f.write('Appending a new line.\n')
```

### Using `io` for In-Memory Streams

The `io` module allows you to create in-memory streams, which are useful for handling text or binary data without writing to disk.

```python
import io

# Creating an in-memory text stream
text_stream = io.StringIO()
text_stream.write('This is a string in memory.')
print(text_stream.getvalue())  # Outputs: This is a string in memory.

# Creating an in-memory binary stream
binary_stream = io.BytesIO()
binary_stream.write(b'Binary data in memory.')
print(binary_stream.getvalue())  # Outputs: b'Binary data in memory.'
```

### Working with Different Encodings

You can specify the encoding when opening a file to handle different text encodings.

```python
# Open a file with a specific encoding
with open('example_utf8.txt', 'w', encoding='utf-8') as f:
    f.write('Café Münsterländer')
```

### Handling Binary Files

For binary data, open the file in binary mode by adding `'b'` to the mode string.

```python
# Open a binary file for reading
with open('image.png', 'rb') as f:
    data = f.read()

# Open a binary file for writing
with open('copy_image.png', 'wb') as f:
    f.write(data)
```

### Context Managers

Using `with` statements ensures that files are properly closed after their suite finishes, even if an exception is raised.

```python
with open('example.txt', 'r') as f:
    data = f.read()
# File is automatically closed here
```

### Advanced I/O Operations

The `io` module also provides classes like `StringIO` and `BytesIO` for in-memory text and binary streams, and `BufferedReader` and `BufferedWriter` for buffered I/O operations.

For more advanced usage, refer to the [io module documentation](https://docs.python.org/3/library/io.html). 📖

## Parallel Execution 🔄

Analyzing large datasets can be time-consuming. Many CPUs have multiple cores, allowing tasks to run in parallel, significantly reducing processing time.

Python provides several modules and approaches to achieve parallelism, including threading, multiprocessing, and asynchronous programming.

### Understanding Concurrency vs Parallelism

- **Concurrency** is about dealing with multiple tasks at the same time, but not necessarily simultaneously.
- **Parallelism** involves performing multiple tasks literally at the same time, leveraging multiple CPU cores.

### Sequential Execution

In sequential execution, tasks are performed one after the other.

```python
import time

def func(p):
    print(f"Processing {p}")
    time.sleep(1)
    return 2 * p

inputs = [1, 2, 3, 4]
start_time = time.time()
results = [func(p) for p in inputs]  # Sequential processing
end_time = time.time()
print(f"Sequential processing took {end_time - start_time} seconds")
```

### Parallel Execution with ThreadPoolExecutor

Using `concurrent.futures.ThreadPoolExecutor`, you can execute tasks concurrently using threads. This is suitable for I/O-bound tasks.

```python
import concurrent.futures
import time

def func(p):
    print(f"Processing {p}")
    time.sleep(1)
    return 2 * p

inputs = [1, 2, 3, 4]
start_time = time.time()
with concurrent.futures.ThreadPoolExecutor() as executor:
    results = list(executor.map(func, inputs))  # Parallel processing
end_time = time.time()
print(f"Parallel processing with threads took {end_time - start_time} seconds")
```

### Parallel Execution with ProcessPoolExecutor

For CPU-bound tasks, `concurrent.futures.ProcessPoolExecutor` is more effective as it sidesteps Python's Global Interpreter Lock (GIL) by using separate processes.

```python
import concurrent.futures
import time

def func(p):
    print(f"Processing {p}")
    time.sleep(1)
    return 2 * p

inputs = [1, 2, 3, 4]
start_time = time.time()
with concurrent.futures.ProcessPoolExecutor() as executor:
    results = list(executor.map(func, inputs))  # Parallel processing
end_time = time.time()
print(f"Parallel processing with processes took {end_time - start_time} seconds")
```

### Asynchronous Programming with `asyncio`

For I/O-bound and high-level structured network code, `asyncio` allows writing concurrent code using the `async`/`await` syntax.

```python
import asyncio

async def func(p):
    print(f"Processing {p}")
    await asyncio.sleep(1)
    return 2 * p

async def main():
    inputs = [1, 2, 3, 4]
    tasks = [func(p) for p in inputs]
    results = await asyncio.gather(*tasks)
    print(results)

start_time = time.time()
asyncio.run(main())
end_time = time.time()
print(f"Asynchronous processing took {end_time - start_time} seconds")
```

### Choosing the Right Approach

- **Threading:** Best for I/O-bound tasks where the program spends time waiting for external resources.
- **Multiprocessing:** Ideal for CPU-bound tasks that require heavy computation.
- **Asyncio:** Suitable for handling multiple I/O-bound tasks in a single thread without the overhead of threading.

For more advanced options and detailed explanations, explore the [concurrent.futures](https://docs.python.org/3/library/concurrent.futures.html) and [asyncio](https://docs.python.org/3/library/asyncio.html) modules. 📖

## Other Useful Modules 📦

- **[json](https://docs.python.org/3/library/json.html):** Work with JSON data.
- **[argparse](https://docs.python.org/3/library/argparse.html):** Parse command-line arguments.
- **[pickle](https://docs.python.org/3/library/pickle.html):** Serialize and deserialize Python objects.
- **[Compression](https://docs.python.org/3/library/archiving.html):** Handle zip and tar files.
- **[urllib](https://docs.python.org/3/library/urllib.html):** Fetch data from URLs.

## Summary 📚

In this post, we explored the Python Standard Library, which offers essential tools for data analysis, such as:

- Math and random number generation (`math` and `random`).
- System interaction (`os`).
- File handling (`io`).
- Parallel processing (`concurrent.futures` and `asyncio`).

While these modules are powerful, external libraries like `NumPy` and `Pandas` provide enhanced functionality. Stay tuned for future posts where we’ll explore these libraries in depth! 🚀✨

## Exercises 🛠️📚

### Exercise 1: In-Memory Text Stream
**Task:**
1. Use the `io` module to create an in-memory text stream.
2. Write the string `'Hello, in-memory world!'` to the stream.
3. Read the content from the stream and print it.

<details>
<summary>Solution</summary>

```python
import io

# Create an in-memory text stream
text_stream = io.StringIO()

# Write to the stream
text_stream.write('Hello, in-memory world!')

# Move to the beginning of the stream
text_stream.seek(0)

# Read and print the content
content = text_stream.read()
print(content)  # Outputs: Hello, in-memory world!
```
</details>

### Exercise 2: Copy Binary Data
**Task:**
1. Open a binary file (e.g., an image) in read mode.
2. Use `io.BytesIO` to create an in-memory binary stream.
3. Write the binary data to the in-memory stream.
4. Save the data from the in-memory stream to a new binary file.

<details>
<summary>Solution</summary>

```python
import io

# Read binary data from the original file
with open('original_image.png', 'rb') as original_file:
    binary_data = original_file.read()

# Write binary data to an in-memory stream
memory_stream = io.BytesIO()
memory_stream.write(binary_data)

# Save the data from the in-memory stream to a new file
with open('copy_image.png', 'wb') as copy_file:
    memory_stream.seek(0)
    copy_file.write(memory_stream.read())
```
</details>

### Exercise 3: Parallel Processing with ProcessPoolExecutor
**Task:**
1. Define a CPU-bound function that calculates the factorial of a number.
2. Use `concurrent.futures.ProcessPoolExecutor` to compute the factorial of numbers `[5, 7, 10, 12]` in parallel.
3. Print the results.

<details>
<summary>Solution</summary>

```python
import concurrent.futures
import math

def compute_factorial(n):
    return math.factorial(n)

numbers = [5, 7, 10, 12]

with concurrent.futures.ProcessPoolExecutor() as executor:
    results = list(executor.map(compute_factorial, numbers))

print(results)  # Outputs: [120, 5040, 3628800, 479001600]
```
</details>

### Exercise 4: Asynchronous I/O with `asyncio`
**Task:**
1. Write an asynchronous function that simulates fetching data by sleeping for 2 seconds and then returns a message.
2. Use `asyncio` to run this function concurrently for three different tasks.
3. Print the messages returned by each task.

<details>
<summary>Solution</summary>

```python
import asyncio

async def fetch_data(task_name):
    print(f"Starting {task_name}")
    await asyncio.sleep(2)
    return f"Completed {task_name}"

async def main():
    tasks = [fetch_data(f"Task {i}") for i in range(1, 4)]
    results = await asyncio.gather(*tasks)
    for result in results:
        print(result)

asyncio.run(main())
# Outputs:
# Starting Task 1
# Starting Task 2
# Starting Task 3
# Completed Task 1
# Completed Task 2
# Completed Task 3
```
</details>