---
title: "[부스트캠프 AI Tech / Day3] 파이썬 Tuple & Set"
date: 2020-01-20 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python] # Python
tags: [Python] # CS, 운영체제, Python
---


## **[DAY 3] Tuple & Set**

---

### **Collections**

- List, Tuple, Dict에 대한 Python Built-in 확장 자료 구조(모듈)
- 편의성, 실행 효율 등을 사용자에게 제공함
- 아래의 모듈이 존재함

```python
  - from collections import deque
  - from collections import Counter
  - from collections import OrderedDict
  - from collections import defaultdict
  - from collections import namedtuple
```

### **튜플 (tuple)**

- **값의 변경이 불가능한 리스트**
- 선언 시 "[ ]" 가 아닌 "( )"를 사용
- 리스트의 연산, 인덱싱, 슬라이싱 등을 동일하게 사용
- 사용목적
  - 프로그램을 작동하는 동안 변경되지 않은 데이터의 저장
  - 함수의 반환 값등 사용자의 실수에 의한 에러를 사전에 방지

```bash
>>> t = (1,2,3)
>>> print (t + t , t * 2)
# (1, 2, 3, 1, 2, 3) (1, 2, 3, 1, 2, 3)
# (1, 2, 3, 1, 2, 3) (1, 2, 3, 1, 2, 3)

>>> len(t) # 3

>>> t[1] = 5 # Error 발생
    Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
    TypeError: 'tuple' object does not support item assignment

>>> t = (1) # 일반정수로 인식
# 1
>>> t = (1, ) # 값이 하나인 Tuple은 반드시 "," 를 붙여야 함
# (1, )
```

### **namedtuple**

- collections - namedtuple
- Tuple 형태로 Data 구조체를 저장하는 방법
- 저장되는 data의 variable을 사전에 지정해서 저장함
  
    ```python
    from collections import namedtuple
    
    Point = namedtuple('Point', ['x', 'y'])
    p = Point(11, y=22)
    print(p[0] + p[1])

    x, y = p # 언패킹
    print(x, y)
    print(p.x + p.y)
    print(Point(x=11, y=22))
    ```

    ```python
    from collections import namedtuple
    import csv

    f = open("users.csv", "r")
    next(f)
    reader = csv.reader(f)
    student_list = []
    for row in reader:
        student_list.append(row)
        print(row)

    coloumns = ["user_id", "integration_id", "login_id", "password", 
        "first_name", "last_name", "full_name", "sortable_name", "short_name", "email", "status"]
    Student = namedtuple('Student', " ".join(coloumns))
    student_namedtupe_list = []
    for row in student_list:
        student = Student(*row)
        student_namedtupe_list.append(student)
    print(student_namedtupe_list)
    print(student_namedtupe_list[0].full_name)
    ```

### **집합 (set)**

- 값을 순서없이 저장, 중복 불허 하는 자료형
- set 객체 선언을 이용하여 객체 생성

```python
# 선언
>>> s = set([1,2,3,1,2,3]) # set 함수를 사용 1,2,3을 집합 객체 생성 , a = {1,2,3,4,5} 도 가능

# add, remove
>>> s
#{1, 2, 3}
>>> s.add(1) # 한 원소 1만 추가, 추가, 중복불허로 추가 되지 않음
>>> s
#{1, 2, 3}
>>> s.remove(1) # 1 삭제
>>> s
# {2, 3}

# update, discard, clear
>>> s.update([1,4,5,6,7]) # [1,4,5,6,7] 추가
>>> s
# {1, 2, 3, 4, 5, 6, 7}
>>> s.discard(3) # 3 삭제
>>> s
# {1, 2, 4, 5, 6, 7}
>>> s.clear() # 모든 원소 삭제

# 연산(|, &, union, intersection, difference)
>>> s1 = set([1,2,3,4,5])
>>> s2 = set([3,4,5,6,7])
>>> s1.union(s2) # s1 과 s2의 합집합
# {1, 2, 3, 4, 5, 6, 7}
>>> s1 | s2 # set([1, 2, 3, 4, 5, 6, 7])
# {1, 2, 3, 4, 5, 6, 7}
>>> s1.intersection(s2) # s1 과 s2의 교집합
# {3, 4, 5}
>>> s1 & s2 # set([3, 4, 5])
# {3, 4, 5}
>>> s1.difference(s2) # s1 과 s2의 차집합
# {1, 2}
>>> s1 - s2 # set([1, 2])
# {1, 2}
```
