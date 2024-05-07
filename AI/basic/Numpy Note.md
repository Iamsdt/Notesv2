---
tags:
  - ai
  - numpy
Date: 2024-05-07T22:00:00
---

##### Examining Array:

```python
arr1.dtype # float64
arr2.dtype # int32
arr2.ndim # 2
arr2.shape # (2, 4) - axis 0 is rows, axis 1 is columns
arr2.size # 8 - total number of elements
len(arr2) # 2 - size of first dimension (aka axis)
```

##### Transpose

```python
np.transpose(arr)

arr.T
```

##### Flatten
```python
 arr.flatten()
```

##### Ravel
returns a view of the original array whenever possible.
```python
arr.ravel()
```

##### Numpy internals 
By default Numpy use C convention, ie, Row-major language: The matrix is
stored by rows. In C, the last index changes most rapidly as one moves through the array as
stored in memory.

For 2D arrays, sequential move in the memory will:
- iterate over rows (axis 0)
- iterate over columns (axis 1)
For 3D arrays, sequential move in the memory will:
- iterate over plans (axis 0)
- iterate over rows (axis 1)
* iterate over columns (axis 2)


##### Hstack vs Stack

**np.hstack** (horizontal stack) is used to stack arrays in sequence horizontally (i.e., column-wise). This is equivalent to concatenation along the second axis, except for 1-D arrays where it concatenates along the first axis.
```python
a = np.array([1, 2, 3])  
b = np.array([4, 5, 6])  
  
result = np.hstack((a, b))  
print(result)  # Output: [1 2 3 4 5 6]
```

**np.stack**, on the other hand, joins a sequence of arrays along a new axis. The axis parameter specifies the index of the new axis in the dimensions of the result. For example, if axis=0 it will be the first dimension and if axis=-1 it will be the last dimension.
```python
a = np.array([1, 2, 3])  
b = np.array([4, 5, 6])  
  
result = np.stack((a, b), axis=0)  
print(result)  
# Output: # [[1 2 3]  
#  [4 5 6]]
```


##### Vectorized Operations

```python
np.ceil(nums)
 # also floor, rint (round to nearest int)
```

##### Euclidean distance
The Euclidean distance between two points in either the plane or 3-dimensional space measures the length of a segment connecting the two points. It is the most obvious way of representing distance between two points.

The Euclidean distance between two points `p` and `q` with coordinates `(p1, p2,..., pn)` and `(q1, q2,..., qn)` respectively in n-dimensional space is:

$$
sqrt((q1-p1)^2 + (q2-p2)^2 + ... + (qn-pn)^2)
$$


In the context of computing, when we talk about Euclidean distance, we're generally talking about distance between two vectors. For two vectors `v1` and `v2`, the Euclidean distance is computed as the square root of the sum of absolute squares of its elements.

```python
import numpy as np

# Define two vectors
v1 = np.array([1, 2, 3])
v2 = np.array([4, 5, 6])

# Compute Euclidean distance
np.sqrt(np.sum((v1 - v2) ** 2))
```

In the above code, `np.linalg.norm(v1 - v2)` computes the Euclidean distance between vectors `v1` and `v2`.


Broadcasting
Sources: https://docs.scipy.org/doc/numpy-1.13.0/user/basics.broadcasting.html Implicit con- version to allow operations on arrays of different sizes. - The smaller array is stretched or “broadcasted” across the larger array so that they have compatible shapes. - Fast vectorized operation in C instead of Python. - No needless copies.

Rules
Starting with the trailing axis and working backward, Numpy compares arrays dimensions.
• If two dimensions are equal then continues
• If one of the operand has dimension 1 stretches it to match the largest one
• When one of the shapes runs out of dimensions (because it has less dimensions than
the other shape), Numpy will use 1 in the comparison process until the other shape’s
dimensions run out as well.
