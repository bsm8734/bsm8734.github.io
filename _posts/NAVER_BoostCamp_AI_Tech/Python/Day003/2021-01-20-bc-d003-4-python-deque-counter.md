---
title: "[부스트캠프 AI Tech / Day3] 파이썬 Deque & Counter"
data: 2021-01-20 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python]
tags: [Python]
---


## **[DAY 3] Deque & Counter**

---

### deque

- collections - deque
- Stack과 Queue를 지원하는 모듈
- 효율적 메모리 구조로 처리 속도 향상
- List에 비해 **효율적이고 빠른 자료 저장 방식**을 지원함
- **기존 list 형태의 함수를 모두 지원**
- rotate, reverse등 Linked List의 특성을 지원함

```python

from collections import deque

deque_list = deque()
for i in range(5):
    deque_list.append(i)
print(deque_list)
deque_list.appendleft(10)
print(deque_list)

deque_list.rotate(2)
print(deque_list)
deque_list.rotate(2)
print(deque_list)
print(deque(reversed(deque_list)))

deque_list.extend([5, 6, 7])
print(deque_list)
deque_list.extendleft([5, 6, 7])
print(deque_list)

#deque
from collections import deque
import time

start_time = time.clock()
deque_list = deque()
# Stack
for i in range(10000):
    for i in range(10000):
        deque_list.append(i)
        deque_list.pop()
print(time.clock() - start_time, "seconds")

# general list
import time
start_time = time.clock()
just_list = []
for i in range(10000):
    for i in range(10000):
        just_list.append(i)
        just_list.pop()
print(time.clock() - start_time, "seconds")

```

### **Counter**

- collections - Counter
- Sequence type의 data element들의 갯수를 dict 형태로 반환
- Dict type, keyword parameter 등도 모두 처리 가능
- Set의 연산들을 지원함
- word counter의 기능도 손쉽게 제공함

> collections 모듈의 Counter 클래스는 파이썬의 기본 자료구조인 Dictionary를 확장하고 있기 때문에, 사전에서 제공하는 API를 그대로 다 시용할 수가 있음

- 내부 데이터의 개수를 셀 때 사용

    ```python
    from collections import Counter

    Counter('hello world') 
    # Counter({'l': 3, 'o': 2, 'h': 1, 'e': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})
    ```

- `most_common()`: 데이터의 개수가 많은 순으로 정렬된 배열을 리턴

    ```python
    from collections import Counter

    Counter('hello world').most_common() 
    # [('l', 3), ('o', 2), ('h', 1), ('e', 1), (' ', 1), ('w', 1), ('r', 1), ('d', 1)]
    ```

- 메서드의 인자로 숫자 K를 넘기면 그 숫자 만큼만 리턴
- 가장 개수가 많은 K개의 데이터를 얻을 수 있음

    ```python
    from collections import Counter

    Counter('hello world').most_common(1) # [('l', 3)]
    ```
