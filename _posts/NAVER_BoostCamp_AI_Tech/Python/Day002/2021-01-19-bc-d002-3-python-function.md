---
title: "[부스트캠프 AI Tech / Day2] 파이썬 Function"
date: 2020-01-19 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python]
tags: [Python]
---


## **[DAY 2] Function**

---

### Function(함수)

- 어떤 일을 수행하는 코드의 덩어리
- 코드를 논리적인 단위로 분리
- 반복적인 수행을 용이하게 함
- **캡슐화**: 인터페이스만 알면 타인의 코드 사용할 수 있음
- 함수 수행 순서
  - (1) 함수 부분을 제외한 메인프로그램부터 시작
    - main ➡ func call
  - (2) 함수 호출시 함수 부분을 수행 후 되돌아옴
    - main ⬅ return func

```python
def func(x , y):
    return x * y
```

### 함수 선언

- 함수이름, parameter, indentation, return value(optional)

```python
def 함수_이름 (parmaeter1,…,):  # def name(input):
  수행문 #1(statements)         # 앞 indentation 필요
  수행문 #2(statements)
  return <반환값>
```

### parameter vs argument

- **parameter**: 함수의 입력 값 인터페이스
  - 함수 선언시 input을 지칭하는 것
  - `def func(**x, y**)`
- **argument**: 실제 parameter에 대입된 값
  - 함수를 호출할 때 input에 넣어주는 값
  - `func(**x, y**)`

### 함수 형태

- parameter 유무, 반환 값(return value) 유무에 따라 함수의 형태가 다름
- 함수의 반환값이 필요한지, 필요하지 않은지 따져봐야함
- 반환값이 있는지 없는지에 따라 변수 업데이트 여부 나뉠 수 있음
- 보통 리턴값이 있는 경우, 변수 업데이트 필요

  ```python
    >>> sorted(a)   # 스스로 변화하지않음    # [5, 4, 3, 2, 1] (print 함)
    >>> a.sort()    # 스스로 변화하는 함수   # [1, 2, 3, 4, 5] (print 안함)
    
    # 주의 #
    def f(x):
      return print(x + 10)

    >>> f(10)     # 20          # 값을 변경하지 않음
    >>> c = f(10) # 20          # c에 f 함수의 리턴값을 할당 # 함수 return 전에 x+10출력
    >>> c         # 출력없음    # 그러나 return print()
    # => print는 반환형이 없으므로 출력이 없음 !!!
  ```

### Function-scoping Rule

- 변수의 범위(Scoping Rule)
- 변수가 사용되는 범위(함수 또는 메인 프로그램)

- **전역변수 vs 지역변수**
  - **지역변수**(local variable): 함수내에서만 사용
  - **전역변수**(global variable): 프로그램 전체에서 사용
    - 전역변수는 함수에서 사용가능
    - But, 함수 내에 전역 변수와 같은 이름의 변수를 선언하면 새로운 지역 변수가 생김
    - 함수 내에서 전역변수 사용 시 global 키워드 사용

  ```python
    # Scopingn Rule Test
    def calculate(x, y):
      total = x + y # 새로운 값이 할당되어 함수 내 total은 지역변수가 됨
      print ("In Function")
      print ("a:", str(a), "b:", str(b), "a+b:", str(a+b), "total :", str(total))
      return total
    
    a = 5 # a와 b는 전역변수
    b = 7
    total = 0 # 전역변수 total
    print ("In Program - 1")
    print ("a:", str(a), "b:", str(b), "a+b:", str(a+b))
    
    sum = calculate (a,b)
    print ("After Calculation")
    print ("Total :", str(total), " Sum:", str(sum)) # 지역변수는 전역변수에 영향 X

    """
    결과
    In Program -1
    a: 5 b: 7 a+b: 12
    In function
    a: 5 b: 7 a+b: 12 total : 12
    After Calculation
    Total : 0 Sum: 12
    """
  ```

### Function Type Hints

- **Dynamic Typing**
  - Dynamic Typing: 실행 시에 변수의 타입을 정하는 것
  - Type Hints: 사용자가 interface를 알기 어렵다는 단점을 보완하기 위함
  - `def do_function(var_name: var_type) -> return_type:`
  - `def type_hint_example(name: str) -> str` ➡ 이렇게 미리 지정가능

- **Type Hints의 장점**
  1. 사용자에게 인터페이스를 명확히 알려줄 수 있음
  2. 함수의 문서화시 parameter에 대한 정보를 명확히 알 수 있음
  3. mypy 또는 IDE, linter 등을 통해 코드의 발생 가능한 오류를 사전에 확인
  4. 시스템 전체적인 안정성을 확보할 수 있음

- **Function Docstring**

  - 파이썬 함수에 대한 상세 스펙을 사전에 작성하여, 함수 사용자의 이행도를 높이는 것
  - 세개의 따옴표로 docstring 영역표시(함수명 아래)
  - 함수 작성 가이드 라인
  - 함수는 가능하면 짧게 작성할 것 (줄 수를 줄일 것)
  - 함수 이름에 함수의 역할, 의도가 명확히 들어낼 것
  - `동사_목적어`
    - ex) print_hello_world()
  - 하나의 함수에는 유사한 역할을 하는 코드만 포함
  - 인자로 받은 값 자체를 바꾸진 말 것 (임시변수 선언)
  - 함수는 언제 만드는가?
    - 공통적으로 사용되는 코드는 함수로 변환
    - 복잡한 수식 ➡ 식별 가능한 이름의 함수로 변환
    - 복잡한 조건 ➡ 식별 가능한 이름의 함수로 변환

### etc

- **Debugging(디버깅)**
  - 코드의 오류를 발견하여 수정하는 과정
  - 오류의 *원인*을 알고 *해결책*을 찾아야 함
  - *문법적 에러*를 찾기 위한 에러 메시지 분석
  - *논리적 에러*를 찾기 위한 테스트도 중요
  - 문법적 오류 예시
    - 들여쓰기, 오탈자, 대소문자 구분안함
  - 에러 메시지 분석
    - 에러가 발생하면 인터프리터가 알려줌
  - 논리적 에러
    - 뜻대로 실행되지 않는 코드
    - 중간에 프린터 문을 찍어서 확인
    - 함수 확인하기
    - check print문