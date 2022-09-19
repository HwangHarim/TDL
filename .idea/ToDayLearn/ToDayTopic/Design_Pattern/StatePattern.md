# State Pattern(상테 패턴)

---

## 상태패턴 정의

- 어떤 행위를 수행할 때 상태에 행위를 수행하도록 위임
- 시스템의 각 상태를 클래스로 분리해 표현
- 각 클래스에서 수행하는 행위들을 메서드로 구현
- 외부로부터 캡슐화하기 위해 인터페이스를 생성하여 시스템의 각 상태를 나타나는 클래스로 실체화

![img.png](https://velog.velcdn.com/images%2Fy_dragonrise%2Fpost%2Fb0cd2535-b0f8-4aa6-8fdc-7c1c164e89b2%2Fimage.png)

`State`   
: 시스템의 모든 상태에 공통의 인터페이스를 제공한다. 따라서 이 인터페이스를 실체화한 어떤 상태 클래스도 기존 상태 클래스를 대신해 교체해서 사용할 수 있다.  

`State1, State2, State3`   
: Context 객체가 요청한 작업을 자신의 방식으로 실제 실행한다. 대부분의 경우 다음 상태를 결정해 상태 변경을 Context 객체에 요청하는 역할도 수행한다.

`Context`   
: State를 이용하는 역할을 수행한다. 현재 시스템의 상태를 나타내는 상태 변수 (state)와 실제 시스템의 상태를 구성하는 여러 가지 변수가 있다. 또한 각 상태 클래스에서 상태 변경을 요청해 상태를 바꿀 수 있도록 하는 메서드(setState)가 제공된다.   
Context 요소를 구현한 클래스의 request 메서드는 실제 행위를 실행하는 대신 해당 상태 객체에 행위 실행을 위임한다.

---


![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUeUwe%2FbtqZTVeI6DK%2FhjjE8kV40kes8jsSANOqdk%2Fimg.png)