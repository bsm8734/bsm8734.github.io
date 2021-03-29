---
title: "[부스트캠프 AI Tech / Day3] 파이썬 lambda & map & reduce(수정필요)"
data: 2021-01-20 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python]
tags: [Python]
---


## **[DAY 3] lambda & map & reduce**

---

### Lambda

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

---

### map function

- 두 개 이상의 list에도 적용 가능함
- if filter도 사용 가능
- python3는 iteration을 생성 ➡ list을 붙여줘야 list 사용가능
- 실행시점의 값을 생성, 메모리 효율적
  - python3 는 iteration을 생성 ➡ list을 붙여줘야 list 사용가능
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

---

### reduce function

- map function과 달리 list에 똑같은 함수를 적용해서 통합

    ```python
    from functools import reduce
    print(reduce(lambda x, y: x+y, [1, 2, 3, 4, 5]))
    ```
