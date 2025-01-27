# [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pmRaul/DA-Python/blob/main/07_NumPy/07_NumPy.ipynb)

# NumPy: Numerical Computing in Python 🚀🐍

`NumPy` (*Numerical Python*) is one of the most essential and widely used libraries in the Python ecosystem, especially for numerical computation. In previous posts, we explored Python’s basic data structures and modules like `math` for mathematical operations. `NumPy` takes these capabilities to the next level by:

- Offering the `ndarray` object, a fast and flexible array structure optimized for numerical computation.
- Enabling mathematical operations directly on arrays without loops.
- Providing efficient methods for file I/O.
- Supporting linear algebra, random number generation, and Fourier transforms.

The core of `NumPy` is implemented in C, offering Python bindings for seamless interaction, resulting in high performance. Many data analysis and machine learning libraries are built on top of `NumPy`, using its arrays as the foundational data structure. Let’s explore why `NumPy` is so powerful! 🌟

## Installation and Setup ⚙️

`NumPy` is an external library, so you need to install it first. You can do this using:

- `conda install numpy` if you use Anaconda.
- `pip install numpy` for the default Python environment.

If you need guidance on installing libraries, revisit our [Python installation guide](https://github.com/pmRaul/DA-Python/blob/main/01_Python_introduction/01_Python_introduction.md). ✅

## Why Use `NumPy`? 🤔

Let’s compare a simple operation in Python and `NumPy` to see the difference in performance:

```python
# Using Python lists
l = [i for i in range(10_000_000)]

%time l2 = [2 * i for i in l]
# Output: CPU times: user X s, sys: Y s, total: Z s

# Using NumPy arrays
import numpy as np

array = np.array(l)

%time array2 = 2 * array
# Output: CPU times: user A s, sys: B s, total: C s
```

You’ll notice that `NumPy` is significantly faster! 🏎️ This is because `NumPy` operations are implemented in optimized C code. Instead of iterating through each element (as in Python lists), operations are vectorized, meaning they are applied to the entire array at once. Additionally, `NumPy` uses less memory thanks to its efficient data storage. 📈

### Memory Usage Comparison 🧠

Beyond performance, `NumPy` consumes less memory than Python lists for storing the same data:

```python
import sys
import numpy as np

# Python list
l = list(range(1000))
print(sys.getsizeof(l))  # Example: 8056 bytes

# NumPy array
array = np.array(l)
print(array.nbytes)      # Example: 4000 bytes
```

This is crucial when working with large datasets, as `NumPy` allows you to handle more data efficiently. 💾✨

## The `ndarray` Object 🔢

At the heart of `NumPy` is the `ndarray`, a multi-dimensional array structure that allows us to represent scalars, vectors, matrices, and higher-dimensional tensors. Here’s how to create arrays:

```python
import numpy as np

# 1D array (vector)
vector = np.array([1, 2, 3])

# 2D array (matrix)
matrix = np.array([[1, 2, 3], [4, 5, 6]])

# 3D array (tensor)
tensor = np.ones((2, 3, 4))
```

### Properties of an Array 🛠️

```python
# Shape (dimensions of the array)
print(tensor.shape)  # Outputs: (2, 3, 4)

# Number of dimensions
print(tensor.ndim)   # Outputs: 3

# Total number of elements
print(tensor.size)   # Outputs: 24

# Data type of the elements
print(tensor.dtype)  # Outputs: float64
```

## Array Creation Functions 🎨

NumPy provides several functions to create arrays quickly:

```python
# Array of zeros
np.zeros((2, 3))

# Array of ones
np.ones((2, 3))

# Array with a specific value
np.full((2, 3), 7)

# Uninitialized array (random content)
np.empty((2, 3))

# Sequential arrays
np.arange(1, 10, 2)      # Similar to Python’s range()
np.linspace(0, 1, 5)     # Evenly spaced values

# Random arrays
np.random.rand(2, 3)     # Uniform distribution
np.random.randn(2, 3)    # Normal distribution
```

### More Array Creation Examples 🧬

```python
# Identity matrix
np.eye(4)

# Diagonal matrix
np.diag([1, 2, 3, 4])

# Repeat elements
np.repeat([1, 2, 3], 3)  # Output: [1 1 1 2 2 2 3 3 3]
```

## Operations on Arrays ➕➖✖️➗

One of `NumPy`'s most powerful features is its ability to perform element-wise operations directly on arrays:

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

# Element-wise operations
print(a + b)  # Output: [5 7 9]
print(a - b)  # Output: [-3 -3 -3]
print(a * b)  # Output: [ 4 10 18]
print(a / b)  # Output: [0.25 0.4  0.5 ]
```

### Mathematical Functions 🧮

`NumPy` includes a wide range of mathematical functions that are efficiently applied to arrays:

```python
# Universal functions (ufuncs)
print(np.sqrt(a))   # Square root: [1.         1.41421356 1.73205081]
print(np.log(a))    # Natural logarithm: [0.         0.69314718 1.09861229]
print(np.exp(a))    # Exponential: [  2.71828183   7.3890561   20.08553692]

# Aggregated operations
print(np.sum(a))    # Sum: 6
print(np.mean(a))   # Mean: 2.0
print(np.max(a))    # Max: 3
print(np.min(a))    # Min: 1
```

### Broadcasting 📡

Broadcasting is a powerful feature of `NumPy` that allows operations between arrays of different shapes:

```python
# 1D array and scalar
a = np.array([1, 2, 3])
b = 2
print(a + b)  # Output: [3 4 5]

# 2D array and vector
matrix = np.array([[1, 2, 3], [4, 5, 6]])
vector = np.array([1, 0, 1])
print(matrix + vector)
# Output:
# [[2 2 4]
#  [5 5 7]]
```

This greatly simplifies complex mathematical operations without the need for explicit loops. 🔄✨

## Reshaping Arrays 🧩

You can reshape arrays to change their dimensions without altering their data:

```python
# Create a 1D array
array = np.arange(12)

# Reshape to 2D
array2d = array.reshape((3, 4))
print(array2d)
# Output:
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]

# Flatten back to 1D
array_flat = array2d.ravel()
print(array_flat)  # Output: [ 0  1  2  3  4  5  6  7  8  9 10 11]
```

### More Reshaping Techniques 🔄

```python
# Transpose a matrix
matrix = np.array([[1, 2, 3], [4, 5, 6]])
print(matrix.T)
# Output:
# [[1 4]
#  [2 5]
#  [3 6]]

# Stack arrays
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
print(np.vstack((a, b)))
# Output:
# [[1 2 3]
#  [4 5 6]]
print(np.hstack((a, b)))
# Output: [1 2 3 4 5 6]
```

## Indexing and Slicing 📐

`NumPy` adopts Python-like indexing and slicing but extends its capabilities for multi-dimensional arrays:

```python
array = np.arange(10)

# Access individual elements
print(array[2])  # Output: 2

# Slicing
print(array[2:5])  # Output: [2 3 4]

# Multi-dimensional arrays
matrix = np.arange(1, 10).reshape(3, 3)
print(matrix[1, 2])  # Output: 6

# Multi-dimensional slicing
print(matrix[:, 1])  # Output: [2 5 8]
```

### More Indexing Techniques 🧩

```python
# Boolean indexing
a = np.array([1, 2, 3, 4, 5])
print(a[a > 3])  # Output: [4 5]

# Advanced indexing
indices = [0, 2, 4]
print(a[indices])  # Output: [1 3 5]
```

## Saving and Loading Data 💾

Save arrays to disk for future use:

```python
# Save and load in binary format
np.save('array', array)
loaded_array = np.load('array.npy')
print(loaded_array)  # Output: [0 1 2 3 4 5 6 7 8 9]

# Save and load in text format
np.savetxt('array.csv', array, delimiter=',')
loaded_array_csv = np.loadtxt('array.csv', delimiter=',')
print(loaded_array_csv)  # Output: [0. 1. 2. 3. 4. 5. 6. 7. 8. 9.]
```

### Advanced Formats 📁

```python
# Save multiple arrays in a compressed file
np.savez_compressed('arrays.npz', a=a, b=b)
data = np.load('arrays.npz')
print(data['a'], data['b'])  # Output: saved arrays
```

## Advanced Operations in `NumPy` 🔍

To make the most of `NumPy`, it’s useful to know some of its more advanced operations:

### Linear Algebra 🧮

```python
# Matrix multiplication
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
print(np.dot(A, B))
# Output:
# [[19 22]
#  [43 50]]

# Inverse of a matrix
print(np.linalg.inv(A))
# Output:
# [[-2.    1. ]
#  [ 1.5 -0.5]]
```

### Statistics 📊

```python
data = np.random.randn(1000)

# Statistical measures
print(np.mean(data))          # Mean
print(np.std(data))           # Standard deviation
print(np.percentile(data, 50))  # Median
```

### Data Manipulation 🛠️

```python
# Sorting an array
sorted_array = np.sort(array)
print(sorted_array)

# Finding indices of elements
indices = np.where(array > 5)
print(indices)  # Output: (array([6, 7, 8, 9]),)
```

## Summary 📚

In this post, we introduced `NumPy`, the go-to library for numerical computation in Python. We explored its key features, including:

- **The efficient `ndarray` object**: A multi-dimensional data structure optimized for numerical operations.
- **Array creation functions**: Quick methods to generate arrays of zeros, ones, specific values, sequential, and random data.
- **Element-wise and advanced operations**: Performing mathematical operations without loops, utilizing universal functions and techniques like broadcasting.
- **Reshaping arrays**: Changing the shape and structure of arrays to fit different needs.
- **Indexing and slicing**: Efficiently accessing and manipulating data within arrays.
- **Saving and loading data**: Storing and retrieving arrays for future use.
- **Advanced operations**: Linear algebra, statistics, and data manipulation for more complex analyses.

Additionally, we compared the performance and memory usage of `NumPy` against Python lists, demonstrating its superiority in efficiency and ability to handle large volumes of data. 📈🐍

As we proceed, we’ll use `NumPy` extensively as the backbone for data analysis and machine learning tasks. Stay tuned to explore its incredible capabilities! 🚀✨

# Happy Coding! 💻🎉

## Exercises 🛠️📚

### Exercise 1: Creating and Inspecting Arrays
**Task:**
1. Create a 2D NumPy array with shape `(4, 5)` filled with zeros.
2. Change the data type of the array to `int32`.
3. Print the shape, data type, and size of the array.

<details>
<summary>Solution</summary>

```python
import numpy as np

# Create a 2D array of zeros with shape (4, 5)
array = np.zeros((4, 5), dtype=np.int32)

# Print properties
print("Shape:", array.shape)       # Output: Shape: (4, 5)
print("Data type:", array.dtype)   # Output: Data type: int32
print("Size:", array.size)         # Output: Size: 20
```
</details>

### Exercise 2: Array Operations and Broadcasting
**Task:**
1. Create a 1D NumPy array `a` with values `[10, 20, 30, 40, 50]`.
2. Create a scalar `b` with value `5`.
3. Perform the following operations and print the results:
   - Add `b` to `a`.
   - Multiply `a` by `b`.
   - Subtract `b` from `a`.
   - Divide `a` by `b`.

<details>
<summary>Solution</summary>

```python
import numpy as np

# Create array and scalar
a = np.array([10, 20, 30, 40, 50])
b = 5

# Perform operations
print("a + b:", a + b)       # Output: [15 25 35 45 55]
print("a * b:", a * b)       # Output: [ 50 100 150 200 250]
print("a - b:", a - b)       # Output: [ 5 15 25 35 45]
print("a / b:", a / b)       # Output: [2. 4. 6. 8. 10.]
```
</details>

### Exercise 3: Reshaping and Transposing Arrays
**Task:**
1. Create a NumPy array with values from `0` to `11`.
2. Reshape the array into a `3x4` matrix.
3. Transpose the matrix.
4. Print both the reshaped matrix and its transpose.

<details>
<summary>Solution</summary>

```python
import numpy as np

# Create array
array = np.arange(12)

# Reshape to 3x4 matrix
matrix = array.reshape((3, 4))
print("Reshaped Matrix:\n", matrix)
# Output:
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]

# Transpose the matrix
transpose = matrix.T
print("Transposed Matrix:\n", transpose)
# Output:
# [[ 0  4  8]
#  [ 1  5  9]
#  [ 2  6 10]
#  [ 3  7 11]]
```
</details>

### Exercise 4: Indexing and Boolean Masking
**Task:**
1. Create a NumPy array `data` with values from `1` to `20`.
2. Reshape `data` into a `4x5` matrix.
3. Use boolean masking to extract all elements greater than `10`.
4. Print the extracted elements.

<details>
<summary>Solution</summary>

```python
import numpy as np

# Create and reshape array
data = np.arange(1, 21)
matrix = data.reshape((4, 5))
print("Original Matrix:\n", matrix)
# Output:
# [[ 1  2  3  4  5]
#  [ 6  7  8  9 10]
#  [11 12 13 14 15]
#  [16 17 18 19 20]]

# Boolean masking for elements greater than 10
filtered = matrix[matrix > 10]
print("Elements greater than 10:", filtered)
# Output: [11 12 13 14 15 16 17 18 19 20]
```
</details>

### Exercise 5: Saving and Loading Arrays
**Task:**
1. Create a NumPy array `arr` with random values of shape `(3, 3)`.
2. Save the array to a file named `random_array.npy`.
3. Load the array from the file and print it to verify.

<details>
<summary>Solution</summary>

```python
import numpy as np

# Create a random array
arr = np.random.rand(3, 3)
print("Original Array:\n", arr)

# Save the array to a file
np.save('random_array.npy', arr)

# Load the array from the file
loaded_arr = np.load('random_array.npy')
print("Loaded Array:\n", loaded_arr)
```
</details>

### Exercise 6: Linear Algebra Operations
**Task:**
1. Create two `2x2` matrices `A` and `B` with arbitrary integer values.
2. Compute the matrix product of `A` and `B`.
3. Calculate the inverse of matrix `A` (if it exists).
4. Print all results.

<details>
<summary>Solution</summary>

```python
import numpy as np

# Create matrices
A = np.array([[2, 3], [1, 4]])
B = np.array([[5, 6], [7, 8]])

print("Matrix A:\n", A)
print("Matrix B:\n", B)

# Matrix product
product = np.dot(A, B)
print("Product of A and B:\n", product)
# Output:
# [[2*5 + 3*7, 2*6 + 3*8] => [29, 30]
#  [1*5 + 4*7, 1*6 + 4*8] => [33, 38]]

# Inverse of A
inverse_A = np.linalg.inv(A)
print("Inverse of A:\n", inverse_A)
# Output:
# [[ 0.8 -0.6]
#  [-0.2  0.4]]
```
</details>

### Exercise 7: Statistical Analysis
**Task:**
1. Generate a NumPy array `scores` with 1000 random values following a normal distribution (mean=50, std=10).
2. Calculate and print the mean, median, standard deviation, and the 90th percentile of the `scores`.
3. Identify and print how many scores are above the 90th percentile.

<details>
<summary>Solution</summary>

```python
import numpy as np

# Generate scores
scores = np.random.normal(loc=50, scale=10, size=1000)

# Calculate statistics
mean = np.mean(scores)
median = np.median(scores)
std_dev = np.std(scores)
percentile_90 = np.percentile(scores, 90)

print(f"Mean: {mean:.2f}")
print(f"Median: {median:.2f}")
print(f"Standard Deviation: {std_dev:.2f}")
print(f"90th Percentile: {percentile_90:.2f}")

# Count scores above the 90th percentile
above_90 = np.sum(scores > percentile_90)
print(f"Number of scores above the 90th percentile: {above_90}")
```
</details>

### Exercise 8: Manipulating Multi-dimensional Arrays
**Task:**
1. Create a 3D NumPy array `tensor` with shape `(2, 3, 4)` filled with sequential integers starting from 0.
2. Extract a `2x4` matrix by selecting the first two layers and all rows of the second dimension.
3. Print the extracted matrix.

<details>
<summary>Solution</summary>

```python
import numpy as np

# Create 3D tensor
tensor = np.arange(24).reshape((2, 3, 4))
print("Original Tensor:\n", tensor)
# Output:
# [[[ 0  1  2  3]
#   [ 4  5  6  7]
#   [ 8  9 10 11]]
#
#  [[12 13 14 15]
#   [16 17 18 19]
#   [20 21 22 23]]]

# Extract a 2x4 matrix from the first two layers and all rows of the second dimension
extracted = tensor[:, 1, :]
print("Extracted Matrix:\n", extracted)
# Output:
# [[ 4  5  6  7]
#  [16 17 18 19]]
```
</details>

# Happy Coding! 💻🎉