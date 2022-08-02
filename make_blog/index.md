# 블로그를 만들어보자


# Hugo를 이용해 블로그를 만들어보자

```text
먼저, 개발 의지력과 도움을 준 Minwook Jae
감사합니다.
```

이직 후에 내 개발 블로그를 만들어야지, 만들어야지 하다가 가장 개발자로서 존경하는 전회사 동기의 한 마디와 포스팅 덕에 시작하게 되었다. 많은 github.io 블로그에 사용된 `Jekyll` 를 사용할까 했었으나, 무엇보다 `Hugo`를  선택한 이유는, 리스펙하는 동료가 사용해서라는 단순한 이유였다. 현재 블로그에는 개발관련 공부 내용과 정리, 업무 내용을 포스팅 예정이고, 나의 관심사, 취미, 일상은 현재 운영 중인 티스토리에 분할하여 운영하려고 한다.





## 1. 환경설정

- ### Hugo 설치

```shell
# hugo install
$ brew install hugo
# check
$ hugo version
```

### 

- ### Github 리포 생성

​		Github.io 리포에 바로 만들어도 되겠지만, 템플릿과 `Hugo`를 이용해 만들려면 아래 두 개 리포를 만들어둔다.(`blog`의 이름은 자유)

​		`blog`

​		`<github name>.github.io`



* ### Hugo 프로젝트 생성

```shell
# hugo 프로젝트 생성
$ hugo new site blog
# 생성 완료되면 출력 문구
Congratulations! Your new Hugo site is created in /Users/user/Workspaces/blog.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
```

