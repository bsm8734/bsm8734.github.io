---
title: "[부스트캠프 AI Tech / Day5] 파이썬 Log Handling"
date: 2020-01-22 20:33:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python] # Python
tags: [Python] # CS, 운영체제, Python
---


## **[DAY 5] Log Handling**

---

### **Logging Handling**

- **Logging**: 로그 남기기
- <u>프로그램이 실행되는 동안 일어나는 정보를 기록을 남기기 (현재 상황 기록)</u>
- 유저의 접근, 프로그램의 Exception, 특정 함수의 사용
- Console 화면에 출력, 파일에 남기기, DB에 남기기 등등
- 기록된 로그를 분석하여 의미있는 결과를 도출 할 수 있음
- 실행시점에서 남겨야 하는 기록: 유저분석
- 개발시점에서 남겨야하는 기록: 에러잡기, 디버깅 쉽게하기

### **print vs logging**

- 기록을 print로 남기는 것도 가능함
- 그러나 Console 창에만 남기는 기록은 분석시 사용불가(콘솔창 끄면 사용 불가)
- 때로는 레벨별(개발, 운영등... 어떤 레벨에 속하는 지에 따라)로 기록을 남길 필요도 있음
- 모듈별로 별도의 logging을 남길필요도 있음
- 이러한 기능을 체계적으로 지원하는 모듈이 필요함

### **logging 모듈**

- Python의 기본 Log 관리 모듈

    ```python
    import logging
    logging.debug("틀렸잖아!")
    logging.info("확인해")
    logging.warning("조심해!")
    logging.error("에러났어!!!")
    logging.critical ("망했다...")
    ```

### **Logging Level**

- 프로그램 진행 상황에 따라 다른 Level의 Log를 출력함
- 개발 시점, 운영 시점 마다 다른 Log가 남을 수 있도록 지원함
- DEBUG(개발자) > INFO(운영) > WARNING(사용자~) > ERROR > Critical
- Log 관리시 가장 기본이 되는 설정 정보 관리하기 위함

### **Log가 하는 일**

- log는 print가 하는 일과 거의 유사
- debug 개발시 처리 기록을 남겨야하는 로그 정보를 남김
- info 처리가 진행되는 동안의 정보를 알림(프로그램 시작, 종료...)
- warning 사용자가 잘못 입력한 정보나 처리는 가능하나 원래 개발시 의도치 않는 정보가 들어왔을 때 알림.
- 더이상 쓰면 안될때: depreciate
- error 잘못된 처리로 인해 에러가 났으나, 프로그램은 동작할 수 있음을 알림
- critical 잘못된 처리로 데이터 손실이나 더이상 프로그램이 동작할 수 없음을 알림
- 아래와 같이 실제 프로그램을 실행할 때는 여러 설정이 필요
- 데이터 파일 위치, 파일 저장 장소, operation type등
- 이러한 정보를 설정해 줄 방법이 필요

    ```python
    import logging
    logger = logging.getLogger("main") # logger 선언
    stream_hander = logging.StreamHandler() # logger의 output 방법 선언
    logger.addHandler(stream_hander) logger의 # output 등록


    logger.debug("틀렸잖아!")
    logger.info("확인해")
    logger.warning("조심해!") # 여기부터서만 뜬다
    logger.error("에러났어!!!")
    logger.critical("망했다...")

    # logger.setLevel(logging.DEBUG)

    # 이유는 기본 로깅 레벨이 warning 이상이므로..
    # 왜냐면 operation에서 사용자에게 알려주는 레벨

    #####
    import logging

    logger = logging .getLogger("main")
    logging.basicConfig(level = logging.DEBUG) # 기본세팅
    logger.setLevel(logging.INFO) # 레벨 변경 # 3.8 이상 부터는 두개를 함께 써야함

    # 출력을 어디에 할 것인가 : my.log에 해줄 것/append mode
    # steam_handler = logging.FileHandler("my.log", mode="a", encoding="utf=8") 
    # logger.addHandler(steam_handler) 

    logger.debug("틀렸잖아!")
    logger.info("확인해")
    logger.warning("조심해!") # 여기부터서만 뜬다
    logger.error("에러났어!!!")
    logger.critical("망했다...")

    ```

### **Logging 적용하기**

- **Logging formmater**
  - formatter 사용
  - Log의 결과값의 format을 지정해줄 수 있음

    ```python
    """
    formatter = logging.Formatter('%(asctime)s %(levelname)s %(process)d %(message)s')
    2018-01-18 22:47:04,385 ERROR 4410 ERROR occurred
    2018-01-18 22:47:22,458 ERROR 4439 ERROR occurred
    2018-01-18 22:47:22,458 INFO 4439 HERE WE ARE
    2018-01-18 22:47:24,680 ERROR 4443 ERROR occurred
    2018-01-18 22:47:24,681 INFO 4443 HERE WE ARE
    2018-01-18 22:47:24,970 ERROR 4445 ERROR occurred
    2018-01-18 22:47:24,970 INFO 4445 HERE WE ARE
    """
    ```

- **Log config file 사용하여 format 불러오기**

    ```python
    """
    logging.config.fileConfig('logging.conf')
    logger = logging.getLogger()
    """
    ```

- **log의 세팅, 사전에 세팅설정**

    ```python
    """
    [loggers]
    keys=root

    [handlers]
    keys=consoleHandler

    [formatters]
    keys=simpleFormatter

    [logger_root]
    level=DEBUG
    handlers=consoleHandler

    [Handler_consoleHandler]
    class=StreamHandler
    level=DEBUG
    formatter=simpleFormatter
    args=(sys.stdout, )
    """
    ```

    ```python
    logger.info('Open file {0}'.format("customers.csv",))
    try:
        with open("customers.csv", "r") as customer_data:
        customer_reader = csv.reader(customer_data, delimiter=',', quotechar='"')
        for customer in customer_reader:
        if customer[10].upper() == "USA": #customer 데이터의 offset 10번째 값
        logger.info('ID {0} added'.format(customer[0],))
        customer_USA_only_list.append(customer) #즉 country 필드가 “USA” 것만
    except FileNotFoundError as e:
        logger.error('File NOT found {0}'.format(e,))
    ```