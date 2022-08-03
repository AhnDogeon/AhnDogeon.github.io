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



- ### 테마 설치

```shell
$ git init
# 브랜치를 main으로 변경
$ git branch -M main
# git remote add origin <YOUR ROOT REPOSITORY>
$ git remote add origin https://github.com/ahndogeon/blog.git
# git submodule add https://github.com/<theme 경로>.git themes/<theme 이름>
$ git submodule add https://github.com/dillonzq/LoveIt.git themes/LoveIt
$ cp themes/hugo-tranquilpeak-theme/exampleSite/config.toml config.toml
```

copy한 config.toml을 내 블로그에 맞게 수정해준다. BaseURL을 수정하고, 각 텍스트를 내 블로그에 맞게 수정해줬다.

이러면 대략적인 베이스 준비는 끝났다. 터미널에서 서버를 실행시켜주고 로컬에서 확인해보자.

```null
$ hugo server 
Start building sites …
hugo v0.89.4+extended darwin/amd64 BuildDate=unknown

                   | EN-US
-------------------+--------
  Pages            |     9
  Paginator pages  |     0
  Non-page files   |     0
  Static files     |     4
  Processed images |     0
  Aliases          |     1
  Sitemaps         |     1
  Cleaned          |     0

Built in 9 ms
Watching for changes in /Users/user/workspace/blog/{archetypes,content,data,layouts,static,themes}
Watching for config changes in /Users/user/workspace/blog/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```



## 2. Git 리포 연결 및 간편 배포 스크립트 작성

`blog`에 `Github blog`, `blog/public`에 `Github <username>.github.io`를 연결한다.

```shell
# blog -> blog 레포지토리 연결
# git remote add origin http://github.com/<username>/blog.git
$ git remote add origin https://github.com/ahndogeon/blog.git

# blog/public -> <username>.github.io 연결
# git submodule add -b main http://github.com/<username>/<username>.github.io.git public
$ git submodule add -b main http://github.com/ahndogeon/ahndogeon.github.io.git public
```



배포는 역시 ``deploy.sh`` 로 간편하게 하는 것이 최고다.
**blog/deploy.sh**

```null
#!/bin/sh

# If a command fails then the deploy stops
set -e
printf "\033[0;32mDeploying updates to GitHub...\033[0m\n"

printf "\033[0;32mBuild the project.\033[0m\n"
hugo -D
# hugo -t timeline # if using a theme, replace with `hugo -t <YOURTHEME>`


printf "\033[0;32m  Go To Public folder \033[0m\n"
cd public


printf "\033[0;32m  Setting for submodule commit \033[0m\n"
git config --local user.name "#######"
git config --local user.email "######"
git submodule update --init --recursive


printf "\033[0;32m  Add changes to git. \033[0m\n"
git add .

printf "\033[0;32m  Commit changes.. \033[0m\n"
msg="rebuilding site $(date)"
if [ -n "$*" ]; then
	msg="$*"
fi
git commit -m "$msg"

printf "\033[0;32m  Push blog(presentation) source and build repos. \033[0m\n"
git push origin main


printf "\033[0;32m  Come Back up to the Project Root \033[0m\n"
cd ..
echo $pwd

printf "\033[0;32m  root repository Commit & Push. \033[0m\n"
git add .

msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi

git commit -m "$msg"

git push origin main
```

터미널에서 chmod 파일 권한을 주고 실행하면?

```null
# deploy.sh 실행 파일 권한 부여
$ chmod 777 deploy.sh

# 배포 실행
$ ./deploy.sh
```

커피 한 잔 하고 오면 `https://ahndogeon.github.io` 에서 나만의 블로그를 볼 수 있다.

앞으로도 포스팅 후에는 ``./deploy.sh`` 명령어 하나로 배포할 수 있다.

블로그가 어느 정도 활성화되면 ``google adsense`` 를 추가해야겠다.

## 3. 정리하며.

간단한 블로그 배포에도 결국 트러블 슈팅에 시간을 꽤 잡아먹었다. 우선 빠르게 두 가지 ``개발 블로그 배포``, ``입사 후 지금까지 플젝 정리`` 가 필요하여, 동기의 추천 테마를 사용해 빠르게 배포하였다. 조금의 시간과 의지가 허락한다면, 테마가 아닌 AtoZ로 개발하고 싶긴하다.(언제가 될지..) 사실 지금까지 개발자로 지내며, 공유하고 싶은 내용이 산더미다. 그것부터 진행하고 싶다. 부서 특성 상 좋은 기회로 여러 프로젝트를 할 수 있었다. 게임 개발, 람다 활용한 API 서버 개발, 개인적으로 진행한 사이드 프로젝트도 한 번 정리하는 시간을 가져야겠다.

