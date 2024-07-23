```python
import numpy as np
```

# Chapter1

### Exercise 1-1


```python
a1 = np.random.randn(20)
print(a1); print(a1.ndim, a1.shape, a1.dtype)
a1.sort(); print(a1)
a2 = a1[::-1]; print(a2)
```

    [-0.65511341 -0.4955438   0.96528327  0.00923427  0.08076224 -0.58993969
      0.11638102  0.75574087  1.33862132  0.38703599 -0.44892892 -1.9982355
      0.23690423  0.74845293  1.15694385  0.99202339 -0.13840546 -2.95443375
      2.28964718  0.28473092]
    1 (20,) float64
    [-2.95443375 -1.9982355  -0.65511341 -0.58993969 -0.4955438  -0.44892892
     -0.13840546  0.00923427  0.08076224  0.11638102  0.23690423  0.28473092
      0.38703599  0.74845293  0.75574087  0.96528327  0.99202339  1.15694385
      1.33862132  2.28964718]
    [ 2.28964718  1.33862132  1.15694385  0.99202339  0.96528327  0.75574087
      0.74845293  0.38703599  0.28473092  0.23690423  0.11638102  0.08076224
      0.00923427 -0.13840546 -0.44892892 -0.4955438  -0.58993969 -0.65511341
     -1.9982355  -2.95443375]
    

### Exsercise 1-2


```python
a1 = np.array(range(8))
a1.shape = (2, 2, 2)
print(a1)
print(a1.ndim, a1.shape, a1.dtype)
```

    [[[0 1]
      [2 3]]
    
     [[4 5]
      [6 7]]]
    3 (2, 2, 2) int32
    

### Quiz 1


```python
a1 = np.array(range(27)).reshape(3, 3, 3)
print(a1)
print("rank:", a1.ndim, "\nshape:", a1.shape, "\ndtype:", a1.dtype)
```

    [[[ 0  1  2]
      [ 3  4  5]
      [ 6  7  8]]
    
     [[ 9 10 11]
      [12 13 14]
      [15 16 17]]
    
     [[18 19 20]
      [21 22 23]
      [24 25 26]]]
    rank: 3 
    shape: (3, 3, 3) 
    dtype: int32
    

# Chapter 2

### Exercise 2-1


```python
a1 = np.array(range(100))
print(a1[95])
print(a1[:30])
```

    95
    [ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23
     24 25 26 27 28 29]
    

### Exercise 2-2


```python
a1 = np.array(range(9)).reshape(3, 3); print(a1)
print("a[1][1] =", a1[1][1])
print(a1[:, 1:2])
```

    [[0 1 2]
     [3 4 5]
     [6 7 8]]
    a[1][1] = 4
    [[1]
     [4]
     [7]]
    

### Exercise 2-3


```python
a1 = np.array(range(6)).reshape(3, 2) + 1
print(a1)

a1[:, 1:2] = a1[:, 1:2] * 2
print(a1)
a1[0:1, :] = a1[0:1, :] - 1
print(a1)
```

    [[1 2]
     [3 4]
     [5 6]]
    [[ 1  4]
     [ 3  8]
     [ 5 12]]
    [[ 0  3]
     [ 3  8]
     [ 5 12]]
    

###  Exercise 2-4


```python
# Skip this question
```

### Exercise 2-5


```python
a1 = np.arange(6).reshape(3, 2)
a2 = np.arange(start = 6, stop = 12).reshape(3, 2)

print(a1); print(a2)

print(a1 * a2)

a3 = np.dot(a1, a2.transpose())
print(a3)

print(a3.mean(axis = 1))
print(a3.mean(axis = 0))
```

    [[0 1]
     [2 3]
     [4 5]]
    [[ 6  7]
     [ 8  9]
     [10 11]]
    [[ 0  7]
     [16 27]
     [40 55]]
    [[ 7  9 11]
     [33 43 53]
     [59 77 95]]
    [ 9. 43. 77.]
    [33. 43. 53.]
    

### Exercise 2-7


```python
a1 = np.random.randint(0, 11, size = 25).reshape(5, 5)
print(a1)

a1_normalized = (a1 - a1.min()) / (a1.max() - a1.min())
print(a1_normalized)
```

    [[ 4  7  3  3  6]
     [ 5  2  7  6 10]
     [ 1  2  4  3  8]
     [ 0  1  9  1  3]
     [ 3  9  2  7  2]]
    [[0.4 0.7 0.3 0.3 0.6]
     [0.5 0.2 0.7 0.6 1. ]
     [0.1 0.2 0.4 0.3 0.8]
     [0.  0.1 0.9 0.1 0.3]
     [0.3 0.9 0.2 0.7 0.2]]
    

### Exercise 2-8 


```python
arr = np.array([9, 8, 3, 5, 1, 4, 2])

swap = lambda arr, i, j: (
    arr.__setitem__(i, arr[i] ^ arr[j]),
    arr.__setitem__(j, arr[i] ^ arr[j]),
    arr.__setitem__(i, arr[i] ^ arr[j])
)

def bubble_sort_ascending(arr: np.array) -> np.array:
    for i in range(len(arr)):
        for j in range(len(arr) - i -1):
            if arr[j] > arr[j + 1]:
                swap(arr, j, j + 1)
    return arr

def bubble_sort_descending(arr: np.array) -> np.array:
    for i in range(len(arr)):
        for j in range(len(arr) - i -1):
            if arr[j] < arr[j + 1]:
                swap(arr, j, j + 1)
    return arr

print(bubble_sort_ascending(arr.copy()))
print(bubble_sort_descending(arr.copy()))
```

    [1 2 3 4 5 8 9]
    [9 8 5 4 3 2 1]
    

### Exerwcise 3-1


```python
data = np.genfromtxt('highway.csv', delimiter = ',' ,dtype = np.str_, missing_values = '?', filling_values = 'Unknown')

print(data[0:3], '\n')  # The arg 'missing_values' seems to be ineffective, manual replacement is performed as below

data[data == '?'] = 'Unknown'
print(data[0:3])
```

    [['E1' 'M' '3' '1818' 'HIGHWAY' '' '2' 'N' 'THROUGH' 'WOOD' 'SHORT' 'S'
      'WOOD']
     ['E2' 'A' '25' '1819' 'HIGHWAY' '1037' '2' 'N' 'THROUGH' 'WOOD' 'SHORT'
      'S' 'WOOD']
     ['E3' 'A' '39' '1829' 'AQUEDUCT' '?' '1' 'N' 'THROUGH' 'WOOD' '?' 'S'
      'WOOD']] 
    
    [['E1' 'M' '3' '1818' 'HIGHWAY' '' '2' 'N' 'THROUGH' 'WOOD' 'SHORT' 'S'
      'WOOD']
     ['E2' 'A' '25' '1819' 'HIGHWAY' '1037' '2' 'N' 'THROUGH' 'WOOD' 'SHORT'
      'S' 'WOOD']
     ['E3' 'A' '39' '1829' 'AQUEDUCT' 'Unknown' '1' 'N' 'THROUGH' 'WOOD'
      'Unknown' 'S' 'WOOD']]
    

### Exercise 3-2


```python
data = np.genfromtxt('dermatology.csv', delimiter = ',', missing_values = '?', filling_values = 0)
data[data == '?'] = 0

print(data.shape); print(data)

np.random.shuffle(data)

X_data = data[:, 0:34]
Y_data = data[:, -1]

half_len = len(data) // 2

X_train = X_data[:half_len]
X_text = X_data[half_len:]
Y_train = Y_data[:half_len]
Y_text = Y_data[half_len:]

print(X_train.shape, X_text.shape, Y_train.shape, Y_text.shape)
```

    (366, 35)
    [[ 2.  2.  0. ...  0. 55.  2.]
     [ 3.  3.  3. ...  0.  8.  1.]
     [ 2.  1.  2. ...  3. 26.  3.]
     ...
     [ 3.  2.  2. ...  3. 28.  3.]
     [ 2.  1.  3. ...  3. 50.  3.]
     [ 3.  2.  2. ...  0. 35.  1.]]
    (183, 34) (183, 34) (183,) (183,)
    

    c:\ProgramData\anaconda3\envs\jupyter-notebook\lib\site-packages\ipykernel_launcher.py:2: FutureWarning: elementwise comparison failed; returning scalar instead, but in the future will perform elementwise comparison
      
    

### Quiz 3


```python
data = np.genfromtxt('dermatology.csv', delimiter = ',', missing_values = '?', filling_values = -1)
data[data == '?'] = -1

np.random.shuffle(data)

X_data = data[:, :34] + 1
normalize = lambda arr: (arr - arr.min()) / (arr.max() - arr.min())
X_data = normalize(X_data)

Y_data = data[:, -1]

eighty_percentage = int(0.8 * len(data))

X_train = X_data[:eighty_percentage]
X_text = X_data[eighty_percentage:]
Y_train = Y_data[:eighty_percentage]
Y_text = Y_data[eighty_percentage:]
```

    c:\ProgramData\anaconda3\envs\jupyter-notebook\lib\site-packages\ipykernel_launcher.py:2: FutureWarning: elementwise comparison failed; returning scalar instead, but in the future will perform elementwise comparison
      
    

### Quiz 4


```python
arr1, arr2 = np.split(np.random.randint(0, 20, size = 40).reshape(4, 10), indices_or_sections = 2, axis = 0)

print(arr1); print(); print(arr2); print()

arr_vstack = np.vstack((arr1, arr2))
print(arr_vstack); print()

arr_hstack = np.hstack((arr1, arr2))
print(arr_hstack); print()


# np.concatenate() is an option
arr_vstack_concatenate = np.concatenate((arr1, arr2), axis = 0)
print(arr_vstack_concatenate); print()

arr_hstack_concatenate = np.concatenate((arr1, arr2), axis = 1)
print(arr_hstack_concatenate); print()
```

    [[ 5  5 13  4 12 11 14 11  0  0]
     [11  4  4 15 10 17 11  1 12 18]]
    
    [[ 9 17  1  8  4 19 18 13  7 11]
     [19  9  6 16 12  4 16  9  7 14]]
    
    [[ 5  5 13  4 12 11 14 11  0  0]
     [11  4  4 15 10 17 11  1 12 18]
     [ 9 17  1  8  4 19 18 13  7 11]
     [19  9  6 16 12  4 16  9  7 14]]
    
    [[ 5  5 13  4 12 11 14 11  0  0  9 17  1  8  4 19 18 13  7 11]
     [11  4  4 15 10 17 11  1 12 18 19  9  6 16 12  4 16  9  7 14]]
    
    [[ 5  5 13  4 12 11 14 11  0  0]
     [11  4  4 15 10 17 11  1 12 18]
     [ 9 17  1  8  4 19 18 13  7 11]
     [19  9  6 16 12  4 16  9  7 14]]
    
    [[ 5  5 13  4 12 11 14 11  0  0  9 17  1  8  4 19 18 13  7 11]
     [11  4  4 15 10 17 11  1 12 18 19  9  6 16 12  4 16  9  7 14]]
    
    
