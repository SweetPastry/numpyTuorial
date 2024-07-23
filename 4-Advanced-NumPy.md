# Advanced NumPy
- Importing datasets
    - loadtxt
    - genfromtxt
- Processing data
    - Splitting data
- Summarizing data


```python
import numpy as np
```

## 1. More on array manipulation
- Flattening arrays
- Extending arrays
- Splitting arrays

### Flattening arrays
- ```flatten()``` converts multi-dimensional array into one-dimensional array (with same elements)


```python
# flatten example
arr = np.array([[1, 5], [7, 9], [12, 6]])
print(arr)
print('Shape of original array: ', arr.shape)
arr = arr.flatten()
print(arr)
print('Shape of flattened array: ', arr.shape)
```

    [[ 1  5]
     [ 7  9]
     [12  6]]
    Shape of original array:  (3, 2)
    [ 1  5  7  9 12  6]
    Shape of flattened array:  (6,)
    


```python
# above code is idential to below
arr = np.array([[1, 5], [7, 9], [12, 6]])
print(arr)
print('Shape of original array: ', arr.shape)
arr = arr.reshape(6)
print(arr)
print('Shape of flattened array: ', arr.shape)
```

    [[ 1  5]
     [ 7  9]
     [12  6]]
    Shape of original array:  (3, 2)
    [ 1  5  7  9 12  6]
    Shape of flattened array:  (6,)
    

### Extending arrays
- ```newaxis```: adds another axis (with size 1) to array
- ```tile()```: add another axis (while repeating original array) to array


```python
# newaxis example
arr = np.array([1, 2, 3, 4])
print(arr.shape)
arr_ = arr[:, np.newaxis]     # add new axis to second dimension
print(arr_.shape)
arr__ = arr[np.newaxis, :]    # add new axis to first dimension
print(arr__.shape)
print()
print(arr_)
print()
print(arr__)
```

    (4,)
    (4, 1)
    (1, 4)
    
    [[1]
     [2]
     [3]
     [4]]
    
    [[1 2 3 4]]
    


```python
# tile example
arr = np.array([1, 2, 3, 4])
arr_ = np.tile(arr, 2)
print(arr_.shape)
arr__ = np.tile(arr, (2, 3))    # repeat 2 on axis 0, 3 on axis 1
print(arr__.shape)
print()
print(arr_)
print()
print(arr__)
```

    (8,)
    (2, 12)
    
    [1 2 3 4 1 2 3 4]
    
    [[1 2 3 4 1 2 3 4 1 2 3 4]
     [1 2 3 4 1 2 3 4 1 2 3 4]]
    

### Splitting arrays


```python
# splitting into sub-arrays
arr = np.arange(8)
print(arr)
arr_split = np.array_split(arr, 4)
print(arr_split)
```

    [0 1 2 3 4 5 6 7]
    [array([0, 1]), array([2, 3]), array([4, 5]), array([6, 7])]
    


```python
# splitting 2-D arrays
arr = np.arange(12).reshape((4, 3))
print(arr)
arr_split = np.array_split(arr, 4, axis = 0)    # splitting over axis 0 => this is default
print(arr_split)
arr_split = np.array_split(arr, 3, axis = 1)    # splitting over axis 1
print(arr_split)
```

    [[ 0  1  2]
     [ 3  4  5]
     [ 6  7  8]
     [ 9 10 11]]
    [array([[0, 1, 2]]), array([[3, 4, 5]]), array([[6, 7, 8]]), array([[ 9, 10, 11]])]
    [array([[0],
           [3],
           [6],
           [9]]), array([[ 1],
           [ 4],
           [ 7],
           [10]]), array([[ 2],
           [ 5],
           [ 8],
           [11]])]
    

## 2. Broadcasting
- Broadcasting is at the heart of matrix operations in ```NumPy```
    - Broadcasting essentially means **"copying"** smaller array and performing **"implicit loops" **
- Vectorized operations are performed using C, instead of Python when broadcasting


```python
# trivial example
s = 2
arr = np.array([1, 2, 3, 4]) 
result = arr * s       # scalar 2 is "broadcasted" to all elements in array
print(result)
```

    [2 4 6 8]
    

### Efficiency of vectorized operation using implicit for-loop
- Let's see how much broadcasting is faster compared to explicit Python for-loop


```python
%%time
a1 = np.arange(1000000)
a1 = a1 * 2
```

    Wall time: 2.99 ms
    


```python
%%time
a2 = np.arange(1000000)
for i in range(1000000):
    a2[i] = a2[i] * 2
```

    Wall time: 568 ms
    

### Broadcasting rules
- Ground rules
    - All NumPy operations are *element-wise*, as default
    - When operation is performed on two arrays, shape of each array is compared element-wise.
    - Shape comparison starts from trailing dimension (axis = 0), and walks in increasing direction (0 => 1 => 2 => ...)
    - Two dimensions are compatible when
        - they are equal, or
        - one of them is 1 (in this case array with dimension 1 is copied to match the bigger one)
- Broadcasting 
    - Compare shape of two arrays from the back (the trailing dimension) to first dimension
    - If one array is bigger than another array in terms of dimension (i.e., shape), left-pad the shape of smaller array with 1
    - If ground rules are satisfied, broadcasting works. Shape of resulting array is equal to shape of bigger array (smaller array is "copied" repeatedly and operation is performed)
    
- **Example**: consider 2 arrays, ```A``` and ```B```
```ruby
A.shape = (4 X 5)
B.shape = (    5)
```
First, left-pad smaller array (```B```) with 1
```ruby
A.shape = (4 X 5)
B.shape = (1 X 5)
```
Trailing dimensions match (5), and first dimension of ```B``` has size 1, so broadcasting works. ```B``` is repeated 5 times and element-wise operation is fulfilled

- **Example 2**: consider 2 arrays, ```C``` and ```D```
```ruby
C.shape = (3 X 4 X 5)
D.shape = (    4 X 5)
```
First, left-pad smaller array (```D```) with 1
```ruby
C.shape = (3 X 4 X 5)
D.shape = (1 X 4 X 5)
```
Last two dimensions match (4 X 5), and first dimension of ```D``` has size 1, so broadcasting works. ```D``` is repeated 3 times and element-wise operation is fulfilled

- **Example 3**: consider 2 arrays, ```E``` and ```F```
```ruby
E.shape = (2 X 3 X 5)
F.shape = (        3)
```
First, left-pad smaller array (```F```) with 1
```ruby
E.shape = (2 X 3 X 5)
F.shape = (1 X 1 X 3)
```
As trailing dimensions do not match, broadcasting does not work


```python
arr1 = np.array([1, 2, 3])
print(arr1.shape)
arr2 = np.array([[4, 5, 6], [7, 8, 9]])
print(arr2.shape)
arr3 = arr1 + arr2
print(arr3)
```

    (3,)
    (2, 3)
    [[ 5  7  9]
     [ 8 10 12]]
    

## Quiz 4.
- Create two 2-dimensional arrays of random integers, both with shape (2, 10).
- Try two different ways of concatenation: (append one after the other / merge side by side).


```python
## Your answer

```
