---
title: "[DataProcessing] sleep()과 implicitly_wait()의 차이"
date: 2021-02-10 20:30:00 +0800
categories: [DataProcessing, ImgCrawling]
tags: [method]
---


## **time.sleep과 driver.implicitly_wait 차이**

---

페이지 로딩을 기다리기 위해서 사용되는 함수인 `time.sleep()`과 `driver.implicitly_wait()`의 차이는 무엇일까?

- `time.sleep()` : 프로세스 자체를 지정한 시간동안 기다려준다. (무조건 지연된다.)
- `implicity_wait()` : 브라우저에서 사용되는 엔진 자체에서 파싱되는 시간을 기다려준다.

---

### **`implicity_wait()`**

- 셀레늄(selenium)에서만 사용하는 특수한 메소드
- `from selenium import webdriver` 필요
- 지정한 시간 이전에 브라우저 파싱이 완료되면, 이후의 시간은 기다리지 않고 바로 다음 코드를 실행한다.
- 지정한 시간을 기다렸는데, 파싱이 끝나지 않으면 에러를 띄우고 바로 종료하게 된다.

---

### **`time.sleep()`**

- `import time` 필요
- 지정한 시간만큼 반드시 기다리고(쉬고) 다음 코드를 실행한다.

---

### **내 생각**

[인스타그램 크롤링 코드](https://github.com/bsm8734/Data-Crawling/blob/main/instagram/instagram-crawling.md)를 짜면서 두 함수의 차이가 궁금해서 알아봤다.

내가 짠 인스타그램 크롤링 코드를 실행시켜보면 종종 오류가 날 때가 있다. 

- 오류: id, pw는 자동으로 입력되지만, 사용자가 로그인 버튼을 눌러야 로그인이 된다. 사용자가 로그인 return key를 누르지 않고 계속 기다리면 오류가 ~~난다.~~ 났었는데, 고쳤다.

그 이유를 추측해보면... "submit 함수를 쓰지 않아서"인 것 같다.

비밀번호를 보내서 입력하고 엔터를 쳐야하는데 해당 코드가 포함되지 않아서 시간초과 오류가 났었던 것으로 보인다. 따라서 엔터(리턴키)를 입력하는 부분을 새로 짜서 붙이고, wait time을 좀 늘렸더니 성공!

implicity_wait()을 통해서 지정한 시간만큼 기다렸는데도 사용자가 로그인 정보를 넘기지 않아서 파싱이 제대로 안된게 아닐까? 이를 토대로, 사용자의 반응이 필요없도록 코드를 수정~~해보고자 한다.~~ 했다.

또한 코드가 searching area?에 원하는 태그 정보를 입력해주는 역할만 하고, 사용자가 태그 리스트 중에서 원하는 태그를 골라야하는데, 이 과정을 없애고 완전 자동으로 크롤링 해줬으면 좋겠다. 어떻게 해결해야할 지 생각해보고 코드를 수정~~해보자.~~ 했다.

✅ **[수정완료](https://github.com/bsm8734/Data-Crawling/blob/main/instagram/instagram-crawling.md)_코드**