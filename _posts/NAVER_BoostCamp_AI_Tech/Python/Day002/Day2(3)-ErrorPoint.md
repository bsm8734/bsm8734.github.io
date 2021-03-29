
<details markdown="1"> <summary> ✔ 좋은 코드를 작성하는 방법 </summary>

- 코딩은 팀플
- 사람을 위한 코드
- 사람의 이해를 돕기 위해 규칙이 필요(규칙-코딩 컨벤션)
- 파이썬 코딩 컨벤션
  - 명확한 규칙은 없음
  - 때로는 팀마다, 프로젝트마다 따로
  - 중요한 건 일관성!!!
  - 읽기 좋은 코드가 좋은 코드
- 들여쓰기?
  - 들여쓰기는 Tab or 4 Space 논쟁!
  - 일반적으로 4 Space를 권장함
  - 중요한 건 혼합하지 않으면 됨
  - 들여쓰기 공백 4칸을 권장
- 한 줄은 최대 79자까지
- 불필요한 공백은 피함
- `=` 연산자는 1칸 이상 안 띄움
- 주석은 항상 갱신, 불필요한 주석은 삭제
- 코드의 마지막에는 항상 한 줄 추가
- 소문자 l, 대문자 O, 대문자 I 금지
- 함수명은 소문자로 구성, 필요하면 밑줄로 나눔
- `lIO0 = "Hard to Understand"`
- PEP8 – 파이썬 코딩 컨벤션의 기준
- flake8
  - "flake8" 모듈로 체크 – flake8 <파일명>
  - `conda install -c anaconda flake8`
- black
  - 최근에는 black 모듈을 활용하여 pep8 like 수준을 준수
  - `conda install black`
  - `black codename.py` 명령을 사용

</details>
