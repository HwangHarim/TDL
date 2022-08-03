# SpringMVC

---

Spring MVC란?

→ 프론트 컨트롤러 패턴에 기초한 웹 MVC 프레임 워크이다.

<aside>
⚙ Spring 프레임워크 하위 모듈이며 , Model, Wiew, Controller를 명확하게 분리하여 매우 유연하고 확장성이 좋은것이 특징

</aside>

# SpringMVC가 없었을 때

---

URL마다 서블릿을 생성하고 Web.xml로 서블릿을 관리한다.

URL마다 서블릿이 필요하다 보니, 매번 서블릿 인스턴스를 만들어야했다.

각 서블릿마다 공통 기능을 하는 코드들이 중복해서 발생하여 유지 보수가 어려 웠다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/dc3b817c-a55b-4c5e-8de4-c6645d8a958a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220803%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220803T081530Z&X-Amz-Expires=86400&X-Amz-Signature=53a9960cc7b5b276c1f6ba66362e3d1b9074f89362eef11855c5c8c612c7fac1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

# 프로트 컨트롤러 패턴

---

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b1e7fe48-2216-4156-a866-0f2e3bfa1f74/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220803%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220803T081601Z&X-Amz-Expires=86400&X-Amz-Signature=e48c7cd3143c56ed45ede8764d133091b6321d07f88c98c5e9cb6fff2ff3a547&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

프론트 컨트롤러 패턴은 클라이언트 요청을 올바른 컨트롤러로 보내주는 역할을 수행한다.

그래서 공통 기능은 프론트 컨트롤러에서 처리하고, 서로 다른 코드들만 각 컨트롤러에서 처리하도록 할 수 있다.

# DispatcherServlet란?

---

- 표현 계층 전면에서 HTTP프로토콜을 통해 들어오는 모든 요청을 중앙 집중식으로 처리하는 프론트 컨트롤러이다.
- DispatcherServlet은 Spring MVC의 핵심 요소
    - 클라이언트로부터 어떤 요청이 들어오면 서블릿 컨테이너가 요청을 받는다.
    - 이후 공통 작업을 DipatcherServlet에 처리하고, 이외 작업은 적절한 세부 컨트롤러로 위임한다.

# Spring MVC의 동작 흐름

---

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2b7dd4f4-d31c-49eb-88e1-fde6b9baa57e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220803%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220803T081624Z&X-Amz-Expires=86400&X-Amz-Signature=4a64abf0de5c157a88a0bb00f83bf3a2a77f94ceac596e1c44d7c4d88e2dcbdd&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

1. DispatcherServlet으로 클라이언트의 웹 요청이 들어온다.
2. 웹 요청을 Handler Mapping에 위임하여 해당 요청을 처리할 Handler(Controller)를 탐색한다.
3. 찾은 Handler를 실행할 수 있는 HandlerAdapter를 탐색한다.
4. 찾은 Handler Adapter를 사용해서 Handler의 메소드를 실행한다.
5. Handler의 반환 값은 Model과 View이다.
6. View 이름을 ViewResolver에게 전달하고, ViewResolver는 해당하는 View 객체를 전달한다.
7. DispatcherServlet은 View에게 Model을 전달하고 화면 표시를 요청한다. 이때, Model이 null이면 View를 그대로 사용하고, 그렇지 않으면 View에 Model 데이터를 렌더링한다.
8. 최종적으로 DispatcherServlet은 View 결과(HttpServletResponse)를 클라이언트에게 반환한다.

위 흐름은 @Controller 기준이며, @RestController의 경우 6번과 7번 과정이 생략된다. 즉, ViewResolver를 타지 않고 반환 값에 알맞는 MessageConverter를 찾아 응답 본문을 작성한다.