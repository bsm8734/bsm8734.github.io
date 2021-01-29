---
title: "[부스트캠프 AI Tech / Day2] 파이썬 List"
date: 2020-01-19 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python] # Python
tags: [Python] # CS, 운영체제, Python
---


## **[DAY 2] List/Array**

---

### **List**

- 시퀀스 자료형, 여러 데이터들의 집합(데이터 구조)
- int, float 같은 다양한 자료형을 담을 수 있음
- 많은 데이터를 효율적으로 관리할 수 있음
- list 특징, 기능
  - 인덱싱
  - 슬라이싱
  - 다양한 연산
  - 다양한 Data Type이 하나의 리스트에 들어갈 수 있음

<br/>

### **Indexing (인덱싱)**

- list에 있는 값들은 주소(offset)를 가짐
- 주소를 사용해 할당된 값(element)을 호출
- `len(배열)`: 배열의 길이 리턴
  
  ```python
  colors = ['red', 'blue', 'green']
  print (colors[0]) # red
  print (colors[2]) # green
  print (len(colors)) # 3
  # len은 list의 길이를 반환
  ```

<br/>

### **슬라이싱 slicing**

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

<br/>

### **리스트 연산**

- concatenation, is in, 연산 함수들
- 추가/삭제
  - append, extend, insert, remove, del 등 활용
  
  ```bash
    # 슬라이싱과 추가/삭제 연산

    >>> color = ['red', 'blue', 'green']
    >>> color2 = ['orange', 'black', 'white']
    >>> print (color + color2)            # 두 리스트 합치기 # 값은 저장되지 않음
    >>> total_color = color + color2      # concatenate는 저장까지 해줘야함

    >>> len(color)                        # 리스트 길이

    # 추가
    >>> color.append("white")             # 리스트에 "white" 추가       / 변화 O
    >>> color.extend(["black","purple"])  # 리스트에 새로운 리스트 추가 / 변화 O
    >>> color.insert(0,"orange")          # 0번째 주소에 "orange" 추가
    >>> print (color)
    # ['orange', 'yellow', 'blue', 'green', 'white', 'black', 'purple']
    >>> print (color * 2)                 # color 리스트 2회 반복
    # ['orange', 'red', 'blue', 'green', 'white', 'black',
    #    'purple', 'orange', 'red', 'blue', 'green', 'white', 'black', 'purple']

    # 변경
    >>> color[0] = 'yellow'               # 0번째 리스트의 값을 변경

    # 리스트에 특정 값이 있는지 체크
    >>> 'blue' in color2                  # 리스트 color2에 문자열 'blue'가 있는지, 존재 여부 반환
    >>> item in list                      # 리스트에 아이템이 있는지 확인 (있으면 True)
    >>> item not in list                  # 리스트에 아이템이 없는지 확인 (없으면 True)

    # 삭제
    >>> color.remove("white")             # 리스트에 "white" 삭제       / 변화 O
    >>> del color[0]                      # 0번째 주소 리스트 객체 삭제 / 변화 O (메모리를 날림)
  ```

<br/>

### **메모리 저장 방식**

- 파이썬은 해당 리스트 변수에는 리스트 주소값이 저장됨
- `a = b`라고 선언하는 순간 두 변수는 같은 주소값을 저장
  - 따라서, 값을 변화시켰다면 ➡ 두 변수에 변화한 내용이 적용됨
- **`b = a[:]`라고 선언해야 값을 복사**함

  ```bash
    >>> a = [5, 4, 3, 2, 1]
    >>> b = [1, 2, 3, 4, 5]

    >>> b = a       # a와 b가 같은 주소를 가리킴
    >>> print (b)
    # [5, 4, 3, 2, 1]
    
    >>> sorted(a)   # 스스로 변화하지 않음    # [5, 4, 3, 2, 1]
    >>> a.sort()    # 스스로 변화하는 함수   # [1, 2, 3, 4, 5]

    >>> print (b)
    # [1, 2, 3, 4, 5]

    >>> b = [6,7,8,9,10]
    >>> print (a, b)
    # [1, 2, 3, 4, 5] [6, 7, 8, 9, 10]

    # 데이터(값)을 복사하여 가져오는 것(두 변수가 메모리를 따로 사용)
    >>> b = a[:]
  ```

<br/>

### **패킹과 언패킹**

- 패킹 : 한 변수에 여러 개의 데이터를 넣는 것
  - `t = [1, 2, 3]`
- 언패킹 : 한 변수의 데이터를 각각의 변수로 반환
  - `a, b, c = t`
  
  ```python
    t = [1, 2, 3]
    a, b, c = t

    print(t, a, b, c) # [1, 2, 3] 1 2 3
  ```

<br/>

### **이차원 리스트**

- 리스트 안에 리스트를 만들어 행렬(Matrix) 생성
- 이차원 리스트의 *복사*
  - 이차원 리스트의 경우, `a = b[:]` 불가능
  - `import copy`
  - `copy.deepcopy(변수)`

  ```Python
  kor_score = [49,79,20,100,80]
  math_score = [43,59,85,30, 90]
  eng_score = [49,79,48,60,100]
  midterm_score = [kor_score, math_score, eng_score]
  
  print (midterm_score[0][2]) # 20

  copy.deepcopy(midterm_score) # 이차원 배열 복사
  ```
