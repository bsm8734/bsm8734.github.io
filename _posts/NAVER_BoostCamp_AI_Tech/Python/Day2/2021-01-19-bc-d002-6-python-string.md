---
title: "[부스트캠프 AI Tech / Day2] 파이썬 String"
date: 2020-01-19 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python] # Python
tags: [Python] # CS, 운영체제, Python
---


## **[DAY 2] String**

---

### 문자열(string)

- 시퀀스 자료형 ➡ 문자형 데이터를 메모리에 저장
- list와 비슷한 구조 ➡ 1byte의 메모리가 순차적으로 나열되어있다고 생각
- 영문 1글자 = 1byte

### 인덱싱(Indexing)

- 문자열의 각 문자는 개별주소(offset)를 가짐 ➡ 이 주소를 사용하여 할당된 값을 가져오는 것이 인덱싱
- list와 같은 형태로 인덱스로 접근하여 데이터를 처리함
- 문자열의 범위를 넘어가는 인덱싱으로 접근하고자하면, 처음/끝을 자동으로 지정
- `str[10]`
- `"Team" in "We Are Team"` 처럼 (앞)이 (뒤)에 들어가있는지 여부를 알 수 있음
- [문자열 함수 참고](https://m.blog.naver.com/PostView.nhn?blogId=hsj2864&logNo=220752261661&proxyReferer=https:%2F%2Fwww.google.com%2F)

### 다양한 문자열 표현

- 두줄 이상 문자열의 저장
  - `\n`: 줄바꿈을 의미하는 특수 문자
  - 큰따옴표 또는 작은 따옴표 세 번 연속 사용

    ```python
    a = """ It’Ok
        I’m Happy.
        See you. """
    ```

---

### **특수 문자**

- 문자열을 표시할 때 백슬래시 `\` 를 사용하여
- 키보드로 표시하기 어려운 문자들을 표현함

#### **raw string**

- 특수문자 특수 기호인 `\` escape 글자를 무시하고 그대로 출력함

  ```python
  raw_string = "이제 파이썬 강의 그만 만들고 싶다. \n 레알"
  print(raw_string)
  # 이제 파이썬 강의 그만 만들고 싶다.
  # 레알

  raw_string = r"이제 파이썬 강의 그만 만들고 싶다. \n 레알"
  print(raw_string)
  # 이제 파이썬 강의 그만 만들고 싶다. \n 레알
  ```

- 예제

  ```python
  f = open("yesterday.txt", 'r')
  yesterday_lyric = ""
  while True:
      line = f.readline()
      if not line:
          break
      yesterday_lyric = yesterday_lyric + line.strip() + "\n"
  f.close()
  
  n_of_yesterday = yesterday_lyric.upper().count("YESTERDAY") # 대소문자 구분 제거
  print ("Number of a Word 'Yesterday'" , n_of_yesterday)
  ```

### call by object reference

- 함수 호출 방식
  - 함수에서 parameter를 전달하는 방식
    1. 값에 의한 호출(Call by Value)
    2. 참조의 의한 호출(Call by Reference)
    3. 객체 참조에 의한 호출(Call by Object Reference)
  - **Call by value**
    - 함수에 인자를 넘길 때, 값만 넘김
    - 함수 내에 인자 값 변경 시, 호출자에게 영향을 주지 않음
  - **Call by Reference (포인터)**
    - 함수에 인자를 넘길 때, 메모리 주소를 넘김
    - 함수 내에 인자 값 변경 시, 호출자의 값도 변경됨

#### **파이썬 함수 호출 방식 – Call by Object Reference**

- 파이썬은 객체의 주소가 함수로 전달되는 방식
- 전달된 객체를 참조하여 변경 시, 호출자에게 영향을 줌
- 새로운 객체를 만들 경우, 호출자에게 영향을 주지 않음

  ```python
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

- swap()
  - 함수를 통해 변수 간의 값을 교환(Swap)하는 함수
  - Call By XXXX를 설명하기 위한 전통적인 함수 예시

  ```python
    # a = [1,2,3,4,5] 일 때 아래 함수 중 실제 swap이 일어나는 함수는?
    
    # 1) value 교환 # X
    def swap_value (x, y):
      temp = x
      x = y
      y = temp
    # 함수의 값을 가리키는 로컬변수 x, y의 주소값만 자꾸 바뀌는 것
    # 실제로 함수 호출자의 데이터는 변경되지 않음
    
    # 2) 주소 교환 # O
    def swap_offset (offset_x, offset_y):
      temp = a[offset_x]
      a[offset_x] = a[offset_y]
      a[offset_y] = temp
    # 값이 바뀜
    # 인덱스에 접근하여 데이터를 변경
    # 리스트 자체에 접근하여 값을 변경하므로, 당연히 바뀌게 됨
    
    # 3) 리스트를 교환 # O
    def swap_reference (list, offset_x, offset_y):
      temp = list[offset_x]
      list[offset_x] = list[offset_y]
      list[offset_y] = temp
    ```

  - swap_offset: a 리스트의 전역 변수 값을 직접 변경
  - swap_reference: a 리스트 객체의 주소 값을 받아 값을 변경

    ```python
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

---

### etc

- **✔ 1byte ?**
  - 1byte의 메모리 공간?
    - 컴퓨터는 2진수로 데이터를 저장
    - 이진수 한 자릿수는 1bit로 저장됨
    - 즉 1bit는 0 또는 1 이므로,
    - `1byte = 8bit = 2^8 = 256`까지 저장 가능

- **✔ ASCII, UTF-8, cp949 ?**
  - 문자를 인식하는 방법
  - 컴퓨터는 문자를 직접적으로 인식하지 않음 ➡ 모든 데이터는 이진수로 인식
  - 이를 위해 이진수를 문자로 변환하는 표준 규칙을 정함
  - **cp949, utf-8, ASCII**
  - 이러한 규칙에 따라 문자를 이진수로 변환하여 저장하거나 저장된 이진수를 숫자로 변환하여 표시함

- **✔ 자료형의 크기**
  - 각 타입 별로 메모리 공간을 할당 받은 크기가 다름
  - 메모리 공간에 따라 표현할 수 있는 숫자 범위가 다름
    - **정수형(int)**: 4byte ((-2^(21))~(2^(31)-1))
    - **정수형(long)**: 무제한
    - **실수형(float)**: 8byte ((10^(-308))~(10^(308)))