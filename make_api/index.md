# Make_api


> FastAPI로 api 서버를 개발하고, 배포해보자

title: "Initial Post"
date: 2022-07-28T23:00:00+09:00
lastmod: 2022-07-31T12:13:40+09:00
author: "AhnDogeon"
authorLink: "https://github.com/ahndogeon"
description: "This article shows the basic Markdown syntax and format."
draft: false
tags: ["Markdown", "HTML"]
categories: ["Markdown"]
lightgallery: true
featuredImage: "/images/first_post.png"

2021년 상반기에 만들었던 로블록스 게임과 연계해서 이벤트를 해보자는 협업 요청이 들어왔다. 외부앱에서 들어오는 요청에 대한 응답을 해주는 서버 개발이 필요했고, 오픈 일정이 매우 촉박했기에 `FastAPI`로 빠르게 개발하는 것이 좋다는 판단을 했다.

이번 장에서는 `FastAPI` 개발 내용을 정리하고, DB연동과 서버 배포에 대한 내용을 차례로 정리할 계획이다. 

당연하게도 사내 프로젝트인만큼 블로그에서는 상세한 구축법, 코드, 아키텍처를 제외한, 트러블슈팅 내용, 개발 고민, 과정, 간단 코드 위주로 포스팅을 하겠다.



## 서버 스펙 명세

- 버전관리시스템 : Git - GitLab
- API 설계 원칙 : REST API
- 직렬화 포맷 : JSON
- 사용자 인증 : Authorization 헤더
- 인증 스키마 : Bearer + token (Lambda Authorizer 사용)
- 언어 + 웹 프레임워크 : Python + FastAPI
- 컴퓨팅 서비스 : AWS Lambda (ap-northeast-2, seoul)
- 배포 라이브러리 : Mangum (zappa는 FastAPI 지원안함)
- 게이트웨이 : AWS API Gateway
- 데이터베이스 : ~~AWS RDS PostgreSQL(엔진) + sqlalchemy(orm)~~ >>> mysql + sqlalchemy(orm) 
  - **개발 초기 내부망이 아닌 외부망에서 진행 계획이었던 프로젝트라, postgre를 사용하였는데, 개발 도중 내부망으로 들여와야 했다.**



---



## 1. 환경설정

- #### FastAPI 설치

```bash
 $ pip install fastapi
 $ pip install uvicorn
```

- #### main.py 작성

  - `mangum` 이나, `uvicorn`   등 기타 필요한 사항들을 상단에 import 시켜줘야 한다.

```python
app = FastAPI(
    title="<server name>",
    description="<server description>",
    default_response_class=JSONResponse,
)

# 라우터 정의
# 라우터 디렉토리를 두 개로 나누어줬다.
app.include_router(index.router, prefix="/v1")
app.include_router(evntcode.router, prefix="/v1")
```



## 2. API 코드 작성




