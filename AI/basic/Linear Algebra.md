---
Created by: Shudipto Trafder
Created time: 2024-05-21T00:09
Last edited time: 2024-05-21T00:09
tags:
  - ai
  - math
---
## Scalars 
Most everyday mathematics consists of manipulating numbers one at a time. Formally, we call these values _scalars_. We denote scalars by ordinary lower-cased letters (e.g., 𝑥, 𝑦, and 𝑧) and the space of all (continuous) _real-valued_ scalars by 𝑅.  For expedience, we will skip past rigorous definitions of _spaces_: just remember that the expression 𝑥∈𝑅 is a formal way to say that 𝑥 is a real-valued scalar. The symbol ∈ (pronounced “in”) denotes membership in a set. For example, 𝑥,𝑦∈{0,1} indicates that 𝑥 and 𝑦 are variables that can only take values 0 or 1.

## Vectors 
For current purposes, you can think of a vector as a fixed-length array of scalars. For example, if we were training a model to predict the risk of a loan defaulting, we might associate each applicant with a vector whose components correspond to quantities like their income, length of employment, or number of previous defaults. We denote vectors by bold lowercase letters, (e.g., 𝑥, 𝑦, and 𝑧). Vectors are implemented as 1st-order tensors.

$$\begin{split}\mathbf{x} =\begin{bmatrix}x_{1}  \\ \vdots  \\x_{n}\end{bmatrix},\end{split}$$

We can refer to an element of a vector by using a subscript. For example, 𝑥2 denotes the second element of 𝑥. Since 𝑥2 is a scalar, we do not bold it. By default, we visualize vectors by stacking their elements vertically. 

To indicate that a vector contains 𝑛 elements, we write 𝑥∈𝑅^𝑛. Formally, we call 𝑛 the _dimensionality_ of the vector.

## Matrices: 
Just as scalars are 0th-order tensors and vectors are 1st-order tensors, matrices are 2nd-order tensors. We denote matrices by bold capital letters (e.g., 𝑋, 𝑌, and 𝑍), and represent them in code by tensors with two axes. The expression $\mathbf{A} \in \mathbb{R}^{m \times n}$ indicates that a matrix 𝐴 contains 𝑚×𝑛 real-valued scalars, arranged as 𝑚 rows and 𝑛 columns.
$$
\begin{split}\mathbf{A}=\begin{bmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} & a_{m2} & \cdots & a_{mn} \\ \end{bmatrix}.\end{split}
$$
### Functions
1. **Matrix Addition and Subtraction**: Combining matrices by adding or subtracting their corresponding elements.
    
2. **Scalar Multiplication**: Multiplying each element of a matrix by a scalar (a single number).
    
3. **Matrix Multiplication**: Combining two matrices to produce a third matrix. It involves the dot product of rows and columns.
    
4. **Transpose of a Matrix**: Flipping a matrix over its diagonal, turning rows into columns and vice versa.
    
5. **Matrix Inversion**: Finding a matrix that, when multiplied by the original matrix, yields the identity matrix. Matrix inversion is a process by which a given square matrix ( A ) is transformed into another matrix ( A^{-1} ), known as the inverse matrix, such that when ( A ) is multiplied by ( A^{-1} ), the result is the identity matrix ( I ). The identity matrix is a special matrix that has 1’s on the diagonal and 0’s elsewhere.
    
6. **Determinants**: A scalar value that is a function of the entries of a square matrix. It has many properties and is used in matrix inversion and solving systems of linear equations.
    
7. **Eigenvalues and Eigenvectors**: Scalars and vectors associated with a matrix that are invariant under the transformation represented by the matrix.

	- **Eigenvalues**: These are scalars, denoted by ( $\lambda$ ), associated with a linear system of equations (or a matrix). They are values for which there exists a non-zero vector ( v ) such that when the matrix is multiplied by ( v ), the product is the same as scaling ( v ) by ( $\lambda$ ). Mathematically, for a matrix ( A ), the eigenvalue equation is $( Av = \lambda v )$.
    
	- **Eigenvectors**: These are the non-zero vectors ( v ) that satisfy the eigenvalue equation mentioned above. They represent directions in which the application of the matrix ( A ) does not change the direction of ( v ), only its magnitude by the factor of ( $\lambda$ ).
$$
\begin{align*}
&\text{For a matrix } A, \text{ the eigenvalue equation is:} \\
&Av = \lambda v \\
&\text{To find the eigenvalues, solve the characteristic equation:} \\
&\text{det}(A - \lambda I) = 0 \\
&\text{Once the eigenvalues } \lambda \text{ are found, find the eigenvectors by solving:} \\
&(A - \lambda I)v = 0
\end{align*}

$$
## Tensors
Tensors give us a generic way of describing extensions to $n^{\textrm{th}}$-order arrays. We denote general tensors by capital letters with a special font face (e.g., 𝑋, 𝑌, and 𝑍) and their indexing mechanism (e.g., $x_{ijk}$ and $[\mathsf{X}]_{1, 2i-1, 3}$) follows naturally from that of matrices.

The element wise product of two matrices is called their _Hadamard product_ (denoted ⊙). We can spell out the entries of the Hadamard product of two matrices $\mathbf{A}, \mathbf{B} \in \mathbb{R}^{m \times n}$:
$$
\begin{split}\mathbf{A} \odot \mathbf{B} =
\begin{bmatrix}
    a_{11}  b_{11} & a_{12}  b_{12} & \dots  & a_{1n}  b_{1n} \\
    a_{21}  b_{21} & a_{22}  b_{22} & \dots  & a_{2n}  b_{2n} \\
    \vdots & \vdots & \ddots & \vdots \\
    a_{m1}  b_{m1} & a_{m2}  b_{m2} & \dots  & a_{mn}  b_{mn}
\end{bmatrix}.\end{split}
$$
```python
A = torch.arange(6, dtype=torch.float32).reshape(2, 3)
B = A.clone()  # Assign a copy of A to B by allocating new memory

A * B
```

#### Reduction
Often, we wish to calculate the sum of a tensor’s elements. To express the sum of the elements in a vector 𝑥 of length 𝑛, we write $\sum_{i=1}^n x_i$. There is a simple function for it
```python
x = torch.arange(3, dtype=torch.float32)
x, x.sum()
```
To express sums over the elements of tensors of arbitrary shape, we simply sum over all its axes. For example, the sum of the elements of an 𝑚×𝑛 matrix 𝐴 could be written $\sum_{i=1}^{m} \sum_{j=1}^{n} a_{ij}$
To sum over all elements along the rows (axis 0), we specify `axis=0` in `sum`. Specifying `axis=1` will reduce the column dimension (axis 1) by summing up elements of all the columns. Reducing a matrix along both rows and columns via summation is equivalent to summing up all the elements of the matrix.
```python
A.sum(axis=0) # sum row wise
A.sum(axis=1) # sum column wise

A.sum(axis=[0, 1]) == A.sum() # sum in both direction and combine
```
A related quantity is the _mean_, also called the _average_. We calculate the mean by dividing the sum by the total number of elements.
```python
A.mean(), A.sum() / A.numel()
A.mean(axis=0), A.sum(axis=0) / A.shape[0] # vi axis
```

#### Non Reduction Sum:
Sometimes it can be useful to keep the number of axes unchanged when invoking the function for calculating the sum or mean. This matters when we want to use the broadcast mechanism. **Non-Reduction Sum** refers to the sum operation applied to a tensor without reducing its dimensionality.  For example, consider a tensor `X` with shape `(2, 3, 4)`. If we perform a non-reduction sum over the second axis (axis=1), we would sum the elements along this axis but still retain a tensor with three dimensions.

Here’s how it works mathematically:

Given a tensor ( X ) with dimensions ( (i, j, k) ), performing a non-reduction sum over the second axis would result in a new tensor ( Y ) with dimensions ( (i, 1, k) ), where each element of ( Y ) is the sum of the corresponding elements along the second axis of ( X ).

```python
import torch
X = torch.rand(2, 3, 4)  # Random tensor of shape (2, 3, 4)
Y = X.sum(axis=1, keepdims=True)  # Non-reduction sum over the second axis
```

#### Dot Products
One of the most fundamental operations is the dot product. Given two vectors $\mathbf{x}, \mathbf{y} \in \mathbb{R}^d$, their _dot product_ 𝑥⊤𝑦 (also known as _inner product_, ⟨𝑥,𝑦⟩) is a sum over the products of the elements at the same position: $\mathbf{x}^\top \mathbf{y} = \sum_{i=1}^{d} x_i y_i$
Equivalently, we can calculate the dot product of two vectors by performing an element wise multiplication followed by a sum:
```python
torch.sum(x * y) or torch.dot(x, y)
```
Dot products are useful in a wide range of contexts. For example, given some set of values, denoted by a vector $\mathbf{x} \in \mathbb{R}^n$, and a set of weights, denoted by 𝑤∈𝑅𝑛, the weighted sum of the values in 𝑥 according to the weights 𝑤 could be expressed as the dot product 𝑥⊤𝑤. When the weights are non negative and sum to 1, i.e., $\left(\sum_{i=1}^{n} {w_i} = 1\right)$, the dot product expresses a _weighted average_. After normalizing two vectors to have unit length, the dot products express the cosine of the angle between them.
```
a = [1, 2]
b = [3, 4]

ans = 1*3 + 2 *4
```

[Youtube: The meaning of the dot product](https://www.youtube.com/watch?v=BcxfxvYCL1g) 


