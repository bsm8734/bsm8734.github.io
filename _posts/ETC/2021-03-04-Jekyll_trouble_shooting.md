---
title: "[ETC] Github pages Trouble Shooting"
data: 2021-01-20 20:30:00 +0800
categories: [ETC, Ubuntu]
tags: [TroubleShooting, Ubuntu]
---


## Trouble Shooting

---

### 어제까지 잘 되던 빌드가 안될 때

오늘 정말 깃헙페이지 포기할 뻔 했다.  
오늘 올린 포스트들이 오류가 있길래, 다시 저장소를 이전으로 되돌렸는데, 어떻게 해도 빌드오류가 해결이 안되는 문제가 있었다.  

#### 에러

- `LoadError: libffi.so.6: cannot open shared object file: No such file or directory - /home/runner/vendor/bundle/ruby/2.7.0/gems/ffi-1.14.2/lib/ffi_c.so`

![error_log](/assets/img/sources/2021-03-04-02-02-20.png)

---

#### 해결과정

- 여기가 제일 의심스러워서 `LoadError: libffi.so.6` 검색해봤다.
- [여기](https://gitmemory.com/ffi)에 적혀있는 바, Ubuntu 20.04에서 ffi 실행에 문제가 있음을 호소하는 사람들이 있었다.
- Github Actions Tab에서 그냥 지나쳤던 warning... 
    ![github_warning](/assets/img/sources/2021-03-04-02-13-36.png)
- 그리고 빌드 코드를 살펴보니, 아래와 같은 코드를 발견!
  - 위치: `.github/workflows/pages-deploy.yml`
    <img src="/assets/img/sources/2021-03-04-02-14-37.png" width="40%">

---

#### 해결

- ubuntu version을 latest로 두지 말고, 잘 되던 version으로 fix 해놓자.
    <img src="/assets/img/sources/2021-03-04-02-11-58.png" width="40%">
