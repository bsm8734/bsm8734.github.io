# Jekyll로 블로그 제작

##### 환경

- Windows

##### 지킬(Jekyll)

- 정적 사이트 생성기
- 마크다운 포스트 작성하면 yaml 헤더에 따라서 html 파일 생성
- 깃허브 블로그 생성에 테마 지정가능

---

## 깃허브 블로그 만들기
 
### 1. Github - 새로운 Repository 만들기

- 새로운 repo 만들기!
  - repo 이름은 **`깃허브아이디.github.io`**
- 새로 만들어진 repo를 clone하여 로컬에 저장소 만들기
  - `$ git clone 주소`

### 2. 지킬 테마고르기 & 다운로드

- [지킬테마 고르러가기](http://jekyllthemes.org/) ~~고르기어려웠음~~
- [내가 고른 테마 - Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy/)
- 해당 테마의 github들어가서 download zip ~~fork하면 청포도 안채워진대서...~~
- 다운받은 지킬 테마의 압축풀기
- 테마 zip 내의 모든 파일/폴더(최상위폴더 말고!)를 (1)번에서 생성해놓은 로컬저장소 위치에 복사하기
- 그럼 내 로컬 저장소 안에 .git과 동등한 위치에 여러 파일들이 있을거임(/post, _config.yml, index...)

### 4. _config.yml 변경

- `_config.yml`에서 `url` 같은 내용은 반드시 커스텀하여 채워줘야한다고 함
  - `url = https://깃헙아이디.github.io` 이렇게 채워줘야 함
- github page build error
  - `config.yml` 내용을 제대로 채우지 않으면, build fail 발생! (혹은 잘못수정하면..)

---

### 5. Ruby 설치

- [RubyInstaller 다운로드](https://rubyinstaller.org/downloads/)
  - recommended version이 굵은 글씨로 표시되어서 그냥 그거 선택
- 설치파일 실행(accept, default setting 계속 next, finish 클릭)
- 설치끝나면 프롬프트 열리는데, 1번으로 설치하고, 다음건 enter

### 6. Jekyll 및 패키지 설치(Ruby prompt)

- `Start Command Prompt with Ruby` : 루비 프롬프트 실행
- `gem` 명령어 사용하여 지킬과 필요한 패키지 설치

  ```bash
    > gem install jekyll
    > gem install minima
    > gem install bundler
    > gem install jekyll-feed
    > gem install tzinfo-data
  ```

  ```bash
    > bundler
  ```
  
### 7. 설정 및 실행(Ruby prompt)

- ruby prompt에서 로컬 깃허브 저장소(아까 repo clone한 장소)로 이동
  - `tab` (자동완성) 키가 안먹어서 다 일일히 쳐줘야함
  - 윈도우는 `ls, pwd` 불가능하므로, `DIR` 써서 디렉토리 이름 확인할 수 있음

```bash
  > chcp 65001

  # 초기화
  > jekyll new 깃허브아이디.github.io

  # 로컬에서 실행
  # 사이트를 빌드하고 로컬 서버에 적용
  > bundle exec jekyll serve
```

- 브라우저에서 [http://127.0.0.1:4000/](http://127.0.0.1:4000/) 접속해보기
  - 만약 테마를 받을때 봤던 `테마 데모`와 비슷/똑같이 생겼다면 성공!
  - 이거 없이 뒤로 넘어가지 말자..

### 8. 초기화 및 설정(Git)

Chirpy Theme의 README(tutorial) 내용 참고
- 로컬저장소 위치에 가서 `tools/init.sh` 실행 
  - init.sh를 실행하면 .travis.xml과 _post폴더의 문서와 docs폴더가 삭제되는 것을 확인할 수 있음
  - `init.sh` 전/후로 `ls` 명령어 찍어서 파일 비교해보기!
- add-commit-push

```bash
  $ git add --all
  $ git commit -m "initialize"
  $ git push -u origin master
```

- 초기화, 푸시 다 끝내고, 조금 인내심을 가지고... **기다리면** 깃허브에 gh-pages라는 브랜치가 생김
- setting에 가서 `gh-pages 브랜치`를 `publishing source`로 지정하기
  - `/(root)`는 그대로 놔두고!
- `save` 버튼 누르기

8번 과정을 제대로 거치지 않은 상태의 블로그 상태는 거의 백지에 가까울 것  
(색이 하나도 안들어가고, 목차, 카테고리도 없을것임)

> 시간이 꽤 걸리니, 마음의 평화를 가지고 천천히 기다리자...
> 저 gh-pages 브랜치가 빨리 안만들어져서 오류인줄알고 10번 다시 했다...
> 정적사이트라 그런지 오래걸린다고한다...
> [http://127.0.0.1:4000/](http://127.0.0.1:4000/) 와 "https://깃허브아이디.github.io" 와 "테마의 데모 페이지"가 똑같이 보이면 성공!

---

### 에러 발생시 참고 사이트

- [GitHub pages Build Failed](https://velog.io/@shg4821/%EA%B9%83%ED%97%88%EB%B8%8C-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0-1.5)
- [GitHub pages Build Failed - github docs 공식사이트(영어)](https://docs.github.com/en/github/working-with-github-pages/about-jekyll-build-errors-for-github-pages-sites)
- [Bundler::GemNotFound](https://m.blog.naver.com/PostView.nhn?blogId=cyydo96&logNo=221588642260&proxyReferer=https:%2F%2Fwww.google.com%2F)
  -  요약) ruby prompt에서 `bundler` 입력 후 엔터 누르기
  -  ~~install시, exe 형태로 받고, 실제로 실행시키지 않아서 생기는 문제라고 추측됨 => 실행시켜주면 해결!~~
- [Gem::LoadError](https://kwonsoonwoo.github.io/etc/2018/09/03/jekyll-serve-%EC%97%90%EB%9F%AC-%ED%95%B4%EA%B2%B0.html)
  - 요약) ruby prompt에서 `bundle exec jekyll server` 입력 후 엔터 누르기
- [jekyll docs](https://jekyllrb-ko.github.io/docs/)

- **[참고사이트 - Github page 만드는 방법](https://yoon6.github.io/posts/make-github-pages/#%EC%B4%88%EA%B8%B0%ED%99%94-%EC%B4%88%EA%B8%B0%EC%84%A4%EC%A0%95)**