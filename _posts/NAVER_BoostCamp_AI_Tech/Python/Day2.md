# Day2
파이썬 기초 문법

## Variables
- 변수
  - 가장 기초적인 프로그래밍 문법 개념
  - 데이터(값)을 저장하기 위한 메모리 공간(장소)
  - 변수는 메모리 주소를 가지고 있고 변수에 들어가는 값은 메모리 주소에 할당됨
  - 선언되는 순간 메모리 특정영역에 물리적인 공간에 할당됨
- 변수 이름 작명법
  - 알파벳, 숫자, 언더스코어(_)로 선언가능
  - 변수명은 의미있는 단어로 표기하기
  - 변수명은 대소문자가 구분하기
  - 특별한 의미가 있는 예약어는 쓰지않기(for, if, in, ...)
- Basic Operation
  1. 기본자료형(primitive data type)
    - data type: 파이썬이 처리할 수 있는 데이터 유형
    - 자료형의 종류
      - 수치자료형
        - 정수형: integer(32bit)
        - 실수형: float(64bit)
      - 문자형(문자형): string
      - 논리/불린 자료형: boolean
    - 각각의 자료형이 차지하는 공간이 다름
    - Dynamic Typing: 코드 실행시점에 데이터의 Type을 결정하는 방법
      - 실행시점에 인터프리터가 변수형 확인
      - 실행하는 시점에 메모리를 어떻게 할당해야할지 결정하므로 타 언어보다 느림
      - 변수형을 명시하지 않아도 되기 때문에 사용하기 용이함
      - 대부분의 언어들/컴파일러 언어들은 이를 지원하지 않으므로, 항상 변수형을 명시해야 함
    - 변수선언 및 타입확인
      - `type(var)`: 데이터의 타입을 알 수 있음
      - `a = 3`: integer
      - `a = 3.0`: float
      - `a = "3"`: string
      - `a = false`: boolean
  2. 연산자와피연산자
    - `+ , -, * , /` 같은기호들을연산자라고칭함
    - 연산자에 의해 계산이 되는 숫자들은 피연산자라 칭함
    - 수식에서 연산자의 역할은 수학에서 연산자와 동일
    - 연산의 순서는 수학에서 연산순서와 같음
    - 문자간에도 `+` 연산이 가능함(= concatenate)
    - 연산자 사용
      - `**`는 제곱승 계산 연산자
        - `5 ** 3` (= 125)
      - `/`는 나눗셈을 구하는 연산자
        - int가 float로 자동 변환
        - `10 / 2` (= 5.0)
      - `%`는 나머지를 구하는 연산자
      - 증가/감소 연산
        - `a = a + 1` = `a += 1`
        - `a = a - 1` = `a -= 1`
        - `a++`은 사용할 수 없음!
        - 변수는 좌변에 있을 때와 우변에 있을 때의 의미가 다름
          - 좌변의 경우, 저장되는공간
          - 우변의 경우, 메모리에서 읽어오는 값을 의미
  3. 데이터 형변환
    - 형변환하고 나서, 다시 변수에 담아주어야 실제 값이 바뀌게 됨
      ```python
      >>> a = 5
      >>> type(5)       # <class 'int'>
      >>> float(a)      # 5.0
      >>> a             # 5
      >>> a = float(a)  # 5.0
      >>> a             # 5.0
      ```
    - 실수형에서 정수형으로 형 변환 시 소수점 이하는 *내림*
    - 문자열과 숫자 사이에도 *변환* 가능 (*계산은 불가능*)
    - 문자와 숫자를 더하려고 시도하면 concatenate 오류!
    - 문자와 문자, 숫자와 숫자는 서로 더할 수 있음
      ```python
      >>> a = '76.3'
      >>> b = float(a)  # a를 실수형으로 형 변환 후 b에 할당
      >>> print (a)     # 76.3
      >>> print (b)     # 76.3
      >>> print (a + b) # 오류
        # Traceback (most recent call last):
        # File "<stdin>", line 1, in <module>
        # TypeError: cannot concatenate 'str' and 'float' objects
      ```
- List/Array
  - 시퀀스 자료형, 여러 데이터들의 집합(데이터 구조)
  - int, float 같은 다양한 데이터 타입 포함
  - 많은 데이터를 효율적으로 관리할 수 있음
  - list의 특징
    - 인덱싱 indexing
      - list에 있는 값들은 주소(offset)를 가짐
      - 주소를 사용해 할당된 값을 호출(주소를 사용하여 element 접근)
      - `len(배열)`: 배열의 길이 리턴
      ```python
      colors = ['red', 'blue', 'green']
      print (colors[0]) # red
      print (colors[2]) # green
      print (len(colors)) # 3
      # len은 list의 길이를 반환
      ```
    - 슬라이싱 slicing
      - list의 값들을 잘라서 쓰는 것이 슬라이싱
      - list의 주소 값을 기반으로 부분 값을 반환
      - 보통 시작하는 값을 포함하여 시작해서, 끝 값을 포함하지 않음
      ```python
      cities = ['서울', '부산', '인천', '대구', '대전', '광주', '울산', '수원']
      print (cities[0:6])       # a번수의 0부터 5까지
      print(a[-9:])             # -9부터 끝까지
      print (cities[:])         # a변수의 처음부터 끝까지
      print (cities[-50:50])    # 범위를 넘어갈 경우 자동으로 최대 범위를 지정
      print (cities[::2])       # 2칸 단위로
      print(a[::-1])            # 역순으로
      ```
    - 리스트 연산
      - concatenation, is_in, 연산 함수들
      - 추가/삭제
        - append, extend, insert, remove, del 등 활용
      ```python
      # 슬라이싱과 추가/삭제 연산
      >>> color = ['red', 'blue', 'green']
      >>> color2 = ['orange', 'black', 'white']
      >>> print (color + color2)            # 두 리스트 합치기 # 아직 합쳐지지 않았음
      >>> len(color)                        # 리스트 길이
      >>> color[0] = 'yellow'               # 0번째 리스트의 값을 변경
      >>> print (color * 2)                 # color 리스트 2회 반복
      >>> 'blue' in color2                  # 문자열 ‘blue‘가 color2 존재 여부 반환
      >>> total_color = color + color2      # concatenate는 저장까지 해줘야함
      >>> color.append("white")             # 리스트에 “white” 추가       / 변화 O
      >>> color.extend(["black","purple"])  # 리스트에 새로운 리스트 추가 / 변화 O
      >>> color.insert(0,"orange")          # 0번째 주소에 “orange” 추가
      >>> print (color)
      # ['orange', 'yellow', 'blue', 'green', 'white', 'black', 'purple']
      >>> color.remove("white")             # 리스트에 “white” 삭제       / 변화 O
      >>> del color[0]                      # 0번째 주소 리스트 객체 삭제 / 변화 O (메모리를 날림)
      >>> print (color * 2)
      # ['yellow', 'blue', 'green', 'black', 'purple', 'yellow', 'blue', 'green', 'black', 'purple']
      ```
    - 메모리 저장 방식
      - 파이썬은 해당 리스트 변수에는 리스트 주소값이 저장됨
      - `a = b`라고 선언하는 순간 두 변수는 같은 주소값을 저장하므로, 값을 변화시켰다면, 두 변수에 변화한 내용이 적용됨
      - `b = a[:]`라고 선언해야 값을 복사함
      ```Python
      >>> a = [5, 4, 3, 2, 1]
      >>> b = [1, 2, 3, 4, 5]
      >>> b = a       # a와 b가 같은 주소를 가리킴
      >>> print (b)
      # [5, 4, 3, 2, 1]
      >>> sorted(a)   # 스스로 변화하지않음    # [5, 4, 3, 2, 1]
      >>> a.sort()    # 스스로 변화하는 함수   # [1, 2, 3, 4, 5]
      >>> print (b)
      # [1, 2, 3, 4, 5]
      >>> b = [6,7,8,9,10]
      >>> print (a, b)
      # [1, 2, 3, 4, 5] [6, 7, 8, 9, 10]
      ###############################################################
      # 데이터(값)을 복사하여 가져오는 것(두 변수가 메모리를 따로 사용)
      b = a[:]
      ```
    - 패킹과 언패킹
      - 패킹 : 한 변수에 여러 개의 데이터를 넣는 것
        - `t = [1, 2, 3]`
      - 언패킹 : 한 변수의 데이터를 각각의 변수로 반환
        - `a, b, c = t`
      ```python
      t = [1, 2, 3]
      a, b, c = t
      >>> print(t, a, b, c) # [1, 2, 3] 1 2 3
      ```
    - 이차원 리스트
      - 리스트 안에 리스트를 만들어 행렬(Matrix) 생성
      - 이차원 리스트의 *복사*
        - 이차원 리스트의 경우, `a = b[:]` 불가능
        - `import copy`
        - `copy.deepcopy(변수)`
      ```Python
      >>> kor_score = [49,79,20,100,80]
      >>> math_score = [43,59,85,30, 90]
      >>> eng_score = [49,79,48,60,100]
      >>> midterm_score = [kor_score, math_score, eng_score]
      >>> print (midterm_score[0][2]) # 20
      >>> copy.deepcopy(midterm_score) # 이차원 배열 복사
      ```
    - Python 리스트만의 특징
      - 다양한 Data Type이 하나에 List에 들어감

## Function and Console I/O
- function(함수)
  - 어떤 일을 수행하는 코드의 덩어리
  - 함수를 1회 작성 후 호출함으로서, 반복적인 수행을 용이하게 함
  - 코드를 논리적인 단위로 분리
  - 캡슐화: 인터페이스만 알면 타인의 코드 사용
  ```Python
  def func(x , y):
      return x * y
  ```
- 함수 선언 문법
  - 함수이름, parameter, indentation,return value(optional)
  ```Python
  def 함수_이름 (parmaeter1,…,): # def name(input):
    수행문 #1(statements)        # 앞 indentation 필요
    수행문 #2(statements)
    return <반환값>
  ```
- 함수 수행 순서
  - 함수 부분을 제외한 메인프로그램부터 시작 *(1) main -> func call*
  - 함수 호출시 함수 부분을 수행 후 되돌아옴 *(2) main <- return func*
- parameter vs argument
  - parameter: 함수의 입력 값 인터페이스
    - 함수 선언시 input을 지칭하는 것
    - def func(**x, y**)
  - argument: 실제 parameter에 대입된 값
    - 함수를 호출할 때 input에 넣어주는 값
    - func(**x, y**)
- 함수 형태
  - parameter 유무, 반환 값(return value) 유무에 따라 함수의 형태가 다름
  - 함수의 반환값이 필요한지, 필요하지 않은지 따져봐야함
  - 반환값이 있는지 없는지에 따라 변수 업데이트 여부 나뉠 수 있음
  - 보통 리턴값이 있는 경우, 변수 업데이트 필요
  ```Python
  >>> sorted(a)   # 스스로 변화하지않음    # [5, 4, 3, 2, 1] (print 함)
  >>> a.sort()    # 스스로 변화하는 함수   # [1, 2, 3, 4, 5] (print 안함)
  #
  # 주의 #
  def f(x):
    return print(x + 10)
  >>> f(10)     # 20          # 값을 변경하지 않음
  >>> c = f(10) # 20          # c에 f 함수의 리턴값을 할당 # 함수 return 전에 x+10출력
  >>> c         # 출력없음    # 그러나 return print()
  # => print는 반환형이 없으므로 출력이 없음 !!!
  ```
- console in/out
  - 프로그램과 데이터를 주고받는 방법
  - 입력: input
    - `input()` 함수: 콘솔창에서 문자열을 입력받는 함수
    - `var = input()`
    - 숫자 입력 받기: `var = float(input("입력하세요 :"))`
    - 괄호 안에 문자열을 넣는 경우, 콘솔에 입력 가이드처럼 쓸 수 있음
  - 출력: print
    - 콤마(,) 사용할 경우, print 문이연결됨
    - `print ("Hello World!", "Hello Again!!!")`
    - 타입이 다른 경우, 연속적으로 출력하기 위해서 사용
    - 콤마를 사용하지 않는 경우, 형변환 후에 concatenate 해야함
- print formatting
  - 형식(format)에 맞춰서 출력하고자 할 때 사용
  - print문을 활용하여 결과 formatting
    - print문은 기본적인 출력 외에 출력양식 형식을 지정가능
    - (1) % string (2) format 함수 (3) fstring
  - fomatting 방법
    0. % string
      - 일반적으로 %-format 과 str.format() 함수를사용함
      ```Python
      print('%s %s' % ('one', 'two'))
      print('{} {}'.format('one', 'two'))
      print('%d %d' % (1, 2))
      print('{} {}'.format(1, 2))
      ```
    1. %-formatting
      - "%datatype" % (variable) 형태로 출력 양식을 표현
      - % datatype
        - %d: integer
        - %s: string
        - %f: float
      ```Python
      print("I eat %d apples." % 3)
      print("I eat %s apples." % "five")
      number = 3; day="three"
      print("I ate %d apples. I was sick for %s days." % (number, day))
      print("Product: %s, Price per unit: %f." % ("Apple", 5.243))
      #
      print("Product: %5d, Price per unit: %8.2f." % ("Apple", 5.243))
      # 5: 5칸을 비워두라(%5d)
      # 8: 8칸을 비워두라(%8.2f)
      # 2: 소수점은 두자리만 출력(%8.2f) (그 아래는 반올림으로 처리)
      ```
    2. format 함수
      - str.format() 함수
      - "~~~~{datatype}~~~~".format(argument)
      ```Python
      age = 36; name='Sungchul Choi'
      print("I’m {0} years old.".format(age))
      print("My name is {0} and {1} years old.".format(name,age)) # 0과 1은 인덱스
      # "My name is {name} and {age} years old."
      print("My name is {1} and {0} years old.".format(name,age))
      # "My name is {age} and {name} years old."
      print( "Product: {0}, Price per unit: {1:.3f}.".format("Apple", 5.243))
      # 0, 1을 순서대로 넣고, 1번은 소수점 3자리까지 넣기
      "Art: {0:5d}, Price per Unit: {1:8.2f}".format(453, 59.058)
      # Art:   453, Price per Unit:    59.06
      ```
    3. fstring
      - python 3.6 이후, PEP498에 근거한 formatting 기법
      - f라고 앞에 써주고 사용해야함
      - 이전에 선언된 변수명을 그대로 가져와서 사용할 수 있음
      - 왼쪽 정렬이 기본
      ```Python
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
  - padding
    - 여유공간을 지정하여 글자배열 + 소수점 자릿수를 맞추기
    ```Python
    print("Product: %5s, Price per unit: %.5f." % ("Apple", 5.243))
    print("Product: {0:5s}, Price per unit: {1:.5f}.".format("Apple", 5.243))
    print("Product: %10s, Price per unit: %10.3f." % ("Apple", 5.243))
    print("Product: {0:>10s}, Price per unit: {1:10.3f}.".format("Apple", 5.243))
    # 10칸을 비우면서 오른칸으로 정렬(<)   #      5.243
    # 10칸을 비우면서 왼칸으로 정렬(>)     # 5.243
    ```
  - naming
    - 표시할 내용을 변수로 표시하여 입력
    ```Python
    print("Product: %(name)10s, Price per unit: %(price)10.5f." % {"name":"Apple", "price":5.243})
    # Product:      Apple, Price per unit:     5.24300.
    print("Product: {name:>10s}, Price per unit: {price:10.5f}.".format(name="Apple", price=5.243))
    # Product: Apple     , Price per unit:     5.24300.
    ```

## Conditionals and Loops
- condition
  - 조건문: 조건에 따라 특정한 동작을 하게하는 명령어
  - 조건문은 조건을 나타내는 기준과 실행해야 할 명령으로 구성됨
  - 조건의 참, 거짓에 따라 실행해야 할 명령이 수행되거나 되지 않음
  - 파이썬은 조건문으로 if , else , elif 등의 예약어를 사용함
  - if-elif-else
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
        ```Python
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
      ```Python
      >>> if 1:
      ... print "True"
      ... else:
      ... print "False"
      ...
      True
      ```
  - 논리 키워드 사용: `and, or, not`
    - 조건문을 표현할 때, 집합의 논리키워드를 함께 사용하여 참과 거짓을 판단하기도 함
    - list 원소들 내의 and, or 연산: `all(list), any(list)`
    ```Python
    a = 8, b = 5 일 때
    if a == 8 and b ==4   # 거짓
    if a > 7 or b > 7     # 참
    if not (a > 7)        # 거짓, a>7인 것이 참 이므로 거짓으로 판단됨
    list1 = [True, False, True]
    all(list1) # False
    any(list1) # True
    ```
  - 삼항 연산자(Ternary operators)
    - 조건문을 사용하여 참일 경우와 거짓을 경우의 결과를 한 줄에 표현
    ```python
    >>> value = 12
    >>> is_even = True if value % 2 == 0 else False
    # is_even = ((True)         if (value % 2 == 0)    else (False))
    #           (조건만족시)    (if 조건문)            (else 조건불만족시)
    >>> print(is_even)
    True
    ```
- loop
  - 정해진 동작을 반복적으로 수행하게 하는 명령문
  - 반복문은 반복 시작조건, 종료조건, 수행명령으로 구성됨
  - 반복문 역시 반복 구문은 들여쓰기와 block으로 구분됨
  - 파이썬은 반복문으로 `for, while` 등의 명령 키워드를 사용함
  - 기본적인 반복문: 반복 범위를 지정하여 반복문 수행
    1. looper 변수에 1 할당
    2. "Hello" 출력
    3. 리스트(대괄호속 숫자들) 있는 값 차례로 looper 할당
    4. 5까지 할당한 후 반복 block 수행 후 종료
    ```Python
    for i in [1,2,3,4,5]:
      print(i)
    ```
  - range() 사용하기
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
  - 시퀀스형 자료형의 반복문
    - 문자열을 한자씩 리스트로 처리
    ```Python
    for i in "abcdefg":
      print (i)
    ```
    - 각각의 문자열 리스트로 처리
    ```Python
    for i in ["americano", "latte", "frafuchino"]:
      print (i)
    ```
  - while문
    - 조건이 만족하는 동안 반복 명령문을 수행
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
        print (i,)
      else:
        print ("EOP")
      ##################
      i =0
      while i < 10:
        print (i,)
        i += 1
      else:
        print ("EOP")
      ```
  - 반복문 상식
    - 반복문 변수명
      - 임시적인 반복 변수는 대부분 i, j, k로 정함
    - 0부터 시작하는 반복문
      - 반복문은 대부분 0부터 반복을 시작
      - 이것도 일종의 관례로 1부터 시작하는 언어도 존재
      - 2진수가 0부터 시작하기 때문에 0부터 시작하는 것을 권장
    - 무한 loop
      - 반복 명령이 끝나지 않는 프로그램 오류
      - CPU와 메모리 등 컴퓨터의 리소스를 과다하게 점유

## String and advanced function concept
- 문자열(string)
  - 시퀀스 자료형으로 문자형 data를 메모리에 저장
  - 영문자 한 글자는 1byte의 메모리 공간을 사용
  - list와 비슷한 구조
  - 1byte의 메모리가 순차적으로 나열되어있다고 생각
    - 1byte의 메모리 공간
      - 컴퓨터는 2진수로 데이터를 저장
      - 이진수 한 자릿수는 1bit로 저장됨
      - 즉 1bit는 0 또는 1
      - `1byte = 8bit = 2^8 = 256`까지 저장 가능
  - 문자를 인식하는 방법
    - 컴퓨터는 문자를 직접적으로 인식하지 않음
    - 모든 데이터는 이진수로 인식
    - 이를 위해 이진수를 문자로 변환하는 표준 규칙을 정함
      - cp949, utf-8, ASCII
      - 이러한 규칙에 따라 문자를 이진수로 변환하여 저장하거나 저장된 이진수를 숫자로 변환하여 표시함
- 프로그램 언어에서 데이터 타입
  - 각 타입 별로 메모리 공간을 할당 받은 크기가 다름
    - 정수형(int): 4byte ((-2^(21))~(2^(31)-1))
    - 정수형(long): 무제한
    - 실수형(float): 8byte ((10^(-308))~(10^(308)))
  - 메모리 공간에 따라 표현할 수 있는 숫자 범위가 다름
  - 데이터 타입은 메모리의 효율적 활용을 위해 매우 중요
- 문자열 특징
  - 인덱싱(Indexing)
    - 문자열의 각 문자는 개별주소(offset)를 가짐
    - 이 주소를 사용하여 할당된 값을 가져오는 것이 인덱싱
    - list와 같은 형태로 인덱스로 접근하여 데이터를 처리함
    - `str[10]`
    - 범위 넘어가는 인덱싱으로 접근하고자하면, 처음/끝을 자동으로 지정
    - `"Team" in "a"` 처럼 ~가 ~에 들어가있는지 여부를 알 수 있음
  - [문자열 함수 참고](https://m.blog.naver.com/PostView.nhn?blogId=hsj2864&logNo=220752261661&proxyReferer=https:%2F%2Fwww.google.com%2F)
- 다양한 문자열 표현
  - 두줄 이상 문자열의 저장
    - `\n`: 줄바꿈을 의미하는 특수 문자
    - 큰따옴표 또는 작은 따옴표 세 번 연속 사용
      ```Python
      a = """ It’Ok
          I’m Happy.
          See you. """
      ```
  - 특수 문자
    - 문자열을 표시할 때 백슬래시 `\` 를 사용하여
    - 키보드로 표시하기 어려운 문자들을 표현함
  - raw string
    - 특수문자 특수 기호인 `\` escape 글자를 무시하고 그대로 출력함
    ```python
    >>> raw_string = "이제 파이썬 강의 그만 만들고 싶다. \n 레알"
    >>> print(raw_string)
    # 이제 파이썬 강의 그만 만들고 싶다.
    # 레알
    >>> raw_string = r"이제 파이썬 강의 그만 만들고 싶다. \n 레알"
    >>> print(raw_string)
    # 이제 파이썬 강의 그만 만들고 싶다. \n 레알
    ```
    ```Python
    # 예제
      f = open("yesterday.txt", 'r')
      yesterday_lyric = ""
      while True:
          line = f.readline()
          if not line:
              break
          yesterday_lyric = yesterday_lyric + line.strip() + "\n"
      f.close()
      #
      n_of_yesterday = yesterday_lyric.upper().count("YESTERDAY") # 대소문자 구분 제거
      print ("Number of a Word 'Yesterday'" , n_of_yesterday)
    ```
- call by object reference
  - 함수 호출 방식 개요
    - 함수에서 parameter를 전달하는 방식
      1. 값에 의한 호출(Call by Value)
      2. 참조의 의한 호출(Call by Reference)
      3. 객체 참조에 의한 호출(Call by Object Reference)
    - Call by value
      - 함수에 인자를 넘길 때, 값만 넘김
      - 함수 내에 인자 값 변경 시, 호출자에게 영향을 주지 않음
    - Call by Reference (포인터)
      - 함수에 인자를 넘길 때, 메모리 주소를 넘김
      - 함수 내에 인자 값 변경 시, 호출자의 값도 변경됨
  - **파이썬 함수 호출 방식 – Call by Object Reference**
    - 파이썬은 객체의 주소가 함수로 전달되는 방식
    - 전달된 객체를 참조하여 변경 시, 호출자에게 영향을 줌
    - 새로운 객체를 만들 경우, 호출자에게 영향을 주지 않음
    ```Python
      def spam(eggs):
        eggs.append(1)  # 기존 객체의 주소값에 [1] 추가
        # ham과 eggs는 [0, 1]의 주소를 가리킴
        eggs = [2, 3]   # 새로운 객체 생성
        # ham은 [0, 1]의 주소를 가리킴
        # eggs는 [2, 3]의 주소를 가리킴(새 객체를 가리키게됨) // 주소만 끊어버리고 새거 이음
      ham = [0]
      spam(ham)
      print(ham) # [0, 1]
    ```
  - swap
  - 함수를 통해 변수 간의 값을 교환(Swap)하는 함수
  - Call By XXXX를 설명하기 위한 전통적인 함수 예시
  ```Python
    # a = [1,2,3,4,5] 일 때 아래 함수 중 실제 swap이 일어나는 함수는?
    #
    # 1) value 교환 # X
    def swap_value (x, y):
      temp = x
      x = y
      y = temp
    # 함수의 값을 가리키는 로컬변수 x, y의 주소값만 자꾸 바뀌는 것
    # 실제로 함수 호출자의 데이터는 변경되지 않음
    #
    # 2) 주소 교환 # O
    def swap_offset (offset_x, offset_y):
      temp = a[offset_x]
      a[offset_x] = a[offset_y]
      a[offset_y] = temp
    # 값이 바뀜
    # 인덱스에 접근하여 데이터를 변경
    # 리스트 자체에 접근하여 값을 변경하므로, 당연히 바뀌게 됨
    #
    # 3) 리스트를 교환 # O
    def swap_reference (list, offset_x, offset_y):
      temp = list[offset_x]
      list[offset_x] = list[offset_y]
      list[offset_y] = temp
    ```
    - swap_offset: a 리스트의 전역 변수 값을 직접 변경
    - swap_reference: a 리스트 객체의 주소 값을 받아 값을 변경
    ```Python
    a = [1,2,3,4,5]
    swap_value(a[1], a[2])
    print (a) # [1,2,3,4,5]
    swap_offset(1,2)
    print (a) # [1,3,2,4,5]
    swap_reference(a, 1, 2)
    print (a) # [1,3,2,4,5]
    # 변화함
    # 가장 이상적인 접근법
    # 결론: 값을 parameter로 넣기보다는 인덱스, 주소로 접근하는 것이 값을 제대로 바꾸는  것
    # func내의 값은 항상 복사를 해서 사용하는것이 좋음
    # 파라미터는 최대한 변경하지 않는 것이 좋음
  ```
- function-scoping rule
  - 변수의 범위(Scoping Rule)
    - 변수가 사용되는 범위(함수 또는 메인 프로그램)
    - 지역변수(local variable): 함수내에서만 사용
    - 전역변수(global variable): 프로그램 전체에서 사용
      - 전역변수는 함수에서 사용가능
      - But, 함수 내에 전역 변수와 같은 이름의 변수를 선언하면 새로운 지역 변수가 생김
      - 함수 내에서 전역변수 사용 시 global 키워드 사용
      ```Python
        # Scopingn Rule Test
        def calculate(x, y):
          total = x + y # 새로운 값이 할당되어 함수 내 total은 지역변수가 됨
          print ("In Function")
          print ("a:", str(a), "b:", str(b), "a+b:", str(a+b), "total :", str(total))
          return total
        #
        a = 5 # a와 b는 전역변수
        b = 7
        total = 0 # 전역변수 total
        print ("In Program - 1")
        print ("a:", str(a), "b:", str(b), "a+b:", str(a+b))
        #
        sum = calculate (a,b)
        print ("After Calculation")
        print ("Total :", str(total), " Sum:", str(sum)) # 지역변수는 전역변수에 영향 X
        """
        결과
        In Program -1
        a: 5 b: 7 a+b: 12
        In function
        a: 5 b: 7 a+b: 12 total : 12
        After Calculation
        Total : 0 Sum: 12
        """
      ```
- recursive Function
  - 재귀함수
    - 자기자신을 호출하는 함수
    - 점화식과 같은 재귀적 수학 모형을 표현할 때 사용
    - 재귀 종료 조건 존재, 종료 조건까지 함수 호출 반복
- function type hints
  - 파이썬의 가장 큰 특징 – dynamic typing
  - 이는, 처음 함수를 사용하는 사용자가 interface를 알기 어렵다는 단점이 있음
  - python 3.5 버전 이후로는 PEP 484에 기반하여 type hints 기능 제공
  - `def do_function(var_name: var_type) -> return_type:`
  - `def type_hint_example(name: str) -> str` : 이렇게 미리 지정가능
  - Type hints의 장점
    1. 사용자에게 인터페이스를 명확히 알려줄 수 있음
    2. 함수의 문서화시 parameter에 대한 정보를 명확히 알 수 있음
    3. mypy 또는 IDE, linter 등을 통해 코드의 발생 가능한 오류를 사전에 확인
    4. 시스템 전체적인 안정성을 확보할 수 있음
- function docstring
  - 파이썬 함수에 대한 상세 스펙을 사전에 작성하여, 함수 사용자의 이행도를 높이는 것
  - 세개의 따옴표로 docstring 영역표시(함수명 아래)
- 함수 작성 가이드 라인
  - 함수는 가능하면 짧게 작성할 것 (줄 수를 줄일 것)
  - 함수 이름에 함수의 역할, 의도가 명확히 들어낼 것
  - `동사_목적어`
    - ex) `print_hello_world()`
  - 하나의 함수에는 유사한 역할을 하는 코드만 포함
  - 인자로 받은 값 자체를 바꾸진 말 것 (임시변수 선언)
  - 함수는 언제 만드는가?
    - 공통적으로 사용되는 코드는 함수로 변환
    - 복잡한 수식 → 식별 가능한 이름의 함수로 변환
    - 복잡한 조건 → 식별 가능한 이름의 함수로 변환
  - 좋은 코드를 작성하는 방법
    - 코딩은 팀플
    - 사람을 위한 코드
    - 사람의 이해를 돕기 위해 규칙이 필요(규칙-코딩 컨벤션)
    - 파이썬 코딩 컨벤션
      - 명확한 규칙은 없음
      - 때로는 팀마다, 프로젝트마다 따로
      - 중요한 건 일관성!!!
      - 읽기 좋은 코드가 좋은 코드
    - 들여쓰기?
      - 들여쓰기는 Tab or 4 Space 논쟁!
      - 일반적으로 4 Space를 권장함
      - 중요한 건 혼합하지 않으면 됨
      - 들여쓰기 공백 4칸을 권장
    - 한 줄은 최대 79자까지
    - 불필요한 공백은 피함
    - `=` 연산자는 1칸 이상 안 띄움
    - 주석은 항상 갱신, 불필요한 주석은 삭제
    - 코드의 마지막에는 항상 한 줄 추가
    - 소문자 l, 대문자 O, 대문자 I 금지
    - 함수명은 소문자로 구성, 필요하면 밑줄로 나눔
    - `lIO0 = "Hard to Understand"`
  - PEP8 – 파이썬 코딩 컨벤션의 기준
    - flake8
      - "flake8" 모듈로 체크 – flake8 <파일명>
      - conda install -c anaconda flake8
    - black
      - 최근에는 black 모듈을 활용하여 pep8 like 수준을 준수
      - conda install black
      - black codename.py 명령을 사용

## etc
- Debugging(디버깅)
  - 코드의 오류를 발견하여 수정하는 과정
  - 오류의 *원인*을 알고 *해결책*을 찾아야 함
  - *문법적 에러*를 찾기 위한 에러 메시지 분석
  - *논리적 에러*를 찾기 위한 테스트도 중요
  - 문법적 오류 예시
    - 들여쓰기, 오탈자, 대소문자 구분안함
  - 에러 메시지 분석
    - 에러가 발생하면 인터프리터가 알려줌
  - 논리적 에러
    - 뜻대로 실행되지 않는 코드
    - 중간에 프린터 문을 찍어서 확인
    - 함수 확인하기
    - check print문    

---

## 피어세션 정리
- Questions
  - [펭귄] global 키워드는 언제 사용하나요?
  - [MJ] 리눅스를 많이 사용하는 이유
  - [MJ] -5 ~ 256 사이의 숫자의 저장 방식
- 꿀팁
  - [서폿] solved.ac 플래티넘의 알고리즘 공부법
- Day2 리뷰
  - "파이썬 문법 기본적으로 알고 있었지만 잘 몰랐던 부분을 알고 있어서 좋았다"
  - 리스트 복사할 때 [:]을 사용해서 복사하는 것
  - % string, format 함수, f-string 등 다양한 포매팅 방식
  - 최성철 마스터님의 Coding Convention
  - "Git, Cmder, Jupyter, VSCode 등 도구 사용법을 익힐 필요가 있다"

> 위와 관련된 내용에 대하여 이야기를 나누었음  
깃허브에 issue로! 오늘 토론했던 것, 꿀팁(?), 의미있는 내용이라 생각된 것들을 남김

---

## 과제 진행 상황 정리/과제 결과물에 대한 정리
- md 파일을 너무 공들여 만들어서, 시간이 부족
- 과제는 `학습정리 제출` 이후에 하고자 함
- 과제 현황
  - [x] basic_math
  - [X] text_processing
  - [x] text_processing 2
  - [x] Baseball

- text_processing
  - `str.split()`: 중복되는 공백을 하나의 공백으로 생각. 공백을 기준으로 잘라줌
  - `str.split(' ')`: 중복되는 공백도 같이 반환
  ```Python
  # error case
  arr = ['a', 'e', 'i', 'o', 'u']
  for i in arr:
    arr += i.lower()
    # arr의 길이가 계속 길어지고, for문은 늘어간 길이만큼 다시 반복하므로 무한루프에 빠지게 됨
  ```
- text_processing 2
  - `str.find(s)`: str에서 s의 위치를 찾아서 인덱스 값 리턴(없으면 -1)

---

## 오늘의 한마디
- md 정리에 너무 많은 공을 들이지 말자
