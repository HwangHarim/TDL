# 1. Dispatcher-Servlet(디스패처 서블릿)의 개념

---

## Dispatcher-servlet 이란?
- 디스패처 서블릿의 dispatch는 "보내다"라는 뜻을 가지고 있다.

- 디스패처 서블릿은 HTTP 프로토콜로 들어오는 모든 요청을 가장 먼저 받아 적합한 컨트롤러에 위임해주는 프론트 컨트롤러(Front Controller)라고 정의할 수 있다.

- 클라이언트로부터 어떠한 요청이 오면 Tomcat(톰캣)과 같은 서블릿 컨테이너가 요청을 받게 된다.

- 그리고 이 모든 요청을 프론트 컨트롤러인 디스패처 서블릿이 가장 먼저받게 됩니다.

- 그러면 디스패처 서블릿은 공통적인 작업을 먼저 처리한 후에 해당 요청을 처리해야 하는 컨트롤러를 찾아서 작업을 위임합니다.

Front Controller는 주로 서블릿 컨테이너의 제일 앞에서 서버로 들어오는 클라이언트의 모든 요청을 받아서 처리해주는 컨트롤러로써, MVC 구조에서 함께 사용되는 디자인 패턴이다.

## [Dispatcher-servlet 의 장점]

>   Spring MVC는 DisPatcherSrvlet이 등장함에 따라 web.xml의 역할을 상당히 축소 했다.
>
>  dispatcher-servlet이 해당 어플리케이션으로 들어오는 모든 요청을 헨들링 하기 때문
> 
>  공동 작업을 처리하면서 상당히 편리하게 이용할 수 있게 되었다.
>

## [정적 자원(Static Resource)의 처리]

모든 요청을 처리하다보니 이미지나 HTML/CSS/JavaScript 등과 같은 정적 파일에 대한 요청마저 모두 가채는 까닭에 정적 자원을 불러오지 못하는 상황도 발생하곤 했다

이러한 문제를 해결하기 위해 개발자들은 2가지 방법을 고안 했다

    1. 정적 자원에 대한 요청과 애플리케이션에 대한 요청을 분리

    2. 애플리케이션에 대한 요청을 탐색하고 없으면 정적 자원에 대한 요청으로 처리

### 1.정적 자원에 대한 요청과 애플리케이션에 대한 요청을 분리

---
- /apps 의 URL로 접근하면 Dispatcher Servlet이 담당한다.
- /resources 의 URL로 접근하면 Dispatcher Servlet이 컨트롤할 수 없으므로 담당하지 않는다.

### 2.애플리케션에 대한 요청을 탐색하고 없으면 정적 자원에 대한 요청으로 처리

---

    두번째 방법은 Dispatcher-Servlet이 요청을 처리할 컨트롤러를 먼저 찾고,

    요청에 대한 컨트롤러를 찾을 수 없는 경우에, 2차적으로 설정된 자원(Resource) 경로를 탐색하여 자원을 탐색하는 것이다.

    이렇게 영역을 분리하면 효율적인 리소스 관리를 지원할 뿐 아니라 추후에 확장을 용이하게 해준다는 장점이 있다.

---

# Spring MVC의 동작 흐름

---

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbImFbg%2FbtrGzZMTuu2%2FCkY4MiKvl5ivUJPoc5I3zk%2Fimg.png)

1. DispatcherServlet으로 클라이언트의 웹 요청이 들어온다.
2. 웹 요청을 Handler Mapping에 위임하여 해당 요청을 처리할 Handler(Controller)를 탐색한다.
3. 찾은 Handler를 실행할 수 있는 HandlerAdapter를 탐색한다.
4. 찾은 Handler Adapter를 사용해서 Handler의 메소드를 실행한다.
5. Handler의 반환 값은 Model과 View이다.
6. View 이름을 ViewResolver에게 전달하고, ViewResolver는 해당하는 View 객체를 전달한다.
7. DispatcherServlet은 View에게 Model을 전달하고 화면 표시를 요청한다. 이때, Model이 null이면 View를 그대로 사용하고, 그렇지 않으면 View에 Model 데이터를 렌더링한다.
8. 최종적으로 DispatcherServlet은 View 결과(HttpServletResponse)를 클라이언트에게 반환한다.

위 흐름은 @Controller 기준이며, @RestController의 경우 6번과 7번 과정이 생략된다. 즉, ViewResolver를 타지 않고 반환 값에 알맞는 MessageConverter를 찾아 응답 본문을 작성한다.

