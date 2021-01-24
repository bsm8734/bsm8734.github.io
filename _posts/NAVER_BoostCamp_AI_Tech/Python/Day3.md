# Day3

파이썬 기초 문법 2

## Python Data Structure

- 특징이 있는 정보를 저장하는 방법
- 파이썬 기본 데이터 구조
  - 스택과 큐(stack & queue with list)
  - 튜플과 집합(tuple & set)
  - 사전(dictionary)
  - Collection 모듈

### 스택 (Stack)

- 나중에 넣은 데이터를 먼저 반환하도록 설계된 메모리 구조
- Last In First Out (LIFO)
- Data의 입력을 push, 출력을 pop이라고 함
- 리스트를 사용하여 스택 구조를 구현 가능
- push를 `append()`, pop을 `pop()`를 사용
- 특이하게도, pop은 값을 변화하면서, 반환값이 존재
  - `sort()`: 반환값X, 값변경O
  - `sorted()`: 반환값O, 값변경X
  
```python
# 스택 구조를 활용, 입력된 글자를 역순으로 출력
word = input("Input a word : ") # Input Word
word_list = list(word) # String to List
for i in range(len(word_list)):
    print(word_list.pop()) # 하나씩 빼면서 출력
```

### 큐(Queue)

- 먼저 넣은 데이터를 먼저 반환하도록 설계된 메모리 구조
- First In First Out (FIFO)
- Stack과 반대되는 개념
- 파이썬은 리스트를 사용하여 큐 구조를 활용
- put를 append(), get을 pop(0)를 사용

```python
>>> a = [1,2,3,4,5]
>>> a.append(10)
>>> a.append(20)
>>> a.pop(0) # 1 출력
# 1
>>> a.pop(0) # 2 출력
# 2
```

### 튜플 (tuple)

- 값의 변경이 불가능한 리스트
- 선언 시 "[ ]" 가 아닌 "( )"를 사용
- 리스트의 연산, 인덱싱, 슬라이싱 등을 동일하게 사용
- 프로그램을 작동하는 동안 변경되지 않은 데이터의 저장
- 함수의 반환 값등 사용자의 실수에 의한 에러를 사전에 방지

```python
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

### 집합 (set)

- 값을 순서없이 저장, 중복 불허 하는 자료형
- set 객체 선언을 이용하여 객체 생성

```python
>>> s = set([1,2,3,1,2,3]) # set 함수를 사용 1,2,3을 집합 객체 생성 , a = {1,2,3,4,5} 도 가능
>>> s
#{1, 2, 3}
>>> s.add(1) # 한 원소 1만 추가, 추가, 중복불허로 추가 되지 않음
>>> s
#{1, 2, 3}
>>> s.remove(1) # 1 삭제
>>> s
# {2, 3}
>>> s.update([1,4,5,6,7]) # [1,4,5,6,7] 추가
>>> s
# {1, 2, 3, 4, 5, 6, 7}
>>> s.discard(3) # 3 삭제
>>> s
# {1, 2, 4, 5, 6, 7}
>>> s.clear() # 모든 원소 삭제

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

### 사전 (dictionary)

- 데이터를 저장 할 때는 구분 지을 수 있는 값을 함께 저장
- 구분을 위한 데이터 고유 값을 Identifier 또는 Key 라고함
- Key 값을 활용하여, 데이터 값(Value)를 관리함
- key와 value를 매칭하여 key로 value를 검색
- 다른 언어에서는 Hash Table 이라는 용어를 사용
- {Key1:Value1, Key2:Value2, Key3:Value3 ...} 형태

    ```python
    student_info = {20140012:'Sungchul', 20140059:'Jiyong',20140058:'JaeHong'}
    student_info[20140012]
    student_info[20140012] = 'Janhyeok'
    student_info[20140012]
    student_info[20140039] = 'wonchul'
    student_info

    >>> country_code = {} # Dict 생성, country_code = dict() 도 가능
    >>> country_code = {＂America＂: 1, ＂Korea＂: 82, ＂China＂: 86, ＂Japan＂: 81}
    >>> country_code
    # {＇America＇: 1, ＇China＇: 86, ＇Korea＇: 82, ＇Japan＇: 81}
    >>> country_code.items() # Dict 데이터 출력
    # Dict_items([(＇America＇, 1), (＇China＇, 86), (＇Korea＇, 82), (＇Japan＇, 81)])
    >>> country_code.keys() # Dict 키 값만 출력
    # Dict_keys(["America", "China", "Korea", "Japan"])
    >>> country_code["German"]= 49 # Dict 추가
    >>> country_code
    # {'America': 1, 'German': 49, 'China': 86, 'Korea': 82, 'Japan': 81}
    >>> country_code.values() # Dict Value만 출력
    # dict_values([1, 49, 86, 82, 81])

    >>> for k,v in country_code.items():
        print ("Key : ", k)
        print ("Value : ", v)
      
    '''
    Key : America
    Value : 1
    Key : Gernman
    Value : 49
    Key : China
    Value : 86
    Key : Korea
    Value : 82
    Key : Japan
    Value : 81
    '''

    >>> "Korea" in country_code.keys() # Key값에 "Korea"가 있는지 확인
    # True
    >>> 82 in country_code.values() # Value값에 82가 있는지 확인
    # True
    ```

### collections

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
  
### deque

- collections - deque
- Stack과 Queue 를 지원하는 모듈
- List에 비해 효율적인=빠른 자료 저장 방식을 지원함
- rotate, reverse등 Linked List의 특성을 지원함
- 기존 list 형태의 함수를 모두 지원함
- rotate, reverse등 Linked List의 특성을 지원함
- 기존 list 형태의 함수를 모두 지원함
- deque 는 기존 list보다 효율적인 자료구조를 제공
- 효율적 메모리 구조로 처리 속도 향상

```python

    from collections import deque
    deque_list = deque()
    for i in range(5):
        deque_list.append(i)
    print(deque_list)
    deque_list.appendleft(10)
    print(deque_list)

    deque_list.rotate(2)
    print(deque_list)
    deque_list.rotate(2)
    print(deque_list)
    print(deque(reversed(deque_list)))

    deque_list.extend([5, 6, 7])
    print(deque_list)
    deque_list.extendleft([5, 6, 7])
    print(deque_list)

    #deque
    from collections import deque
    import time

    start_time = time.clock()
    deque_list = deque()
    # Stack
    for i in range(10000):
        for i in range(10000):
            deque_list.append(i)
            deque_list.pop()
    print(time.clock() - start_time, "seconds")

    # general list
    import time
    start_time = time.clock()
    just_list = []
    for i in range(10000):
        for i in range(10000):
            just_list.append(i)
            just_list.pop()
    print(time.clock() - start_time, "seconds")

```

### OrderedDict

- collections - OrderedDict
- Dict와 달리, 데이터를 입력한 순서대로 dict를 반환함
- 그러나 dict도 python 3.6 부터 입력한 순서를 보장하여 출력함
- Dict type의 값을, value 또는 key 값으로 정렬할 때 사용 가능

```python
  from collections import OrderedDict

  d = OrderedDict()
  d['x'] = 100
  d['y'] = 200
  d['z'] = 300
  d['l'] = 500

  for k, v in d.items():
  print(k, v)

  for k, v in OrderedDict(sorted(d.items(), key=lambda t: t[0])).items():
      print(k, v)
  for k, v in OrderedDict(sorted(d.items(), key=lambda t: t[1])).items():
      print(k, v)
```

### defaultdict

- collections - defaultdict
- Dict type의 값에 기본 값을 지정, 신규 값 생성시 사용하는 방법

```python
from collections import defaultdict
d = defaultdict(object) # Default dictionary를 생성
d = defaultdict(lambda: 0) # Default 값을 0으로 설정합
print(d["first"])
```

```python
# 하나의 지문에 각 단어들이 몇 개나 있는지 세고 싶을경우?
# Text-mining 접근법 - Vector Space Model
text = """A press release is the quickest and easiest way to get free publicity. If well written, a press rv elease can result in multiple published articles about your firm and its products. And that can mean new prospects contacting you asking you to sell to 
them. ….""".lower().split()
# print(text) # ['a', 'press', ...]

from collections import OrderedDict

word_count = defaultdict(lambda: 0) # Default 값을 0으로 설정합
for word in text:
    word_count[word] += 1
for i, v in OrderedDict(sorted( word_count.items(), key=lambda t: t[1], reverse=True)).items():
print(i, v)
```

- ex) command analyzer
  
```python
    import csv
    def getKey(item): # 정렬을 위한 함수
    return item[1] # 신경 쓸 필요 없음
    command_data = [] # 파일 읽어오기
    with open("command_data.csv", "r") as csvfile:
    spamreader = csv.reader(csvfile, delimiter=',', quotechar='"')
    for row in spamreader:
    command_data.append(row)
    command_counter = {} # dict 생성, 아이디를 key값, 입력줄수를 value값
    for data in command_data: # list 데이터를 dict로 변경
    if data[1] in command_counter.keys(): # 아이디가 이미 Key값으로 변경되었을 때
    command_counter[data[1]] += 1 # 기존 출현한 아이디
    else:
    command_counter[data[1]] = 1 # 처음 나온 아이디
    dictlist = [] # dict를 list로 변경
    for key, value in command_counter.items():
    temp = [key,value]
    dictlist.append(temp)
    sorted_dict= sorted(dictlist, key=getKey, reverse=True) # list를 입력 줄 수로 정렬
    print (sorted_dict[:100]) # List의 상위 10객값만 출력
```

### Counter (내용보완 필요)

- collections - Counter
- Sequence type의 data element들의 갯수를 dict 형태로 반환
- Dict type, keyword parameter 등도 모두 처리 가능
- Set의 연산들을 지원함
- word counter의 기능도 손쉽게 제공함

### namedtuple

- collections - namedtuple
- Tuple 형태로 Data 구조체를 저장하는 방법
- 저장되는 data의 variable을 사전에 지정해서 저장함
  
```python
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(11, y=22)
print(p[0] + p[1])
x, y = p
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

## Pythonic code

- (파이썬 스타일 코드)
- 파이썬 스타일의 코딩 기법
- 파이썬 특유의 문법을 활용하여 효율적으로 코드를 표현함
- 그러나 더 이상 파이썬 특유는 아님, 많은 언어들이 서로의 장점을 채용
- 고급 코드를 작성 할 수록 더 많이 필요해짐
- 남 코드에 대한 이해도
- 효율(빠른 속도, 짧은 코드)

### split & join

- split 함수
  - string type의 값을 “기준값”으로 나눠서 List 형태로 변환
- join 함수
  - String으로 구성된 list를 합쳐 하나의 string으로 반환
  
```python
    # split
    >>> items = 'zero one two three'.split() # 빈칸을 기준으로 문자열 나누기
    >>> print (items)
    # ['zero', 'one', 'two', 'three']
    >>> example = 'python,java,javascript' # ","을 기준으로 문자열 나누기
    >>> example.split(",")
    # ['python', ‘java', 'javascript']
    >>> a, b, c = example.split(",")
    # 리스트에 있는 각 값을 a,b,c 변수로 unpacking
    >>> example = ‘teamlab.technology.io'
    >>> subdomain, domain, tld = example.split('.')
    # "."을 기준으로 문자열 나누기 → Unpacking

    # join
    >>> colors = ['red', 'blue', 'green', 'yellow']
    >>> result = ''.join(colors)
    >>> result
    # 'redbluegreenyellow'
    >>> result = ' '.join(colors) # 연결 시 빈칸 1칸으로 연결
    >>> result
    # 'red blue green yellow'
    >>> result = ', '.join(colors) # 연결 시 ", "으로 연결
    >>> result
    # 'red, blue, green, yellow'
    >>> result = '-'.join(colors) # 연결 시 "-"으로 연결
    >>> result
    # 'red-blue-green-yellow'
```

### list comprehension

- 기존 List 사용하여 간단히 다른 List를 만드는 기법
- 포괄적인 List, 포함되는 리스트라는 의미로 사용됨
- 파이썬에서 가장 많이 사용되는 기법 중 하나
- 일반적으로 for + append 보다 속도가 빠름
  
```python
    ##### general style
    >>> result = []
    >>> for i in range(10):
        result.append(i)
    
    >>> result
    # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

    ##### list comprehension
    >>> result = [i for i in range(10)]
    >>> result
    # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    >>> result = [i for i in range(10) if i % 2 == 0]
    >>> result
    # [0, 2, 4, 6, 8]

    ############################################################
    >>> word_1 = "Hello"
    >>> word_2 = "World"
    >>> result = [i+j for i in word_1 for j in word_2]
    # Nested For loop
    >>> result
    # ['HW', 'Ho', 'Hr', 'Hl', 'Hd', 'eW', 'eo', 'er',
    # 'el', 'ed', 'lW', 'lo', 'lr', 'll', 'ld', 'lW',
    # 'lo', 'lr', 'll', 'ld', 'oW', 'oo', 'or', 'ol', 'od']

    ############################################################
    >>> case_1 = ["A","B","C"]
    >>> case_2 = ["D","E","A"]
    >>> result = [i+j for i in case_1 for j in case_2]
    >>> result
    # ['AD', 'AE', 'AA', 'BD', 'BE', 'BA', 'CD', 'CE', 'CA']
    >>> result = [i+j for i in case_1 for j in case_2 if not(i==j)]
    # Filter: i랑 j과 같다면 List에 추가하지 않음
    # [i+j if not(i==j) else i for i in case_1 for j in case_2]
    >>> result
    # ['AD', 'AE', 'BD', 'BE', 'BA', 'CD', 'CE', 'CA']
    >>> result.sort()
    >>> result
    # ['AD', 'AE', 'BA', 'BD', 'BE', 'CA', 'CD', 'CE']

    ############################################################
    >>> words = 'The quick brown fox jumps over
    the lazy dog'.split()
    # 문장을 빈칸 기준으로 나눠 list로 변환
    >>> print (words)
    ['The', 'quick', 'brown', 'fox', 'jumps',
    'over', 'the', 'lazy', 'dog']
    >>>
    >>> stuff = [[w.upper(), w.lower(), len(w)]
    for w in words]
    # list의 각 elemente들을 대문자, 소문자, 길이로 변환하여 two dimensional list로 변환

    >>> for i in stuff:
        print (i)
    
    ['THE', 'the', 3]
    ['QUICK', 'quick', 5]
    ['BROWN', 'brown', 5]
    ['FOX', 'fox', 3]
    ['JUMPS', 'jumps', 5]
    ['OVER', 'over', 4]
    ['THE', 'the', 3]
    ['LAZY', 'lazy', 4]
    ['DOG', 'dog', 3]
    ############################################################
    # Two dimensional vs One dimensional
    >>> case_1 = ["A","B","C"]
    >>> case_2 = ["D","E","A"]
    ['AD', 'AE', 'AA', 'BD', 'BE', 'BA', 'CD', 'CE', 'CA']
    >>> result = [i+j for i in case_1 for j in case_2]
    >>> result
    ['AD', 'AE', 'AA', 'BD', 'BE', 'BA', 'CD', 'CE', 'CA']
    >>> result = [ [i+j for i in case_1] for j in case_2]
    >>> result
    [['AD', 'BD', 'CD'], ['AE', 'BE', 'CE'], ['AA', 'BA', 'CA']]
```

### enumerate & zip

- enumerate : list의 element를 추출할 때 번호를 붙여서 추출
- zip : 두 개의 list의 값을 병렬적으로 추출함

```python
    # enumerate
    >>> for i, v in enumerate(['tic', 'tac', 'toe']):
        print (i, v) # list의 있는 index와 값을 unpacking
    # 0 tic
    # 1 tac
    # 2 toe

    >>> mylist = ['a', 'b', 'c', 'd']
    >>> list(enumerate(mylist)) # list의 있는 index와 값을 unpacking하여 list로 저장
    # [(0, 'a'), (1, 'b'), (2, 'c'), (3, 'd')]
    >>> {i:j for i,j in enumerate('Artificial intelligence (AI), is intelligence demonstrated by machines, unlike the natural intelligence displayed by humans and animals.'.split())}
    # 문장을 list로 만들고 list의 index와 값을 unpacking하여 dict로 저장
    # {0: 'Artificial', 1: 'intelligence', 2: '(AI),', 3: 'is', 4: 'intelligence', 5: 'demonstrated', 6: 'by',
    # 7: 'machines,', 8: 'unlike', 9: 'the', 10: 'natural', 11: 'intelligence', 12: 'displayed', 13: 'by', 14:
    # 'humans', 15: 'and', 16: 'animals.'}

    ############################################################
    # zip
    >>> alist = ['a1', 'a2', 'a3']
    >>> blist = ['b1', 'b2', 'b3']
    >>> for a, b in zip(alist, blist): # 병렬적으로 값을 추출
        print (a,b)
    
    # a1 b1
    # a2 b2
    # a3 b3
    >>> a,b,c =zip((1,2,3),(10,20,30),(100,200,300)) #각 tuple의 같은 index 끼리 묶음
    # (1, 10, 100) (2, 20, 200) (3, 30, 300)
    >>> [sum(x) for x in zip((1,2,3), (10,20,30), (100,200,300))]
    # 각 Tuple 같은 index를 묶어 합을 list로 변환
    # [111, 222, 333]

    ############################################################
    # enumerate & zip 동시 사용 예제
    >>> alist = ['a1', 'a2', 'a3']
    >>> blist = ['b1', 'b2', 'b3']
    >>>
    >>> for i, (a, b) in enumerate(zip(alist, blist)):
        print (i, a, b) # index alist[index] blist[index] 표시
       
    # 0 a1 b1
    # 1 a2 b2
    # 2 a3 b3

```

### lambda & map & reduce

##### Lambda

- 함수 이름 없이, 함수처럼 쓸 수 있는 익명함수
- 수학의 람다 대수에서 유래함
- Python 3부터는 권장하지는 않으나 여전히 많이 쓰임
- lambda problmes
  - 어려운 문법
  - 테스트의 어려움
  - 문서화 docstring 지원 미비
  - 코드 해석의 어려움
  - 이름이 존재하지 않는 함수의 출현
  - 그래도 많이 씀

```python

# general function
def f(x, y):
return x + y
print(f(1, 4))

# lambda function
f = lambda x, y: x + y
print(f(1, 4))

f = lambda x, y: x + y
print(f(1, 4))

f = lambda x: x ** 2
print(f(3))

f = lambda x: x / 2
print(f(3))

print((lambda x: x +1)(5))
```

##### map function

- 두 개 이상의 list에도 적용 가능함, if filter도 사용가능
- python3 는 iteration을 생성  list을 붙여줘야 list 사용가능
- 실행시점의 값을 생성, 메모리 효율적
- python3 는 iteration을 생성  list을 붙여줘야 list 사용가능
- 실행시점의 값을 생성, 메모리 효율적
- Lambda, map, reduce는 간단한 코드로 다양한 기능을 제공
- 그러나 코드의 직관성이 떨어져서 lambda나 reduce는 python3에서 사용을 권장하지 않음
- Legacy library나 다양한 머신러닝 코드에서 여전히 사용중

```python
ex = [1,2,3,4,5]
f = lambda x, y: x + y
print(list(map(f, ex, ex)))

list(map(lambda x: x ** 2 if x % 2 == 0 else x, ex))

ex = [1,2,3,4,5]
print(list(map(lambda x: x+x, ex)))
print((map(lambda x: x+x, ex)))
f = lambda x: x ** 2
print(map(f, ex))
for i in map(f, ex):
    print(i)

result = map(f, ex)
print(next(result))
```

##### reduce function

- map function과 달리 list에 똑같은 함수를 적용해서 통합

```python
from functools import reduce
print(reduce(lambda x, y: x+y, [1, 2, 3, 4, 5]))
```

### iterable object

- Sequence형 자료형에서 데이터를 순서대로 추출하는 object
- Characteristics
  - 내부적 구현으로 `__iter__` 와 `__next__` 가 사용됨
  - iter() 와 next() 함수로 iterable 객체를 iterator object로 사용
  
```python
for city in ["Seoul", "Busan", "Pohang"]:
    print(city, end="\t")
for language in ("Python", "C", "Java"):
    print(language, end="\t")
for char in "Python is easy":
    print(char, end = " ")

# characteristics
cities = ["Seoul", "Busan", "Jeju"]
iter_obj = iter(cities)
print(next(iter_obj))
print(next(iter_obj))
print(next(iter_obj))
next(iter_obj)
```

### generator

- iterable object를 특수한 형태로 사용해주는 함수
- element가 사용되는 시점에 값을 메모리에 반환
- yield를 사용해 한번에 하나의 element만 반환함
- generator comprehension
  - list comprehension과 유사한 형태로 generator형태의 list 생성
  - generator expression 이라는 이름으로도 부름
  - `[ ]` 대신 `( )` 를 사용하여 표현
- 일반적인 iterator는 generator에 반해 훨씬 큰 메모리 용량 사용
- generator은 언제 사용?
  - list 타입의 데이터를 반환해주는 함수는 generator로 만들기
    - : 읽기 쉬운 장점, 중간 과정에서 loop 이 중단될 수 있을 때
  - 큰 데이터를 처리할 때는 generator expression을 고려하기
    - : 데이터가 커도 처리의 어려움이 없음
  - 파일 데이터를 처리할 때도 generator를 쓰자

```python
def general_list(value):
    result = []
    for i in range(value):
        result.append(i)
    return result

def geneartor_list(value):
    result = []
    for i in range(value):
        yield i

# generator comprehension
gen_ex = (n*n for n in range(500))
print(type(g)) 

# memory issue
from sys import getsizeof
gen_ex = (n*n for n in range(500))
print(getsizeof(gen_ex))
print(getsizeof(list(gen_ex)))
list_ex = [n*n for n in range(500)]
print(getsizeof(list_ex))
```

### function passing arguments

- 함수에 입력되는 arguments의 다양한 형태
  - 1) Keyword arguments
  - 2) Default arguments
  - 3) Variable-length arguments
- Keyword arguments
  - 함수에 입력되는 parameter의 변수명을 사용, arguments를 넘김

    ```python
    def print_somthing(my_name, your_name):
        print("Hello {0}, My name is {1}".format(your_name, my_name))

    print_somthing("Sungchul", "TEAMLAB")
    print_somthing(your_name="TEAMLAB", my_name="Sungchul")
    ```

- Default arguments
  - parameter의 기본 값을 사용, 입력하지 않을 경우 기본값 출력
  
    ```python
    def print_somthing_2(my_name, your_name="TEAMLAB"):
        print("Hello {0}, My name is {1}".format(your_name, my_name))
    print_somthing_2("Sungchul", "TEAMLAB")
    print_somthing_2("Sungchul")
    ```

### asterisk

##### variable-length asterisk

- 함수의 parameter가 정해지지 않았을 경우
- 가변인자 using asterisk
- 가변인자 (variable-length)
  - 개수가 정해지지 않은 변수를 함수의 parameter로 사용하는 법
  - Keyword arguments와 함께, argument 추가가 가능
  - Asterisk(*) 기호를 사용하여 함수의 parameter를 표시함
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

- 키워드 가변인자 (Keyword variable-length )
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

- asterisk
  - 흔히 알고 있는 * 를 의미함
  - 단순 곱셈, 제곱연산, 가변 인자 활용 등 다양하게 사용됨
  - unpacking a container
    - tuple, dict 등 자료형에 들어가 있는 값을 unpacking
    - 함수의 입력값, zip 등에 유용하게 사용가능

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

## 피어세션 정리

- generator에 대해서 다시 공부하기
- asterisk에 대해서 다시 공부하기

## 오늘의 한마디

- 나태해지지말자!