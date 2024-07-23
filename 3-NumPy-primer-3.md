# NumPy Primer - 3
- Importing datasets
    - loadtxt
    - genfromtxt
- Processing data
    - Splitting data
- Summarizing data


```python
import numpy as np
```

## 1. Importing Datasets
- Datasets in text files (```.txt, .csv```, etc.) can be imported using ```loadtxt()``` for ```genfromtxt()```

### loadtxt()
- ```loadtxt()``` is used when there do not exist missing values
- Hence, number of values in each row should be equal
- Key parameters
    - ```fname```: designates name of text file to be imported
    - ```dtype```: data type of array to be created as result (default: ```float```)
    - ```delimiter```: string used to separate values (default: whitespace)
    - ```skiprows```: skip first *n* rows (default: 0)
    - ```usecols```: column indices to be read (default: ```None``` => all cols are used)


```python
# importing dataset with default settings
data = np.loadtxt('even_numbers.txt')
print(data)
print(type(data))
```

    [[ 2.  4.  6.  8. 10.]
     [12. 14. 16. 18. 20.]
     [22. 24. 26. 28. 30.]
     [32. 34. 36. 38. 40.]
     [42. 44. 46. 48. 50.]]
    <class 'numpy.ndarray'>
    


```python
# importing dataset with parameter settings
# skiprows is especially useful when you want to get rid of "header" of dataset 
data = np.loadtxt('even_numbers.txt', dtype = int, skiprows = 1, usecols = (1,3))
print(data)
```

    [[14 18]
     [24 28]
     [34 38]
     [44 48]]
    


```python
# importing dataset with parameter settings
data = np.loadtxt('even_numbers.txt', dtype = np.str_, usecols = 0)
print(data)        # note that resulting array is 1-D
```

    ['2' '12' '22' '32' '42']
    


```python
# .csv files could be imported as well
# in this case, delimiter should be set to ','
data = np.loadtxt('glass.csv', delimiter = ',')
print(data.shape)        # dataset with 214 rows & 11 columns
print(data.dtype)        # dtype is float64 as default
data = data[:, 1:]
print(data)
```

    (214, 11)
    float64
    [[ 1.52101 13.64     4.49    ...  0.       0.       1.     ]
     [ 1.51761 13.89     3.6     ...  0.       0.       1.     ]
     [ 1.51618 13.53     3.55    ...  0.       0.       1.     ]
     ...
     [ 1.52065 14.36     0.      ...  1.64     0.       7.     ]
     [ 1.51651 14.38     0.      ...  1.57     0.       7.     ]
     [ 1.51711 14.23     0.      ...  1.67     0.       7.     ]]
    

### genfromtxt()
- ```genfromtxt()``` is used when dataset has some missing values
- Otherwise, it is largely identical to ```loadtxt()```


```python
# when ' '(whitespace) is used as delimiter
data = np.genfromtxt('odd_numbers.txt', invalid_raise = False)
print(data)      # you can see that last row is removed
```

    [[ 1.  3.  5.  7.  9.]
     [11. 13. 15. 17. 19.]
     [21. 23. 25. 27. 29.]
     [31. 33. 35. 37. 39.]]
    

    <ipython-input-7-4eff7b6b822f>:2: ConversionWarning: Some errors were detected !
        Line #5 (got 4 columns instead of 5)
      data = np.genfromtxt('odd_numbers.txt', invalid_raise = False)
    


```python
# when ',' is used as delimiter
data = np.genfromtxt('odd_numbers.csv', delimiter = ',')
print(data)      # you could see that last element is set to nan
```

    [[ 1.  3.  5.  7.  9.]
     [11. 13. 15. 17. 19.]
     [21. 23. 25. 27. 29.]
     [31. 33. 35. 37. 39.]
     [43. 45. 47. 49. nan]]
    


```python
# value to fill missing element can be deisgnated
data = np.genfromtxt('odd_numbers.csv', delimiter = ',', filling_values = 0)
print(data)       # fill missing value with 100.
```

    [[ 1.  3.  5.  7.  9.]
     [11. 13. 15. 17. 19.]
     [21. 23. 25. 27. 29.]
     [31. 33. 35. 37. 39.]
     [43. 45. 47. 49.  0.]]
    


```python
# if there is certain string to designate missing value ('?' here)
data = np.genfromtxt('odd_numbers_2.csv', delimiter = ',', missing_values = '?', \
                     filling_values = 99)
print(data)       # fill missing value with 99.
```

    [[ 1.  3.  5.  7.  9.]
     [11. 13. 15. 17. 19.]
     [21. 23. 25. 27. 29.]
     [31. 33. 35. 37. 39.]
     [43. 45. 47. 49. 99.]]
    

### Exercise 3-1.
- Import ```highway.csv``` using genfromtxt()
    - Set ```dtype``` as string
    - Replace missing values (```'?'```) with ```'Unknown'```
    - Print first three rows of resulting array


```python
## Your answer

```

## 2. Processing data
- Processing imported dataset is essential task in data mining
- Many techniques we have learnt so far are used

### Splitting data
- In most cases, dataset is splitted into ```X data``` (input variables) and ```Y data``` (output variables), or other variable splits
    - Then, dataset is splitted *column-wise*
- Then, dataset is splitted into ```training data``` and ```validation/test data```, or cross-validated
    - Then, dataset is splitted *row-wise*
- In either case, array indexing & slicing are utilized

**glass dataset**
- source: https://archive.ics.uci.edu/ml/machine-learning-databases/glass/glass.names
- Number of instances (# rows): 214
- Number of attributes (# columns): 10
    - ID number: 1 to 214
    - RI: refractive index
    - Na: Sodium (unit measurement: weight percent in corresponding oxide, as are attributes 4-10)
    - Mg: Magnesium
    - Al: Aluminum
    - Si: Silicon
    - K: Potassium
    - Ca: Calcium
    - Ba: Barium
    - Fe: Iron
    - Type of glass: (class attribute)
        - 1: building_windows_float_processed
        - 2: building_windows_non_float_processed
        - 3: vehicle_windows_float_processed
        - 4: vehicle_windows_non_float_processed (none in this database)
        - 5: containers
        - 6: tableware
        - 7: headlamps


```python
# import dataset
data = np.loadtxt('glass.csv', delimiter = ',')
print(data.shape)
print(data[0])
```

    (214, 11)
    [  1.00000000e+00   1.52101000e+00   1.36400000e+01   4.49000000e+00
       1.10000000e+00   7.17800000e+01   6.00000000e-02   8.75000000e+00
       0.00000000e+00   0.00000000e+00   1.00000000e+00]
    


```python
# excluding ID number variable
data_1 = data[:, 1:]
print(data_1.shape)        # 10 columns now
```

    (214, 10)
    


```python
# selecting only X data (excluding ID number & Type of glass variables)
X_data = data[:, 1:-1]
print(X_data.shape)        # 9 columns now
```

    (214, 9)
    


```python
# selecting only RI, Na, Mg variables
X_partial = data[:, 1:4]
print(X_partial.shape)
```

    (214, 3)
    


```python
# selecting only Y data
Y_data = data[:, -1]
print(Y_data.shape)
```

    (214,)
    


```python
# splitting data into train-test set
# first 150 data instances into train set, others into test set
X_train = X_data[:150,:]
X_test = X_data[150:, :]
Y_train = Y_data[:150]
Y_test = Y_data[150:]

print(X_train.shape)
print(X_test.shape)
print(Y_train.shape)
print(Y_test.shape)
```

    (150, 9)
    (64, 9)
    (150,)
    (64,)
    


```python
# randomly performing train-test split
data_shulffled = data               # copy data
np.random.shuffle(data_shulffled)   # shulffle dataset randomly

X_data = data_shulffled[:, 1:-1]
Y_data = data_shulffled[:, -1]

X_train = X_data[:150,:]
X_test = X_data[150:, :]
Y_train = Y_data[:150]
Y_test = Y_data[150:]

print(X_train.shape)
print(X_test.shape)
print(Y_train.shape)
print(Y_test.shape)
```

    (150, 9)
    (64, 9)
    (150,)
    (64,)
    

### Exercise 3-2.
- Import ```dermatology.csv``` using ```genfromtxt()``` function
    - Replace missing values ('?') with 0
- Assign data in first 34 columns into X_data
- Assign data in last column into Y_data
- Perform train-test split
    - Randomly assign half into train set, another half into test set


```python
## Your answer

```

## Quiz 3.
- Import data from `dermatology.csv`, replacing unknown values denoted by '?' with -1.
- Increment each number in the first 34 columns by 1 and assign to `X_data`.
- Normalize `X_data` for each column (normalize to follow a normal distribution).
- Assign the last column to `Y_data`.
- Perform train-test split:
   - Randomly select 80% of the data for the train set, and the remaining for the test set.


```python
## Your answer

```
