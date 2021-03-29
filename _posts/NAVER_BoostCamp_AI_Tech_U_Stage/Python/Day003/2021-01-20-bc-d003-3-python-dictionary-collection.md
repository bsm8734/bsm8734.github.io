---
title: "[부스트캠프 AI Tech / Day3] 파이썬 Dictionary & Collection"
data: 2021-01-20 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python]
tags: [Python]
---


## **[DAY 3] Dictionary**

---

### **사전 (dictionary)**

- 데이터를 저장 할 때는 구분 지을 수 있는 값을 함께 저장
- 구분을 위한 데이터 고유 값을 Identifier 또는 Key 라고함
- Key 값을 활용하여, 데이터 값(Value)를 관리함
- key와 value를 매칭하여 key로 value를 검색
- 다른 언어에서는 Hash Table 이라는 용어를 사용
- {Key1:Value1, Key2:Value2, Key3:Value3 ...} 형태

    ```python
    student_info = {20140012:'Sungchul', 20140059:'Jiyong',20140058:'JaeHong'}
    student_info[20140012]
    student_info[20140012] = 'Janhyeok'
    student_info[20140012]
    student_info[20140039] = 'wonchul'
    student_info

    >>> country_code = {} # Dict 생성, country_code = dict() 도 가능
    >>> country_code = {＂America＂: 1, ＂Korea＂: 82, ＂China＂: 86, ＂Japan＂: 81}

    >>> country_code
    # {＇America＇: 1, ＇China＇: 86, ＇Korea＇: 82, ＇Japan＇: 81}

    >>> country_code.items() # Dict 데이터 출력
    # Dict_items([(＇America＇, 1), (＇China＇, 86), (＇Korea＇, 82), (＇Japan＇, 81)])

    >>> country_code.keys() # Dict 키 값만 출력
    # Dict_keys(["America", "China", "Korea", "Japan"])

    >>> country_code["German"]= 49 # Dict 추가
    >>> country_code
    # {'America': 1, 'German': 49, 'China': 86, 'Korea': 82, 'Japan': 81}

    >>> country_code.values() # Dict Value만 출력
    # dict_values([1, 49, 86, 82, 81])

    >>> for k,v in country_code.items():
        print ("Key : ", k)
        print ("Value : ", v)
      
    '''
    Key : America
    Value : 1
    Key : Gernman
    Value : 49
    Key : China
    Value : 86
    Key : Korea
    Value : 82
    Key : Japan
    Value : 81
    '''

    >>> "Korea" in country_code.keys() # Key값에 "Korea"가 있는지 확인
    # True
    >>> 82 in country_code.values() # Value값에 82가 있는지 확인
    # True
    ```

### **OrderedDict**

- collections - OrderedDict
- Dict와 달리, 데이터를 입력한 순서대로 dict를 반환함
- 그러나 dict도 python 3.6 부터 입력한 순서를 보장하여 출력함
- Dict type의 값을, value 또는 key 값으로 정렬할 때 사용 가능

    ```python
    from collections import OrderedDict

    d = OrderedDict()
    d['x'] = 100
    d['y'] = 200
    d['z'] = 300
    d['l'] = 500

    for k, v in d.items():
    print(k, v)

    for k, v in OrderedDict(sorted(d.items(), key=lambda t: t[0])).items():
        print(k, v)
    for k, v in OrderedDict(sorted(d.items(), key=lambda t: t[1])).items():
        print(k, v)
    ```

### **defaultdict**

- collections - defaultdict
- Dict type의 값에 기본 값을 지정, 신규 값 생성시 사용하는 방법

    ```python
    from collections import defaultdict

    d = defaultdict(object) # Default dictionary를 생성
    d = defaultdict(lambda: 0) # Default 값을 0으로 설정합

    print(d["first"])
    ```

- ex) 하나의 지문에 각 단어들이 몇 개나 있는지 세고 싶은 경우

    ```python
    # Text-mining 접근법 - Vector Space Model
    text = """A press release is the quickest and easiest way to get free publicity. If well written, a press rv elease can result in multiple published articles about your firm and its products. And that can mean new prospects contacting you asking you to sell to 
    them. ….""".lower().split()
    # print(text) # ['a', 'press', ...]

    from collections import OrderedDict

    word_count = defaultdict(lambda: 0) # Default 값을 0으로 설정합
    for word in text:
        word_count[word] += 1
    for i, v in OrderedDict(sorted( word_count.items(), key=lambda t: t[1], reverse=True)).items():
        print(i, v)
    ```

- ex) command analyzer
  
    ```python
    import csv

    def getKey(item): # 정렬을 위한 함수
        return item[1] # 신경 쓸 필요 없음

    command_data = [] # 파일 읽어오기
    with open("command_data.csv", "r") as csvfile:
        spamreader = csv.reader(csvfile, delimiter=',', quotechar='"')
        for row in spamreader:
            command_data.append(row)
    command_counter = {} # dict 생성, 아이디를 key값, 입력줄수를 value값
    for data in command_data: # list 데이터를 dict로 변경
        if data[1] in command_counter.keys(): # 아이디가 이미 Key값으로 변경되었을 때
            command_counter[data[1]] += 1 # 기존 출현한 아이디
        else:
            command_counter[data[1]] = 1 # 처음 나온 아이디

    dictlist = [] # dict를 list로 변경
    for key, value in command_counter.items():
        temp = [key,value]
        dictlist.append(temp)
        
    sorted_dict= sorted(dictlist, key=getKey, reverse=True) # list를 입력 줄 수로 정렬
    print (sorted_dict[:100]) # List의 상위 10객값만 출력
    ```
