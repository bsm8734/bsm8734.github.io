---
title: "[ETC] VS code에서 Colab 사용하기 (for Mac M1)"
data: 2021-02-09 02:30:00 +0800
categories: [ETC, Colab]
tags: [Colab, M1_Mac]
use_math: True
---


## **VS code에서 colab 실행**

---

### **Colab**

- 다음의 코드를 실행
  `!pip install colab-ssh --upgrade`
  `from colab_ssh import launch_ssh_cloudflared, init_git_cloudflared`
  `launch_ssh_cloudflared(password="패스워드")`
- **VSCode Remote SSH** 에서 url 복사

### **VS Code**

- ctrl + shift + P
- `Remote-SSH: Connect to Host...` 선택
- url 넣기 ➡ Linux ➡ continue ➡ 비밀번호 입력
- open folder (`/content/drive/MyDrive/Colab Notebooks/`)

---

- [ngrok](https://dashboard.ngrok.com/get-started/setup) 들어가서
  `./ngrok authtoken ( 얻기 )`

```python
NGROK_TOKEN = '토큰' # ngrok 토큰
PASSWORD = '접속할 비밀번호' # 비밀번호 설정

!pip install colab-ssh

from colab_ssh import launch_ssh
launch_ssh(NGROK_TOKEN, PASSWORD)
```