---
title: "[부스트캠프 AI Tech / Day3] 파이썬 enumerate & zip"
date: 2020-01-20 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python]
tags: [Python]
---


## **[DAY 3] enumerate & zip**

---

- enumerate : list의 element를 추출할 때 번호를 붙여서 추출
- zip : 두 개의 list의 값을 병렬적으로 추출함


### **Enumerate**

- list를 인자로 넘기면 index값을 추가시켜, Dictionary 형식과 같이 만들어줌
- 사용법
  - `enumerate(list)`
  - `enumerate(['a', 'b', 'c'])`
  - `for i, v in enumerate(['a', 'b', 'c']):`
- 결과: `{0: 'a', 1: 'b', 2: 'c'}`

```python
    # enumerate
    >>> for i, v in enumerate(['tic', 'tac', 'toe']):
        print (i, v) # list의 있는 index와 값을 unpacking
    # 0 tic
    # 1 tac
    # 2 toe

    >>> mylist = ['a', 'b', 'c', 'd']
    >>> list(enumerate(mylist)) # list의 있는 index와 값을 unpacking하여 list로 저장
    # [(0, 'a'), (1, 'b'), (2, 'c'), (3, 'd')]

    s1 = 'Artificial intelligence (AI), is intelligence demonstrated by machines, unlike the natural intelligence displayed by humans and animals.'

    >>> {i:j for i,j in enumerate(s1.split())}
    # 문장을 list로 만들고 list의 index와 값을 unpacking하여 dict로 저장

    # {0: 'Artificial', 1: 'intelligence', 2: '(AI),', 3: 'is', 
    #   4: 'intelligence', 5: 'demonstrated', 6: 'by',
    #   7: 'machines,', 8: 'unlike', 9: 'the', 10: 'natural',
    #   11: 'intelligence', 12: 'displayed', 13: 'by', 
    #   14: 'humans', 15: 'and', 16: 'animals.'}
```

### **zip**

- 각 tuple의 같은 index 끼리 묶어서 반환
- 사용법
  - `zip((a1, a2, a3), (b1, b2, b3))`
  - `zip([a1, a2, a3], [b1, b2, b3])`
- 결과: `[a1, b1], [a2, b2], [c1, c2]`

```python
    # zip
    >>> alist = ['a1', 'a2', 'a3']
    >>> blist = ['b1', 'b2', 'b3']
    >>> for a, b in zip(alist, blist): # 병렬적으로 값을 추출
        print (a,b)
    
    # a1 b1
    # a2 b2
    # a3 b3

    >>> a,b,c = zip((1,2,3),(10,20,30),(100,200,300))
    # (1, 10, 100) (2, 20, 200) (3, 30, 300)
    >>> [sum(x) for x in zip((1,2,3), (10,20,30), (100,200,300))]
    # 각 Tuple 같은 index를 묶어 합을 list로 변환
    # [111, 222, 333]
```

```python
    # enumerate & zip 동시 사용 예제
    >>> alist = ['a1', 'a2', 'a3']
    >>> blist = ['b1', 'b2', 'b3']
    >>>
    >>> for i, (a, b) in enumerate(zip(alist, blist)):
        print (i, a, b) # index alist[index] blist[index] 표시
       
    # 0 a1 b1
    # 1 a2 b2
    # 2 a3 b3
```
