---
title: "[부스트캠프 AI Tech / Day4] 파이썬 Module & Project"
date: 2020-01-21 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python] # Python
tags: [Python] # CS, 운영체제, Python
---


## **[DAY 4] Module & Project**

- 공개된 코드들의 공통적인 형식은 모듈로 이루어져 있다는 것
- 모듈과 프로젝트로 이루어진 *라이브러리*를 불러와서 쓸 수 있는 기능이 매우 강력
- 남이 만든 프로그램을 쓰는 법: 객체 < 모듈
- 객체가 모듈안에 들어가있음, 모듈은 프로젝트 안에 들어가있음

---

### **모듈과 패키지**

- 모듈은 패키지 안에 들어가있음
- **모듈**: 어떤 대상의 부분 혹은 조각
- **패키지**: 모듈을 모아놓은 단위, 하나의 프로그램
- **프로젝트**: 패키지를 공개한 것

### **모듈**

- 프로그램에서는 작은 프로그램 조각들, 모듈들을 모아서 하나의 큰 프로그램을 개발함
- 프로그램을 모듈화 시키면 다른 프로그램이 사용하기 쉬움
- 남들이 만든 프로젝트를 단위로 가져와 사용하는 경우,
  - "모듈화 된 프로그램을 가져와 사용했다. API를 사용한다."
- Python 내부의 모듈
  - Built-in Module인 Random을 사용, 난수를 쉽게 생성할 수 있음
- <u>파이썬의 Module == py 파일을 의미</u>
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

#### **namespace**

- 모듈을 호출할 때 범위 정하는 방법
- 모듈 안에는 함수와 클래스 등이 존재 가능
- 필요한 내용만 골라서 호출 할 수 있음
- from 과 import 키워드를 사용함
  - `from (  ) import (   )`
- ex)
  - 모듈명을 별칭으로 써서 (Alias 설정하기)

    ```python
    import fah_converter as fah     # fah_converter를 fah라는 이름으로 부름
    print(fah.covert_c_to_f(41.6))  # 그 안에 covert_c_to_f 함수 사용
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

>
- `__pycache__/fah_converter.cpython-38.pyc` 폴더가 새로 생김
- `.pyc` : 컴파일 된 파일
  - python 인터프리터가 해석/컴파일
  - 뒷단에서 돌아가고 있는 프로그램이 파이썬을 쉽게 호출하기 위해 기계어로 번역해서 pycache에 저장
  - 내 폴더를 빠르게 메모리에 로딩하기 위해서 컴파일한 것을 저장
  - 캐시가 생성되면, 자동완성 기능 사용가능

<br>

#### **Built-in Modules**

- 파이썬이 기본 제공하는 라이브러리
- 문자처리, 웹, 수학 등 다양한 모듈이 제공됨
- 별다른 조치없이 import 문으로 활용 가능
- 수 많은 파이썬 모듈은 어떻게 검색할 것인가?
  - 1) 구글 검색
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

<br>

---
