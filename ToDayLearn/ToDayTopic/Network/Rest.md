![restApi](https://gmlwjd9405.github.io/images/network/rest.png)

Rest 란?
---

- "Representational State Transfer” 의 약자
- 자원의 이름으로 구분하여 해당 자원의 상태를 주고 받는 것을 의미
  - 자원의 표현에 의한 전달
    - 사진, 텍스트, 소프트웨어의 모든것
  - 상태의 전달 
    - 데이터가 요청되어지는 시점에서 자원의 상태(정보)를 전달한다.
    - JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다
- HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시

  - 즉, REST는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.
  - 웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여한다.
    - CRUD Operation   
    Create : 생성(POST)  
    Read : 조회(GET)
    Update : 수정(PUT)  
    Delete : 삭제(DELETE)  
    HEAD: header 정보 조회(HEAD)

- (www)월드와이드웹을 그대로 사용하기 때문에 웹의 장점을 그대로 다 활용 할 수 있다.
  - 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.

### 장점

- HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라가 필요 없다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화
- 서버와 클라이언트를 명확하게 구분 할 수 있음

### 단점
- 표준이 존재하지 않는다.
- 사용 할 수 있는 메소드가 4개뿐이다.
- 구형 브라우져는 아직 Get과 Post만을 지원한다.

### Rest의 필요성
- 애플리캐이션과 분리
- 다양한 클라이언트 (안드로이드 아이폰)에서도 웹에 관련된 데이터를 갖기 때문

### Rest의 구성
- 자원 : 모든 자원은 고유의 id를 갖임, 이 자원은 server에서 존재함(ex>board/{id})
- 행위 : 메서드를 의미함(Get,Post,Patch,Put,Delete)
- 표현 : json이나 xml을 통해 일반적으로 전달함.

### REST 특징
- Server-Client(서버-클라이언트 구조)
  >자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다.   
 REST Server: API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.  
 Client: 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다. 
 서로 간 의존성이 줄어든다.


- Stateless(무상태)    
  >HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.  
  Client의 context를 Server에 저장하지 않는다.  
  즉, 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.  
  Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.  
  각 API 서버는 Client의 요청만을 단순 처리한다.  
  즉, 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.  
  물론 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용한다.  
  Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.


- Cacheable(캐시 처리 가능)  
  >웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.  
  즉, HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.  
  HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.   
  대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.   
  캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.
  

- Layered System(계층화)   
  >Client는 REST API Server만 호출한다.  
  REST Server는 다중 계층으로 구성될 수 있다.  
  API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.  
  또한 로드밸런싱, 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있다.  
  PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.


- Code-On-Demand(optional)   
  >Server로부터 스크립트를 받아서 Client에서 실행한다.  
  반드시 충족할 필요는 없다.


- Uniform Interface(인터페이스 일관성)   
  >URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.  
  HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.  
  특정 언어나 기술에 종속되지 않는다.

---
참조
- https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html