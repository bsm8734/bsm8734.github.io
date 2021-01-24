# day5

## Exception/File/Log Handling

## Exception

- 예상 가능한 예외
  - 발생 여부를 프로그래머가, 사전에 인지할 수 있는 예외
  - 사용자의 잘못된 입력, 파일 호출 시 파일 없음
  - 개발자가 반드시 명시적으로 정의, 처리 해야함
- 예상이 불가능한 예외
  - 인터프리터 과정에서 발생하는 예외, 개발자 실수
  - 리스트의 범위를 넘어가는 값 호출, 정수 0으로 나눔
  - 수행 불가시 인터프리터가 자동 호출

### 예외 처리 (Exception Handling)

- 예외가 발생할 경우 후속조치등 대처필요
  1) 없는파일호출→ 파일없음을알림
  2) 게임이상종료→ 게임정보저장
- 프로그램 = 제품, 모든 잘못된상황에 대처가 필요 : **Exception Handling**
- if/else로 처리해도되지만, Exception 발생시키고, 이를 처리하는 방식을 권장하는 경우도 있음
- try ~ except 문법
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

#### exception의 종류
  
- Built-in Exception: 기본적으로 제공하는 예외 (빌트인 에러)
  - IndexError: List의 Index 범위를 넘어갈 때
  - NameError: 존재하지 않은 변수를 호출 할 때
  - ZeroDivisionError: 0으로 숫자를 나눌 때
  - ValueError: 변환할 수 없는 문자/숫자를 변환할 때
  - FileNotFoundError: 존재하지 않는 파일을 호출할 때

- try ~ except ~ else
  - `try`: 예외 발생 가능 코드
  - `except <Exception Type>`: 예외 발생시 동작하는 코드
  - `else`: 예외가 발생하지 않을 때 동작하는 코드

- try ~ except ~ finally
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

> if문 : 정상적인, 로직적인 문제
> exception: 사용자의 입력등으로 인해, 데이터가 잘못 입력되거나 잘못 처리되기 쉬운 경우
> ex) empty data => exception

##### raise 구문

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

##### assert 구문

- 특정조건에 만족하지 않을 경우, 예외발생
- `assert 예외조건`

```python
  def get_binary_nmubmer(decimal_number : int): # :int로 타입 hinting까지 줬는데도 잘못입력하는 경우가 있음
    assert isinstance(decimal_number, int) # 이 부분이 True / False로 나올 수 있도록 하고, False인 경우, assertionError 발생시켜, 멈추게함
    return bin(decimal_number)
  print(get_binary_nmubmer(10))
```

### 파일 핸들링(File Handling)

#### File system, 파일 시스템

- File system, 파일 시스템
  - OS에서 파일을 저장하는 트리구조 저장 체계
- File
  - 컴퓨터 등의 기기에서 의미 있는 정보를 담는 논리적인 단위
  - 모든 프로그램은 파일로 구성되어 있고, 파일을 사용
  - 가장 기본적인 정보 저장 단위
- 파일과 디렉토리
  - 파일의 기본 체계 – 파일 vs 디렉토리
- 디렉토리 (Directory)
  - 폴더 또는 디렉토리로 불림
  - 파일과 다른 디렉토리를 포함할 수 있음
- 파일 (File)
  - 컴퓨터에서 정보를 저장하는 논리적인 단위 (wikipedia)
  - 파일은 파일명과 확장자로 식별됨 (예: hello.py)
  - 실행, 쓰기, 읽기 등을 할 수 있음

- 파일의 종류
  - 기본적인 파일 종류로 text 파일과 binary 파일로 나눔
  - 컴퓨터는 text 파일을 처리하기 위해 binary 파일로 변환시킴 (예: pyc파일)
  - 모든 text 파일도 실제는 binary 파일,
  - ASCII/Unicode 문자열 집합으로 저장되어 사람이 읽을 수 있음
  - Binary vs Text
    - Binary File
      - 컴퓨터만 이해할 수 있는 형태인 이진(법)형식으로 저장된 파일
      - 일반적으로 메모장으로 열면 내용이 깨져 보임 (메모장 해설 불가)
      - 엑셀파일, 워드 파일 등등
      - 어플리케이션에 종속적
    - Text File
      - 인간도 이해할 수 있는 형태인 문자열 형식으로 저장된 파일
      - 메모장으로 열면 내용 확인 가능
      - 메모장에 저장된 파일, HTML 파일, 파이썬 코드 파일 등
      - 실제로 컴퓨터에 저장되기 위해서는 Binary로 만들지만, 사람이 알아들을 수 있게 하기 위해서 데이터 저장 표준(ASCII)에 맞도록 저장하게 함

#### Python File I/O

- 파이썬은 파일 처리를 위해 "open" 키워드를 사용함
- `f = open("<파일이름>", "접근 모드")` : 파일 열기
- `f.close()` : 파일 닫기
- 파일 열기모드 설명(접근모드 지정)
  - r 읽기모드 - 파일을 읽기만 할 때 사용
  - w 쓰기모드 - 파일에 내용을 쓸 때 사용
  - a 추가모드 - 파일의 마지막에 새로운 내용을 추가 시킬 때 사용

- 파이썬의 File Read

- read() txt 파일 안에 있는 내용을 통째로 문자열로 반환

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

- 한 줄씩 읽어와서 List Type으로 반환함

  ```python
  with open("i_have_a_dream.txt", "r") as my_file:
    content_list = my_file.readlines() #파일 전체를 list로 반환
    print(type(content_list)) #Type 확인
    print(content_list) #리스트 값 출력
  ```

  > 첫번째 시작하자마자 모든것을 메모리에 올리는 것

- 실행시마다 한 줄 씩 읽어 오기

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

  > 한 줄씩 읽어오면서 그때그때 메모리에 올리는 것
  >  시간을 포기하는 대신 메모리를 얻을 수 있음

- 예제

```python
  #단어 통계 정보 산출
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

##### 파이썬의 File Write

- mode는 “w”, encoding=“utf8”

  ```python
  # 맥: utf-8, 윈도우: cp-949 => utf-8로 통일하기
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

##### 파이썬의 directory 다루기

- os 모듈을 사용하여 Directory 다루기
  
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

  - 객체로 다루니까 디렉토리나 파일에 접근하는게 훨씬 용이해짐

- 디렉토리가 있는지 확인하기

  ```python
    if not os.path.isdir("log"):
    os.mkdir("log")
  ```

- Log 파일 생성하기
  - 1) 디렉토리가 있는지, 2) 파일이 있는지 확인 후
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

      # 실행할 때마다 log라는 파일에 정보를 저장
     ```

객체의 위치는 메모리!
실행시키려면 메모리에 올라와야함
메모리 종료 -> 파이썬 인터프리터 종료시
얘를 저장(영속화)하여 계속 쓰고싶을 것. 이를 어떻게 가져와서 쓸까? -> 피클!

- Pickle
  - 파이썬의 객체를 영속화(persistence)하는 built-in 객체
  - 데이터, object 등 실행중 정보를 저장불러와서 사용
  - 저장해야하는 정보, 계산 결과(모델) 등 활용이 많음
  - 파이썬에 특화된 바이너리 파일
  - 영속화: 하나의 객체를 파일로 저장하여 기록

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

#### Logging Handling

- 로그 남기기 - Logging
- 프로그램이 실행되는 동안 일어나는 정보를 기록을 남기기 (현재 상황 기록)
- 유저의 접근, 프로그램의 Exception, 특정 함수의 사용
- Console 화면에 출력, 파일에 남기기, DB에 남기기 등등
- 기록된 로그를 분석하여 의미있는 결과를 도출 할 수 있음
- 실행시점에서 남겨야 하는 기록: 유저분석
- 개발시점에서 남겨야하는 기록: 에러잡기, 디버깅 쉽게!

- print vs logging
  - 기록을 print로 남기는 것도 가능함
  - 그러나 Console 창에만 남기는 기록은 분석시 사용불가(콘솔창 끄면 사용 불가)
  - 때로는 레벨별(개발, 운영등... 어떤 레벨에 속하는 지에 따라)로 기록을 남길 필요도 있음
  - 모듈별로 별도의 logging을 남길필요도 있음
  - 이러한 기능을 체계적으로 지원하는 모듈이 필요함

- logging 모듈
  - Python의 기본 Log 관리 모듈

    ```python
    import logging
    logging.debug("틀렸잖아!")
    logging.info("확인해")
    logging.warning("조심해!")
    logging.error("에러났어!!!")
    logging.critical ("망했다...")
    ```

log는 print가 하는 일과 거의 유사
 
- Logging level
  - 프로그램 진행 상황에 따라 다른 Level의 Log를 출력함
  - 개발 시점, 운영 시점 마다 다른 Log가 남을 수 있도록 지원함
  - DEBUG(개발자) > INFO(운영) > WARNING(사용자~) > ERROR > Critical
  - Log 관리시 가장 기본이 되는 설정 정보 관리하기 위함


debug 개발시 처리 기록을 남겨야하는 로그 정보를 남김
info 처리가 진행되는 동안의 정보를 알림(프로그램 시작, 종료...)
warning 사용자가 잘못 입력한 정보나 처리는 가능하나 원래 개
발시 의도치 않는 정보가 들어왔을 때 알림. 더이상 쓰면 안될때: depreciate
error 잘못된 처리로 인해 에러가 났으나, 프로그램은 동작할
수 있음을 알림
critical 잘못된 처리로 데이터 손실이나 더이상 프로그램이 동
작할 수 없음을 알림

```python
import logging
logger = logging.getLogger("main") # logger 선언
stream_hander = logging.StreamHandler() # logger의 output 방법 선언
logger.addHandler(stream_hander) logger의 # output 등록


logger.debug("틀렸잖아!")
logger.info("확인해")
logger.warning("조심해!") # 여기부터서만 뜬다
logger.error("에러났어!!!")
logger.critical("망했다...")

# logger.setLevel(logging.DEBUG)

# 이유는 기본 로깅 레벨이 warning 이상이므로..
# 왜냐면 operation에서 사용자에게 알려주는 레벨

#####
import logging

logger = logging .getLogger("main")
logging.basicConfig(level = logging.DEBUG) # 기본세팅
logger.setLevel(logging.INFO) # 레벨 변경 # 3.8 이상 부터는 두개를 함께 써야함

# 출력을 어디에 할 것인가 : my.log에 해줄 것/append mode
# steam_handler = logging.FileHandler("my.log", mode="a", encoding="utf=8") 
# logger.addHandler(steam_handler) 

logger.debug("틀렸잖아!")
logger.info("확인해")
logger.warning("조심해!") # 여기부터서만 뜬다
logger.error("에러났어!!!")
logger.critical("망했다...")

```

- 위와 같이 실제 프로그램을 실행할 때는 여러 설정이 필요
- 데이터 파일 위치, 파일 저장 장소, operation type등
- 이러한 정보를 설정해 줄 방법이 필요

상태를 저장하거나 상태를 입력하는 방법
1. configparser - 파일에 저장
2. argparser - 실행시점에 

configparser
- 프로그램의 실행 설정을 file에 저장함
- Section, Key, Value 값의 형태로 설정된 설정 파일을 사용
- 설정파일을 Dict Type으로 (관리) 호출후 사용

- config file

```text
  [SectionOne] // section- 대괄호
  Status: Single
  Name: Derek
  Value: Yes
  Age: 30
  Single: True
  // 속성 - key:value

  [SectionTwo]
  FavoriteColor = Green

  [SectionThree]
  FamilyName: Johnson
```

configparser file
```python
import configparser
config = configparser.ConfigParser()
config.sections()

config.read('example.cfg')
config.sections()

for key in config['SectionOne']:
  print(key)
config['SectionOne']["status"]
```

```text
'example.cfg'
[SectionOne]
Status: Single
Name: Derek
Value: Yes
Age: 30
Single: True
[SectionTwo]
FavoriteColor = Green
[SectionThree]
FamilyName: Johnson
```

##### argparser

- 콘솔창에서 실행할 때, 세팅 정보를 전달
- Console 창에서 프로그램 실행시 Setting 정보를 저장함
- 거의 모든 Console 기반 Python 프로그램 기본으로 제공
- 특수 모듈도 많이 존재하지만(TF), 일반적으로 argparse를 사용
- Command-Line Option 이라고 부름

```python
import argparse
parser = argparse.ArgumentParser(description='Sum two integers.')

# 짧은 이름, 긴 이름, 표시 명, help 설명, argument type
parser.add_argument('-a', "--a_value", dest=”A_value", help="A integers", type=int)
parser.add_argument('-b', "--b_value", dest=”B_value", help="B integers", type=int)
args = parser.parse_args()
print(args)
print(args.a)
print(args.b)
print(args.a + args.b)
```
- 커맨드라인 옵션이라고도 함
- arg 가이드라인을 제공할 수 있음
- usage처럼! -? 어떻게?
- 이렇게 넣어지면, 타입과 같은 것을 검증 가능!
- arg 미리 넣어둬서 사용자가 실험해볼 수 있도록 만들어둠

```python
def main():
  parser = argparse.ArgumentParser(description='PyTorch MNIST Example')
  parser.add_argument('--batch-size', type=int, default=64, metavar='N', help='input batch size for training (default:
  64)')
  parser.add_argument('--test-batch-size', type=int, default=1000, metavar='N', help='input batch size for testing
  (default: 1000)')
  parser.add_argument('--epochs', type=int, default=10, metavar='N', help='number of epochs to train (default: 10)')
  parser.add_argument('--lr', type=float, default=0.01, metavar='LR', help='learning rate (default: 0.01)')
  parser.add_argument('--momentum', type=float, default=0.5, metavar='M', help='SGD momentum (default: 0.5)')
  parser.add_argument('--no-cuda', action='store_true', default=False, help='disables CUDA training')
  parser.add_argument('--seed', type=int, default=1, metavar='S', help='random seed (default: 1)’)
  parser.add_argument('--save-model', action='store_true', default=False, help='For Saving the current Model')
  args = parser.parse_args()

if __name__ == '__main__':
  main()
```

#### Logging 적용하기

- formatter 사용
- Logging formmater
Log의 결과값의 format을 지정해줄 수 있음
formatter = logging.Formatter('%(asctime)s %(levelname)s %(process)d %(message)s')
2018-01-18 22:47:04,385 ERROR 4410 ERROR occurred
2018-01-18 22:47:22,458 ERROR 4439 ERROR occurred
2018-01-18 22:47:22,458 INFO 4439 HERE WE ARE
2018-01-18 22:47:24,680 ERROR 4443 ERROR occurred
2018-01-18 22:47:24,681 INFO 4443 HERE WE ARE
2018-01-18 22:47:24,970 ERROR 4445 ERROR occurred
2018-01-18 22:47:24,970 INFO 4445 HERE WE ARE

- Log config file
logging.config.fileConfig('logging.conf')
logger = logging.getLogger()

log의 세팅을, 사전에 세팅설정
```text
[loggers]
keys=root

[handlers]
keys=consoleHandler

[formatters]
keys=simpleFormatter

[logger_root]
level=DEBUG
handlers=consoleHandler

[Handler_condoleHandler]
class=StreamHandler
level=DEBUG
formatter=simpleFormatter
args=(sys.stdout, )
...
```

```python
logger.info('Open file {0}'.format("customers.csv",))
try:
    with open("customers.csv", "r") as customer_data:
    customer_reader = csv.reader(customer_data, delimiter=',', quotechar='"')
    for customer in customer_reader:
      if customer[10].upper() == "USA": #customer 데이터의 offset 10번째 값
      logger.info('ID {0} added'.format(customer[0],))
    customer_USA_only_list.append(customer) #즉 country 필드가 “USA” 것만
except FileNotFoundError as e:
  logger.error('File NOT found {0}'.format(e,))
```


## Python data handling

- 지금까지 우리가 다룬 데이터는 :tablue 데이터
- 우리가 처리하는 데이터 저장 방식들
  - csv, 웹(html), xml, json

### CSV(Comma Seperate Values)

- CSV, 필드를 쉼표(,)로 구분한 **텍스트 파일**
- 엑셀 양식의 데이터를 **프로그램에 상관없이** 쓰기 위한 데이터 형식이라고 생각하면 쉬움(손쉽게 공유하기 위해서)
  - shell linux와 같은 경우, xlsx보다는 csv는 텍스트이므로 쉽게 처리 가능
  - 엑셀처럼 생긴 텍스트 데이터
- 탭(TSV, Tab Seperate Value), 빈칸(SSV) 등으로 구분해서 만들기도 함
- 통칭하여 character-separated values (CSV) 부름
- 엑셀에서는 “다름 이름 저장” 기능으로 사용 가능

엑셀로 CSV 파일 만들기
  1) 파일 다운로드 - https://bit.ly/2KGjLxR
  2) 파일 열기
  3) 파일 → 다른 이름으로 저장
  → CSV(쉼표로 분리) 선택 후 → 파일명 입력
  4) 엑셀 종료 후 Notepad로 파일 열어보기
- 데이터가 “,” 로 나눠져 있음
- Text 파일형태로데이터처리예제
- 예제데이터: customer.csv (https://bit.ly/3psoUZb)
- 일반적textfile을처리하듯파일을읽어온후, 한줄한줄씩데이터를처리함
- 엑셀은 텍스트 파일로 열면, 이상한 값으로 보임


- CSV 파일 읽기 예제

```python

line_counter = 0 #파일의 총 줄수를 세는 변수
data_header = [] #data의 필드값을 저장하는 list
customer_list = [] #cutomer 개별 List를 저장하는 List

with open ("customers.csv") as customer_data: #customer.csv 파일을 customer_data 객체에 저장
  while True:
    data = customer_data.readline() #customer.csv에 한줄씩 data 변수에 저장
    if not data: break #데이터가 없을 때, Loop 종료
    if line_counter==0: #첫번째 데이터는 데이터의 필드
      data_header = data.split(",") #데이터의 필드는 data_header List에 저장, 데이터 저장시 “,”로 분리
    else:
      customer_list.append(data.split(",")) #일반 데이터는 customer_list 객체에 저장, 데이터 저장시 “,”로 분리
      line_counter += 1

print("Header :\t", data_header) #데이터 필드 값 출력
for i in range(0,10): #데이터 출력 (샘플 10개만)
  print ("Data",i,":\t\t",customer_list[i])
print (len(customer_list)) #전체 데이터 크기 출력

```

- CSV 파일 쓰기 예제

```python
line_counter = 0
data_header = []
employee = []
customer_USA_only_list = []
customer = None

with open ("customers.csv", "r") as customer_data:
  while 1:
    data = customer_data.readline()
    if not data:
      break
    if line_counter==0:
      data_header = data.split(",")
    else:
      customer = data.split(",")
      if customer[10].upper() == "USA": #customer 데이터의 offset 10번째 값
        customer_USA_only_list.append(customer) #즉 country 필드가 “USA” 것만
    line_counter+=1 #sutomer_USA_only_list에 저장
print ("Header :\t", data_header)
for i in range(0,10):
  print ("Data :\t\t",customer_USA_only_list[i])
print (len(customer_USA_only_list))

with open ("customers_USA_only.csv", "w") as customer_USA_only_csv:
for customer in customer_USA_only_list:
customer_USA_only_csv.write(",".join(customer).strip('\n')+"\n")
#cutomer_USA_only_list 객체에 있는 데이터를 customers_USA_only.csv 파일에 쓰기
```

##### CSV 객체로 CSV 처리
- Text 파일형태로데이터처리시문장내에들어가있는"," 등에대해 전처리과정이필요
  - 주소와 같은 건 "," 이런게 들어갈 수 있음
  - 이런건 코딩하며 빼줘야함
- 파이썬에서는간단히CSV파일을처리하기위해csv 객체를제공함
- 예제데이터: korea_foot_traffic_data.csv (from http://www.data.go.kr)
- 예제데이터는국내주요상권의유동인구현황정보
- 한글로되어있어한글처리가필요

-시간대/조사일자/행정구역/날씨등을기준으로
연령별/성별유동인가해당지역에몇명인가표시

##### CSV 객체 활용

```python
import csv
reader = csv.reader(f, delimiter=',', quotechar= '"', quoting=csv.QUOTE_ALL)
# quotechar= '"' # quotation field, level 지정 가능 # 어디서 자르지?에 관련
```

~~공공데이터포털~~

Attribute | Default | Meaning
delimiter , 글자를 나누는 기준
lineterminator \r\n 줄 바꿈 기준
quotechar " 문자열을 둘러싸는 신호 문자
quoting QUOTE_MINIMAL 데이터 나누는 기준이 quotechar에 의해 둘러싸인 레벨

```python
# 유동인구데이터중성남데이터만수집
import csv
seoung_nam_data = []
header = []
rownum = 0

with open("korea_floating_population_data.csv","r", encoding="cp949") as p_file:
  csv_data = csv.reader(p_file) #csv 객체를 이용해서 csv_data 읽기
  for row in csv_data: #읽어온 데이터를 한 줄씩 처리
    if rownum == 0:
      header = row #첫 번째 줄은 데이터 필드로 따로 저장
    location = row[7]
    #“행정구역”필드 데이터 추출, 한글 처리로 유니코드 데이터를 cp949로 변환
    if location.find(u"성남시") != -1: # 유니코드의 약자
      seoung_nam_data.append(row)
    #”행정구역” 데이터에 성남시가 들어가 있으면 seoung_nam_data List에 추가
    rownum +=1

with open("seoung_nam_floating_population_data.csv","w", encoding="utf8") as s_p_file:
  writer = csv.writer(s_p_file, delimiter='\t', quotechar="'", quoting=csv.QUOTE_ALL)
  # ''으로 싸서, tab을 중간에 넣어주겠다는 것
  # csv.writer를 사용해서 csv 파일 만들기 delimiter 필드 구분자
  # quotechar는 필드 각 데이터는 묶는 문자, quoting는 묶는 범위
  writer.writerow(header) #제목 필드 파일에 쓰기
  for row in seoung_nam_data:
    writer.writerow(row) #seoung_nam_data에 있는 정보 list에 쓰기
```

csv를 window에서 작업하면 자동으로 cp-949로 저장해줌
vs code에서 열면, utf-8로 열어주기 때문에 초기에 깨져서 나올 수 있음
대신 encoding = "cp949"로 바꿔줘도 된다.

- 한줄 띄우는 기준: 윈도우: \n 맥: \r\n 
- ``으로 데이터를 묶어서 저장함
- 중요
  - 인코딩에 신경써라 : 윈도우는 cp949일 가능성이 높음
  - 안되면 utf-8로 해보기
  - 웬만하면 utf8로 저장하기
  - delimeter는 데이터를 자르는 기준
  - quotation: 데이터를 싸매는 기준
  - 애매하면 작은 quotatoin mark로 싸주기(그게 데이터에 없다면..)
-->  나중에는 pandas로 처리할 것


### Web

인터넷
html은 텍스트 덩어리
브라우저가 렌더링을 하여 우리에게 보여줌
- World Wide Web(WWW), 줄여서 웹이라고 부름
- 우리가 늘 쓰는 인터넷 공간의 정식 명칭
- 팀 버너스리에 의해 1989년 처음 제안되었으며,
원래는 물리학자들간 정보 교환을 위해 사용됨
- 데이터 송수신을 위한 HTTP 프로토콜 사용,
데이터를 표시하기 위해 HTML 형식을 사용

web의 동작
1. 요청: 웹주소, form, header
2. 처리: Database 처리 등 요청 대응
3. 응답: HTML, XML등 으로 결과 반환
4. 렌더링: HTML, XML 표시

- 웹 상의 정보를 구조적으로 표현하기 위한 언어
- 제목, 단락, 링크 등 요소 표시를 위해 Tag를 사용
  - <title> </title>
- 모든 요소들은 꺾쇠 괄호 안에 둘러 쌓여 있음
<title> Hello, World </title> ＃제목 요소, 값은 Hello, World
- 모든 HTML은 트리 모양의 포함관계를 가짐
- 일반적으로 웹 페이지의 HTML 소스파일은
컴퓨터가 다운로드 받은 후 웹 브라우저가 해석/표시

HTML(Hyper Text Markup Language)
```
<!doctype html>
<html>
<head>
<title>Hello HTML</title>
</head>
<body>
<p>Hello World!</p>
</body>
</html>
```

HTML 구조
<html> – <head> – <title>
– <body> – <p>

Element, Attribute Value 이루어짐

```
<tag attribute1=＂att_value1" attribute2="
att_value1 ">
보이는 내용(Value)
</tag>
```

- 왜 웹을 알아야 하는가?
  - 정보의 보고, 많은 데이터들이 웹을 통해 공유됨
  환율정보: https://finance.naver.com/
  날씨정보 : http://goo.gl/nwi8WE
  미국 특허정보: http://bit.ly/3pxFkjb
  - HTML도 일종의 프로그램, 페이지 생성 규칙이 있음
  : 규칙을 분석하여 데이터의 추출이 가능
  - 추출된 데이터를 바탕으로 하여 다양한 분석이 가능

- 규칙을 잘 분석하면, 데이터를 분석할 수 있음
  - HTML 분석 -> string, regex(정규식), beautiful soup

- 정규식 (regular expression)
  - 문자표현공식
  - 정규 표현식, regexp 또는 regex 등으로 불림
  - 복잡한 문자열 패턴을 정의하는 문자 표현 공식
  - 특정한 규칙을 가진 문자열의 집합을 추출
  010-0000-0000 ^\d{3}\-\d{4}\-\d{4}$
  203.252.101.40 ^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$ 

- 정규식 for HTML Parsing
  - 주민등록 번호, 전화번호, 도서 ISBN 등 형식이 있는
  문자열을 원본 문자열로부터 추출함
  - HTML역시 tag를 사용한 일정한 형식이 존재하여
  정규식으로 추출이 용이함
  - 관련자료: http://www.nextree.co.kr/p4327/

ctrl+f로, vs code에서 문자열 규칙을 통해 문자열 다룰 수 있음

- 정규식 for HTML Parsing
  - 문법 자체는 매우 방대, 스스로 찾아서 하는 공부 필요
  - 필요한 것들은 인터넷 검색을 통해 찾을 수 있음
  - 기본적인 것을 공부 한 후 넓게 적용하는 것이 중요
  - 공부법
    - 많이 쓰이는 정규식-> ppt 확인
    - https://zetawiki.com/wiki/%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D_%EC%98%88%EC%8B%9C
    - 1) 정규식연습장(http://www.regexr.com/) 으로이동
    - 2) 테스트하고싶은문서를Text 란에삽입
    - 3) 정규식을사용해서찾아보기

정규식 기본 문법 #1
  문자 클래스 [ ]: [ 와 ] 사이의 문자들과 매치라는 의미
  예) [abc]  해당 글자가 a,b,c중 하나가 있다.
  “a”, “before”, “deep” , “dud”, “sunset”
  “-“를 사용 범위를 지정할 수 있음
  예) [a-zA-z] – 알파벳 전체, [0-9] – 숫자 전체

정규식 기본 문법 – 메타 문자
  https://wikidocs.net/4308
  정규식 표현을 위해 원래 의미가 아닌, 다른 용도로 사용되는 문자
  . ^ $ * + ? { } [ ] \ | ( )
  `.` - 줄바꿈 문자인 \n를 제외한 모든 문자와 매치 a[.]b
  `*` - 앞에 있는 글자를 반복해서 나올 수 있음
        tomor*ow tomorrow tomoow tomorrrrow
  `+` - 앞에 있는 글자를 최소 1회 이상 반복
  {3} 3회 반복
  띄어쓰기도 넣을 수 있음

정규식 기본 문법 – 메타 문자
https://wikidocs.net/4308
정규식 표현을 위해 원래 의미 X, 다른 용도로 사용되는 문자
. ^ $ * + ? { } [ ] \ | ( )
{m.n} - 반복 횟수를 지정 {1,} , {0,} {1,3}
203.252.101.40 [0-9]{1,3} \d{1,3}
? - 반복 횟수가 1회 01[01]?-[0-9]{4}-[0-9]{4}
| - or (0|1){3} ^ - not
  

정규식 추출 연습
  ①정규식연습장(http://www.regexr.com/) 으로이동
  ②구글USPTO Bulk Download 데이터페이지소스보기클릭
  ③소스전체복사후정규식연습장페이지에붙여넣기
  ④상단Expression 부분을수정해가며“Zip”로끝나는파일명만추출
  ⑤Expression에(http)(.+)(zip) 를입력

정규식 in 파이썬
- re 모듈을 import 하여 사용 : import re
- 함수: search – 한 개만 찾기, findall – 전체 찾기
- 추출된 패턴은 tuple로 반환됨
- 연습 - 특정 페이지에서 ID만 추출하기 https://bit.ly/3rxQFS4
- ID 패턴: [영문대소문자|숫자] 여러 개, 별표로 끝남
"([A-Za-z0-9]+\*\*\*)“ 정규식

정규식 in 파이썬
```python
import re
import urllib.request
url =
"https://bit.ly/3rxQFS4"
html = urllib.request.urlopen(url)
html_contents = str(html.read())
id_results = re.findall(r"([A-Za-z0-9]+\*\*\*)", html_contents)
#findall 전체 찾기, 패턴대로 데이터 찾기

for result in id_results:
  print (result)

#################################################################3
import urllib.request # urllib 모듈 호출
import re
url = "http://www.google.com/googlebooks/uspto-patents-grants-text.html"
#url 값 입력
html = urllib.request.urlopen(url) # url 열기
html_contents = str(html.read().decode("utf8"))
# html 파일 읽고, 문자열로 변환
url_list = re.findall(r"(http)(.+)(zip)", html_contents)
for url in url_list:
print("".join(url)) # 출력된 Tuple 형태 데이터 str으로 join
```

- ex 정규식 in 파이썬 for html
```text
<dl class="blind">
  <dt>종목 시세 정보</dt>
  <dd>2020년 01월 17일 16시 10분 기준 장마감</dd>
  <dd>종목명 삼성전자</dd>
  <dd>종목코드 005930 코스피</dd>
  <dd>현재가 61,300 전일대비 상승 600 플러스 0.99 퍼센트</dd>
  <dd>전일가 60,700</dd>
  <dd>시가 61,900</dd>
  <dd>고가 62,000</dd>
  <dd>상한가 78,900</dd>
  <dd>저가 61,000</dd>
  <dd>하한가 42,500</dd>
  <dd>거래량 15,451,576</dd>
  <dd>거래대금 949,344백만</dd>
</dl>
```
① <dl class=“blind”> ~~~~ </dl>
(\<dl class=\"blind\"\>)([\s\S]+?)(\<\/dl\>)
<dl class에서 시작해서 / 사이에 아무 글자나 있고 / </dl> 로 끝내기
② <dd> ~~~~ </dd> 정보를 추출하면 됨
(\<dd\>)([\s\S]+?)(\<\/dd\>)
<dd> 에서 시작해서 / 사이에 아무 글자나 있고 / </dl> 로 끝내기
① 를 먼저 찾고 ① 안에 ②를 차례대로 찾으면 됨

```python
import urllib.request
import re
url = "http://finance.naver.com/item/main.nhn?code=005930"
html = urllib.request.urlopen(url)
html_contents = str(html.read().decode("ms949"))
stock_results = re.findall("(\<dl class=\"blind\"\>)([\s\S]+?)(\<\/dl\>)", html_contents)
samsung_stock = stock_results[0] # 두 개 tuple 값중 첫번째 패턴
samsung_index = samsung_stock[1] # 세 개의 tuple 값중 두 번째 값
# 하나의 괄호가 tuple index가 됨
index_list= re.findall("(\<dd\>)([\s\S]+?)(\<\/dd\>)", samsung_index)
for index in index_list:
print (index[1]) # 세 개의 tuple 값중 두 번째 값
```

### eXtensible Markup Language

- XML이란
  - 데이터의 구조와 의미를 설명하는
  TAG(MarkUp)를 사용하여 표시하는 언어
  - TAG와 TAG사이에 값이 표시되고,
  구조적인 정보를 표현할 수 있음
  - HTML과 문법이 비슷, 대표적인 데이터 저장 방식
  - 정보의 구조에 대한 정보인 스키마와 DTD 등으로
  정보에 대한 정보(메타정보)가 표현되며, 용도에 따라
  다양한 형태로 변경가능
  - XML은 컴퓨터(예: PC ↔ 스마트폰)간에 정보를
  주고받기 매우 유용한 저장 방식으로 쓰이고 있음

```html
- XML 예제
<?xml version="1.0"?>
<고양이> 
  <이름>나비</이름> <품종>샴</품종> <나이>6</나이> <중성화>예</중성화> <발톱 제거>아니요</발톱 제거>
  <등록 번호>Izz138bod</등록 번호>
  <소유자>이강주</소유자>
</고양이>
```

어떤 필드, 값, 필드 닫고
트리구조를 가지게 된다.

- XML Parsing in Python
  - XML도 HTML과 같이 구조적 markup 언어
  - 정규표현식으로 Parsing이 가능함
  - 그러나 좀 더 손쉬운 도구들이 개발되어 있음
  - 가장 많이 쓰이는 parser인 beautifulsoup으로 파싱

BeautifulSoup
- HTML, XML등 Markup 언어 Scraping을 위한 대표적인 도구
- https://www.crummy.com/software/BeautifulSoup/
- lxml 과 html5lib 과 같은 Parser를 사용함
- 속도는 상대적으로 느리나 간편히 사용할 수 있음
--> 랩핑

파이썬은 자체적 파서 제공

<?xml version="1.0"?>
<books>
    <book>
    <author>Carson</author>
    <price
    format="dollar">31.95</price>
    <pubdate>05/01/2001</pubdate>
    </book>
    <pubinfo>
    <publisher>MSPress</publisher>
    <state>WA</state>
  </pubinfo>
</books> 

beautifulsoup 설치
- conda 가상 환경으로 lxml과 beautifulsoup 설치

```bash
activate python_mooc
conda install lxml
conda install -c anaconda beautifulsoup4=4.5.1
```

- beautifulsoup 모듈 사용
  `from bs4 import BeautifulSoup`
  - 모듈 호출
  - 객체 생성
  `soup = BeautifulSoup(books_xml, "lxml")`
  - Tag 찾는 함수 find_all 생성
  `soup.find_all("author")` : "author" 태그 찾기

객체 생성(어떤 파일을 열건지, 어떤 파서로 열건지)
parser : xml을 분석하는 도구

- beautifulsoup 모듈 사용

  - find_all: 정규식과 마찬가지로 해당 패턴을 모두 반환
  - `find(‘invention-title’)` // `Tag 네임 = title`
  - get_text(): 반환된 패턴의 값 반환 (태그와 태그 사이)

  ```html
  <invention-title id="d2e43">
  Adjustable shoulder device for hard upper torso suit
  </invention-title>```

  http://goo.gl/aeKMGS, http://goo.gl/lKhFzh 참고

##### beautifulsoup Example
- 데이터 다운로드 받기
https://s3.ap-northeast-2.amazonaws.com/teamlab-gachon/books.xml
```python
from bs4 import BeautifulSoup
with open("books.xml", "r", encoding="utf8") as books_file:
books_xml = books_file.read() # File을 String으로 읽어오기
soup = BeautifulSoup(books_xml, "lxml") # lxml Parser를 사용해서 데이터 분석
# author가 들어간 모든 element 추출
for book_info in soup.find_all("author"):
print (book_info)
print (book_info.get_text())
```

beautifulsoup 예제 데이터
- 미국 특허청 (USPTO) 특허 데이터는 XML로 제공됨
- 해당 데이터중 등록번호 “08621662” 인 "Adjustable shoulder device for hard upper torso suit" 분석
참고: http://www.google.com/patents/US20120260387

https://s3.ap-northeast-2.amazonaws.com/teamlab-gachon/US08621662-20140107.XML

- XML 데이터를 Beautiful Soup을 통해 데이터 추출

beautifulsoup 예제 데이터
https://s3.ap-northeast-2.amazonaws.com/teamlab-gachon/US08621662-20140107.XML
```python
import urllib.request
from bs4 import BeautifulSoup
with open("US08621662-20140107.XML",
"r"
, encoding="utf8") as patent_xml:
xml = patent_xml.read() # File을 String으로 읽어오기
soup = BeautifulSoup(xml,
"lxml") #lxml parser 호출
#invention-title tag 찾기
invention_title_tag = soup.find("invention-title")
print (invention_title_tag.get_text())
```

beautifulsoup 예제 데이터
- 특허의 출원번호, 출원일, 등록번호, 등록일, 상태, 특허명을 추출
```html
<publication-reference> 등록 관련 정보
<document-id>
<country>US</country>
<doc-number>08621662</doc-number> 등록번호
<kind>B2</kind> 상태
<date>20140107</date> 등록일자
</document-id>
</publication-reference>
<application-reference appl-type="utility"> 출원 관련 정보
<document-id>
<country>US</country>
<doc-number>13175987</doc-number> 출원 번호
<date>20110705</date> 출원일
</document-id>
</application-reference>
```

beautifulsoup 예제 데이터
```
publication_reference_tag = soup.find("publication-reference")
p_document_id_tag = publication_reference_tag.find("document-id")
p_country = p_document_id_tag.find("country").get_text()
p_doc_number = p_document_id_tag.find("doc-number").get_text()
p_kind = p_document_id_tag.find("kind").get_text()
p_date = p_document_id_tag.find("date").get_text()
application_reference_tag = soup.find("application-reference")
a_document_id_tag = publication_reference_tag.find("document-id")
a_country = p_document_id_tag.find("country").get_text()
a_doc_number = p_document_id_tag.find("doc-number").get_text()
a_date = p_document_id_tag.find("date").get_text()
```

```
<publication-reference>
<document-id>
<country>US</country>
<doc-number>08621662</doc-number>
<kind>B2</kind>
<date>20140107</date>
</document-id>
</publication-reference>
<application-reference appltype="utility">
<document-id>
<country>US</country>
<doc-number>13175987</doc-number>
<date>20110705</date>
</document-id>
</application-reference>
```
특허 // 출원:신청, 등록:인정

- 이중으로 짜여있는 것은 코드도 이중으로 짜야함
- xml 구조를 알아야함


### JSON (JavaScript Object Notation)

JSON
- JavaScript Object Notation
- 원래 웹 언어인 Java Script의 데이터 객체 표현 방식
- 간결성으로 기계/인간이 모두 이해하기 편함
- 데이터 용량이 적고, Code로의 전환이 쉬움
- 이로 인해 XML의 대체제로 많이 활용되고 있음
https://www.flickr.com/photos/xmodulo/26106186415
Python의 Dict Type과 유사,
key:value 쌍으로 데이터 표시

```json
// xml
<?xml version="1.0" encoding="UTF8" ?> <employees>
<name>Shyam</name>
<email>shyamjaiswal@gmail.com</e
mail> </employees>
<employees>
<name>Bob</name>
<email>bob32@gmail.com</email>
</employees> <employees>
<name>Jai</name>
<email>jai87@gmail.com</email>
</employees>
```

```json
// json 훨씬 간결함 // dict type과 완전 유사
{"employees":[
{"name":"Shyam"
,
"email":"shyamjaiswal@gmail.com"},
{"name":"Bob"
,
"email":"bob32@gmail.com"},
{"name":"Jai"
,
"email":"jai87@gmail.com"} ]
} 

```

JSON in Python

- json 모듈을 사용하여 손 쉽게 파싱 및 저장 가능
- 데이터 저장 및 읽기는 dict type과 상호 호환 가능
- 웹에서 제공하는 API는 대부분 정보 교환 시 JSON 활용
- 페이스북, 트위터, Github 등 거의 모든 사이트
- 각 사이트 마다 Developer API의 활용법을 찾아 사용

JSON Read
- JSON 파일의 구조를 확인 -> 읽어온 후 -> Dict Type처럼 처리

JSON Data
```
{"employees":[
{"firstName":"John", "lastName":"Doe"},
{"firstName":"Anna", "lastName":"Smith"},
{"firstName":"Peter", "lastName":"Jones"}
]}
```

```
import json
with open("json_example.json", "r", encoding="utf8") as f:
contents = f.read()
json_data = json.loads(contents)
print(json_data["employees"])
```

JSON Write
- Dict Type으로 데이터 저장 -> josn모듈로 Write

```
import json
dict_data = {'Name': 'Zara','Age': 7,'Class': 'First'}
with open("data.json","w") as f:
  json.dump(dict_data, f)
```

```
import json
dict_data = {'Name': 'Zara','Age': 7, 'Class': 'First'}
with open("data.json","w") as f:
  json.dump(dict_data, f)
```


---

## 피어세션 정리

- 팀원들과 과제 리뷰
- 팀원들과 세미나 진행 계획 세움

---

## 과제 진행 상황 정리/과제 결과물에 대한 정리

- 학습정리 공간을 깃허브 블로그로 결정하고 현재 만드는 중! (마크다운 소스는 준비됨!)
- 오늘 학습정리는 주말에 날잡고 실습 한번 다시 해야할거같아서 일단 대충 정리했음

---

## 오늘의 한마디

- 밤새기 금지...