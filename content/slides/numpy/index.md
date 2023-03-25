---
title: Introduction to NumPy
summary: An introduction to using Wowchemy's Slides feature.
authors: ["Parsa Abbasi"]
tags: ["NumPy"]
categories: []
date: '2019-02-05T00:00:00Z'
slides:
  # Choose a theme from https://github.com/hakimel/reveal.js#theming
  # black, white, league, beige, night, serif, simple, solarized, sky, moon, blood, dracula 
  theme: moon 
  # Choose a code highlighting style (if highlighting enabled in `params.toml`)
  #   Light style: github. Dark style: dracula (default).
  highlight_style: dracula
---

## Introduction to NumPy
[Installation](https://numpy.org/install/) | [Documentation](https://numpy.org/doc/stable/)

<div style="font-size:18px; margin-top:80px">
Last updated: March 26, 2023
</div>

---

### Introduction
NumPy, short for Numerical Python, is a fundamental library for data analysis and scientific computing in the `Python` programming language. 

---

### Advantages (1)

- **Multidimensional Arrays:** NumPy arrays can have any number of dimensions, which makes it possible to store and manipulate complex data sets.

- **High Performance:** NumPy core is based on a highly optimized `C` implementation, which means that it can perform mathematical and numerical operations much faster than pure Python.

---

### Advantages (2)

- **Mathematical Functions:** NumPy provides a wide variety of mathematical functions for operations, including statistics, linear algebra, and Fourier Transforms.

- **Efficient and Fast Computation:** NumPy allows for fast and accurate computation through powerful vectorized operations and optimized mathematical functions. 

---

### N-dimensional array

One of the key features of NumPy is its N-dimensional array object, or `ndarray`, which is a fast, flexible container for large datasets in Python.

**Note:** An 'ndarray' is a multidimensional, <u>homogeneous</u> array which means that all the elements in the array are of the same type.

---

### Creating a NumPy array (1)
The easiest way to create an `ndarray` is to use the `array()` function and pass any sequence-like object (e.g. a list, tuple, or another array) to it.

```python
import numpy as np
data = [1, 2.5, 3.1, 4, 5.6]
arr = np.array(data)
```

```output
array([1. , 2.5, 3.1, 4. , 5.6])
```

---

### Creating a NumPy array (2)

```python
import numpy as np
data = [[1, 2, 3, 4], [5, 6, 7, 8]]
arr = np.array(data)
```

```output
array([[1, 2, 3, 4],
       [5, 6, 7, 8]])
```

---

### Number of dimensions
We can check the number of dimensions of an array using the `ndim` attribute.

```output
array([[1, 2, 3, 4],
       [5, 6, 7, 8]])
```

```python
arr.ndim
```

```output
2
```

---

### Shape of an array
The `shape` attribute returns a tuple of integers indicating the size of the array in each dimension.

```output
array([[1, 2, 3, 4],
       [5, 6, 7, 8]])
```

```python
arr.shape
```

```output
(2, 4)
```

---

### Data type (1)

The `dtype` attribute is an object describing the type of the elements in the array. Unless specified, NumPy tries to infer a good data type for the array that it creates.

```output
array([[1, 2, 3, 4],
       [5, 6, 7, 8]])
```

```python
arr.dtype
```

```output
dtype('int64')
```

---

### Data type (2)
A full list of NumPy data types can be found [here](https://numpy.org/devdocs/user/basics.types.html).
<div style="font-size:20px">
<table>
  <thead>
    <tr>
      <th>Type</th>
      <th>Type code</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>bool</code></td>
      <td><code>?</code></td>
      <td>Boolean (True or False) stored as a byte</td>
    </tr>
    <tr>
      <td><code>int8</code></td>
      <td><code>i1</code></td>
      <td>Byte (-128 to 127)</td>
    </tr>
    <tr>
      <td><code>int16</code></td>
      <td><code>i2</code></td>
      <td>Integer (-32768 to 32767)</td>
    </tr>
    <tr>
      <td><code>int32</code></td>
      <td><code>i4</code></td>
      <td>Integer (-2147483648 to 2147483647)</td>
    </tr>
    <tr>
      <td><code>int64</code></td>
      <td><code>i8</code></td>
      <td>Integer (-9223372036854775808 to 9223372036854775807)</td>
    </tr>
    <tr>
      <td><code>uint8</code></td>
      <td><code>u1</code></td>
      <td>Unsigned integer (0 to 255)</td>
    </tr>
    <tr>
      <td><code>float16</code></td>
      <td><code>f2</code></td>
      <td>Half precision float: sign bit, 5 bits exponent, 10 bits mantissa</td>
    </tr>
    <tr>
      <td><code>float32</code></td>
      <td><code>f4</code></td>
      <td>Single precision float: sign bit, 8 bits exponent, 23 bits mantissa</td>
    </tr>
    <tr>
      <td><code>float64</code></td>
      <td><code>f8</code></td>
      <td>Double precision float: sign bit, 11 bits exponent, 52 bits mantissa</td>
    </tr>
    <tr>
      <td><code>string_</code></td>
      <td><code>S</code></td>
      <td>Fixed-length ASCII string type (1 byte per character)</td>
    </tr>
    <tr>
      <td><code>unicode_</code></td>
      <td><code>U</code></td>
      <td>Fixed-length Unicode type (number of bytes platform specific)</td>
    </tr>
    <tr>
      <td><code>object</code></td>
      <td><code>O</code></td>
      <td>Python object type</td>
    </tr>
  </tbody>
</table>

</div>

---

### Data type examples (1)

Boolean

```python
array = np.array([True, False, True], dtype=bool)
```

```output
array([ True, False,  True])
```

String

```python
array = np.array(['hello', 'world', 'numpy'], dtype=np.string_)
```

```output
array([b'hello', b'world', b'numpy'], dtype='|S5')
```

---
### Data type examples (2)

Unicode

```python
array = np.array([u'سلام',u'بله',u'خیر'], dtype=np.unicode_)
```

```output
array(['سلام', 'بله', 'خیر'], dtype='<U4')
```

Object

```python
array = np.array([{"name": "John", "age": 25}, [1, 2, 3], "hello"], dtype=object)
```

```output
array([{'name': 'John', 'age': 25}, list([1, 2, 3]), 'hello'],
      dtype=object)
```

---
### Casting data type
You can explicitly cast an array from one dtype to another using ndarray's `astype` method.

```python
array = np.array([1, 2, 3, 4, 5])
```

```output
array([1, 2, 3, 4, 5])
```

```python
array.astype(np.float64)
```

```output
array([1., 2., 3., 4., 5.])
```
<div style="font-size:20px">
<b style="color:orange">Note:</b> Calling <code>astype</code> always creates a <u>copy</u> of the data, even if the new dtype is the same as the old dtype.
</div>

---

### Array creation functions (1)
`zeros` and `ones` create arrays of `0`'s or `1`'s, respectively, with a given length or shape. `empty` creates an array without initializing its values to any particular value.

```python
np.zeros(10)
```

```output
array([0., 0., 0., 0., 0., 0., 0., 0., 0., 0.])
```

```python
np.ones((2, 6))
```

```output
array([[1., 1., 1., 1., 1., 1.],
       [1., 1., 1., 1., 1., 1.]])
```

```python
np.empty((1, 2))
```

```output
array([[1., 1.]])
```

---

### Array creation functions (2)
zeros_like and ones_like create arrays of 0's or 1's with the same shape and dtype as a given array.

```python
array = np.array([[1, 2, 3], [4, 5, 6]])
```

```output
array([[1, 2, 3],
       [4, 5, 6]])
```

```python
np.zeros_like(array)
```

```output
array([[0, 0, 0],
       [0, 0, 0]])
```

```python
np.ones_like(array)
```

```output
array([[1, 1, 1],
       [1, 1, 1]])
```

---

### Array creation functions (3)
`full` creates an array of a given length or shape and fills it with a given value.

```python
np.full((2, 2), 5)
```

```output
array([[5, 5],
       [5, 5]])
```

```python
np.full((2, 2), np.pi)
```

```output
array([[3.14159265, 3.14159265],
       [3.14159265, 3.14159265]])
```

---

### Array creation functions (4)
`arange` is an array-valued version of the built-in Python `range` function. It returns an array instead of a list.

```python
np.arange(10)
```

```output
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
```

```python
np.arange(1, 10, 2)
```

```output
array([1, 3, 5, 7, 9])
```

---

### Array creation functions (5)
`linspace` creates an array of evenly spaced values within a given interval.

```python
np.linspace(0, 10, 5)
```

```output
array([ 0.,  2.5,  5.,  7.5, 10.])
```

```python
np.linspace(0, 10, 5, endpoint=False)
```

```output
array([0., 2., 4., 6., 8.])
```

---

### Array creation functions (6)
`eye` and `identity` create square `N x N` identity matrices. `1`'s on the diagonal and `0`'s elsewhere.

```python
np.eye(2)
```

```output
array([[1., 0.],
       [0., 1.]])
```

```python
np.identity(3)
```

```output
array([[1., 0., 0.],
       [0., 1., 0.],
       [0., 0., 1.]])
```

<div style="font-size:20px">
<b style="color:orange">Note:</b> <code>eye</code> is more flexible in creating identity matrices with diagonal shifted by any position (using <code>k</code> parameter), while <code>identity</code> is simpler and faster for creating square identity matrices with diagonal in center.
</div>

---

### Arithmetic operations (1)
Vectorization is the ability of NumPy to perform mathematical computations and array operations on entire arrays without the need to write explicit loops.

Any arithmetic operations between equal-size arrays applies the operation <u>element-wise</u>.

```python
array1 = np.array([1, 2, 3, 4, 5])
array2 = np.array([5, 4, 3, 2, 1])
```

```python
array1 - array2
```

```output
array([-4, -2,  0,  2,  4])
```

```python
array1 * array2
```

```output
array([5, 8, 9, 8, 5])
```

---

### Arithmetic operations (2)
Arithmetic operations with scalars propagate the scalar argument to each element in the array.

```python
array1 = np.array([1, 2, 3, 4, 5])
```

```python
1 / array1
```

```output
array([1.        , 0.5       , 0.33333333, 0.25      , 0.2       ])
```

```python
array1 ** 2
```

```output
array([ 1,  4,  9, 16, 25])
```

---

### Arithmetic operations (3)
Comparison operators between arrays are also vectorized.

```python
array1 = np.array([1, 2, 3, 4, 5])
array2 = np.array([5, 4, 3, 2, 1])
```

```python
array1 > array2
```

```output
array([False, False, False,  True,  True])
```

```python
array1 == array2
```

```output
array([False, False,  True, False, False])
```

---

### Broadcasting (1)
Arithmetic operations between differently sized arrays is called <b>broadcasting</b>. Broadcasting allows arithmetic operations between arrays of different shapes.

```python
array1 = np.array([[1, 2, 3], [4, 5, 6]])
array2 = np.array([1, 2, 3])
```

```python
array1 + array2
```

```output
array([[2, 4, 6],
       [5, 7, 9]])
```

---

### Broadcasting (2)
Broadcasting is a powerful mechanism that allows NumPy to work with arrays of different shapes when performing arithmetic operations. However, if the arrays do not have compatible shapes, a <b>ValueError</b> will be raised.

```python
array1 = np.array([[1, 2, 3], [4, 5, 6]])
array2 = np.array([1, 2])
```

```python
array1 + array2
```

```output
ValueError: operands could not be broadcast together with shapes (2,3) (2,) 
```

---