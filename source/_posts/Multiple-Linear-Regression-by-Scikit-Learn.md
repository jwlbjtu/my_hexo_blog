---
title: Multiple Linear Regression by Scikit-Learn
date: 2018-03-15 23:22:31
categories:
- [Machine Learning, Regression]
tags:
- Machine Learning
- Python
- Scikit-Learn
---


### Multiple Linear Regression Intuition

**Multiple Linear Regression** presents linear relationship between mutiple independent variables and dependent variable. 

**Formula**: $$y = b_0 + b_1 \* X_1 + ... + b_n \* X_n$$
<!-- more -->
### Multiple Linear Regression Implementaion


```python
# Importing the libaraies
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd

# Importing the dataset
dataset = pd.read_csv('50_Startups.csv')

# show dataset
dataset
```
|  | R&amp;D Spend | Administration | Marketing Spend |   State    |   Profit  |
|--|:-------------:|:--------------:|:---------------:| ----------:| ---------:|
|0 | 165349.20     | 136897.80      | 471784.10       | New York   | 192261.83 |
|1 | 162597.70     | 151377.59      | 443898.53       | California | 191792.06 |
|2 | 153441.51     | 101145.55      | 407934.54       | Florida    | 191050.39 |
|3 | 144372.41     | 118671.85      | 383199.62       | New York   | 182901.99 |
|4 | 142107.34     | 91391.77       | 366168.42       | Florida    | 166187.94 |
|5 | 131876.90     | 99814.71       | 362861.36       | New York   | 156991.12 |
|6 | 134615.46     | 147198.87      | 127716.82       | California | 156122.51 |
|7 | 130298.13     | 145530.06      | 323876.68       | Florida    | 155752.60 |
|8 | 120542.52     | 148718.95      | 311613.29       | New York   | 152211.77 |
|9 | 123334.88     | 108679.17      | 304981.62       | California | 149759.96 |
...

```python
X = dataset.iloc[:, :-1].values
y = dataset.iloc[:, 4].values
```


```python
# Show X
X
```




    array([[165349.2, 136897.8, 471784.1, 'New York'],
           [162597.7, 151377.59, 443898.53, 'California'],
           [153441.51, 101145.55, 407934.54, 'Florida'],
           [144372.41, 118671.85, 383199.62, 'New York'],
           [142107.34, 91391.77, 366168.42, 'Florida'],
           [131876.9, 99814.71, 362861.36, 'New York'],
           [134615.46, 147198.87, 127716.82, 'California'],
           [130298.13, 145530.06, 323876.68, 'Florida'],
           [120542.52, 148718.95, 311613.29, 'New York'],
           [123334.88, 108679.17, 304981.62, 'California'],
           ...], dtype=object)




```python
# Show y
y
```




    array([ 192261.83,  191792.06,  191050.39,  182901.99,  166187.94,
            156991.12,  156122.51,  155752.6 ,  152211.77,  149759.96,
            ... ])




```python
# Caegorical data encoding
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelEncoder_X = LabelEncoder()
X[:, 3]= labelEncoder_X.fit_transform(X[:, 3])
oneHotEncoder = OneHotEncoder(categorical_features = [3])
X = oneHotEncoder.fit_transform(X).toarray()

# Show X
X
```




    array([[  0.00000000e+00,   0.00000000e+00,   1.00000000e+00,
              1.65349200e+05,   1.36897800e+05,   4.71784100e+05],
           [  1.00000000e+00,   0.00000000e+00,   0.00000000e+00,
              1.62597700e+05,   1.51377590e+05,   4.43898530e+05],
           [  0.00000000e+00,   1.00000000e+00,   0.00000000e+00,
              1.53441510e+05,   1.01145550e+05,   4.07934540e+05],
           [  0.00000000e+00,   0.00000000e+00,   1.00000000e+00,
              1.44372410e+05,   1.18671850e+05,   3.83199620e+05],
           [  0.00000000e+00,   1.00000000e+00,   0.00000000e+00,
              1.42107340e+05,   9.13917700e+04,   3.66168420e+05],
           [  0.00000000e+00,   0.00000000e+00,   1.00000000e+00,
              1.31876900e+05,   9.98147100e+04,   3.62861360e+05],
           [  1.00000000e+00,   0.00000000e+00,   0.00000000e+00,
              1.34615460e+05,   1.47198870e+05,   1.27716820e+05],
           [  0.00000000e+00,   1.00000000e+00,   0.00000000e+00,
              1.30298130e+05,   1.45530060e+05,   3.23876680e+05],
           [  0.00000000e+00,   0.00000000e+00,   1.00000000e+00,
              1.20542520e+05,   1.48718950e+05,   3.11613290e+05],
           [  1.00000000e+00,   0.00000000e+00,   0.00000000e+00,
              1.23334880e+05,   1.08679170e+05,   3.04981620e+05],
           ...])



During the categorical data encoding, we created three dummy variables to present 'New York', 'California' and 'Florida'. Because they have strong co-relationship between each other, to avoid dummy variable trap we need to remove one dummy variable.


```python
# Avoiding the Dummy Variable Trap
X = X[:, 1:]

# Show X
X
```




    array([[  0.00000000e+00,   1.00000000e+00,   1.65349200e+05,
              1.36897800e+05,   4.71784100e+05],
           [  0.00000000e+00,   0.00000000e+00,   1.62597700e+05,
              1.51377590e+05,   4.43898530e+05],
           [  1.00000000e+00,   0.00000000e+00,   1.53441510e+05,
              1.01145550e+05,   4.07934540e+05],
           [  0.00000000e+00,   1.00000000e+00,   1.44372410e+05,
              1.18671850e+05,   3.83199620e+05],
           [  1.00000000e+00,   0.00000000e+00,   1.42107340e+05,
              9.13917700e+04,   3.66168420e+05],
           [  0.00000000e+00,   1.00000000e+00,   1.31876900e+05,
              9.98147100e+04,   3.62861360e+05],
           [  0.00000000e+00,   0.00000000e+00,   1.34615460e+05,
              1.47198870e+05,   1.27716820e+05],
           [  1.00000000e+00,   0.00000000e+00,   1.30298130e+05,
              1.45530060e+05,   3.23876680e+05],
           [  0.00000000e+00,   1.00000000e+00,   1.20542520e+05,
              1.48718950e+05,   3.11613290e+05],
           [  0.00000000e+00,   0.00000000e+00,   1.23334880e+05,
              1.08679170e+05,   3.04981620e+05],
           ...])




```python
# Split the dataset into Training set and Test set
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 0)

# Fitting Multiple Linear Regression to the Training set
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(X_train, y_train)

# Predicting the Test set
y_pred = regressor.predict(X_test)

# Show predict result
y_pred
```




    array([ 103015.20159795,  132582.27760817,  132447.73845176,
             71976.09851257,  178537.48221058,  116161.24230165,
             67851.69209675,   98791.73374686,  113969.43533013,
            167921.06569553])




```python
# Show Test set result
y_test
```




    array([ 103282.38,  144259.4 ,  146121.95,   77798.83,  191050.39,
            105008.31,   81229.06,   97483.56,  110352.25,  166187.94])


