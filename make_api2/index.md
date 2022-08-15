# API 서버 구축기 2탄


> FastAPI로 api 서버를 개발하고, 배포해보자 2탄



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



