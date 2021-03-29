---
title: "[부스트캠프 AI Tech / Day6] 파이썬 Numpy"
data: 2021-01-25 20:30:00 +0800
categories: [네이버 부스트캠프 AI Tech, Python]
tags: [Python]
use_math: True
---


## **[DAY 6] Numpy**

---

### **Numpy**

- Numerical Python
- 파이썬의 고성능 과학 계산용 패키지
- matrix, vector와 같은 array 연산의 사실상 표준
- 특징
  - 일반 list에 비해 빠르고, 메모리 효율적
  - 반복문 없이 데이터 배열에 대한 처리를 지원함
  - 선형대수와 관련된 다양한 기능을 제공함
  - C, C++, 포트란 등의 언어와 통합 가능
- 어떻게 행렬과 매트릭스를 코드로 표현할 것인가 ➡ 리스트 형태
- 코드로 방정식 표현하기 ➡ 파이썬의 라이브러리 활용
  - 다양한 matrix 계산하기
  - 큰 matrix에 대한 표현
  - 처리속도문제 - python은 interpreter 언어
- **`import numpy as np`**
  - numpy의 호출방법
  - 일반적으로 numpy는 np라는 alias(별칭) 이용하여 호출

> $2𝑥_1 + 2𝑥_2 + 𝑥_3 = 9$  
> $2𝑥_1 − 𝑥_2 + 2𝑥_3 = 6$  
> $𝑥_1 − 𝑥_2 + 2𝑥_3 = 5$  
> 
> [2,  2, 1, 9]  
> [2, -1, 2, 6]  
> [1, -1, 2, 5]  
> 
> coefficient_matrix = [ [2, 2, 1], [2, -1, 2], [1, -1, 2] ]  
> constant_vector = [9, 6, 5]

<br/>

---

### **ndarray**

#### **ndarray 생성**

- numpy는 **np.array 함수를 활용하여 배열을 생성**함 ➡ **ndarray 객체**
- numpy는 **하나의 데이터 type만 배열에 넣을 수 있음**
  - 다른 데이터 형식이 들어와도 형변환해서 들어가게 됨
- list와 가장 큰 차이점 ➡ dynamic typing not supported
- C의 array를 사용하여 배열을 생성함
  - **`np.array([리스트], dtype)`**

    ```python
    test_array = np.array([1, 4, 5, 8], float)
    print(test_array)

    type(test_array)
    #numpy.ndarray

    type(test_array[3])
    # numpy.float
    ```

#### **python `array` vs `numpy`**

- **python array**
  - python은 -5~256의 값
  - 계속 가리키게됨
  - 리스트의 변형이 굉장히 쉬움

    ```python
    a = [1, 2, 3, 4, 5]
    b = [2, 3, 4, 5, 1]

    >>> a[0] is b[-1]
    # True - 서로 같은 메모리 주소를 가리키기 때문임
    ```

- **numpy ndarray**
  - numpy는 그냥 옆에 담음
  - 메모리의 위치를 고려하여 더할 수 있으므로 메모리 접근성 좋음

    ```python
    a = np.array(a)
    a = np.array(b)
    
    >>> a[0] is b[-1]
    # False - 서로 다른 메모리 주소를 가리키기 때문임
    ```

<br/>

---

### **shape**

- shape: numpy array의 dimension 구성을 반환함
- dtype: numpy array의 데이터 type을 반환함

  ```python
  test_array = np.array([1, 4, 5, "8"], float) # string type의 데이터를 입력해도 
  test_array
  # array([1., 4., 5., 8.])

  type(test_array[3]) # float type으로 자동 형변환을 실시
  # numpy.float64

  test_array.dtype # array(배열) 전체의 데이터 type을 반환함
  # dtype('float64')

  test_array.shape # array(배열)의 shape을 tuple 타입으로 반환함
  # (4,)

  a = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
  np.array(a).shape
  # (3, 3) 3 by 3 matrix 임을 tuple형태로 알려줌
  ```

#### **rank**

- rank name: array의 rank에 따라 불리는 이름이 있음
  - 0: scalar (dimension이 없음)
  - 1: vector
  - 2: matrix
  - 3: 3-tensor
  - n: n-tensor(n order tensor)
    - 선형대수에서 값을 표현하는 방법

#### **array shape**

- matrix
  - `a = [ , , , ]`
    - `(4,)`
  - `b = [[ , , ], [ , , ], [ , , ]]`
    - `(3, 4)`
- ndim (=rank, number of dimensions)
- size (=data, element)의 개수

#### **array dtype**

- **dtype: ndarray의 single element가 가지는 data type**
- numpy는 한가지 타입만 저장할 수 있음
- 각 element가 차지하는 memory의 크기가 결정됨
- ex
  - dtype=int
  - dtype=np.float32

> int64: 2^63(패리티 비트 빠짐) 표현가능

#### **array nbytes**

- nbyte (=ndarray object)의 메모리 크기를 반환함

    ```python
    np.array([1, 2, 3], [4.5, 5, 6], dtype=np.float32).nbyte
    # 32bits = 4bytes # 6*4 bytes

    np.array([1, 2, 3], [4.5, 5, 6], dtype=np.int8).nbyte
    # 8bits = 1bytes # 6*1 bytes

    np.array([1, 2, 3], [4.5, 5, 6], dtype=np.float64).nbyte
    # 64bits = 8bytes # 8*4 bytes
    ```

<br/>

---

### **shape handling**

#### **reshape**

- array의 **shape의 크기를 변경**함, **element의 갯수는 동일**
- **동일한 사이즈가 나오게 하도록 shape을 변경**함

  ```python
  np.array(test_matrix).reshape(2,4).shape
  # (2, 4) ➡ (8,)
  # [[ , , , ][ , , , ]] ➡ [ , , , , , , , ]

  np.array(test_matrix).reshape(-1,2).shape
  # -1 : size를 기반으로 row 개수를 선정

  np.array(test_matrix).reshape(1,-1,2).shape
  # (1, 4, 2)
  ```

#### **flatten**

- 다차원 array를 1차원 array로 변환(한줄로 펴줌)
- (2, 2, 4) ➡ (16,)

#### **indexing & slicing**

- **indexing**
  - list와 달리(`[0][0]`) 이차원 배열에서 `[0,0]` 표기법을 제공함
  - matrix 일 경우, 앞은 row, 뒤는 column을 의미함
  - start:end:step
  - `arr[:, ::2]` # 짝수열만 가져옴
- **slicing**
  - list와 달리 행과 열 부분을 나눠서 slicng이 가능함
  - matrix의 부분집합을 추출할 때 유용함

    ```python
    a = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]], int)
    a[:,2:] # 전체 Row의 2열 이상
    a[1]    # array([6, 7, 8, 9, 10])
    a[1,1:3] # 1 Row의 1열 ~ 2열 # array([[6, 7, 8, 9, 10]])
    a[1:3] # 1 Row ~ 2Row의 전체
    # [행, 열]
    ```

    ```python
    a = np.arange(100).reshape(10, 10)
    a
    # array ([[0, 1, ... , 9],
    #
    #
    #        [90, 91, ... , 99]])

    a[:, -1]
    # array([9, 19, 29, ..., 99])
    ```

---

### **creation function**

#### **arange**

- **array의 범위를 지정하여, 값의 list를 생성**하는 명령어

  ```python
  np.arange(30)         # 0~29까지의 배열 추출 int

  np.arange(0, 10, 0.5) # floating point도 표시 가능
  #(start, end, step)

  np.arange(30).reshape(5, 6)
  ```

#### **ones, zeros, empty**

- **zeros: 0으로 가득찬 ndarray 생성**
- **ones: 1으로 가득찬 ndarray 생성**
- **empty: shape만 주어지고 비어있는 ndarray 생성**
  - memory initialization이 되지 않음
  - 이전에 그 자리에 쓰인 값이 있었다면, 그 값을 동일하게 가져옴
  - Garbage Collection이 실행되면 메모리가 풀리는데, 그 메모리는 초기화되지 않은 채로 풀리게 되므로, 쓰레기 값이 들어가있을 수 있음
- 셋은 동일하게 사용
  - (shape, dtype, order)
- `np.zeros(shape=(10,), dtype=np.int8)`
  - (10,)의 zero vector 생성
- shape은 항상 tuple값으로 들어감
- `np.zeros((2, 5))`
  - (2, 5)의 zero matrix 생성

#### **somthing_like**

- 기존 ndarray의 shape 크기만큼 1, 0 또는 empty array를 반환
  - `np.ones_like()`
  - `np.zeros_like()`
  - `np.empty_like()`

  ```python
  test_matrix = np.sarange(30).reshape(5, 6)
  np.ones_like(test_matrix)
  ```

#### **identity**

- 단위행렬(I 행렬)을 생성함
- **단위행렬: 대각행렬이 1인 행렬**
- `np.identity(n=3, dtype=np.int8)` (n: number of rows)
- `np.identity(5)`

#### **eye**

- 대각선이 1인 행렬, k값을 설정하여, 어디서부터 1을 시작할지 선택 가능
- 시작하는 index의 변경이 가능(1행의 k열부터 1, `a[1][k] == 1`)

  ```python
  np.eye(3)
  """
  array([[1., 0., 0.]
         [0., 1., 0.]
         [0., 0., 1.]])
  """

  np.eye(3, 5, k=2) # 마지막: 시작열
  """
  array([[0., 0., 1., 0., 0.]
         [0., 0., 0., 1., 0.]
         [0., 0., 0., 0., 1.]])
  """

  np.eye(N=3, M=5, dtype=np.int8)
  """
  array([[1, 0, 0, 0, 0]
         [0, 1, 0, 0, 0]
         [0, 0, 1, 0, 0]], dtype=int8)
  """
  ```

#### **diag**

- 대각행렬의 값을 추출함

  ```python
  matrix = np.arange(9).reshape(3, 3)
  np.diag(matrix)
  # array([0, 4, 8])

  np.diag(matrix, k=1) # k: start index
  # array([1, 5])
  ```

#### **random sampling**

- **데이터분포에 따른 sampling으로 array를 생성**
- 모수값이 중요(언제 어떻게 쓰이는데? - 더 알아보기)

- **균등분포(uniform)**
  - `np.random.uniform(0, 1, 10).reshape(2, 5)`
  - uniform(모수값(시작), 모수값(끝), 사이즈(데이터 수))
  - 시작~끝까지 균등한 확률로 값을 뽑아줌
  - 확률 분포별로 랜덤값 생성
- **정규분포(normal)**
  - `np.random.normal(0, 1, 10).shape(2, 5)`
- **지수분포(exponential)**
  - `np.random.exponential(scale)=2, size=100)`

---

### **operation function**

#### **sum**

- **ndarray의 element들 간의 합**을 구함, list의 sum 기능과 동일

  ```python
  # sum
  test_array = np.arange(1, 11) # array([1, 2, ..., 10])
  test_array.sum(dtype=np.float) # 55.0
  # mean, std, sqrt, exp도 있음 : 통계학에서 사용하는 연산이 많이 들어가있음
  # mathematical functions 찾아보기, 강의노트 p55

  sum(list) # 와 비슷함
  ```

#### **axis**

- 모든 operation **function을 실행할 때 기준이 되는 dimension 축**
- (3, 4) : (axis=0, axis=1)
  - axis=1 : 가로로 작동
  - axis=0 : 세로로 작동
  - ex) test_array.sum(axis=1) : 가로로 더한 값을 반환함
- **항상 새로 생긴 축이 axis=0**이 된다고 생각하기

#### **concatenate**

- **numpy array를 합치는, 붙이는 함수**
- vstack: 세로로 붙임
- hstack: 가로로 붙임

  ```python
  a = np.array([1, 2, 3])
  b = np.array([2, 3, 4])

  np.vstack((a, b)) # vertical
  # array([[1, 2, 3],[2, 3, 4]])

  a = np.array([[1], [2], [3]])
  b = np.array([[2], [3], [4]])

  np.hstack((a, b)) # horizontal
  # array([[1, 2],[2, 3],[3, 4]])
  ```

- concatenate / axis = 0: 붙였을 때 생성되는 axis (== ➡ ㅡ)
- concatenate / axis = 1: 붙였을 때 생성되는 axis (|| ➡ |)
- `concatenate((a, b), axis=0)`
- **인자로 넣은 축이 줄어든다고 생각!**

#### **축을 추가하는 방법**
  
- np.newaxis

  ```python
  b = np.array([5, 6])

  b.reshape(-1, 2)
  # array([[5, 6]])

  b[np.newaxis, :]
  # array([[5, 6]])
  ```

#### **array operations**

- numpy는 array간의 기본적인 사칙연산을 지원

##### **element-wise operations** (용어 중요 🔥)

- **array간 shape가 같을 때 일어나는 연산**
- **결과값은 matrix**(input과 동일한 shape)

##### **Dot product**

- matrix의 기본연산, dot 함수 사용
- 행렬간 곱셈연산
- a.dot(b)
- `[X,Y].dot([Y,Z]) => [X,Z]`

##### **transpose(전치행렬)**

- transpose 또는 T attribute 사용
- dot product 사용하기 편함
- 행렬의 행과 열을 변경해줌
- matrix간 곱셈
  - `a.T.dot(a)`

##### **broadcasting**

- **shape이 다른 배열 간 연산을 지원**하는 기능
  - 같으면 그냥 element wise operation 진행
- <u>서로의 row, col로 크기를 확장하여 맞추고, 연산하는 것</u>
- matrix + scalar인 경우, matrix의 모든 값에 scalar의 값이 더해짐
- scalar-vector 외에도 vector-matrix간의 연산도 지원

> 여기서 scalar는 그냥 value임, `array([1,])` 뭐 이런거 아님
  
---

### comparisions

numpy array들 간의 비교  

#### all & any

- `np.any(a>5)`
  - broadcasting 실행됨
  - `a > 5`: True or False의 boolean array가 나옴
  - all or any에 대한 조건탐색 함

#### comparison operation

- 비교 operation
  - numpy는 배열의 크기가 동일할 때, **element간 비교의 결과를 boolean type value 1개로 반환**
  - `(a > b).any()` : True
  - broadcasting, element wise operation 일어남

#### **logical_and**

- `np.logical_and( a>0, a<3 )`
- **두 인자가 모두 boolean 타입**인 경우, and 조건의 condition
- **각각 element wise 비교**
- `np.logical_not(b)`
- `np.logical_or(b)`

#### **where**

##### `np.where(condition, True, False)`

- 배열을 반환함
- 방식
  - 1) 데이터의 개수만큼,
    - t, f ➡ t인 경우에 두번째 인자가 리턴
    - t, f ➡ f인 경우에 세번째 인자를 그 자리에 넣어서 결국 배열을 리턴
  - 2) 인자를 하나만 넣어서, 조건에 맞는 인덱스 값들의 배열을 리턴
    - 튜플형태로 반환

##### `np.isnan(a)`

- not a number
- 조건을 찾는 것
- 메모리의 값이 존재하지 않는 경우를 찾음

##### `np.isfinite(a)`

- is finite number
- 한정되지 않은 값을 찾는 것
- 발산하는 경우를 찾음

  ```python
  a = np.array([1, np.NaN, np.Inf], float)
  np.isnan(a)
  # array([False, True, False])
  ```

#### **argmax & argmin**

- **`argmax, argmin`**
  - array 내의 최대값 또는 최소값의 index를 반환함

  ```python
  a = np.array([1, 2, 3, 4, 5, 8, 78, 23, 3])
  np.argmax(a), np.argmin(a)
  # (5, 0)
  
  a[np.argmin(a)] # 1

  a = np.array([[1, 2, 4, 7],[9, 88, 6, 45],[9, 76, 3, 4]])
  np.argmax(a, axis=1), np.argmin(a, axis=0)
  # |:0, ㅡ:1
  # (array([3, 1, 1]), array([0, 0, 2, 2]))
  ```

- **`a.argsort()`**
  - array([0, 1, 7, 2, 3, 4, 6, 5])

---

### **boolean & fancy index**

- 특정 조건에 따른 값을 배열 형태로 추출
- comparison operation함수들도 모두 사용가능

#### **boolean index**

- **condition: boolean list 사용**
- 사용하고자하는 두 배열의 shape이 같아야함
- boolean array가 들어가서 데이터를 쿼리해오는 것(가져오는 것)
- 특정 조건(condition)에 따름
- `b[a>3]`
  - a>3:조건(condition), 결과:TF array 
  - true인 인덱스에 있는 값만 빼줄 수 있음
  - a, b 두 배열의 shape이 동일해야함

#### fancy index

- bool 대신 index값을 넣어줌
- **condition: integer list 사용**
- 사용하고자하는 두 배열의 shape이 같지않아도 됨
  - 그러나 찾고자하는 인덱스의 값(인자 배열의 values)이 대상배열의 크기를 벗어나면 안됨
- `a[b]`
  - b는 반드시 integer로 선언
- `a.take(b)`
  - take함수: bracket index와 같은 효과
- matrix 형태의 데이터도 가능

  ```python
  a = np.array([[1, 4], [9, 16]], float)
  b = np.array([0, 0, 1, 1, 0], int)
  c = np.array([0, 1, 1, 1, 1], int)

  a[b, c] # b를 row index, c를 column index로 변환하여 표시함
  # array([1., 4., 16., 16., 4.])

  a[b]
  # row만 넣어주면, row 값만 가져옴
  # array([[1., 4.], [1., 4.], [9., 16.], [9., 16.], [1., 4.]])
  ```

---

### numpy data I/O

persistence ?  

#### loadtxt & savetxt

```python
a = np.loadtxt("./filename.txt") # csv같은
a[:10]

# int type 변환
a_int = a.astype(int)
a_int[:3]

# int_data.csv로 저장
np.savetxt('int_data.csv', a_int, delimiter=',')
# 파일명, 저장하고싶은 array, 데이터 저장하는/자르는 기준값

np.savetxt('int_data.csv', a_int, fmt="%.2e", delimiter=',')
# 소수점 2자리까지 저장

#################333
# numpy object - npy
np.save("npy_teset_object", arr=a_int) # pickle 저장
a_test = np.load(file="npy_teset_object.npy")
a_test
```

---

### **ETC**

#### **numpy performance**

- **timeit**: jupyter 환경에서 코드의 퍼포먼스를 체크하는 함수
- 일반적으로 속도는 아래와 같은 순서로 빠름
  - **`for loop < list comprehension < numpy`**
  - numpy가 list보다 빠름
  - 100,000,000번의 loop를 돌 때, 약 4배 이상의 성능차이를 보임
  - <u>numpy는 c로 구현되어있어, 성능을 확보하는 대신, 파이썬의 가장 큰 특징인 dynamic typing을 포기함</u>
  - 대용량 계산에서 가장 흔히 사용됨
  - concatenate처럼 계산이아닌 할당에서는 연산 속도의 이점이 없음
