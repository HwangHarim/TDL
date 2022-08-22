# Maven vs Gradle

---

- Maven 같은 경우는 스프링프로젝트에서 pom.xml로 사용된다.
- Gradle은 스프링부트, 안드로이드에서 많이 사용한다.

# Maven이란?

### Maven은 프로젝트의 전체적인 라이프사이클을 관리하는 도구

> 프로젝트를 진행하다 보면 많은 라이브러리들을 사용 많은 라이브러리 들을 관리하기 위해 사용하는 것이 Maven
> 
>내가 사용할 라이브러리 뿐만 아니라 해당 라이브러리가 작동하는데 필요한 다른 라이브러리들까지 관리하여 네트워크를 통해 자동으로 다운 받아준다.
> 

#Maven의 Lifecycle

 - maven 에서는 미리 정의하고 있는 빌드 순서가 있으며 이 순서를 라이프사이클이라고 한다. 
 - 라이프 사이클의 가 빌드 단계를 Phase라고 한다.

   - Clean : 이전 빌드에서 생성된 파일들을 삭제하는 단계
   - Validate : 프로젝트가 올바른지 확인학고 필요한 모든 정보를 사용할 수 있는 지 확인하는 단계
   - Compile : 프로젝트의 소스코드를 컴파일하는 단계
   - Test : 유닛(단위) 테스트를 수행하는 단계(테스트 실패시 빌드 실패로 처리, 스킵 가능)
   - Package : 실제 컴파일된 소스 코드와 리소스들을 jar등의 배포를 위한 패키지로 만드는 단계
   - Verify : 통합테스트 결과에 대한 검사를 실행하여 품질 기준을 충족하는지 확인하는 단계
   - Install : 패키지를 로컬 저장소에 설치하는 단계
   - Site : 프로젝트 문서를 생성하는 단계
   - Deploy : 만들어진 Package를 원격 저장소에 release하는 단계


###POM.XML
Maven의 기능을 이용하기 위해 POM이 사용

POM은 약자 이름 그대로 Project Object Model의 정보를 담고 있는 파일
>pom.xml에서 주요하게 다루는 기능들은 아래와 같습니다.
- 프로젝트 정보 : 프로젝트의 이름, 라이센스 등
- 빌드 설정 : 소스, 리소스, 라이프사이클별 실행한 플로그인 등 빌드와 관련된 설정
- 빌드 환경 : 사용자 환경 별로 달라질 수 있는 프로파일 정보
- pom 연관 정보 : 의존 프로젝트(모듈), 상위 프로젝트, 포함하고 있는 하위 모듈 등


#Gradle

> Gradle이란 기본적으로 빌드 배포 도구(Build Tool)이다. 안드로이드 앱을 만들때 필요한 공식 빌드시스템이기도 하며 JAVA, C/C++, Python 등을 지원한다.
> 
> 기본 메이븐의 경우 XML로 라이브러리를 정의하고 활용하도록 되어 있으나, Gradle의 경우 **별도의 빌드스크립트를 통하여 사용할 어플리케이션 버전, 라이브러리등의 항목을 설정** 할 수 있다.
>


### 라이브러리 관리 
    메이븐 레파지토리를 동일하게 사용할 수 있어서 설정된 서버를 통하여 라이브러리를 다운로드 받아 모두 동일한 의존성을 가진 환경을 수정할 수 있다. 자신이 추가한 라이브러리도 레파지토리 서버에 올릴 수 있다.

### 프로젝트 관리 
    모든 프로젝트가 일관된 디렉토리 구조를 가지고 빌드 프로세스를 유지하도록 도와준다.

### 단위 테스트 시 의존성 관리
    junit 등을 사용하기 위해서 명시한다.


## Gradle을 사용하는 이유

- Build라는 동적인 요소를 XML로 정의하기에는 어려운 부분이 많다.
  - 설정 내용이 길어지고 가독성 떨어짐
  - 의존관계가 복잡한 프로젝트 설정하기에는 부적절
  - 상속구조를 이용한 멀티 모듈 구현
  - 특정 설정을 소수의 모듈에서 공유하기 위해서는 부모 프로젝트를 생성하여 상속하게 해야함 (상속의 단점 생김)
  

- Gradle은 그루비를 사용하기 때문에, 동적인 빌드는 Groovy 스크립트로 플러그인을 호출하거나 직접 코드를 짜면 된다.
  - Configuration Injection 방식을 사용해서 공통 모듈을 상속해서 사용하는 단점을 커버했다.
  - 설정 주입시 프로젝트의 조건을 체크할 수 있어서 프로젝트별로 주입되는 설정을 다르게 할 수 있다.


**Groovy?**

    Groovy는 Java 가상 머신에서 실행되는 스크립트 언어
    Java와는 달리 소스 코드를 컴파일 할 필요는 없다.
    Groovy는 스크립트 언어이고, 소스 코드를 그대로 실행
    또한 Java와 호환되고, Java 클래스 파일을 그대로 Groovy 클래스로 사용할 수 있다.
    Java 문법과 유사하여 빌드 처리를 관리
    

>**Gradle이 Maven보다 최대 100배 빠르다.**
> 
![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdKtmEU%2Fbtq8bsvQoKc%2FDjilAAylpcHLJFRtXQCd01%2Fimg.png)
![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbS9riQ%2Fbtq8aN1zMjC%2FKn1fpOCrvzF1lWKkoDNy4K%2Fimg.png)
![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcEGqWA%2Fbtq8dulsWv5%2FRPudjkBsjzmp0gKd3Qk0z1%2Fimg.png)

---
참고 : https://dev-coco.tistory.com/65 , https://hyojun123.github.io/2019/04/18/gradleAndMaven/