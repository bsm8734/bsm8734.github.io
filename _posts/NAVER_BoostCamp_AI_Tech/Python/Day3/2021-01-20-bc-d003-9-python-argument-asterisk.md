---
title: "[부스트캠프 AI Tech / Day3] 파이썬 Argument & Asterisk"
date: 2020-01-20 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python] # Python
tags: [Python] # CS, 운영체제, Python
---


## **[DAY 3] Argument & Asterisk**

---

### **Function Passing Arguments**

- 함수에 입력되는 arguments의 다양한 형태
  - 1) Keyword arguments
  - 2) Default arguments
  - 3) Variable-length arguments

#### **Keyword arguments**

- 함수에 입력되는 parameter의 변수명을 사용, arguments를 넘김

    ```python
    def print_somthing(my_name, your_name):
        print("Hello {0}, My name is {1}".format(your_name, my_name))

    print_somthing("Sungchul", "TEAMLAB")
    print_somthing(your_name="TEAMLAB", my_name="Sungchul")
    ```

#### **Default arguments**

- parameter의 기본 값을 사용, 입력하지 않을 경우 기본값 출력

    ```python
    def print_somthing_2(my_name, your_name="TEAMLAB"):
        print("Hello {0}, My name is {1}".format(your_name, my_name))
    print_somthing_2("Sungchul", "TEAMLAB")
    print_somthing_2("Sungchul")
    ```

</br>

---

### **Asterisk(*)**

#### **asterisk**

- 흔히 알고 있는 * 를 의미함
- 단순 곱셈, 제곱연산, 가변 인자 활용 등 다양하게 사용됨
- unpacking a container
  - tuple, dict 등 자료형에 들어가 있는 값을 unpacking
  - 함수의 입력값, zip 등에 유용하게 사용가능

#### **Variable-length asterisk(가변인자)**

- 함수의 parameter가 정해지지 않았을 경우 ➡ 가변인자 using asterisk 사용
- 가변인자 (variable-length)
  - 개수가 정해지지 않은 변수를 함수의 parameter로 사용하는 법
  - Keyword arguments와 함께, argument 추가 가능
  - **Asterisk(*) 기호를 사용하여 함수의 parameter를 표시**
  - 입력된 값은 tuple type으로 사용할 수 있음
  - 가변인자는 오직 한 개만 맨 마지막 parameter 위치에 사용가능
  - 가변인자는 일반적으로 *args를 변수명으로 사용
  - 기존 parameter 이후에 나오는 값을 tuple로 저장함

    ```python
    def asterisk_test(a, b, *args):
        return a+b+sum(args)
    print(asterisk_test(1, 2, 3, 4, 5))

    def asterisk_test_2(*args):
        x, y, z = args
        return x, y, z
    print(asterisk_test_2(3, 4, 5))
    ```

#### **Keyword variable-length asterisk(키워드 가변인자)**

- Parameter 이름을 따로 지정하지 않고 입력하는 방법
- asterisk(*) 두개를 사용하여 함수의 parameter를 표시함
- 입력된 값은 dict type으로 사용할 수 있음
- 가변인자는 오직 한 개만 기존 가변인자 다음에 사용

  ```python
  def kwargs_test_1(**kwargs):
    print(kwargs)

  def kwargs_test_2(**kwargs):
    print(kwargs)
    print("First value is {first}".format(**kwargs))
    print("Second value is {second}".format(**kwargs))
    print("Third value is {third}".format(**kwargs))

  def kwargs_test_3(one,two, *args, **kwargs):
    print(one+two+sum(args))
    print(kwargs)
  kwargs_test_3(3,4,5,6,7,8,9, first=3, second=4, third=5)
  ```

---

- ex)

```python
# *args
def asterisk_test(a, *args):
print(a, args)
print(type(args))
asterisk_test(1,2,3,4,5,6)

# **kargs
def asterisk_test(a, **kargs):
print(a, kargs)
print(type(kargs))
asterisk_test(1, b=2, c=3, d=4, e=5, f=6)

# unpacking a container
def asterisk_test(a, *args):
print(a, args)
print(type(args))
asterisk_test(1, *(2,3,4,5,6))

def asterisk_test(a, args):
print(a,*args)
print(type(args))
asterisk_test(1, (2,3,4,5,6))

a, b, c = ([1, 2], [3, 4], [5, 6])
print(a, b, c)
data = ([1, 2], [3, 4], [5, 6])
print(*data)

def asterisk_test(a, b, c, d,):
print(a, b, c, d)
data = {"b":1 , "c":2, "d":3}
asterisk_test(10, **data)

for data in zip(*([1, 2], [3, 4], [5, 6])):
print(data)

```