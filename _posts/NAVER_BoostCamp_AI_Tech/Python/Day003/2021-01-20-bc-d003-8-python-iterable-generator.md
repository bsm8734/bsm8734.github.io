---
title: "[부스트캠프 AI Tech / Day3] 파이썬 Iterable & Generator (수정필요)"
data: 2021-01-20 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python]
tags: [Python]
---


## **[DAY 3] Iterable & Generator**

---

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

---

### generator

- iterable object를 특수한 형태로 사용해주는 함수
- element가 사용되는 시점에 값을 메모리에 반환
- **yield**를 사용해 한번에 하나의 element만 반환함
- **generator comprehension**
  - list comprehension과 유사한 형태로 generator형태의 list 생성
  - generator expression 이라는 이름으로도 부름
  - `[ ]` 대신 `( )` 를 사용하여 표현
- 일반적인 iterator는 generator에 반해 훨씬 큰 메모리 용량 사용
- generator은 언제 사용?
  - list 타입의 데이터를 반환해주는 함수는 generator로 만들기
    - 읽기 쉬운 장점, 중간 과정에서 loop 이 중단될 수 있을 때
  - 큰 데이터를 처리할 때는 generator expression을 고려하기
    - 데이터가 커도 처리의 어려움이 없음
  - 파일 데이터를 처리할 때도 generator를 쓰자!

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
