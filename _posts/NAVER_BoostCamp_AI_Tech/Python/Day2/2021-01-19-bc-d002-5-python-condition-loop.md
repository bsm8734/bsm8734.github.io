---
title: "[부스트캠프 AI Tech / Day2] 파이썬 조건문, 반복문"
date: 2020-01-19 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python] # Python
tags: [Python] # CS, 운영체제, Python
---


## **[DAY 2] 파이썬 Conditionals and Loops**

---

### **조건문** (Conditionals)

- 조건문: 조건에 따라 특정한 동작을 하게하는 명령어
- 조건문은 조건을 나타내는 기준과 실행해야 할 명령으로 구성됨
- 조건의 참, 거짓에 따라 실행해야 할 명령이 수행되거나 되지 않음
- 파이썬은 조건문으로 if , else , elif 등의 예약어를 사용함

#### **if-elif-else**

- if-else문 문법
  - (1) 조건 판단 방법
  - (2) 조건 일치 시 수행 명령 block ":"와 들여쓰기
  - (3) 조건 불일치 시 수행 명령 block
  - if를 계속 반복해서 쓰면, 조건 만족 시에도 아래 if문을 전부 방문(elif 쓰기)
  - 하나의 if문에는 *if절이 하나, elif절이 0개 이상, else절이 1개 이하*
  - else 키워드 뒤엔 조건 삭제

  ```python
  if <조건>: # if를 쓰고 조건 삽입 후 “:” 입력
    <수행 명령1-1> # 들여쓰기(indentation)후 수행명령 입력
    <수행 명령1-2> # 같은 조건하에 실행일 경우 들여쓰기 유지
  else: # 조건이 불일치할 경우 수행할 명령 block
    <수행 명령2-1> # 조건 불일치 시 수행할 명령 입력
    <수행 명령2-2> # 조건 불일치 시 수행할 명령 들여쓰기 유지
  ```

- 조건 판단 방법
  - if 다음에 조건을 표기하여 참 또는 거짓을 판단함
  - 참/거짓의 구분을 위해서는 비교연산자를 활용
  - `x is y`, `x is not y`: 메모리의 주소를 비교(같은 메모리 주소를 가지고 있는지 확인)
  - `<, >, ==, <=, >=`: 값을 비교
  - `-5 ~ 255`범위의 `is`
    - `-5 ~ 255`는 많이 사용하는 숫자였기 때문에 메모리주소를 고정하고, 가리키는 형태로 만들게 되었음

    ```python
    a = -5
    b = -5
    if(a is b):
      print("same!") # 출력됨
    a = -6
    b = -6
    if(a is b):
      print("same!") # 출력되지 않음
    ```

- 조건 참/거짓의 구분
  - 숫자형의 경우는 수학에서의 참/거짓과 동일
  - 컴퓨터는 존재하면 참 없으면 거짓이라고 판단함
  - 마찬가지로, `if "abc":`는 참, `if "":`은 거짓임

  ```python
  if 1:
    print("True")
  else:
    print("False")
  
  # True
  ```

- **논리 키워드**: `and, or, not`
  - 조건문을 표현할 때, 집합의 논리키워드를 함께 사용하여 참과 거짓을 판단하기도 함
  - list 원소들 내의 and, or 연산: `all(list), any(list)`
  
  ```python
  a = 8, b = 5
  if a == 8 and b ==4:   # 거짓
  if a > 7 or b > 7:     # 참
  if not (a > 7):        # 거짓, a>7인 것이 참 이므로 거짓으로 판단됨

  list1 = [True, False, True]
  all(list1) # False
  any(list1) # True
  ```

- **삼항 연산자(Ternary operators)**
  - 조건문을 사용하여 참일 경우와 거짓을 경우의 결과를 한 줄에 표현

  ```python
  >>> value = 12
  >>> is_even = True if value % 2 == 0 else False
  # is_even = ((True)         if (value % 2 == 0)    else (False))
  #           (조건만족시)    (if 조건문)            (else 조건불만족시)
  >>> print(is_even)
  True
  ```

---

### **반복문** (loop)

- 정해진 동작을 반복적으로 수행하게 하는 명령문
- 반복문은 반복 시작조건, 종료조건, 수행명령으로 구성됨
- 반복문 역시 반복 구문은 들여쓰기와 block으로 구분됨
- 파이썬은 반복문으로 `for, while` 등의 명령 키워드를 사용함
- 기본적인 반복문: 반복 범위를 지정하여 반복문 수행
  1. looper 변수에 1 할당
  2. "Hello" 출력
  3. 리스트(대괄호속 숫자들) 있는 값 차례로 looper 할당
  4. 5까지 할당한 후 반복 block 수행 후 종료
  
  ```python
  for i in [1,2,3,4,5]:
    print(i)
  ```

- **range()**
  - range()는 마지막 숫자 바로 앞까지 리스트를 만들어줌
  - `range(0,5)` = `[0,1,2,3,4]` = `range(5)`는 *같은 의미*
  
    ```python
    for looper in [1,2,3,4,5]:
      print ("hello")
    for looper in range(0,5):
      print ("hello")
    # Hello
    # Hello
    # Hello
    # Hello
    # Hello
    #
    for looper in range(0, 5):
      print(f"{looper} : Hello")
    # 0 : Hello
    # 1 : Hello
    # 2 : Hello
    # 3 : Hello
    # 4 : Hello
    ```

  - 간격을 두고 세기
  
    ```python
    # 1부터 10까지 2씩 증가시키면서 반복문 수행
    for i in range(1, 10, 2):
      print (i)
    ```

  - 역순으로 반복문 수행

    ```python
    # 10부터 1까지 -1씩 감소시키면서 반복문 수행
    for i in range(10, 1, -1):
      print (i)
    ```

- **시퀀스형 자료형의 반복문**
  - 문자열을 한자씩 리스트로 처리
  
  ```python
  for i in "abcdefg":
    print (i)
  ```

  - 각각의 문자열 리스트로 처리
  
  ```python
  for i in ["americano", "latte", "frafuchino"]:
    print (i)
  ```

### while문

- <u>조건이 만족하는 동안</u> 반복 명령문을 수행
- for문은 while문으로 변환 가능
  - for문은 반복 실행횟수를 명확히 알 때 사용
  - while문은 반복 실행횟수가 명확하지 않을 때 사용
- 반복의 제어(break, continue, else)
  - break: 특정 조건에서 반복 종료
  - continue: 특정 조건에서 남은 반복 명령을 skip
  - else: 반복 조건이 만족하지 않을 경우 반복 종료하고 1회 수행
    - (주의) break로 종료된 반복문은 else block이 수행되지 않음

  ```python
    for i in range(10):
      print (i)
    else:
      print ("EOP")

    i =0
    while i < 10:
      print (i,)
      i += 1
    else:
      print ("EOP")
  ```

  <details markdown="2"> <summary> 📌 반복문 상식 </summary>

  - 반복문 변수명  
    - 임시적인 반복 변수는 대부분 i, j, k로 정함
  - 0부터 시작하는 반복문
    - 반복문은 대부분 0부터 반복을 시작
    - 이것도 일종의 관례로 1부터 시작하는 언어도 존재
    - 2진수가 0부터 시작하기 때문에 0부터 시작하는 것을 권장
  - 무한 loop
    - 반복 명령이 끝나지 않는 프로그램 오류
    - CPU와 메모리 등 컴퓨터의 리소스를 과다하게 점유

  </details>