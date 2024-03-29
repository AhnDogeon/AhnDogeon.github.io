# API 서버 구축기 1탄


> FastAPI로 api 서버를 개발하고, 배포해보자

<!--more-->

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

라우터를 설정해주면, 남은건 API를 만들 시간이다. 서버의 주요기능을 작성하는만큼 미리 명세를 잘 짜두고, 기본적인 것이지만 어떤 인자를 써야할지, GET 요청인지, POST 요청인지 등등을 정리해두고 개발하길 추천한다.



가장 먼저, 현재 시간 리턴하는 서버 상태 체크용 GET요청 함수를 만들어줬다. 

**routes/index.py**

```python
@router.get("", include_in_schema=False)
async def index():
    """
    상태 체크용 API
    :return:
    """
    
    current_time = datetime.utcnow()
    return Response(f"server time: {current_time.strftime('%Y.%m.%d %H:%M:%S')})")
```



이후는 명세에 필요한 POST 요청을 하나하나 만들어줘야 하는데, POST인만큼 DB모델링과 schema를 만들어줘야 했다. 해당 경로로 가자

**app/db/models.py**

```python
from sqlalchemy import <사용할 데이터 타입> 
from sqlalchemy.orm import relationship

from .conn import Base
    
class ForExample(Base):
    """
    포스팅을 위한 예시 모델링 클래스다.
    """
    __tablename__ = '<your table name>'
    # # =========================================================================================
    # # 1. 사용할 칼럼들을 모델링 
    # # =========================================================================================
    evntcode = Column(Text, primary_key=True, nullable=False, unique=True)            
    cost = Column(Integer, nullable=False)              
```



간단하게 모델링 예시를 들어봤다. 클래스 안에 칼럼들을 쭉 써주면 되는데, 각 칼럼들에 맞게 타입을 지정해주고, 필요 인자들을 넣어주면 된다. 추후에 적을 것이지만, 내부망으로 들여오는 작업을 진행하면서 이 DB들을 내부망에 맞게 싹 바꿔줘야 했는데, 굉장히 난해한 작업이었다. ~~칼럼명부터 한글이다.~~ 다시 API 코드 작성으로 돌아가자. 아래는 간략한 POST 코드다.

**routes/evntcode.py**

```python
@router.post('/<경로 이름짓기가 은근 힘들다.>')
async def <함수이름도 마찬가지>(request: Request, body: <bodyname>,
                  credentials: HTTPAuthorizationCredentials = Security(security),
                  db: Session = Depends(get_db)):
    """
    POST 요청 예시 \n
    """
    # Authrization Check (Bearer Token)
    # token 인증 외에도 TLS, 보안솔루션 설치 등의 절차가 꼭 필요하다
    # DB update
    result = crud.DB_UpdateFunc(db, body.code)
    
    return result
```



---



## 3. 정리하며

이런 식으로 명세에 맞게 설계한 API들을 쭉 개발해주면 된다. 개발 과정에서 명세 또한 계속해서 바뀌고, 그 과정에서 코드를 수정하며, 조금 더 효율적으로 바꿀 수 있지 않을까? 하며 명세를 자체적으로 수정하여 컨펌 받기도 했다. 포스팅 마지막 탄에 다시 이야기하겠지만, 취업을 준비할 때와 처음 싸피 과정을 진행할 때는 시중에 나와있는 오픈API 만 사용하였는데, 직접 API 서버를 만들어 배포해보니, 내가 썼던 API들에 녹여있는 개발자들의 피땀눈물이 느껴졌다. 이 자리를 빌어 다시 한 번 감사의 인사를 올려야겠다.

다음 포스팅에서는 배포를 위한 AWS 세팅에 관해 포스팅하겠다.

