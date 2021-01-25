---
title: "[부스트캠프 AI Tech / Day4] 파이썬 Class"
date: 2020-01-21 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python] # Python
tags: [Python] # CS, 운영체제, Python
---


## **[DAY 4] Class**

---

### **클래스와 객체**

- **객체지향프로그래밍** (Object-Oriented Programming, OOP)
  - 각각의 *주체*를 선정하여 그들이 하는 *행동*과 *데이터 구조*를 중심으로 프로그램 작성 후, 연결
  - 만들어 놓은 코드를 재사용
  - **객체**: 실생활에서 일종의 물건 *속성(Attribute)*와 *행동(Action)*을 가짐
  - OOP는 이러한 객체(list, integer...) 개념을 프로그램으로 표현
  - 속성은 **변수(variable)**, 행동은 **함수(method)**로 표현됨
  - 파이썬 역시 객체 지향 프로그램 언어
  - 예시
    - 인공지능 축구 프로그램을 작성한다고 가정
    - 객체 종류: 팀, 선수, 심판, 공
    - Action
      - 선수 – 공을 차다, 패스하다.
      - 심판 – 휘슬을 불다, 경고를 주다.
    - Attribute
      - 선수 – 선수 이름, 포지션, 소속팀
      - 팀 – 팀 이름, 팀 연고지, 팀소속 선수
  - OOP는 설계도에 해당하는 클래스(class)와 실제 구현체인 인스턴스(instance)로 나눔
    - 붕어빵 예시, 붕어빵 틀(클래스), 붕어빵(인스턴스, 객체, 실제로 사용하는 것)
    - 기본 붕어빵(객체)에 다양한 앙금(기능)을 더 추가하여 커스텀 할 수 있음 ~~배고파~~

---

### **class 구현하기**

- 축구 선수 정보를 Class로 구현하기
rr
```python
  class SoccerPlayer(object):
    def __init__(self, name, position, back_number):
      self.name = name
      self.position = position
      self.back_number = back_number
    def change_back_number(self, new_number):
      print("선수의 등번호를 변경합니다 : From %d to %d" % (self.back_number, new_number))
      self.back_number = new_number

  jinhyun = SoccerPlayer("Jinhyun", "MF", 10)
  print("현재 선수의 등번호는 :", jinhyun.back_number)
  jinhyun.change_back_number(5)
  print("현재 선수의 등번호는 :", jinhyun.back_number)
```

#### **1. 클래스 선언하기**

- class 선언, object는 python3에서 자동 상속
  - `class SoccerPlayer(object):`
  - `class 예약어` `class 이름` (`상속받는 객체명`)
  - 함수 선언과 비슷
  - class naming은 *CamelCase naming rule* 적용
  > Python naming rule  
      - Objects in Python  
        - 변수와 Class명 함수명은 짓는 방식이 존재  
        - snake_case  
          - 띄워쓰기 부분에 "_" 를 추가  
          - 뱀 처럼 늘여쓰기, 파이썬 함수/변수명에 사용  
        - CamelCase  
          - 띄워쓰기 부분에 대문자  
          - 낙타의 등 모양, 파이썬 Class명에 사용  

    ```python
    class SoccerPlayer(object): # Object 클래스 상속
        pass

    a = SoccerPlayer(x, y, z)
    b = SoccerPlayer(x, y, z)
    # 같은 클래스에서 파생된 세개의 객체
    # 이들은 다른 객체이며, 메모리 주소도 다름

    >>> a is b
    # False

    # c = SoccerPlayer() # 오류 # init의 인자로 주어지는 값인 parameter가 없음
    ```

#### **2. Attribute 추가하기**

- Attribute 추가는 `__init___` , `self`와 함께함
  - `__init__`은 객체 초기화 예약 함수
  - `self.`으로 객체의 정보 선언할 수 있음

  ```python
  # class SoccerPlayer( ): # 자동상속
  class SoccerPlayer(object):
    def __init__(self, name, position, back_number): # 객체 초기화
      self.name = name # self 내부의 name에 parameter로 받은 name의 값을 넣음(할당)
      self.position = position
      self.back_number = back_number

  ```

  - **magic method**
    - `__`는 특수한 예약 함수나 변수 그리고 함수명 변경(맨글링)으로 사용
    - 기존의 함수를 조금 바꿔서 사용하는 것
    - 예) __main__ , __add__ , __str__ , __eq__
      - `__str__` : 함수 선언 시, print문 사용하면, 지정한 형식의 문자열을 return
      - `__add__` : 함수 선언 시, + operation 사용하면, 인자로 받은 것을 더한 것을 반환

    ```python
    class SoccerPlayer(object):
      def __str__(self):
        return "Hello, My name is %s. I play in %s in center " % (self.name, self.position)
        # print(objA)
      def __add__(self, other):
        return self.name + other.name
        # >> objA + objB

    park = SoccerPlayer("Park" , "MF", 13)
    jinhyun = SoccerPlayer("Jinhyun" , "MF", 10)
    print(jinhyun)
    # Hello, My name is Jinhyun. I play in MF in center 10
    # __str__ 함수 없으면, 객체의 메모리 주소가 찍힘

    >>> jinhyun + park
    # JinhyunPark
    ```

#### **3. Method 구현하기**

- method(Action) 추가는 기존 함수와 같으나, 반드시 self를 추가해야만 class 함수로 인정됨
- `def func(self, a, b, c):`
- `def 예약어` `함수이름` (`self`, `parameter`)

  ```python
  class SoccerPlayer(object):
    def change_back_number(self, new_number):
      print("선수의 등번호를 변경합니다 :
            From %d to %d" % \
            (self.back_number, new_number))
      self.back_number = new_number
  ```

#### **4. objects(instance) 사용하기**

- Object 이름 선언과 함께 초기값 입력 하기
  - `self`: 생성된 인트턴스 자신
    - class 내에서 부르는 자신(객체): `self`
    - class 외부에서 부르는 이름: `객체이름`
  - `def __init__(self, name, position, back_number):`
  - `def __init__(self, name : str, position : str, back_number : int):`
    - 인자에 대한 힌트 제공
- `객체명` = `클래스 명`(`__init__함수 interface`, `초기값`)
  - `jinhyun = SoccerPlayer("Jinhyun", "MF", 10)`

  ```python
  class SoccerPlayer(object):
    # ........
    jinhyun = SoccerPlayer("Jinhyun", "MF", 10)
    print("현재 선수의 등번호는 :", jinhyun.back_number)

    jinhyun.change_back_number(5)
    print("현재 선수의 등번호는 :", jinhyun.back_number)

    jinhyun.back_number = 5 # 가능하지만, 권장하지 않음
  ```

---

- 예제
  - Note class

  ```python
  class Note(object):
    def __init__(self, content = None):
      self.content = content
    def write_content(self, content):
      self.content = content
    def remove_all(self):
      self.content = ""
    def __add__(self, other):
      return self.content + other.content
    def __str__(self):
      return self.content
  ```

  - NoteBook class

  ```python
  class NoteBook(object):
    def __init__(self, title):
      self.title = title
      self.page_number = 1
      self.notes = {}
    def add_note(self, note, page = 0):
      if self.page_number < 300:
        if page == 0:
          self.notes[self.page_number] = note
          self.page_number += 1
        else:
          self.notes = {page : note}
          self.page_number += 1
      else:
        print("Page가 모두 채워졌습니다.")
    def remove_note(self, page_number):
      if page_number in self.notes.keys():
        return self.notes.pop(page_number)
      else:
        print("해당 페이지는 존재하지 않습니다")
    def get_number_of_pages(self):
      return len(self.notes.keys())
  ```

  - source code

  ```python
    from 파일명 import note
    from 파일명 import NoteBook

    my_notebook = NoteBook("팀랩 강의노트")
    >>> my_notebook.title
    # '팀랩 강의노트'

    new_note = Note('아 수업하기 싫다')
    print(new_note)
    # 노트에 적힌 내용입니다.: 아 수업하기 싫다
    >>> new_note
    # 메모리 주소 나옴 # print안에 넣어야 __str__ 사용가능

    new_note_2 = Note('파이썬 강의')
    my_notebook.add_note(new_note) # 맨 뒤에 추가
    my_notebook.add_note(new_note_2, 100) # 지정된 위치에 추가

    print(my_notebook.notes[100])
    # 노트에 적힌 내용입니다.: 아 수업하기 싫다
    my_notebook.get_number_of_pages()
    # 2
    print(my_notebook.notes[3])
    # 오류!
  ```