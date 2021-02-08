---
title: "[부스트캠프 AI Tech / Day4] 파이썬 Module & Project"
date: 2020-01-21 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python]
tags: [Python]
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

### **패키지**

- 하나의 대형 프로젝트를 만드는 코드의 묶음
- 다양한 모듈들의 합, 폴더로 연결됨
- `__init__` , `__main__` 등 키워드 파일명이 사용됨
- 다양한 오픈소스들이 모두 패키지로 관리됨

- **Package 만들기**

  1. 기능들을 세부적으로 나눠 폴더로 만듦
  2. 각 폴더별로 필요한 모듈을 구현함
  3. 1차 Test –python shell
  4. *폴더별로* `__init__.py` 구성하기
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

  5. `__main__.py` 파일만들기
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

  6. 실행하기 – 패키지 이름만으로 호출하기

#### **package namespace**

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

<br>

---

### **가상환경** (Virtual Environment)

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

---

#### **Anaconda**

##### **conda 명령어**

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
  - 패키지명: 설치하고자 하는 패키지명 입력
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

  ```python
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
