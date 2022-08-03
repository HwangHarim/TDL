## Servlet은 무슨 일을 할까?

- post할 때 데이터 전송

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/13e6ba46-0ee8-414b-9a40-ac5656f6de47/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220803%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220803T075257Z&X-Amz-Expires=86400&X-Amz-Signature=1ac367dbc7016022701494ba2d52f6b717d43efcc97742f03aa90c5f72419bae&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

## 서버에서 처리해야 하는 업무

- 웹 애플리케이션 서버 직접 구현

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f3e2374c-f385-4b07-82aa-470467297780/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220803%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220803T080704Z&X-Amz-Expires=86400&X-Amz-Signature=bf39ff1eaced95478cd63a2d12c95872ae1457ad448a7a01f7d669aea9f3fefa&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

서버 TCp/IP 연결대기, 소캣 연결 → HTTP 요청 메시지 파싱에해서 읽기 → Post방식,/save URL 인지 → Content-Type 확인 → HTTP 메시지 바디 내용 파싱 → 저장 프로세스 실행

---

비지니스 로직 실행

---

HTTP 응답 메시지 생성 시작

- HTTP 시작 라인 생성
- Header 생성
- 메시지 바디에 HTML 생성에서 입력

→ TCP/IP에 응답 전달, 소켓 종료

## 서블릿을 지원하는 WAS 사용

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a235f7dc-a600-4c0c-aab3-131695aaf391/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220803%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220803T080745Z&X-Amz-Expires=86400&X-Amz-Signature=6d083839678d655138c0284875b52c1f1e54d253c424a4bb05c0be38df02ad29&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

WAS (WEB Application Server)

→ 동적(비즈니스) 애플리케이션 로직이 실행되는 서버

---

# 서블릿

### 특징

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/449c84be-19fc-4fb3-ba8d-b1ea49fe5a6f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220803%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220803T080804Z&X-Amz-Expires=86400&X-Amz-Signature=d9357c2b637ea551a0e55744124b9efe538a4f39c4f046911f7ae43bd233964e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- urlPattetns(/hello)의 URL이 호출되면 서블릿 코드가 실행
- HTTP 요청 정보를 편리하게 사용할 수 있는 HttpServletRequest
- HTTP 응답 정보를 편리하게 제공할 수 있는 HttpServletResponse
- 개발자는 HTTP 스펙을 매우 편리하게 사용

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b24cd4b7-d55c-47a4-b977-7e2099ae52e7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220803%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220803T080829Z&X-Amz-Expires=86400&X-Amz-Signature=0702888407d7bf587cd15217e372c63b68d153b14f5157214c79efc6dcfd3129&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

---

# 서블릿

### HTTP 요청, 응답 흐름

- HTTP 요청시
    - WAS는 Request, Response 객체를 새로 만들어서 서블릿 객체[ㅔ 호출
    - 개발자는 Request 객체에서 HTTP 요청 정보를 쳔리하게 꺼내서 사용
    - 개발자는 Response 객체에 HTTP 응답 정보를 편리하게 입력
    - WAS는 Response 객체에 담겨있는 내용으로 HTTP 응답 정보를 생성

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e62a3536-99c3-4dab-b9af-00a0b0e143f4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220803%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220803T080847Z&X-Amz-Expires=86400&X-Amz-Signature=d7bec156427eba4badf651bca9917e248130c6ea9f324bcd33072b0b7f7d529c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- 톰캣처럼 서블릿을 지원하는 WAS를 서블릿 컨테이너라고 함
- 서블릿 컨테이너는 서블릿 객체를 생성, 초기화, 호출, 종료하는 생명주기를 관리한다.
- 서블릿 객체는 싱글톤으로 관리
    - 고객의 요청이 올 때 마다 계속 객체를 생성하는 것은 비효율
    - 최초 로딩 시점에 서블릿 객체를 미리 만들어 두고 재활용
    - 모든 고객 요청은 동일한 서블릿 객체 인스턴스에 접근
    - 공유 변수 사용 주의
    - 서블릿 컨테이너 종료시 함께 종료
- JSP도 서블릿으로 변환 되어서 사용
- 동시 요청을 위한 멀티 쓰레드 처리 지원

---

## 동작 과정

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b0d87d2b-511e-4309-8513-87b9207591cc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220803%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220803T080937Z&X-Amz-Expires=86400&X-Amz-Signature=8b33469ccaedd44fbcc2df9a3de702b730448697ce6fb30cca6344b8433f39e4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- 웹 브라우저에서 웹 서버로 request를 보내면, 웹서버는 받은 HTTP 요청을  WAS의 WEB Server로 전달한다.
- WAS의 웹 서버는 HTTP 요청을 서블릿 컨테이너로 전달한다.
- 서블릿 컨테이너는 HTTP 요청 처리에 필요한 서블릿 인스턴스가 힙 메모리 영역에 있는지 확인한다. 존재하지 않는 다면, 서블릿 인스턴스를 생성하고 해당 서블릿 인스턴스의 init() 메소드를 호출하여 서블릿 인스턴스를 초기화한다.
- 서블릿 컨테이너는 서블릿 인스턴의 service()메소드를 호출하여 HTTP 요청을 처리하고 WAS의 웹 서버에게 처리 결과를 전달
- WAS의 웹서버는 HTTP 응방을 앞 단에 위치한 웹서버에게 전달하고, 앞단의 웹서버는 받은 HTTP응답을 웹브라우저로 전달한다.