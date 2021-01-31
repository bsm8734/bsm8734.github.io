---
title: "[부스트캠프 AI Tech / Day5] 파이썬 Exception"
date: 2020-01-22 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python] # Python
tags: [Python] # CS, 운영체제, Python
---


## **[DAY 5] Exception**

---

### **Exception**

- 예상 가능한 예외
  - 발생 여부를 프로그래머가, 사전에 인지할 수 있는 예외
  - 사용자의 잘못된 입력, 파일 호출 시 파일 없음
  - 개발자가 반드시 명시적으로 정의, 처리 해야함
- 예상이 불가능한 예외
  - 인터프리터 과정에서 발생하는 예외, 개발자 실수
  - 리스트의 범위를 넘어가는 값 호출, 정수 0으로 나눔
  - 수행 불가시 인터프리터가 자동 호출

#### **Exception의 종류**
  
- **Built-in Exception**: 기본적으로 제공하는 예외 (빌트인 에러)
  - `IndexError`: List의 Index 범위를 넘어갈 때
  - `NameError`: 존재하지 않은 변수를 호출 할 때
  - `ZeroDivisionError`: 0으로 숫자를 나눌 때
  - `ValueError`: 변환할 수 없는 문자/숫자를 변환할 때
  - `FileNotFoundError`: 존재하지 않는 파일을 호출할 때

---

### **예외 처리 (Exception Handling)**

- 예외가 발생할 경우 후속조치등 대처필요
  1) 없는파일 호출 ➡ 파일없음을 알림
  2) 게임 이상종료 ➡ 게임정보 저장
- 프로그램 = 제품, 모든 잘못된상황에 대처가 필요 : **Exception Handling**
- `if ~ else`로 처리해도 되지만, Exception 발생시키고, 이를 처리하는 방식을 권장하는 경우도 있음
- **try ~ except** 문법
  - `try`: 예외 발생 가능 코드
  - `except <Exception Type>`: 예외 발생시 대응하는 코드

```python
# 0으로숫자를나눌때예외처리하기
for i in range(10):
try:
    print(10 / i) # exception 발견
except ZeroDivisionError as e: # error catch / handling
    print(e): # e에는 어떤 예외인지에 대한 정보가 들어가있음
    print("Not divided by 0")
except IndexError as e: # error catch / handling
    print(e): #  index out of range~
except Exception as e # 가장 큰 exception(모든 exception을 포함) # 어디서 에러가 났는지 알기 힘들기때문에, 큰 Exception은 좋은 코드가 아님
    print(e):
```

#### **try ~ except ~ else**

- `try`: 예외 발생 가능 코드
- `except <Exception Type>`: 예외 발생시 동작하는 코드
- `else`: 예외가 발생하지 않을 때 동작하는 코드

#### **try ~ except ~ finally**

- `try`: 예외 발생 가능 코드
- `except <Exception Type>`: 예외 발생시 동작하는 코드
- `finally`: 예외 발생 여부와 상관없이 실행됨

```python
try:
    for i in range(1, 10):  # 에러가 아닌 경우
    result = 10 // i
    print(result)
except ZeroDivisionError: # 에러인 경우
    print("Not divided by 0")
finally:                  # 에러인 경우든, 에러가 아닌 경우든 실행
    print("종료되었습니다.")
```

> if 문 : 정상적인, 로직적인 문제
> exception: 사용자의 입력등으로 인해, 데이터가 잘못 입력되거나 잘못 처리되기 쉬운 경우
> ex) empty data ➡ exception

#### **raise 구문**

- 남들이 내가 만든 코드를 잘못 사용하는 경우
- 잘못되었을 경우, 빠르게 프로그램을 종료하는게 나을 수 있음(자원//메모리, 시간낭비 방지하기 위함)
- 필요에 따라 강제로 Exception을 발생
- `raise <Exception Type>(예외정보)`

```python
while True:
  value = input("변환할 정수 값을 입력해주세요")
  for digit in value:
    if digit not in "0123456789":
      raise ValueError("숫자값을 입력하지 않으셨습니다")
  print("정수값으로 변환된 숫자 -", int(value))
```

#### **assert 구문**

- 특정조건에 만족하지 않을 경우, 예외발생
- `assert 예외조건`

```python
  def get_binary_nmubmer(decimal_number : int): # :int로 타입 hinting까지 줬는데도 잘못입력하는 경우가 있음
    assert isinstance(decimal_number, int) # 이 부분이 True / False로 나올 수 있도록 하고, False인 경우, assertionError 발생시켜, 멈추게함
    return bin(decimal_number)
  print(get_binary_nmubmer(10))
```
