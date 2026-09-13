# Week 09 - NumPy 배열 연산 실습

이번 주차에서는 Python의 NumPy를 이용하여 배열을 생성하고,
다차원 배열의 구조와 기본적인 배열 연산을 실습했다.

## 1. NumPy 환경 구성

NumPy, Pandas, Matplotlib을 설치하고 불러오는 방법을 실습했다.

```python
!pip install numpy pandas matplotlib
```

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as pit
```

NumPy 배열의 기본 자료형이 `numpy.ndarray`임을 확인했다.

## 2. NumPy 배열 생성

다양한 방법으로 NumPy 배열을 생성했다.

### 직접 배열 생성

```python
arr = np.array([1, 2, 3])
```

### 0으로 채운 배열

```python
zero_arr = np.zeros((2, 3))
```

### 1로 채운 배열

```python
one_arr = np.ones((2, 3))
```

### 연속된 숫자로 배열 생성

```python
np.arange(3)
np.arange(start=1, stop=4)
```

## 3. ndim과 shape

NumPy 배열의 차원과 형태를 확인했다.

- `ndim` : 배열의 차원 수
- `shape` : 각 차원의 크기

```python
array2 = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(array2.ndim)
print(array2.shape)
```

2차원뿐만 아니라 3차원 배열도 직접 생성하여
차원과 배열의 구조를 확인했다.

## 4. Array Indexing

배열의 Index를 이용하여 원하는 원소에 접근했다.

### 1차원 배열

```python
array1 = np.array([1, 2, 3])
array1[2]
```

### 2차원 배열

```python
array2 = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

array2[1, 2]
```

### 3차원 배열

```python
array3 = np.array([
    [[1, 2, 3], [4, 5, 6]],
    [[7, 8, 9], [10, 11, 12]],
    [[13, 14, 15], [16, 17, 18]]
])

array3[1, 1, 2]
```

다차원 배열에서는 각 차원의 위치를 순서대로 지정하여
특정 원소에 접근할 수 있다.

## 5. Axis와 배열 정렬

`np.sort()`를 이용하여 배열을 정렬하고,
`axis` 값에 따라 정렬 방향이 어떻게 달라지는지 확인했다.

```python
arr1 = np.array([
    [5, 2, 7],
    [4, 3, 6]
])
```

### axis=0

```python
np.sort(arr1, axis=0)
```

### axis=1

```python
np.sort(arr1, axis=1)
```

3차원 배열에서도 `axis=0`을 기준으로 정렬하여
다차원 배열에서 Axis가 어떻게 적용되는지 실습했다.

## 6. 배열의 사칙연산

두 NumPy 배열을 이용하여 덧셈과 뺄셈을 수행했다.

```python
arr1 = np.array([
    [5, 2, 7],
    [4, 3, 6]
])

arr2 = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
```

### Addition

```python
np.add(arr1, arr2)
arr1 + arr2
```

### Subtraction

```python
np.subtract(arr1, arr2)
arr1 - arr2
```

NumPy 함수를 사용하는 방법과 연산자를 직접 사용하는 방법을 모두 실습했다.

## 7. Dot Product

`np.dot()`을 이용하여 벡터와 행렬의 내적을 계산했다.

### Vector

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

np.dot(a, b)
```

### Matrix

```python
A = np.array([
    [1, 2],
    [3, 4]
])

B = np.array([
    [5, 6],
    [7, 8]
])

np.dot(A, B)
```

## 8. Reshape

`reshape()`를 이용하여 배열의 원소 수는 유지하면서
배열의 형태를 변경했다.

```python
array_default1 = np.arange(6)
array_default1.reshape(3, 2)
```

또한 `-1`을 사용하여 나머지 차원의 크기를
자동으로 계산하도록 하는 방법도 실습했다.

```python
array3 = array1.reshape(-1, 3)
```

## 9. Mean

`np.mean()`을 이용하여 배열 전체와
각 Axis를 기준으로 평균을 계산했다.

```python
arr = np.array([
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
])
```

### 전체 평균

```python
np.mean(arr)
```

### 행 기준 평균

```python
np.mean(arr, axis=1)
```

### 열 기준 평균

```python
np.mean(arr, axis=0)
```

## 10. Sum

`sum()`을 이용하여 Axis에 따른 합을 계산했다.

```python
arr = np.array([
    [5, 2, 7],
    [4, 3, 6]
])
```

### axis=0

```python
arr.sum(axis=0)
```

### axis=1

```python
arr.sum(axis=1)
```

## 11. 종합 실습

다음 배열을 이용하여 이번 주차에서 배운 내용을 종합적으로 실습했다.

```python
array4 = np.array([
    [11, 10, 3, 4],
    [7, 1, 2, 9],
    [6, 8, 5, 12]
])
```

### 각 행의 합

```python
array4.sum(axis=1)
```

### 각 열의 평균

```python
array4.mean(axis=0)
```

### 전체 데이터를 정렬한 뒤 다시 3 × 4 배열로 변환

```python
result = np.sort(array4.reshape(-1)).reshape(3, 4)
result
```

결과:

```text
[[ 1,  2,  3,  4],
 [ 5,  6,  7,  8],
 [ 9, 10, 11, 12]]
```

## Practice Files

- [NumPy Practice Notebook](./practice/numpy_practice.ipynb)
- [Practice Submission](./practice/practice_submission.docx)