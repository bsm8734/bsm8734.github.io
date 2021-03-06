---
title: "[부스트캠프 AI Tech / Day6] Math_AI 행렬"
data: 2021-01-25 20:30:00 +0800
categories: [네이버 부스트캠프 AI Tech, Math_AI]
tags: [Math]
use_math: True
---


## **[DAY 6] 행렬**

---

### **행렬**

- **행렬(matrix)은 벡터를 원소로 가지는 2차원 배열**
- `np.array([[ ],[ ],[ ]])` : numpy에서는 행(row)이 기본단위
  - 세개의 행 벡터를 담는 이차원 배열로 해석됨
- 행렬은 행(row)와 열(column)이라는 인덱스(index)를 가짐
- **행렬표기**: $X=(a_{xy})$ : $i$ 번째 행벡터에 있는 $j$ 번째 원소
  - $N*M$ 행렬: N개의 행(M개의 열)으로 이루어짐
  - $x$: 배열, $X$: 행렬
  - 행렬의 특정 행(열)을 고정하면 행(열)벡터라 부름
- **전치행렬**
  - $X^T=(x_{ji})$
  - 전치행렬(transpose matrix)은 행과 열의 인덱스가 바뀐 행렬
  - 행벡터는 열벡터가 되고, 열벡터는 행벡터가 됨

---

### **행렬의 이해방법(1)**

- <u>벡터가 공간에서 한 점을 의미한다면 행렬은 여러 점들을 나타냄</u>
- **행렬**: 공간상의 여러점들의 집합
- 행렬의 행벡터(ㅡ): $x_i$는 $i$번째 데이터를 의미
- 행렬의 $x_{ij}$는 $i$번째 데이터의 $j$번째 변수의 값을 말함

#### 행렬의 덧셈, 뺄셈, 성분곱, 스칼라곱

- 행렬은 벡터를 원소로 가지는 2차원 배열

##### **덧셈, 뺄셈**

- 행렬끼리 같은 모양을 가지면 덧셈, 뺄셈을 계산할 수 있음
- $X \pm Y=(x_{ij} \pm y_{ij})$

##### **성분곱, 스칼라곱**

- **성분곱**은 벡터와 같음
  - $X {\odot} Y=(x_{ij}y_{ij})$
- **스칼라곱**도 벡터와 차이가 없음
  - $aX=(ax_{ij})$
- **행렬 곱셈**
  - matrix multiplication
  - 행렬곱셈은 $i$번째 행벡터와 $j$번째 열벡터 사이의 *내적을 성분으로 가지는* 행렬을 계산
  - $XY=(\sum_{k=1}^N x_{ik}y_{kj})$
  - **행렬곱은 X의 열의 개수와 Y의 행의 개수가 같아야함**(둘을 내적)
    - 두 벡터의 내적을 구하기 위해서는 두 벡터의 인자 수가 같아야 하기 때문
  - 결과는 하나의 value가 도출됨(배열, 행렬 형태X)
  - numpy에서는 `@`연산을 사용
  - $XY != YX$ 어떤 행렬을 앞에 놓고 뒤에 놓느냐에 따라서 값이 달라짐

##### **행렬의 내적?**

- 행렬은 벡터에서 정의했던 내적이 존재할까? YES
- numpy의 `np.inner`은 **i번째 행 벡터와 j번째 행벡터 사이의 내적**을 성분으로 가지는 행렬을 계산
- 수학에서 말하는 내적과는 다름을 주의
- 수학에서의 행렬의 내적-> trace(?) 💥
  - numpy의 내적과 다름(?!) 💥
- $X$행렬과 $Y$의 전치행렬($Y^T$)의 행렬곱 역할
- 행렬곱은: 두 벡터의 행, 열을 곱함
- $X{Y^T}= (\sum_{k=1}^N x_{ik}y_{jk})$
- **두 행렬의 행벡터의 크기가 서로 같아야 사용할 수 있음**
- 결과는 X의 행의 수가 행, Y의 행의 수가 열이 되어서 나옴
- (3,3) (2,3) ➡ (3,2)

---

### **행렬을 이해하는 방법(2)**

- <u>행렬은 벡터공간에서 사용되는 연산자(operator)</u>
- <u>행렬곱을 통해 벡터를 다른 차원의 공간으로 보낼 수 있음</u>
- 행렬곱을 통해 패턴을 추출할 수 있고 데이터를 압축할 수도 있음
- 모든 선형변환(linear transform)은 행렬곱으로 계산할 수 있음
- $z_i = \sum_{=h1}^N a_{ij}x_j$
- N개의 원소로 이루어져있는 M개의 벡터
- **벡터: M개의 행, 1개의 열로 볼 수 있음**
- 따라서 벡터와 행렬의 연산이 가능
- 이때의 a는 N개의 행과 M개의 열로 이루어져있음
- Z와 X는 A와 어떻게 연결되어있냐면,
  - `[|]=[=][|]` 이렇게 Z와 X를 A로 이어줄 수 있으므로 A를 연산자로 볼 수 있다는 것
- 행렬곱을 통해 두 벡터를 이어줄 수 있고
- N차원 공간으로 한 점을 맵핑한다고 볼수있음
- 행렬곱을 통해 패턴을 추출할 수 있고, 데이터를 압축할 수도 있음
- 선형모델, 선형변환의 이해
- 딥러닝은 선형과 비선형변환 함수로 이루어져있으므로 이 파트는 중요!

#### **역행렬**

- $A^{-1}$: **어떤 행렬 A의 연산을 거꾸로 되돌리는 행렬**을 역행렬(Inverse matrix)이가 부름
- 역행렬은 **행과 열 숫자가 같고** **행렬식(determinant)이 0이 아닌 경우에만** 계산할 수 있음
- 되돌리는 연산
- $AA^{-1} = A^{-1}A = I$ (항등행렬)
  - 항등행렬의 역할
  - 임의의벡터를 곱했을 때, 자기 자신이 나옴
- $X$ ➡ $Z$ ➡ $X$ 가능

##### **linear algebra lib 사용**

- `np.linalg.inv(x)`
- 사용 위해서는 위에 나온 두개의 조건을 만족해야함
- 역행렬 조건이 가능한지 먼저 확인해야함
- `X @ np.linalg.inv(x)` 항등행렬과 비슷한 값이 나옴(? 왜 똑같이 안나옴?) 💥
  - 아마도 연산 과정에서 반올림되는 부분에서의 값 차이가 생기나봄

- 만일 역행렬을 계산할 수 없다면 **유사역행렬(pseudo-inverse)** 또는 **무어-펜로즈(Moore-Pensore) 역행렬 $A^+$** 을 이용함
  - 이를 활용하여 항등행렬과 유사하게 유도할 수 있음
  - (행)$n \ge m$(열)인 경우, $A^+ = (A^T A)^{-1} A^T$
    - 원래 보다 먼저 곱해주기 => 주의
  - $n \le m$인 경우, $A^+ = A^T (A A^T)^{-1}$
    - 원래 보다 나중에 곱해주기 => 주의
  - $n \ge m$이면 $A^+ A = I$가 성립하고
  - $n \le m$이면 $A A^+ = I$가 성립함
- $+$: 선형대수에서 쓰임 ➡ 더 알아보기 💥
- <u>행과 열의개수가 달라도 유사하게 사용할 수있음</u>
  - 만약 주어진 경우에서 행의 경우가 열의 갯수보다 더 크거나 작은 경우의 곱하는 경우가 다름
- `np.linalg.pinv(Y)`
  - p(seudo-)inv(erse)의 약자
  - `np.linalg.pinv(Y) @ Y`는 역행렬과 유사하게 나옴

### 응용 1

- `np.linalg.pinv`를이용하면연립방정식의해를구할수있다
- 식의 해가 변수의 갯수와 같아야 해를 구할 수 있음
- 식의 수 < 변수의 개수 : 해가 무한하다/부정 ➡ 그 해 중 하나를 구하는 것이 유사역행렬
- 연립방정식을 행렬을 사용하여 표현: Ax=b
- $A (N, M)$의 행렬이고, $n \le M$이라면, 식이 변수 개수보다 작거나 같은 경우임
- $n \le m$이면, 무어-펜로즈 역행렬을 이용하면 해를 하나 구할 수 있음
- $Ax=b$
- $x = A^{+} b = A^T (A A^T)^{-1} b$

### 응용2

- **선형회귀분석**
- 변수 > 식인 경우, 선형회귀에 많이 사용됨
- 유사역행렬 응용
- 데이터를 표현하는 선형모델을 해석 ➡ 선형모델에 해당하는 선형회귀식 표현가능
- 데이터를 행렬 $X$로 표현
- 여러 점을 하나의 점으로 표현하여 이를 모아 $X$라 표현
- $X_{\beta}$ : **계수벡터(coefficient vector)**
- 어떤 $\beta$를 써야 잘 해석할 수있는가 ? 선형회귀!
- 방정식을 푸는것은 불가능
  - $X_{\beta}$는 $y$를 만족하는 $x$찾기 불가능
  - 왜냐면 데이터가 선형위에 올려져있지 않기 때문
  - **이 선이 데이터를 최대한 잘 표현하게** 하면, 그것이 최선!
  - 최선의 회귀식(선형) ➡ 데이터의 y값을 예측할 때
  - 선형모델 식: $\hat{y}$
  - 데이터에 주어진 데이터의 정답: $y$ 벡터
  - 둘의 차가 최소가 되는 경우가 잘 만든 경우
  - L2-norm을 최소화 하는 계수 베타를 찾게되면, 주어진 데이터를 사용하여 선형모델을 잘 표현했다고 할 수 있음
  - 무어펜로즈를 사용하면 y에 가장 근접하는 $\hat{y}$을 사용할 수 있음(L2-norm 사용하여)
  - $X$행렬의 무어펜로즈 역행렬을 $y$에 곱해주면 이때 주어진 베타가 가장 최적의 선형회귀 계수임
  - p.35참고
- **두가지 방법**
  - `np.linalg.pinv`를 이용
    - 데이터를 선형모델(linear model)로 해석하는 선형회귀식을 찾을 수 있음
  - `sklearn의LinearRegression`과 같은 결과를 가져올 수 있음
  
    ```python
    # Scikit Learn을 활용한 회귀분석
    from sklearn.linear_model import LinearRegression
    model = LinearRegression()
    model.fit(X, y)
    y_test = model.predict(x_test)
    # y절편항을 같이 고려해주어야함
    # 자동으로 y절편을 더해서 추정해줌

    ##################

    # Moore-Penrose의 역행렬
    beta = np.linalg.pinv(X) @ y
    y_test = np.append(x_test) @ betas

    # y 절편 항을 직접 추가해서 구해중야함
    # 그래야 위와 같은 결과를 도출할 수 있음

    X_ = np.array([np.append(x, [1]) for x in X])
    beta = np.linalg.pinv(X_) @ y
    y_test - np.append(x, [1]) @ beta
    ```
