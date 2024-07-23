# NumPy Primer - 2
- Array indexing & slicing
    - Indexing
    - Slicing
- Array operations
- Array functions
    - Creating sequence of numbers
    - Manipulating arrays
    - Matrix/vector multiplications
    - Basic statistics


```python
import numpy as np
```

## 1. Indexing & slicing
- Array indexing & slicing is largely similar to Python indexing & slicing

<br>
<img src="https://www.safaribooksonline.com/library/view/python-for-data/9781449323592/httpatomoreillycomsourceoreillyimages1346880.png" style="width: 400px"/>

<img src="https://www.safaribooksonline.com/library/view/python-for-data/9781449323592/httpatomoreillycomsourceoreillyimages1346882.png" style="width: 400px"/>

### Indexing
- Note than index starts with ```axis 0 ``` and increments


```python
# case of 1-D arrays
a1 = np.array([1, 2, 3, 4, 5])
print(a1[0])
print(a1[2])
print(a1[-1])
```

    1
    3
    5
    


```python
# case of 2-D arrays
a2 = np.array([[1, 2, 3], [4, 5, 6]])
print(a2[0])
print(a2[0, 1])
```

    [1 2 3]
    2
    


```python
# case of 3-D arrays
a3 = np.array([[[1,2,3], [4,5,6], [7,8,9], [10,11,12]]])
print(a3[0])
print(a3[0][1])
print(a3[0][1][1])
```

    [[ 1  2  3]
     [ 4  5  6]
     [ 7  8  9]
     [10 11 12]]
    [4 5 6]
    5
    

### Slicing


```python
# case of 1-D arrays
a4 = np.array([1, 2, 3, 4, 5])
print(a4[2:])
print(a4[:-2])
```

    [3 4 5]
    [1 2 3]
    


```python
# case of 2-D arrays
a5 = np.array([[1,2,3],[3,4,5]])
print(a5[:, 0])         # selecting all rows in 0th column
print(a5[0, :])         # selecting all columns in 0th row
print(a5[0, :2])        # selecting first two columns in 0th row
print(a5[:, 1:])        # selecting last two columns in every row
```

    [1 3]
    [1 2 3]
    [1 2]
    [[2 3]
     [4 5]]
    

### Boolean indexing
- Boolean array has same shape with original array
    - If each element satisfy certain condition, corresponding element in boolean array is ```True```
    - If not, ```False```


```python
# creating boolean array
a6 = np.array([1, 2, 3, 4, 5])
bool_arr = (a6 % 2 == 1)   # index only even integers
print(bool_arr)
```

    [ True False  True False  True]
    


```python
# using boolean array to index
print(a6[a6%2 == 0])         # 2 and 4 as result
```

    [2 4]
    


```python
# applying 1-D boolean array to multi-dimensional array
a7 = np.array([[1, 2], [3, 4], [5, 6], [7, 8], [9, 10]])    # shape = (5, 2)
bool_arr = np.array([True, True, False, False, True])       # shape = (5,)
print(a7[bool_arr])
```

    [[ 1  2]
     [ 3  4]
     [ 9 10]]
    

### Exercise 2-1.
- Create 1-D array containing integers 0 to 99
- Using indexing, print element in position ```(95,)```
- Using slicing, select and print first 30th elements in array 


```python
## Your answer

```

### Exercise 2-2.
- Create 2-D array with ```shape (3,3) ``` containing integers 1 to 9
- Using indexing, print element in position ```(1,1)```
- Using slicing, select and print 2nd column of array, i.e., ```(,1)```


```python
### Your answer
```

## 2. Array operations
- NumPy array operations are rather different from Python list operations
    - Array operations are *element-wise* as default
    - So, to perform array operations, ```shape``` of arrays should be the same
    - Correspondingly, ```shape``` of resulting array is identical as well
- To perform operations other than element-wise operations, NumPy functions should be used


```python
# case of 1-D lists
l1 = [1, 2, 3]
l2 = [4, 5, 6]
print(l1 + l2)
```

    [1, 2, 3, 4, 5, 6]
    


```python
# case of 1-D arrays
a1 = np.array(l1)
a2 = np.array(l2)
print(a1 + a2)
```

    [5 7 9]
    


```python
# case of 2-D arrays
a3 = np.array([[1,2,3], [4,5,6]])
a4 = np.array([[7,8,9], [10,11,12]])
print(a3 + a4)
print(a3 - a4)
print(a3 * a4)
print(a3 / a4)    # note that result is array of floats
```

    [[ 8 10 12]
     [14 16 18]]
    [[-6 -6 -6]
     [-6 -6 -6]]
    [[ 7 16 27]
     [40 55 72]]
    [[0.14285714 0.25       0.33333333]
     [0.4        0.45454545 0.5       ]]
    


```python
# operation between scalar and array
# scalar is "spread out" to each element in array
a5 = np.array([[1,2], [3,4]])
print(a5 + 2)
print(a5 - 2)
print(a5 * 2)
print(a5 / 2)     # note that result is array of floats
```

    [[3 4]
     [5 6]]
    [[-1  0]
     [ 1  2]]
    [[2 4]
     [6 8]]
    [[0.5 1. ]
     [1.5 2. ]]
    

### Exercise 2-3.
- Create 2-D array with ```shape (3, 2) ``` containing integers 1 from 6
- By slicing,
    - Twice elements only in second column of array (i.e., multiply by 2)
    - Reduce elements only in third row of array by 1 (i.e., minus by 1)


```python
## Your answer
```

### Exercise 2-4.
- Perform same operation in Exercise 2-4 by creating another matrix with same shape


```python
## Your answer
```

## 3. Array functions
- NumPy provides a number of functions useful for data processing

### Creating sequence of numbers
- NumPy supports functions to effectively create sequence of numbers, similar to ```range()``` function in Python


```python
# arange() generates sequence of integers as 1-D array
a1 = np.arange(10)
print(type(a1))
print(a1)
```

    <class 'numpy.ndarray'>
    [0 1 2 3 4 5 6 7 8 9]
    


```python
# step parameter can be set up
a2 = np.arange(10, step = 2)
print(a2)
```

    [0 2 4 6 8]
    


```python
# linspace() generates sequence of evenly spaced numbers over a specified interval
a3 = np.linspace(start = 0, stop = 5, num = 10)
print(a3)
a4 = np.linspace(start = 0, stop = 5, endpoint = False, num = 10) # stop exclusive
print(a4)
```

    [0.         0.55555556 1.11111111 1.66666667 2.22222222 2.77777778
     3.33333333 3.88888889 4.44444444 5.        ]
    [0.  0.5 1.  1.5 2.  2.5 3.  3.5 4.  4.5]
    

### Manipulating arrays
- Arrays can be manipulated using diverse functions


```python
# reshaping array
a1 = np.arange(9)
a2 = a1.reshape(3,3)
print(a2)
a3 = np.arange(8)
a4 = a3.reshape(4,2)
print(a4)
```

    [[0 1 2]
     [3 4 5]
     [6 7 8]]
    [[0 1]
     [2 3]
     [4 5]
     [6 7]]
    


```python
# transposing array
# colums & rows are reversed
# (M, N)  => (N, M)
a5 = np.arange(8).reshape(2,4)
print(a5)
print(a5.shape)
a6 = a5.transpose()
print(a6)
print(a6.shape)
```

    [[0 1 2 3]
     [4 5 6 7]]
    (2, 4)
    [[0 4]
     [1 5]
     [2 6]
     [3 7]]
    (4, 2)
    


```python
# merging two arrays
a7 = np.arange(5)
a8 = np.arange(5, 10)
a9 = np.concatenate((a7, a8))
print(a9)
```

    [0 1 2 3 4 5 6 7 8 9]
    


```python
# stacking arrays
a10 = np.hstack((a7, a8))    # stacking arrays horizontally (column-wise)
print(a10)
a11 = np.vstack((a7, a8))    # stacking arrays vertically (row-wise)
print(a11)
```

    [0 1 2 3 4 5 6 7 8 9]
    [[0 1 2 3 4]
     [5 6 7 8 9]]
    


```python
# sorting arrays
a12 = np.random.randint(0, 10, 10)    # create random array
print(a12)
a12.sort()                            # sort in ascending order
print(a12)
a12 = a12[::-1]                       # sort in descending order
print(a12)
```

    [9 1 5 0 5 6 1 1 1 6]
    [0 1 1 1 1 5 5 6 6 9]
    [9 6 6 5 5 1 1 1 1 0]
    

### Matrix/vector multiplications
- As seen in section 2, array multiplications are *element-wise* as default
- By using ```inner()``` or ```dot()``` functions, inner products (dot products) can be performed
    - Note that to perform matrix multiplication using ```dot()```, number of columns of first matrix (size of second ```dimension```) and number of rows of second matrix (size of first ```dimension```) should match
    - e.g., consider the case of multiplying array with shape (2, 3) and array with shape (3, 2)
        - Number of columns of first matrix = 3
        - Number of rows of second matrix = 3
        - Resulting matrix shape = (2, 2
    
<br>
<img src="https://www.mathsisfun.com/algebra/images/matrix-multiply-a.svg" style="width: 500px"/>    


```python
# case of 1-D arrays
a1 = np.array([1,2,3])
a2 = np.array([4,5,6])
print(a1 * a2)
print(np.inner(a1, a2))
print(np.dot(a1, a2))
```

    [ 4 10 18]
    32
    32
    


```python
# case of 2-D arrays
a3 = np.array([[1,2,3], [4,5,6]])     # shape = (2, 3)
a4 = np.array([[2,4,6]])              # shape = (1, 3)
print(a3 * a4)                   # note that a4 is "broadcasted" to a3
print(np.inner(a3, a4))          # note that a4 is "broadcasted" to a3
print(np.dot(a3, a4))            # not defined as shapes does not match
```

    [[ 2  8 18]
     [ 8 20 36]]
    [[28]
     [64]]
    


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    C:\Users\Administrator\AppData\Local\Temp\ipykernel_22816\4020098090.py in <module>
          4 print(a3 * a4)                   # note that a4 is "broadcasted" to a3
          5 print(np.inner(a3, a4))          # note that a4 is "broadcasted" to a3
    ----> 6 print(np.dot(a3, a4))            # not defined as shapes does not match
    

    <__array_function__ internals> in dot(*args, **kwargs)
    

    ValueError: shapes (2,3) and (1,3) not aligned: 3 (dim 1) != 1 (dim 0)



```python
a5 = np.array([[1,2], [3,4], [5,6]])
a6 = np.array([[1,2,2], [1,2,2]])
print(np.dot(a5, a6))           # matrix multiplication is defined
print(np.inner(a5, a6))         # not able to broadcast as shapes are not compatible
print(a5 * a6)                  # not able to broadcast as shapes are not compatible
```

    [[ 3  6  6]
     [ 7 14 14]
     [11 22 22]]
    


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    C:\Users\Administrator\AppData\Local\Temp\ipykernel_22816\281691594.py in <module>
          2 a6 = np.array([[1,2,2], [1,2,2]])
          3 print(np.dot(a5, a6))           # matrix multiplication is defined
    ----> 4 print(np.inner(a5, a6))         # not able to broadcast as shapes are not compatible
          5 print(a5 * a6)                  # not able to broadcast as shapes are not compatible
    

    <__array_function__ internals> in inner(*args, **kwargs)
    

    ValueError: shapes (3,2) and (3,2) not aligned: 2 (dim 1) != 3 (dim 0)


### Basic statistics
- NumPy supports useful functions to compute basic statistics
- In calculating statistics, one should carefully set ```axis``` parameter


```python
#  case of 1-D arrays
a1 = np.arange(1, 11)
print(a1)
print(a1.mean())             # average of all elements
print(a1.std())              # standard deviation of all elements
print(a1.max())              # maximum among all elements
print(a1.min())              # minimum among all elements
print(a1.argmax())           # index of max element
print(a1.argmin())           # index of min element
```

    [ 1  2  3  4  5  6  7  8  9 10]
    5.5
    2.8722813232690143
    10
    1
    9
    0
    


```python
# case of 2-D arrays
a2 = np.arange(9).reshape(3,3)
print(a2)
print(a2.mean())            # average of all elements
print(a2.mean(axis = 0))    # average of elements along axis 0 (column-wise average)
print(a2.mean(axis = 1))    # average of elements along axis 1 (row-wise average)
```

    [[0 1 2]
     [3 4 5]
     [6 7 8]]
    4.0
    [3. 4. 5.]
    [1. 4. 7.]
    


```python
# correlation coeff between two 1-D arrays (i.e., two variables)
a3 = np.array([2, 4, 5, 1, 3])
a4 = np.array([9, 8, 6, 7, 5])
print(np.corrcoef(a3, a4))
```

    [[ 1.  -0.3]
     [-0.3  1. ]]
    

$$
r =  \frac{\displaystyle\sum_{i=1}^n(x_i-\bar{x})(y_i-\bar{y})}{\sqrt{\displaystyle\sum_{i=1}^{n}(x_i-\bar{x})^2\sum_{i=1}^{n}(y_i-\bar{y})^2}}
$$


```python
# correlation coeff among rows in 2-D array
a5 = np.array([[2, 4, 5, 1, 3], [9, 8, 6, 7, 5]])
print(a5)
print(np.corrcoef(a5))
```

    [[2 4 5 1 3]
     [9 8 6 7 5]]
    [[ 1.  -0.3]
     [-0.3  1. ]]
    


```python
a6 = np.array([[2, 4, 5, 1, 3], [9, 8, 6, 7, 5]]).transpose()
print(a6)
print(np.corrcoef(a6, rowvar = False))
```

    [[2 9]
     [4 8]
     [5 6]
     [1 7]
     [3 5]]
    [[ 1.  -0.3]
     [-0.3  1. ]]
    

### Exercise 2-5.
- Create two 2-D arrays of ```shape (3,2)``` which contains integers 0 from 5 and 6 from 11, respectively
- Compute element-wise multiplication of two arrays and print out result
- Transpose second array and perform matrix multiplication. Print out result
- Print row-wise and column-wise average of elements in matrix computed


```python
## Your answer

```

### Exercise 2-6.
- There are three arrays, ```class_a_scores```, ```class_b_scores```, ```class_c_scores```, which designates scores of classmates in class A, B, and C.
<br>
```class_a_scores = array([90, 78, 54, 39, 100]), ```
```class_b_scores = array([70, 99, 80, 67, 33]), ```
```class_c_scores = array([30, 49, 98, 100, 34])```
<br>
    - Compute average of all 15 students
    - Compute maximum scores of each class
    - Compute minimum score among all 15 students


```python
## Your answer

```

### Exercise 2-7.
- Create 2-D matrix of ```shape (5,5)``` which is consisted of random integers between 0 and 10
- Normalize elements in matrix
    - Normalization scheme: ```X_normalized = (X-min(X))/(max(X)-min(X))```


```python
## Your answer

```

### Exercise 2-8.
- Create 1-D matrix ```arr = array([9, 8, 3, 5, 1, 4, 2])```
- Sort array in *ascending* order without using sort() or argsort() function
- Sort array in *descending* order without using sort() or argsort() function


```python
## Your answer

```
