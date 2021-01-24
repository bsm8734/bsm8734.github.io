# Day4

파이썬 기초 문법

## Python Object Oriented Programming

### 클래스와 객체

- 객체지향프로그래밍(Object-Oriented Programming, OOP)
  - 각각의 *주체*를 선정하여 그들이 하는 *행동*과 *데이터 구조*를 중심으로 프로그램 작성 후, 연결
  - 만들어 놓은 코드를 재사용
  - 객체: 실생활에서 일종의 물건 *속성(Attribute)*와 *행동(Action)*을 가짐
  - OOP는 이러한 객체(list, integer...) 개념을 프로그램으로 표현
  - 속성은 변수(variable), 행동은 함수(method)로 표현됨
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
    - 기본 붕어빵(객체)에 다양한 앙금(기능)을 더 추가하여 커스텀 할 수 있음
---

- class 구현하기
  - 축구 선수 정보를 Class로 구현하기

  ```Python
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

  1. 클래스 선언하기
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

#### 1. Attribute 추가하기

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

  - magic method
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

#### 2. Method 구현하기

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

#### 3. objects(instance) 사용하기

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

- 예제
  - Note class

  ```Python
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

  ```Python
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

### 객체지향언어의 특징

- 실제 세상을 모델링
- Inheritance(상속)
- Polymorphism(다형성)
- Visibility(Hidden class, 가시성)

#### Inheritance(상속)

- 부모클래스로 부터 속성과 Method를 물려받은 자식 클래스를 생성 하는 것
- `super`: 자신의 부모 클래스
- `self`: 자기자신(클래스,객체)

```python
class Person(object):
  def __init__(self, name, age):
    self.name = name
    self.age = age

  class Korean(Person): # 상속을 받았기 때문에, Person 내부의 속성을 사용가능
    pass

  first_korean = Korean("Sungchul", 35)
  print(first_korean.name)
```

- inheritance example

  ```python
  # class Person: # 이렇게 써도 됨
  # 따로 상속받지 않은 클래스는 자동으로 Object class를 상속받음
  class Person(object): # 부모 클래스 Person 선언
    def __init__(self, name, age, gender):
      self.name = name
      self.age = age
      self.gender = gender
    def about_me(self): # Method 선언
      print("저의 이름은 ", self.name, "이구요, 제 나이는 ", str(self.age), "살 입니다.")

  class Employee(Person): # 부모 클래스 Person으로 부터 상속
    def __init__(self, name, age, gender, salary, hire_date):
      super().__init__(name, age, gender) # 부모객체 사용
      self.salary = salary
      self.hire_date = hire_date # 속성값 추가
    def do_work(self): # 새로운 메서드 추가
      print("열심히 일을 합니다.")
    def about_me(self): # 부모 클래스 함수 재정의
      super().about_me() # 부모 클래스 함수 사용
      print("제 급여는 ", self.salary, "원 이구요, 제 입사일은 ", self.hire_date,
    " 입니다.")
  ```

#### Polymorphism(다형성)

- 같은 이름 메소드의 내부 로직을 다르게 작성
- Dynamic Typing 특성으로 인해 파이썬에서는 같은 부모클래스의 상속에서 주로 발생함
- 같은 일을 하지만, 세부 구현이 다른 경우
- 같은 이름, 다른 역할
- 같은 이름을 쓰되, 각각의 목적에 따라 다르게 구현하는 것

```python
class Animal:
  def __init__(self, name): # Constructor of the class
    self.name = name
  def talk(self): # Abstract method, defined by convention only
    raise NotImplementedError("Subclass must implement abstract method")

class Cat(Animal):
  def talk(self):
    return 'Meow!'

class Dog(Animal):
  def talk(self):
    return 'Woof! Woof!'

animals = [Cat('Missy'), Cat('Mr. Mistoffelees'), Dog('Lassie')]
for animal in animals:
  print(animal.name + ': ' + animal.talk())
```

#### Visibility(가시성)

- 객체의 정보를 볼 수 있는 레벨을 조절하는 것
- 누구나 객체 안에 모든 변수를 볼 필요가 없음
  - 1) 객체를 사용하는 사용자가 임의로 정보 수정
  - 2) 필요 없는 정보에는 접근 할 필요가 없음
  - 3) 만약 제품으로 판매한다면? 소스의 보호
- Encapsulation (비슷한 용어)  
  - 캡슐화 또는 정보 은닉(Information Hiding)  
  - Class를 설계할 때, 클래스 간 간섭/정보공유의 최소화  
  - 심판 클래스가 축구선수 클래스 가족 정보를 알아야 하나?  
  - 캡슐을 던지듯, 인터페이스만 알아서 써야함  
  - 사용법만 알고있다면 내 코드를 누구나 마음대로 쓸 수 있음
- Visibility Example 1
  - Product 객체를 Inventory 객체에 추가
  - Inventory에는 오직 Product 객체만 들어감
  - Inventory에 Product가 몇 개인지 확인이 필요
  - Inventory에 Product items는 **직접 접근이 불가**

  ```python
    class Product(object):
      pass

    class Inventory(object):
      def __init__(self):
        self.__items = [] # private 변수로 선언, 타 객체가 변수에 접근하지 못함
      def add_new_item(self, product):
        if type(product) == Product: # Product 클래스 타입인지 확인
          self.__items.append(product)  # 리스트에 추가
          print("new item added")
        else:
          raise ValueError("Invalid Item")
      def get_number_of_items(self):
        return len(self.__items)

    my_inventory = Inventory()
    my_inventory.add_new_item(Product())
    my_inventory.add_new_item(Product())  # 가능

    # self.items = []
    my_inventory.items.append("abc")      # 가능
    data = my_inventory.items             # 가능

    # self.__items = []
    # 직접 접근, 수정 불가능
    my_inventory.__items.append("abc")      # 불가능
    data = my_inventory.__items             # 불가능

    print(my_inventory.get_number_of_items())
    print(my_inventory.__items)
    my_inventory.add_new_item(object)
  ```

- Visibility Example 2
  - Product 객체를 Inventory 객체에 추가
  - Inventory에는 오직 Product 객체만 들어감
  - Inventory에 Product가 몇 개인지 확인이 필요
  - Inventory에 Product items **접근 허용**

  ```python
  class Inventory(object):
    def __init__(self):
      self.__items = []
    @property # property decorator: 숨겨진 변수를 반환하게 해줌
    def items(self):
      return self.__items
    # 함수명을 변수명으로 쓸 수 있게 해줌
    # 데이터 복사 없이, 객체 내부 변수를 바로 반환하면, 내부 변수까지 수정하는 경우 있을 수 있음
    # 데이터를 복사하여 리턴하는 경우가 많음

    my_inventory = Inventory()
    my_inventory.add_new_item(Product())
    my_inventory.add_new_item(Product())
    print(my_inventory.get_number_of_items())

    items = my_inventory.__items      # 불가능
    items = my_inventory.items        # 가능(내부 접근 가능, 내부에서 접근하여(함수로) 반환 가능)
    my_inventory.items.append("abc")  # 가능
    # 값을 바꿔버릴 수 있기 때문에 아래와 같이 데이터를 복사한 후, 리턴하게 됨
    """
    @property
    def items(self):
      ret = self.__items[:]
      return ret
    """

    items.append(Product())
    print(my_inventory.get_number_of_items())
  ```

#### decorate

- first-class objects(1급 함수)
- inner function
- decorator

##### First-class objects

- 일등함수 또는 일급객체
- 변수나 데이터 구조에 할당이 가능한 객체(객체를 변수에 할당)
- 파라미터로 전달이 가능 + 리턴값으로 사용 가능
- 파이썬의 함수는 일급함수
- ex) `map(f, ex)`

```python
def square(x):
  return x * x
f = square # 함수를 변수로 사용
f(5)

##################################
def square(x):
  return x * x
def cube(x):
  return x*x*x
def formula(method, argument_list): # 함수를 파라메터로 사용
  return [method(value) for value in argument_list]

# 두개의 formula를 만드는 것보다, 하나의 formula가 다른 메소드를 활용할 수 있게 함
# 장점: 구조화 체계를 만들어 줌
# 단점: 이해하기 어려움
# formula(square, ~)
# formula(cube, ~)
```

##### Inner function

- 함수 내에 또 다른 함수가 존재

  ```python
  def print_msg(msg):
    def printer():
      print(msg)
    printer()

  print_msg("Hello, Python")
  ```

- closures : inner function을 return값으로 반환

  ```python
  def print_msg(msg):
    def printer():
     print(msg)
    return printer  # inner class return # 함수를 리턴
  another = print_msg("Hello, Python") # another은 함수!
  another()
  ```

  - 예시(closure example)

    ```python
      def tag_func(tag, text):
        text = text
        tag = tag
        def inner_func():
          return '<{0}>{1}<{0}>'.format(tag, text)
        return inner_func

      h1_func = tag_func('title', "This is Python Class")
      p_func = tag_func('p', "Data Academy")
      # 비슷한 목적을 가지는 다양한 함수 생성 가능
    ```

- Decorator function
  - 복잡한 클로져 함수를 간단하게

  ``` python
  def star(func):
    def inner(*args, **kwargs):
      print("*" * 30)
      func(*args, **kwargs)
      print("*" * 30)
    return inner

  @star               # star라는 이름의 func에
  def printer(msg):   # 인자로 들어감
    print(msg)

  printer("Hello")
  """
  ******************************
  Hello
  ******************************
  """
  printer("Hello", "&")
  """
  &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
  Hello
  &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
  """
  ```

  ```python
  def star(func):
    def inner(*args, **kwargs):
      print("*" * 30)
      func(*args, **kwargs)
      print("*" * 30)
    return inner

  def percent(func):
    def inner(*args, **kwargs):
      print("%" * 30)
      func(*args, **kwargs)
      print("%" * 30)
    return inner

  @star
  @percent
  def printer(msg):
    print(msg)
  printer("Hello")

  """
  ******************************
  &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
  Hello
  &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
  ******************************
  """
  ```

  ```python
  def generate_power(exponent): # 2
    def wrapper(f): # f = raise_two
      def inner(*args): # n
        result = f(*args)
        print(result) # 49
        return exponent**result
      return inner
    return wrapper

  @generate_power(2)
  def raise_two(n):
    return n**2

  print(raise_two(7))
  # 562949953421312 (= 2**49)
  ```

## Module and Project

- 공개된 코드들의 공통적인 형식은 모듈로 이루어져 있다는 것
- 모듈과 프로젝트로 이루어진 *라이브러리*를 불러와서 쓸 수 있는 기능이 매우 강력
- 남이 만든 프로그램을 쓰는 법: 객체 < 모듈
- 객체가 모듈안에 들어가있음, 모듈은 프로젝트 안에 들어가있음

### 모듈과 패키지

- 모듈은 패키지 안에 들어가있음
- 모듈: 어떤 대상의 부분 혹은 조각
- 패키지: 모듈을 모아놓은 단위, 하나의 프로그램
- 프로젝트: 패키지를 공개한 것
- 모듈
  - 프로그램에서는 작은 프로그램 조각들, 모듈들을 모아서 하나의 큰 프로그램을 개발함
  - 프로그램을 모듈화 시키면 다른 프로그램이 사용하기 쉬움
  - 남들이 만든 프로젝트를 단위로 가져와 사용하는 경우,
    - "모듈화 된 프로그램을 가져와 사용했다. API를 사용한다."
  - Python 내부의 모듈
    - Built-in Module인 Random을 사용, 난수를 쉽게 생성할 수 있음

### 모듈

- 파이썬의 Module == py 파일을 의미
- **같은 폴더/디렉토리**에 Module에 해당하는 .py 파일과, 사용하는 .py을 저장한 후
- import 문을 사용해서 module을 호출(로딩)

```python
#########################################
# fah_converter.py
def covert_c_to_f(celcius_value):
  return celcius_value * 9.0 / 5 + 32

#########################################3
# module_ex.py
import fah_converter # 불러오기, 로딩
# 모든 코드가 메모리로 로딩이 됨
# 접근하기 위해서 (모듈이름).(함수명) => 작동!

print ("Enter a celsius value: "),
celsius = float(input())
fahrenheit = fah_converter.covert_c_to_f(celsius)
# 함수명으로 접근해서 쓸 수 있음
print ("That's ", fahrenheit, " degrees Fahrenheit")
##########################################
```

#### namespace

- 모듈을 호출할 때 범위 정하는 방법
- 모듈 안에는 함수와 클래스 등이 존재 가능
- 필요한 내용만 골라서 호출 할 수 있음
- from 과 import 키워드를 사용함
- namespace example

  – 모듈명을 별칭으로 써서 (Alias 설정하기)

    ```python
    import fah_converter as fah # fah_converter를 fah라는 이름으로 그 안에 covert_c_to_f 함수를 쓰겠다
    print(fah.covert_c_to_f(41.6))
    ```

  - 모듈에서 특정 함수 또는 클래스만 호출하기

    ```python
    from fah_converter
    #이렇게만 호출하면 fah_converter.py 내의 모든 내용이 메모리에 로딩

    from fah_converter import covert_c_to_f
    print(covert_c_to_f(41.6)) # covert_c_to_f 함수만 호출함
    # 필요한 내용만 불러오기 위해서 namespace 사용
    ```

  - 모듈에서 모든 함수 또는 클래스를 호출하기

    ```python
    from fah_converter import *
    print(covert_c_to_f(41.6)) # 전체 호출
    ```

  - `__pycache__/fah_converter.cpython-38.pyc` 폴더가 새로 생김
  - `.pyc` : 컴파일 된 파일
    - python 인터프리터가 해석/컴파일
    - 뒷단에서 돌아가고 있는 프로그램이 파이썬을 쉽게 호출하기 위해 기계어로 번역해서 pycache에 저장
    - 내 폴더를 빠르게 메모리에 로딩하기 위해서 컴파일한 것을 저장
    - 캐시가 생성되면, 자동완성 기능 사용가능

#### Built-in Modules

- 파이썬이 기본 제공하는 라이브러리
- 문자처리, 웹, 수학 등 다양한 모듈이 제공됨
- 별다른 조치없이 import 문으로 활용 가능
- 수 많은 파이썬 모듈은 어떻게 검색할 것인가?
  - 1) 구글신에게 물어보기
  - 2) 모듈을 import후 구글 검색 또는 Help 쓰기
  - 3) [공식 문서](https://docs.python.org/3/library/)를 읽어보기

```python
  """1 부터 100까지 특정 난수를 뽑기"""
  #난수
  import random
  print (random.randint (0,100)) # 0~100사이의 정수 난수를 생성
  print (random.random()) # 일반적인 난수 생성

  #시간
  import time
  print(time.localtime()) # 현재 시간 출력

  #웹
  import urllib.request
  response = urllib.request.urlopen("http://thetemlab.io")
  print(response.read())
```

### 패키지

- 하나의 대형 프로젝트를 만드는 코드의 묶음
- 다양한 모듈들의 합, 폴더로 연결됨
- `__init__` , `__main__` 등 키워드 파일명이 사용됨
- 다양한 오픈소스들이 모두 패키지로 관리됨
- Package 만들기
  - 1) 기능들을 세부적으로 나눠 폴더로 만듦
  - 2) 각 폴더별로 필요한 모듈을 구현함
  - 3) 1차 Test –python shel
  - 4) *폴더별로* `__init__.py` 구성하기
    - 현재 폴더가 패키지임을 알리는 초기화 스크립트
    - 없을 경우 패키지로 간주하지 않음 (3.3+ 부터는 X)
    - 하위 폴더와 py 파일(모듈)을 모두 포함함
    - 폴더로 이루어져 있더라도, 이를 모듈처럼 다룰 수 있음
      - 어떤 폴더 안에 있다면, from으로 부를 수 있음
    - import와 `__all__` keyword 사용
      - 최상위 폴더에 위치하는 `__init__.py`는 `` 이런 식으로

      ```python
        __all__= ['image', 'stage', 'sound'] # 폴더명을 나열해줌

        from . import image
        from . import stage
        from . import sound
      ```

      - linux, `touch __init__.py`로 파일 생성 가능
      - windows, copy con?
  - 5) __main__.py 파일만들기
    - 보통 파이썬 패키지를 프로젝트로서 공개하게 되면, 폴더 자체를 실행 가능
    - 폴더 실행을 위해서 main필요
    - 다른 폴더에 존재하는 여러 모듈들을 한번에 폴더에 묶어서 처리: 패키지
    - 이를 공유하는 것이 프로젝트

    ```python
      from stage.main import game_start
      from stage.sub import set_stage_level
      from image.character import show_character
      from sound.bgm import bgm_play

      if __name__ == '__main__':
        print('hello game')
        game_start()
        set_stage_level(5)
        bgm_play(10)
        show_character()
    ```

  - 6) 실행하기 – 패키지 이름만으로 호출하기

- package namespace
  - Package 내에서 다른 폴더의 모듈을 부를때 상대참조로 호출하는 방법

  ```python
  # 현재 : game/
  # >>> ls
  # __init__.py
  # sound/: __init__.py, bgm.py, echo.py
  # image/: __init__.py, character.py, object.py  
  # stage/: __init__.py, main.py, sub.py

  from game.graphic.render import render_test   # 절대참조
  from .render import render_test               # .   현재디렉토리기
  from ..sound.echo import echo_test            # .. 부모 디렉토리 기준
  ```

### 가상환경 (Virtual Environment)

- 오픈소스 라이브러리 사용하기
- 각 프로젝트에 맞춰서 환경을 새로 설정할 수 있음
- 프로젝트 진행 시 필요한 패키지만 설치하는 환경
- 기본 인터프리터 + 프로젝트 종류별 패키지 설치
  - ex) 웹 프로젝트, 데이터 분석 프로젝트
- 각각 패키지 관리할 수 있는 기능
- 다양한 패키지 관리 도구를 사용함
- 대표적인 도구 virtualenv와 conda가 있음
- **virtualenv** vs **conda**
  - virtualenv + pip conda
    - 가장 대표적인 가상환경 관리 도구
    - 레퍼런스+패키지 개수
    - pip로 설치, 유용
    - compile된 코드가 들어가있지 않은 경우 있음

  - conda
    - 상용 가상환경도구
    - miniconda 기본 도구
    - 설치의 용이성
    - Windows에서 장점
    - 컴파일 된 도구 존재(C기반의 python에 유리)

#### Anaconda

##### conda 명령어

- 가상환경 생성
  - `conda create -n my_project python=3.8`
  - `conda create -n (가상환경이름) python=(파이썬버전)`
- 가상환경 호출
  - `conda activate my_project`
  - `conda activate (가상환경이름)`
- 가상환경해제
  - `conda deactivate`
- 패키지 설치
  - `conda install matplotlib`
  - `conda install <패키지명>`
  - <패키지명>: 설치하고자 하는 패키지명 입력
- `conda` vs `pip`
  - Windows에서는 `conda`
    - Windows에서는 컴파일된C 라이브러리 설치 필요
    - conda는 컴파일된 c 라이브러리 파일을 자동으로 설치한다는 장점이 존재
  - linux, mac에서는 `conda or pip`
- `matplotlib`
  - matplotlib 활용한 그래프 표시
  - 대표적인 파이썬 그래프 관리 패키지
  - 엑셀과 같은 그래프들을 화면에 표시함
  - 다양한 데이터 분석 도구들과 함께 사용됨
- `tqdm`
  - 프로그램 돌릴때, 내가 지금 어떤 상태에 있는지 확인 필요
  - 긴 반복문 수행시 용이
  - 특히 대용량 데이터
  - 확인할 수 있는 코드 돌리는 게 유리

```
  conda install matplotlib
  conda install tqdm
```
```python
  # matplotlib
  import matplotlib.pyplot as plt
  plt.plot([1,2,3,4])
  plt.ylabel('some numbers')
  plt.show()
```
```python
  # tqdm
  from tqdm import tqdm
  import time
  for i in tqdm(range(100000)):
    if i % 1000 == 0:
      time.sleep(1)
```

---

## 피어세션 정리

- 팀원들과 과제 리뷰함
  - string 라이브러리(자주 사용하는 string을 호출하여 사용가능)
  - 내장함수 사용법 숙지하기
  - zip, lambda와 기타 Day3에서 배웠던 내용을 활용하면 코드를 간결하게 만들 수 있음
  - set을 사용하면 중복검사 용이(입력값과 출력값이 원소 수 비교)
  - python 예약어를 변수명으로 사용하지 않기
  - flag를 사용하여 while문을 빠져나갈 수 있게 하는 방법이 있음 `while (flag):`

---

## 과제 진행 상황 정리/과제 결과물에 대한 정리

- 아직도 학습정리 공간 못정함 -> 이번주 내로 꼭 정할것!
- 과제는 하는 중...
- 과제 현황
  - [ ] morsecode

---

## 오늘의 한마디

- 점심먹고 비몽사몽 금지
