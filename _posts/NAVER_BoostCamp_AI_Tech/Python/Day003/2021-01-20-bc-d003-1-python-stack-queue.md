---
title: "[부스트캠프 AI Tech / Day3] 파이썬 Stack & Queue"
date: 2020-01-20 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python]
tags: [Python]
---


## **[DAY 3] Stack & Queue**

---

### Python Data Structure

- 특징이 있는 정보를 저장하는 방법
- 파이썬 기본 데이터 구조
  - 스택과 큐(stack & queue with list)
  - 튜플과 집합(tuple & set)
  - 사전(dictionary)
  - Collection 모듈

---

### **스택 (Stack)**

- 나중에 넣은 데이터를 먼저 반환하도록 설계된 메모리 구조
- **Last In First Out (LIFO)**
- Data의 입력을 push, 출력을 pop이라고 함
- 리스트를 사용하여 스택 구조를 구현 가능
- push를 **`append()`**, pop을 **`pop()`**를 사용
- 특이하게도, **pop은 값을 변화하면서, 반환값이 존재**
  - `sort()`: 반환값X, 값변경O
  - `sorted()`: 반환값O, 값변경X
  
```python
# 스택 구조를 활용, 입력된 글자를 역순으로 출력
word = input("Input a word : ") # Input Word
word_list = list(word) # String to List

for i in range(len(word_list)):
    print(word_list.pop()) # 하나씩 빼면서 출력
```

---

### **큐 (Queue)**

- 먼저 넣은 데이터를 먼저 반환하도록 설계된 메모리 구조
- First In First Out (FIFO)
- Stack과 반대되는 개념
- 파이썬은 리스트를 사용하여 큐 구조를 활용
- put를 append(), get을 pop(0)를 사용

```python
>>> a = [1,2,3,4,5]
>>> a.append(10)
>>> a.append(20)
>>> a.pop(0) # 1 출력
# 1
>>> a.pop(0) # 2 출력
# 2
```
