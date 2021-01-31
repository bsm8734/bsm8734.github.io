---
title: "[부스트캠프 AI Tech / Day5] 파이썬 Data Handling(csv, json)"
date: 2020-01-22 20:30:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python] # Python
tags: [Python] # CS, 운영체제, Python
---


## **[DAY 5] Data Handling**

---

### **Python Data Handling**

- 지금까지 우리가 다룬 데이터: Tableau 데이터
- 우리가 처리하는 데이터 저장 방식들
  - `csv`, 웹(`html`), `xml`, `json`

### **CSV(Comma Seperate Values)**

- CSV, 필드를 쉼표(,)로 구분한 **텍스트 파일**
- 엑셀 양식의 데이터를 **프로그램에 상관없이** 쓰기 위한 데이터 형식이라고 생각하면 쉬움(손쉽게 공유하기 위해서)
  - shell linux와 같은 경우, xlsx보다는 csv는 텍스트이므로 쉽게 처리 가능
  - 엑셀처럼 생긴 텍스트 데이터
- 탭(TSV, Tab Seperate Value), 빈칸(SSV) 등으로 구분해서 만들기도 함
- 통칭하여 character-separated values (CSV) 부름
- 엑셀에서는 “다름 이름 저장” 기능으로 사용 가능

- 엑셀로 CSV 파일 만들기
  - 1) 파일 다운로드 - https://bit.ly/2KGjLxR
  - 2) 파일 열기
  - 3) 파일 → 다른 이름으로 저장
      → CSV(쉼표로 분리) 선택 후 → 파일명 입력
  - 4) 엑셀 종료 후 Notepad로 파일 열어보기
- 데이터가 "," 로 나눠져 있음
- Text 파일 형태로 데이터 처리 예제
- 예제데이터: customer.csv (https://bit.ly/3psoUZb)
- 일반적 textfile을 처리하듯 파일을 읽어온 후, 한줄 한줄씩 데이터를 처리함
- 엑셀은 텍스트 파일로 열면, 이상한 값으로 보임

#### **CSV 파일 읽기 예제**

```python

line_counter = 0 #파일의 총 줄수를 세는 변수
data_header = [] #data의 필드값을 저장하는 list
customer_list = [] #cutomer 개별 List를 저장하는 List

with open ("customers.csv") as customer_data: #customer.csv 파일을 customer_data 객체에 저장
while True:
    data = customer_data.readline() #customer.csv에 한줄씩 data 변수에 저장
    if not data: break #데이터가 없을 때, Loop 종료
    if line_counter==0: #첫번째 데이터는 데이터의 필드
    data_header = data.split(",") #데이터의 필드는 data_header List에 저장, 데이터 저장시 “,”로 분리
    else:
    customer_list.append(data.split(",")) #일반 데이터는 customer_list 객체에 저장, 데이터 저장시 “,”로 분리
    line_counter += 1

print("Header :\t", data_header) #데이터 필드 값 출력
for i in range(0,10): #데이터 출력 (샘플 10개만)
print ("Data",i,":\t\t",customer_list[i])
print (len(customer_list)) #전체 데이터 크기 출력
```

#### **CSV 파일 쓰기 예제**

```python
line_counter = 0
data_header = []
employee = []
customer_USA_only_list = []
customer = None

with open ("customers.csv", "r") as customer_data:
while 1:
    data = customer_data.readline()
    if not data:
    break
    if line_counter==0:
    data_header = data.split(",")
    else:
    customer = data.split(",")
    if customer[10].upper() == "USA": #customer 데이터의 offset 10번째 값
        customer_USA_only_list.append(customer) #즉 country 필드가 “USA” 것만
    line_counter+=1 #sutomer_USA_only_list에 저장
print ("Header :\t", data_header)
for i in range(0,10):
print ("Data :\t\t",customer_USA_only_list[i])
print (len(customer_USA_only_list))

with open ("customers_USA_only.csv", "w") as customer_USA_only_csv:
for customer in customer_USA_only_list:
customer_USA_only_csv.write(",".join(customer).strip('\n')+"\n")
#cutomer_USA_only_list 객체에 있는 데이터를 customers_USA_only.csv 파일에 쓰기
```

#### **CSV 객체로 CSV 처리**

- Text 파일 형태로 데이터 처리시, 문장내에 들어가 있는 "," 등에 대해 전처리과정이 필요
  - 주소와 같은 건 "," 이런게 들어갈 수 있음
  - 이런건 코딩하며 빼줘야 함
- 파이썬에서는 간단히 CSV 파일을 처리하기 위해 csv 객체를 제공함
- 예제데이터: `korea_foot_traffic_data.csv` (from http://www.data.go.kr)
  - 예제데이터는 국내 주요상권의 유동인구 현황 정보
  - 한글로 되어있어 한글처리가 필요
  - 시간대/조사일자/행정구역/날씨등을 기준으로 연령별/성별유동인구가 해당지역에 몇명인지 표시

#### **CSV 객체 활용**

- csv를 window에서 작업하면 자동으로 cp-949로 저장해줌
- vs code에서 열면, utf-8로 열어주기 때문에 초기에 깨져서 나올 수 있음
- 대신 encoding = "cp949"로 바꿔줘도 됨
- 한줄 띄우는 기준: 윈도우: `\n`, 맥: `\r\n`
- `""`으로 데이터를 묶어서 저장함
- **중요**
  - 인코딩에 신경써라 : 윈도우는 cp949일 가능성이 높음
  - 안되면 utf-8로 해보기
  - 웬만하면 utf8로 저장하기
  - delimeter는 데이터를 자르는 기준
  - quotation: 데이터를 싸매는 기준
  - 애매하면 작은 quotatoin mark로 싸주기(그게 데이터에 없다면..)
    ➡ 나중에는 pandas로 처리할 것

```python
import csv
reader = csv.reader(f, delimiter=',', quotechar= '"', quoting=csv.QUOTE_ALL)
# quotechar= '"' # quotation field, level 지정 가능 # 어디서 자르지?에 관련
```

![14](/assets/img/sources/2021-01-31-18-57-57.png)

```python
# 유동인구데이터중성남데이터만수집
import csv
seoung_nam_data = []
header = []
rownum = 0

with open("korea_floating_population_data.csv","r", encoding="cp949") as p_file:
csv_data = csv.reader(p_file) #csv 객체를 이용해서 csv_data 읽기
for row in csv_data: #읽어온 데이터를 한 줄씩 처리
    if rownum == 0:
    header = row #첫 번째 줄은 데이터 필드로 따로 저장
    location = row[7]
    #“행정구역”필드 데이터 추출, 한글 처리로 유니코드 데이터를 cp949로 변환
    if location.find(u"성남시") != -1: # 유니코드의 약자
    seoung_nam_data.append(row)
    #”행정구역” 데이터에 성남시가 들어가 있으면 seoung_nam_data List에 추가
    rownum +=1

with open("seoung_nam_floating_population_data.csv","w", encoding="utf8") as s_p_file:
writer = csv.writer(s_p_file, delimiter='\t', quotechar="'", quoting=csv.QUOTE_ALL)
# ''으로 싸서, tab을 중간에 넣어주겠다는 것
# csv.writer를 사용해서 csv 파일 만들기 delimiter 필드 구분자
# quotechar는 필드 각 데이터는 묶는 문자, quoting는 묶는 범위
writer.writerow(header) #제목 필드 파일에 쓰기
for row in seoung_nam_data:
    writer.writerow(row) #seoung_nam_data에 있는 정보 list에 쓰기
```

~~공공데이터포털~~

---

### **Web**

- 인터넷
- html은 텍스트 덩어리
- 브라우저가 렌더링을 하여 우리에게 보여줌
- World Wide Web(WWW), 줄여서 웹이라고 부름
- 우리가 늘 쓰는 인터넷 공간의 정식 명칭
- 팀 버너스리에 의해 1989년 처음 제안되었으며,원래는 물리학자들간 정보 교환을 위해 사용됨
- 데이터 송수신을 위한 HTTP 프로토콜 사용, 데이터를 표시하기 위해 HTML 형식을 사용

#### **web의 동작**

1. 요청: 웹주소, form, header
2. 처리: Database 처리 등 요청 대응
3. 응답: HTML, XML등 으로 결과 반환
4. 렌더링: HTML, XML 표시

- 웹 상의 정보를 구조적으로 표현하기 위한 언어
- 제목, 단락, 링크 등 요소 표시를 위해 Tag를 사용
  - `<title> </title>`
- 모든 요소들은 꺾쇠 괄호 안에 둘러 쌓여 있음
  - `<title> Hello, World </title> ＃제목 요소, 값은 Hello, World`
- 모든 HTML은 트리 모양의 포함관계를 가짐
- 일반적으로 웹 페이지의 HTML 소스파일은
- 컴퓨터가 다운로드 받은 후 웹 브라우저가 해석/표시

#### **HTML(Hyper Text Markup Language)**

```python
"""
<!doctype html>
<html>
<head>
<title>Hello HTML</title>
</head>
<body>
<p>Hello World!</p>
</body>
</html>
"""
```

#### **HTML 구조**

- `<html> – <head> – <title> – <body> – <p>`
- Element, Attribute Value 이루어짐

```python
"""
<tag attribute1=＂att_value1" attribute2="att_value1 ">
    보이는 내용(Value)
</tag>
"""
```

- 왜 웹을 알아야 하는가?
  - 정보의 보고, 많은 데이터들이 웹을 통해 공유됨
    - 환율정보: https://finance.naver.com/
    - 날씨정보 : http://goo.gl/nwi8WE
    - 미국 특허정보: http://bit.ly/3pxFkjb
  - HTML도 일종의 프로그램, 페이지 생성 규칙이 있음: 규칙을 분석하여 데이터의 추출이 가능
    - 추출된 데이터를 바탕으로 하여 다양한 분석이 가능
- 규칙을 잘 분석하면, 데이터를 분석할 수 있음
  - **HTML 분석 ➡ `string, regex(정규식), beautiful soup`**

#### **정규식 (regular expression)**

- 문자표현공식
- 정규 표현식, regexp 또는 regex 등으로 불림
- 복잡한 문자열 패턴을 정의하는 문자 표현 공식
- 특정한 규칙을 가진 문자열의 집합을 추출
  - `010-0000-0000 ^\d{3}\-\d{4}\-\d{4}$`
  - `203.252.101.40 ^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$ `

- 정규식 for HTML Parsing
  - 주민등록 번호, 전화번호, 도서 ISBN 등 형식이 있는 문자열을 원본 문자열로부터 추출함
  - HTML역시 tag를 사용한 일정한 형식이 존재하여, 정규식으로 추출이 용이함
  - [관련자료](http://www.nextree.co.kr/p4327/)
  - 문법 자체는 매우 방대, 스스로 찾아서 하는 공부 필요
  - 필요한 것들은 인터넷 검색을 통해 찾을 수 있음
  - 기본적인 것을 공부 한 후 넓게 적용하는 것이 중요
  - 공부법
    - 많이 쓰이는 정규식 ➡ ppt 확인
    - [링크](https://zetawiki.com/wiki/%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D_%EC%98%88%EC%8B%9C)
    - 1) 정규식 연습장(http://www.regexr.com/) 으로이동
    - 2) 테스트하고 싶은 문서를 Text란에 삽입
    - 3) 정규식을 사용해서 찾아보기

> `ctrl+f` 로, vs code에서 문자열 규칙을 통해 문자열 다룰 수 있음

##### **정규식 기본 문법 #1**

- 문자 클래스 `[ ]`: `[` 와 `]` 사이의 문자들과 매치라는 의미
- 예) `[abc]` ➡ 해당 글자에 a,b,c중 하나가 있음
- 'a", "before", "deep" , "dud", "sunset"
- “-“를 사용 범위를 지정할 수 있음
- 예) `[a-zA-z]` – 알파벳 전체, `[0-9]` – 숫자 전체

##### **메타 문자**

- [링크](https://wikidocs.net/4308)
- 정규식 표현을 위해 원래 의미가 아닌, 다른 용도로 사용되는 문자

- `. ^ $ * + ? { } [ ] \ | ( )`
- `.`: 줄바꿈 문자인 \n를 제외한 모든 문자와 매치 a[.]b
- `*`: 앞에 있는 글자를 반복해서 나올 수 있음
  - ex) `tomor*ow tomorrow tomoow tomorrrrow`
- `+`: 앞에 있는 글자를 최소 1회 이상 반복
- `{m.n}`: 반복 횟수를 지정 {1,} , {0,} {1,3}
  - ex) `{3}`: 3회 반복, 띄어쓰기도 넣을 수 있음
  - ex) `203.252.101.40 [0-9]{1,3} \d{1,3}`
- `?`: 반복 횟수가 1회
  - ex) `01[01]?-[0-9]{4}-[0-9]{4}`
- `|`: or
  - ex) `(0|1){3} `
- `^`: not
  
> 정규식 추출 연습
> 1) [정규식 연습장](http://www.regexr.com/) 으로이동
> 2) 구글USPTO Bulk Download 데이터 페이지 소스보기 클릭
> 3) 소스 전체 복사 후, 정규식 연습장 페이지에 붙여넣기
> 4) 상단Expression 부분을 수정해가며 "Zip"로 끝나는 파일명만 추출
> 5) Expression에`(http)(.+)(zip)` 를 입력

##### 정규식 in 파이썬

- **re 모듈**을 import 하여 사용: `import re`
- 함수
  - `search()`: 한 개만 찾기
  - `findall()`: 전체 찾기
- 추출된 패턴은 tuple로 반환됨
- 연습 - 특정 페이지에서 ID만 추출하기 [링크](https://bit.ly/3rxQFS4)
- ID 패턴: `[영문대소문자|숫자]` 여러 개, 별표로 끝남
  - `"([A-Za-z0-9]+\*\*\*)"` 정규식

    ```python
    import re
    import urllib.request
    url = "https://bit.ly/3rxQFS4"
    html = urllib.request.urlopen(url)
    html_contents = str(html.read())
    id_results = re.findall(r"([A-Za-z0-9]+\*\*\*)", html_contents)
    #findall 전체 찾기, 패턴대로 데이터 찾기

    for result in id_results:
        print (result)

    #################################################################3
    import urllib.request # urllib 모듈 호출
    import re

    url = "http://www.google.com/googlebooks/uspto-patents-grants-text.html" #url 값 입력
    html = urllib.request.urlopen(url) # url 열기
    html_contents = str(html.read().decode("utf8"))

    # html 파일 읽고, 문자열로 변환
    url_list = re.findall(r"(http)(.+)(zip)", html_contents)
    for url in url_list:
        print("".join(url)) # 출력된 Tuple 형태 데이터 str으로 join
    ```

- 예제) HTML에 쓰이는 정규식

    ```python
    import urllib.request
    import re
    url = "http://finance.naver.com/item/main.nhn?code=005930"
    html = urllib.request.urlopen(url)
    html_contents = str(html.read().decode("ms949"))
    stock_results = re.findall("(\<dl class=\"blind\"\>)([\s\S]+?)(\<\/dl\>)", html_contents)
    samsung_stock = stock_results[0] # 두 개 tuple 값중 첫번째 패턴
    samsung_index = samsung_stock[1] # 세 개의 tuple 값중 두 번째 값
    # 하나의 괄호가 tuple index가 됨
    index_list= re.findall("(\<dd\>)([\s\S]+?)(\<\/dd\>)", samsung_index)
    for index in index_list:
    print (index[1]) # 세 개의 tuple 값중 두 번째 값
    ```

---

### **XML(eXtensible Markup Language)**

- XML이란
  - 데이터의 구조와 의미를 설명하는 TAG(MarkUp)를 사용하여 표시하는 언어
  - TAG와 TAG사이에 값이 표시되고, 구조적인 정보를 표현할 수 있음
  - HTML과 문법이 비슷, 대표적인 데이터 저장 방식
  - 정보의 구조에 대한 정보인 스키마와 DTD 등으로 정보에 대한 정보(메타정보)가 표현되며, 용도에 따라 다양한 형태로 변경가능
  - XML은 컴퓨터(예: PC ↔ 스마트폰)간에 정보를 주고받기 매우 유용한 저장 방식으로 쓰이고 있음
  - - 어떤 필드, 값, 필드 닫고 트리구조를 가지게 됨

- XML 예제

    ```python
    """
    <?xml version="1.0"?>
    <고양이> 
    <이름>나비</이름> <품종>샴</품종> <나이>6</나이> <중성화>예</중성화> <발톱 제거>아니요</발톱 제거>
    <등록 번호>Izz138bod</등록 번호>
    <소유자>이강주</소유자>
    </고양이>
    """
    ```

#### **XML Parsing in Python**

- XML도 HTML과 같이 구조적 markup 언어
- 정규표현식으로 Parsing이 가능함
- 그러나 좀 더 손쉬운 도구들이 개발되어 있음
- 가장 많이 쓰이는 parser인 beautifulsoup으로 파싱

### **BeautifulSoup**

- HTML, XML등 Markup 언어 Scraping을 위한 대표적인 도구
- [링크](https://www.crummy.com/software/BeautifulSoup/)
- lxml 과 html5lib 과 같은 Parser를 사용함
- 속도는 상대적으로 느리나 간편히 사용할 수 있음
    ➡ Wrapping
- 파이썬은 자체적 파서 제공

```python
"""
<?xml version="1.0"?>
<books>
    <book>
    <author>Carson</author>
    <price
    format="dollar">31.95</price>
    <pubdate>05/01/2001</pubdate>
    </book>
    <pubinfo>
    <publisher>MSPress</publisher>
    <state>WA</state>
  </pubinfo>
</books> 

beautifulsoup 설치
- conda 가상 환경으로 lxml과 beautifulsoup 설치

```bash
activate python_mooc
conda install lxml
conda install -c anaconda beautifulsoup4=4.5.1
"""
```

#### **beautifulsoup 모듈 사용**


- 모듈 호출: `from bs4 import BeautifulSoup`
- 객체 생성: `soup = BeautifulSoup(books_xml, "lxml")` - 어떤 파일을 열건지, 어떤 파서로 열건지
- Tag 찾는 함수 find_all 생성: `soup.find_all("author")` - "author" 태그 찾기
- parser : xml을 분석하는 도구

- `find_all`: 정규식과 마찬가지로 해당 패턴을 모두 반환
- `find('invention-title')`
- `Tag 네임 = title`
- `get_text()`: 반환된 패턴의 값 반환 (태그와 태그 사이)

- 이중으로 짜여있는 것은 코드도 이중으로 짜야함
- xml 구조를 알아야함
- 예제는 너무 많으니까 PPT 참고, Google 참고

[참고1](http://goo.gl/aeKMGS), [참고2](http://goo.gl/lKhFzh)

---

### **JSON (JavaScript Object Notation)**

- JSON: JavaScript Object Notation
- 원래 웹 언어인 Java Script의 데이터 객체 표현 방식
- 간결성으로 기계/인간이 모두 이해하기 편함
- 데이터 용량이 적고, Code로의 전환이 쉬움
- 이로 인해 XML의 대체제로 많이 활용되고 있음
- Python의 Dict Type과 유사 ➡ `key:value 쌍`으로 데이터 표시
- ![flickr](/assets/img/sources/2021-01-31-19-24-17.png)

    ```json
    // xml
    <?xml version="1.0" encoding="UTF8" ?> <employees>
    <name>Shyam</name>
    <email>shyamjaiswal@gmail.com</e
    mail> </employees>
    <employees>
    <name>Bob</name>
    <email>bob32@gmail.com</email>
    </employees> <employees>
    <name>Jai</name>
    <email>jai87@gmail.com</email>
    </employees>
    ```

    ```python
    # json 훨씬 간결함
    # dict type과 완전 유사
    """
    {"employees":
        [{"name":"Shyam","email":"shyamjaiswal@gmail.com"},
        {"name":"Bob","email":"bob32@gmail.com"},
        {"name":"Jai","email":"jai87@gmail.com"} ]
    } 
    """
    ```

#### **JSON in Python**

- json 모듈을 사용하여 손 쉽게 파싱 및 저장 가능
- 데이터 저장 및 읽기는 dict type과 상호 호환 가능
- 웹에서 제공하는 API는 대부분 정보 교환 시 JSON 활용
- 페이스북, 트위터, Github 등 거의 모든 사이트
- 각 사이트 마다 Developer API의 활용법을 찾아 사용

##### **JSON Read**

- JSON 파일의 구조를 확인 ➡ 읽어온 후 ➡ Dict Type처럼 처리

##### **JSON Data**

```python
"""
{"employees":[
    {"firstName":"John", "lastName":"Doe"},
    {"firstName":"Anna", "lastName":"Smith"},
    {"firstName":"Peter", "lastName":"Jones"}
]}
""
```

```python
import json
with open("json_example.json", "r", encoding="utf8") as f:
contents = f.read()
json_data = json.loads(contents)
print(json_data["employees"])
```

##### **JSON Write**

- Dict Type으로 데이터 저장 ➡ josn 모듈로 Write

```python
import json
dict_data = {'Name': 'Zara','Age': 7,'Class': 'First'}
with open("data.json","w") as f:
  json.dump(dict_data, f)
```

```python
import json
dict_data = {'Name': 'Zara','Age': 7, 'Class': 'First'}
with open("data.json","w") as f:
  json.dump(dict_data, f)
```
