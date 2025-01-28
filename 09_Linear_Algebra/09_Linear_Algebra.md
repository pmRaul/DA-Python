[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pmRaul/DA-Python/blob/main/09_Linear_Algebra/09_Linear_Algebra.ipynb)

# Linear Algebra in Python 🧮🚀

`Linear Algebra` is a cornerstone of mathematics with countless applications in science, engineering, and especially in Artificial Intelligence (AI). 🌐 A solid understanding of linear algebra is crucial for developing AI algorithms, particularly in `Machine Learning` 🤖 and `Deep Learning` 🧠. In this post, we will cover essential linear algebra concepts tailored for AI applications. Let’s dive in! 🌟

---

## Mathematical Objects 📐

Throughout our journey into AI algorithm development, we will frequently encounter these mathematical objects. Understanding these foundational elements is key to mastering linear algebra in Python.

### 1. Scalars 🔢
A `scalar` is a single number, distinct from other objects in linear algebra that often represent collections of numbers. Scalars are usually represented with lowercase letters (e.g., `n` for the number of neurons in a neural network).

**Real-World Example:** Temperature, speed, or a single data point in a dataset.

```python
# Scalar example
x = 42
print(x)  # Output: 42
```

### 2. Vectors 📏
A `vector` is a sequence of numbers organized in a specific order. Each element in the vector is identified by its position:

$$\mathbf{x} = \begin{bmatrix}x_1 \\ x_2 \\ \vdots \\ x_n\end{bmatrix}$$

**Real-World Example:** Representing a point in 3D space, a time series, or word embeddings in Natural Language Processing (NLP). 📝

```python
import numpy as np

# Vector example
vector = np.array([1, 2, 3, 4])
print(vector[0])  # Access first element: Output: 1
```
> ⚠️ **Note:** Python uses **zero-based indexing**, so the first element has index `0`.

### 3. Matrices 📊
A `matrix` is a two-dimensional collection of numbers, identified by two indices (row and column). For example:

$$\mathbf{A} = \begin{bmatrix}A_{1,1} & A_{1,2} \\ A_{2,1} & A_{2,2}\end{bmatrix}$$

**Real-World Example:** Representing images, layers in neural networks, or transformation operations in graphics. 🎨

```python
# Matrix example
matrix = np.array([[1, 2], [3, 4]])
print(matrix[0, 0])  # Access element in first row, first column: Output: 1
```

### 4. Tensors 🌀
A `tensor` generalizes matrices to higher dimensions. A scalar is a 0D tensor, a vector is a 1D tensor, and a matrix is a 2D tensor. Tensors with more dimensions represent complex datasets such as color videos or 3D models.

**Real-World Example:** Storing RGB values for images, sequences in video data, or multi-dimensional data in scientific computations.

```python
# Tensor example
tensor = np.ones((3, 4, 5))  # 3D tensor
print(tensor.shape)  # Outputs: (3, 4, 5)
```

---

## Basic Operations 🛠️

Mastering basic operations is essential for manipulating mathematical objects in linear algebra. Let’s explore some fundamental operations with Python examples.

### 1. Transpose 🔄
Switch the rows and columns of a matrix. This operation is crucial in various algorithms, including those in machine learning.

**Formula:**
$$\mathbf{A}^T_{i,j} = \mathbf{A}_{j,i}$$

```python
# Transpose a matrix
matrix = np.array([[1, 2, 3], [4, 5, 6]])
transposed = matrix.T
print(transposed)
# Output:
# [[1 4]
#  [2 5]
#  [3 6]]
```

### 2. Matrix Addition ➕
You can add matrices element-wise if they have the same shape. This operation is useful in combining data or adjusting weights in neural networks.

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
C = A + B
print(C)
# Output:
# [[ 6  8]
#  [10 12]]
```

### 3. Matrix Multiplication ✖️
Matrix multiplication is essential in machine learning, used in layer computations in neural networks. If $\mathbf{A}$ is of shape $(m, n)$ and $\mathbf{B}$ is $(n, p)$, their product $\mathbf{C} = \mathbf{A}\mathbf{B}$ has shape $(m, p)$.

**Formula:**
$$\mathbf{C}_{i,j} = \sum_{k=1}^{n} \mathbf{A}_{i,k} \mathbf{B}_{k,j}$$

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
C = A @ B
print(C)
# Output:
# [[19 22]
#  [43 50]]
```

### 4. Element-wise Multiplication ✨
Multiply matrices element-by-element. This is different from matrix multiplication and is useful in operations like scaling features.

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[2, 0], [1, 2]])
C = A * B
print(C)
# Output:
# [[2 0]
#  [3 8]]
```

### 5. Dot Product 🔗
The dot product of two vectors results in a scalar and is fundamental in calculating similarities and projections.

**Formula:**
$$\mathbf{a} \cdot \mathbf{b} = \sum_{i=1}^{n} a_i b_i$$

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
dot_product = np.dot(a, b)
print(dot_product)  # Output: 32
```

---

## Identity and Inverse Matrices 🔄

Understanding identity and inverse matrices is vital for solving systems of equations and transformations in linear algebra.

### 1. Identity Matrix 🟦
An identity matrix has `1`s on the diagonal and `0`s elsewhere. It acts as the multiplicative identity in matrix multiplication.

**Example:**
$$\mathbf{I} = \begin{bmatrix}1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1\end{bmatrix}$$

```python
I = np.eye(3)
print(I)
# Output:
# [[1. 0. 0.]
#  [0. 1. 0.]
#  [0. 0. 1.]]
```

### 2. Inverse Matrix 🧩
The inverse of $\mathbf{A}$, denoted as $\mathbf{A}^{-1}$, satisfies $\mathbf{A}\mathbf{A}^{-1} = \mathbf{I}$. Not all matrices have inverses; a matrix must be square and have a non-zero determinant to possess an inverse.

**Formula:**
$$\mathbf{A} \mathbf{A}^{-1} = \mathbf{I}$$

```python
from numpy.linalg import inv

A = np.array([[1, 2], [3, 4]])
A_inv = inv(A)
print(A_inv)
# Output:
# [[-2.   1. ]
#  [ 1.5 -0.5]]
```
> ⚠️ **Note:** Attempting to invert a singular matrix (determinant = 0) will result in an error.

---

## Solving Systems of Linear Equations 🔍

Solving systems of linear equations is a common task in linear algebra, especially in optimizing machine learning models.

A system of equations can be expressed as:
$$\mathbf{A}\mathbf{x} = \mathbf{b}$$
where $\mathbf{x}$ is the unknown vector we aim to solve for.

**Example:**
$$
2x + y = 1 \\
1x - y = -1
$$

```python
A = np.array([[2, 1], [1, -1]])
b = np.array([1, -1])
from numpy.linalg import solve
x = solve(A, b)
print(x)  # Output: [0. 1.]
```

---

## Additional Concepts 🌟

### 5. Determinant 📏
The determinant of a matrix provides important properties about the matrix, such as whether it is invertible. A matrix is invertible if and only if its determinant is non-zero.

**Formula (for 2x2 matrix):**
$$\text{det}(\mathbf{A}) = ad - bc$$

```python
from numpy.linalg import det

A = np.array([[1, 2], [3, 4]])
det_A = det(A)
print(det_A)  # Output: -2.0000000000000004
```

### 6. Eigenvalues and Eigenvectors 🔑
Eigenvalues and eigenvectors are fundamental in understanding matrix transformations. They are widely used in dimensionality reduction techniques like PCA (Principal Component Analysis).

**Definition:**
For a matrix $\mathbf{A}$, if $\mathbf{A}\mathbf{v} = \lambda\mathbf{v}$, then $\lambda$ is an eigenvalue and $\mathbf{v}$ is the corresponding eigenvector.

```python
from numpy.linalg import eig

A = np.array([[4, -2], [1, 1]])
eigenvalues, eigenvectors = eig(A)
print("Eigenvalues:", eigenvalues)
print("Eigenvectors:\n", eigenvectors)
```

### 7. Norms 📐
Norms measure the size or length of vectors and matrices. They are essential in optimization algorithms to minimize loss functions.

**Common Norms:**
- **L1 Norm (Manhattan Distance):** Sum of absolute values.
- **L2 Norm (Euclidean Distance):** Square root of the sum of squares.

```python
# Vector norms
vector = np.array([1, 2, 3])
l1_norm = np.linalg.norm(vector, 1)
l2_norm = np.linalg.norm(vector, 2)
print("L1 Norm:", l1_norm)  # Output: 6.0
print("L2 Norm:", l2_norm)  # Output: 3.7416573867739413
```

---

## Exercises 🛠️📚

### Exercise 1: Transpose 🔄
Create a $3 \times 2$ matrix and compute its transpose.

<details>
<summary>Solution</summary>

```python
import numpy as np

A = np.array([[1, 2], [3, 4], [5, 6]])
print("Original Matrix:\n", A)
transposed_A = A.T
print("Transposed Matrix:\n", transposed_A)
# Output:
# Original Matrix:
# [[1 2]
#  [3 4]
#  [5 6]]
# Transposed Matrix:
# [[1 3 5]
#  [2 4 6]]
```
</details>

### Exercise 2: Matrix Multiplication ✖️
Given $\mathbf{A} = \begin{bmatrix}1 & 2 \\ 3 & 4\end{bmatrix}$ and $\mathbf{B} = \begin{bmatrix}2 & 0 \\ 1 & 2\end{bmatrix}$, compute $\mathbf{C} = \mathbf{A}\mathbf{B}$.

<details>
<summary>Solution</summary>

```python
import numpy as np

A = np.array([[1, 2], [3, 4]])
B = np.array([[2, 0], [1, 2]])
C = A @ B
print(C)
# Output:
# [[4 4]
#  [10 8]]
```
</details>

### Exercise 3: Solve a System of Equations 🔍
Solve the system:

$$
2x + y = 3 \\
3x + 2y = 5
$$

<details>
<summary>Solution</summary>

```python
import numpy as np
from numpy.linalg import solve

A = np.array([[2, 1], [3, 2]])
b = np.array([3, 5])
x = solve(A, b)
print(x)  # Output: [1. 1.]
```
</details>

### Exercise 4: Compute the Determinant 📏
Find the determinant of the matrix $\mathbf{A} = \begin{bmatrix}4 & 7 \\ 2 & 6\end{bmatrix}$.

<details>
<summary>Solution</summary>

```python
import numpy as np
from numpy.linalg import det

A = np.array([[4, 7], [2, 6]])
det_A = det(A)
print(det_A)  # Output: 10.000000000000002
```
</details>

### Exercise 5: Eigenvalues and Eigenvectors 🔑
Find the eigenvalues and eigenvectors of the matrix $\mathbf{A} = \begin{bmatrix}3 & 1 \\ 0 & 2\end{bmatrix}$.

<details>
<summary>Solution</summary>

```python
import numpy as np
from numpy.linalg import eig

A = np.array([[3, 1], [0, 2]])
eigenvalues, eigenvectors = eig(A)
print("Eigenvalues:", eigenvalues)
print("Eigenvectors:\n", eigenvectors)
# Output:
# Eigenvalues: [3. 2.]
# Eigenvectors:
# [[1.         0.4472136]
#  [0.         0.89442719]]
```
</details>

### Exercise 6: Vector Norms 📐
Given a vector $\mathbf{v} = \begin{bmatrix}3 \\ 4\end{bmatrix}$, compute its L1 and L2 norms.

<details>
<summary>Solution</summary>

```python
import numpy as np

v = np.array([3, 4])
l1_norm = np.linalg.norm(v, 1)
l2_norm = np.linalg.norm(v, 2)
print("L1 Norm:", l1_norm)  # Output: 7.0
print("L2 Norm:", l2_norm)  # Output: 5.0
```
</details>

---

## Conclusion 🎉

You've now covered the fundamental concepts of linear algebra essential for AI applications. From understanding scalars, vectors, matrices, and tensors to performing basic operations and solving systems of equations, these tools form the backbone of many machine learning and deep learning algorithms. 📈

Stay tuned for more advanced linear algebra topics and their applications in AI! 🌟 Whether you're building neural networks, performing dimensionality reduction, or optimizing models, mastering these concepts will significantly enhance your capabilities in the AI field. 🚀

Happy coding! 💻✨