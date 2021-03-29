---
title: "[부스트캠프 AI Tech / Day5] 파이썬 File Handling"
data: 2021-01-22 20:32:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python]
tags: [Python]
---


## **[DAY 5] File Handling**

---

### File system, 파일 시스템

- **File system, 파일 시스템**
  - OS에서 파일을 저장하는 트리구조 저장 체계
- **File**
  - 컴퓨터 등의 기기에서 의미 있는 정보를 담는 논리적인 단위
  - 모든 프로그램은 파일로 구성되어 있고, 파일을 사용
  - 가장 기본적인 정보 저장 단위
- **파일과 디렉토리**
  - 파일의 기본 체계 – 파일 vs 디렉토리
- **디렉토리 (Directory)**
  - 폴더 또는 디렉토리로 불림
  - 파일과 다른 디렉토리를 포함할 수 있음
- **파일 (File)**
  - 컴퓨터에서 정보를 저장하는 논리적인 단위 (wikipedia)
  - 파일은 파일명과 확장자로 식별됨 (예: hello.py)
  - 실행, 쓰기, 읽기 등을 할 수 있음

### **파일**

- **파일의 종류**
  - 기본적인 파일 종류로 text 파일과 binary 파일로 나눔
  - 컴퓨터는 text 파일을 처리하기 위해 binary 파일로 변환시킴 (예: pyc파일)
  - <u>모든 text 파일들이 실제로는 binary 파일</u>
  - ASCII/Unicode 문자열 집합으로 저장되어 사람이 읽을 수 있음
- **Binary vs Text**
  - `Binary File`
    - 컴퓨터만 이해할 수 있는 형태인 이진(법)형식으로 저장된 파일
    - 일반적으로 메모장으로 열면 내용이 깨져 보임 (메모장 해설 불가)
    - 엑셀파일, 워드 파일 등등
    - 어플리케이션에 종속적
  - `Text File`
    - 인간도 이해할 수 있는 형태인 문자열 형식으로 저장된 파일
    - 메모장으로 열면 내용 확인 가능
    - 메모장에 저장된 파일, HTML 파일, 파이썬 코드 파일 등
    - 실제로 컴퓨터에 저장되기 위해서는 Binary로 만들지만, 사람이 알아들을 수 있게 하기 위해서 데이터 저장 표준(ASCII)에 맞도록 저장하게 함

### **Python File I/O**

- **파일 열기**: `f = open("<파일이름>", "접근 모드")`
- **파일 닫기**: `f.close()`
- **파일 열기모드** (접근모드 지정)
  - `r 읽기모드` - 파일을 읽기만 할 때 사용
  - `w 쓰기모드` - 파일에 내용을 쓸 때 사용
  - `a 추가모드` - 파일의 마지막에 새로운 내용을 추가 시킬 때 사용

#### **File Read**

- **파일 읽기**
  - `read()`: txt 파일 안에 있는 내용을 통째로 문자열로 반환
  - `readlines()`: 한 줄씩 읽어와서 List Type으로 반환함
    - 첫번째 시작하자마자 모든것을 메모리에 올리는 것
  - `readline()`: 실행시마다 한 줄 씩 읽어 오기
    - 한 줄씩 읽어오면서 그때그때 메모리에 올리는 것
    - 시간을 포기하는 대신 메모리를 얻을 수 있음

---

- **read()** 예제

    ```python
    f = open("i_have_a_dream.txt", "r" ) # 대상파일이 같은 폴더에 있을 경우에 가능
    contents = f.read()
    print(contents)
    f.close()

    ###############################################
    # with 구문과 함께 사용하기
    # indentation이 지정되는 경우에 쓰일 수 있으며, indentation을 벗어나는 경우에 close() 됨
    with open("i_have_a_dream.txt","r") as my_file: # 파일 읽어올 수 있도록 주소 지정 # 파일이 있는 곳의 주소를 연결해둔것 # my_file이라는 별칭은 indentation 벗어나는 순간 쓸 수 없음
        contents = my_file.read() # 실제로 읽어와서 저장하는 부분
        print (type(contents), contents)
    ```

- **readlines()** 예제

    ```python
    with open("i_have_a_dream.txt", "r") as my_file:
    content_list = my_file.readlines() #파일 전체를 list로 반환
    print(type(content_list)) #Type 확인
    print(content_list) #리스트 값 출력
    ```

- **readline()** 예제

    ```python
    with open("i_have_a_dream.txt", "r") as my_file:
    i = 0
    while True:
        line = my_file.readline()
        if not line: # line에 아무것도 없을 때까지 while True문 돈다
        break
        print (str(i) + " === " + line.replace("\n", "")) #한줄씩 값 출력
        i = i + 1
    ```

- 예제: 단어 통계 정보 산출

```python
with open("i_have_a_dream.txt","r") as my_file:
contents = my_file.read()
word_list = contents.split(" ")
#빈칸 기준으로 단어를 분리 리스트
line_list = contents.split("\n")
#한줄 씩 분리하여 리스트

print("Total Number of Characters :", len(contents))
print("Total Number of Words:", len(word_list))
print("Total Number of Lines :", len(line_list))
```

---

#### **File Write**

- mode="w", encoding="utf8'

```python
# 맥: utf-8, 윈도우: cp-949 ➡ utf-8로 통일하기
f = open("count_log.txt",'w', encoding="utf8") # 한국, 동아시아 계 
for i in range(1, 11):
data = "%d번째 줄입니다.\n" % i
f.write(data)
f.close()

```

```python
with open("count_log.txt",'a', encoding="utf8") as f:
for i in range(1, 11):
data = "%d번째 줄입니다.\n" % i
f.write(data)
```

---

### **Directory Handling**

#### `os 모듈`
  
- 객체로 다루니까 디렉토리나 파일에 접근하는게 훨씬 용이해짐
- 사용법

    ```python
    import os
    os.mkdir("log")

    ###############################
    try:
        os.mkdir("abc")
    except FileExistsError as e:
        print("Already created")

    os.path.exist("abc") # True / False
    os.path.isfile("file.ipynb")

    ############################### 파일을 복사
    import shutil
    source = "file.ipynb"
    dest = os.path.join("abc", "file.ipynb") # 둘을 합쳐줌
    shutil.copy(source, dest) 
    # "abc" + "\\" + "file.ipynb" 이렇게 사용하는것 완전 지양
    # 왜냐면 OS마다 seperator의 기준값이 다르기 때문
    # shutil 사용해서 path join을 권장

    ###############################

    # 최근에는 pathlib 모듈을 사용하여 path를 객체로 다룸
    # OS에 따른 path 규칙을 좀 맞춰줄 수있음
    # 파일이나 디렉토리제 접근하는 것이 좀더 편해짐
    >>> import pathlib
    >>>
    >>> cwd = pathlib.Path.cwd() # current directory
    >>> cwd
    WindowsPath('D:/workspace')
    >>> cwd.parent # 부모 폴더
    WindowsPath('D:/')
    >>> list(cwd.parents) # 부모의 부모 폴더
    [WindowsPath('D:/')]
    >>> list(cwd.glob("*"))
    [WindowsPath('D:/workspace/ai-pnpp
    '), WindowsPath('D:/workspace/cs50_auto_grader'),
    WindowsPath('D:/workspace/data-academy'), WindowsPath('D:/workspace/DSME-AI-SmartYard'), WindowsPath('D:/workspace/introduction_to_python_TEAMLAB_MOOC'),

    ###############################
    import pathlib
    cwd = pathlib.Path.cwd()
    # cwd: 현재 디렉토리 위치
    # cwd.parent: 현재 디렉토리 위치보다 상위에 있는 디렉토리
    # cwd.parent.parent 가능

    cwd.glob('*')
    # generator 생성되기 떄문에 for loop 혹은 iteration 사용 필요
    ```

- 디렉토리가 있는지 확인하기

    ```python
    if not os.path.isdir("log"):
    os.mkdir("log")
    ```

- 예제) Log 파일 생성하기
  - 1) 디렉토리가 있는지 확인
  - 2) 파일이 있는지 확인
  - 실행할 때마다 log라는 파일에 정보를 저장

    ```python
    import os
    if not os.path.isdir("log"): # 파일이 있는지
        os.mkdir("log")

    if not os.path.exists("log/count_log.txt"): # 파일이 있는지 
        f = open("log/count_log.txt", 'w', encoding="utf8")
        f.write("기록이 시작됩니다\n")
        f.close()

    with open("log/count_log.txt", 'a', encoding="utf8") as f:
        import random, datetime
        for i in range(1, 11):
        stamp = str(datetime.datetime.now())
        value = random.random() * 1000000
        log_line = stamp + "\t" + str(value) +"값이 생성되었습니다" + "\n"
        f.write(log_line)
    ```

---

### **Pickle**

- 파이썬의 객체를 영속화(persistence)하는 built-in 객체
- 데이터, object 등 실행중 정보를 저장 ➡ 불러와서 사용
- 저장해야하는 정보, 계산 결과(모델) 등 활용이 많음
- 파이썬에 특화된 **바이너리 파일**
- **영속화**: 하나의 객체를 파일로 저장하여 기록

> 객체의 위치는 메모리!
> 실행시키려면 메모리에 올라와야함
> 메모리 종료 ➡ 파이썬 인터프리터 종료시
> 이것을 저장(영속화)하여 계속 쓰고싶으면, 이를 어떻게 가져와서 쓸까? ➡ 피클!

```python
import pickle
f = open("list.pickle", "wb")
test = [1, 2, 3, 4, 5]
pickle.dump(test, f) # file f에 dump
f.close()

# 여기서 test를 지우더라도 피클을 load 하여 다시 가져올 수 있음

f = open("list.pickle", "rb")
test_pickle = pickle.load(f)
print(test_pickle)
f.close()
```

```python
import pickle
class Mutltiply(object):
  def __init__(self, multiplier):
    self.multiplier = multiplier
  def multiply(self, number):
    return number * self.multiplier

muliply = Mutltiply(5)
muliply.multiply(10)

f = open("multiply_object.pickle", "wb")
pickle.dump(muliply, f) # 영속화
f.close()

del muliply # 삭제

f = open("multiply_object.pickle", "rb") # 가져와서 쓸 수 있음
multiply_pickle = pickle.load(f)
multiply_pickle.multiply(5)
```
