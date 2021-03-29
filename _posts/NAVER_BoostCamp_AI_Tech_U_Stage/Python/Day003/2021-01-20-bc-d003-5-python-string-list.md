---
title: "[부스트캠프 AI Tech / Day3] 파이썬 (Pythonic) String & List"
data: 2021-01-20 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python]
tags: [Python]
---


## **[DAY 3] (Pythonic) String & List**

---

### Pythonic code

- 파이썬 스타일 코드(코딩 기법)
- 파이썬 특유의 문법을 활용하여 효율적으로 코드를 표현함
- 고급 코드를 작성 할 수록 더 많이 필요해짐
- 타인의 코드에 대한 이해도
- 효율(빠른 속도, 짧은 코드)

---

### **split() & join()**

- **split** 함수
  - string type의 값을 “기준값”으로 나눠서 List 형태로 변환
- **join** 함수
  - String으로 구성된 list를 합쳐 하나의 string으로 반환
  
- ex) split

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
  ```

- ex) join

  ```python
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

### **List Comprehension**

- 기존 List 사용하여 간단히 **다른 List를 만드는 기법**
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
