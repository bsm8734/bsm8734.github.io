---
title: "[부스트캠프 AI Tech / Day2] 파이썬 Print Formatting(I/O)"
date: 2020-01-19 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python] # Python
tags: [Python] # CS, 운영체제, Python
---


## **[DAY 2] 파이썬 Print Formatting(I/O)**

---

### 입출력 양식

- console in/out
  - 프로그램과 데이터를 주고받는 방법
  - **입력: input**
    - `input()` 함수: 콘솔창에서 문자열을 입력받는 함수
    - `var = input()`
    - 숫자 입력 받기: `var = float(input("입력하세요 :"))`
    - 괄호 안에 문자열을 넣는 경우, 콘솔에 입력 가이드처럼 쓸 수 있음
  - **출력: print**
    - 콤마(,) 사용할 경우, print 문이연결됨
    - `print ("Hello World!", "Hello Again!!!")`
    - 타입이 다른 경우, 연속적으로 출력하기 위해서 사용
    - 콤마를 사용하지 않는 경우, 형변환 후에 concatenate 해야함

### Print Formatting

- 형식(format)에 맞춰서 출력하고자 할 때 사용
- print문을 활용하여 결과 formatting
- print문은 기본적인 출력 외에 출력양식 형식을 지정가능
- fomatting 방법
  - (1) % string
  - (2) format 함수
  - (3) fstring

#### **1. % string**

- 일반적으로 %-format 과 str.format() 함수를사용함

```python
print('%s %s' % ('one', 'two'))
print('{} {}'.format('one', 'two'))
print('%d %d' % (1, 2))
print('{} {}'.format(1, 2))
```

#### **2. %-formatting**

- "%datatype" % (variable) 형태로 출력 양식을 표현
- % datatype
  - %d: integer
  - %s: string
  - %f: float

```python
  print("I eat %d apples." % 3)
  print("I eat %s apples." % "five")
  number = 3; day="three"
  print("I ate %d apples. I was sick for %s days." % (number, day))
  print("Product: %s, Price per unit: %f." % ("Apple", 5.243))
  
  print("Product: %5d, Price per unit: %8.2f." % ("Apple", 5.243))
  # 5: 5칸을 비워두라(%5d)
  # 8: 8칸을 비워두라(%8.2f)
  # 2: 소수점은 두자리만 출력(%8.2f) (그 아래는 반올림으로 처리)
```

#### **3. format 함수**

- str.format() 함수
- "~{datatype}~".format(argument)

```python
  age = 36; name='Sungchul Choi'
  print("I’m {0} years old.".format(age))

  print("My name is {0} and {1} years old.".format(name, age)) # 0과 1은 인덱스
  # "My name is {name} and {age} years old."

  print("My name is {1} and {0} years old.".format(name, age))
  # "My name is {age} and {name} years old."

  print( "Product: {0}, Price per unit: {1:.3f}.".format("Apple", 5.243))
  # 0, 1을 순서대로 넣고, 1번은 소수점 3자리까지 넣기

  "Art: {0:5d}, Price per Unit: {1:8.2f}".format(453, 59.058)
  # Art:   453, Price per Unit:    59.06
```

#### **4. fstring**

- python 3.6 이후, PEP498에 근거한 formatting 기법
- f라고 앞에 써주고 사용해야함
- 이전에 선언된 변수명을 그대로 가져와서 사용할 수 있음
- 왼쪽 정렬이 기본

```python
  name = "Sungchul"
  age = 39
  print(f"Hello, {name}. You are {age}.") # Hello, Sungchul. You are 39.
  print(f'{name:20}')   # Sungchul
  print(f'{name:>20}')  # Sungchul
  print(f'{name:*<20}') # Sungchul************ # 나머지는 별표로 채워줌
  print(f'{name:*>20}') # ************Sungchul
  print(f'{name:*^20}') # ******Sungchul****** # 가운데 정렬
  number = 3.141592653589793
  print(f'{number:.2f}') # 3.14
```

#### **padding**

- 여유공간을 지정하여 글자배열 + 소수점 자릿수를 맞추기

```python
  print("Product: %5s, Price per unit: %.5f." % ("Apple", 5.243))
  print("Product: {0:5s}, Price per unit: {1:.5f}.".format("Apple", 5.243))
  print("Product: %10s, Price per unit: %10.3f." % ("Apple", 5.243))
  print("Product: {0:>10s}, Price per unit: {1:10.3f}.".format("Apple", 5.243))
  # 10칸을 비우면서 오른칸으로 정렬(<)   #      5.243
  # 10칸을 비우면서 왼칸으로 정렬(>)     # 5.243
```

#### **naming**

- 표시할 내용을 변수로 표시하여 입력

```python
  print("Product: %(name)10s, Price per unit: %(price)10.5f." % {"name":"Apple", "price":5.243})
  # Product:      Apple, Price per unit:     5.24300.
  print("Product: {name:>10s}, Price per unit: {price:10.5f}.".format(name="Apple", price=5.243))
  # Product: Apple     , Price per unit:     5.24300.
```
