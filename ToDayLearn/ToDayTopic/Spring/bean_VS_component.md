# Bean

---
Bean은 Spring IoC Container가 관리하는 자바 객체, Spring Bean Container에 존재하는 객체를 말한다.

Spring IoC(Inversion of Control) Contatiner에 의해 인스턴스화, 관리, 생성된다.

Bean Container는 의존성 주입을 통해 Bean 객체를 사용할 수 있도록 해준다.

Spring에서 Bean은 보통 Singleton으로 존재한다.

Singleton : 어떤 Class가 최초 한번만 메모리를 할당하고(Static) 그 메모리에 객체를 만들어 사용하는 디자인 패턴

![img.png](https://velog.velcdn.com/images%2Fgillog%2Fpost%2F2af99237-b71c-45ae-87f2-84ad73f72f3e%2Fspring-bean.png)
Spring에서 POJO(Plain Old Java Object)를 Beans라고 부른다.

POJO : 본래 자바의 장점을 살리는 특정 '기술'에 종속되어 동작하는 것이 아닌 '오래된' 방식의 '순수한' 자바객체

Beans는 Application의 핵심을 이루는 객체이며, 대부분 Container에 공급하는 설정 메타 데이터(XML 파일/ 어노테이션)에 의해 생성된다.

Container는 이 메타 데이터를 통해 Bean의 생성, Bean Life Cycle, Bean Dependency(종속성) 등을 알 수 있다.

new 연산자로 생성하는 객체는 Bean이 아니고, ApplicationContext.getBean()으로 얻어질 수 있는 객체는 Bean이다.

즉, Spring에서의 Bean은 ApplicationContext가 알고있는 객체, 즉 ApplicationContext가 만들어서 그 안에 담고있는 객체를 의미한다.

---

# Component

---
![img.png](https://i0.wp.com/hanamon.kr/wp-content/uploads/2021/01/%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8.png?resize=768%2C506&ssl=1)

## 컴포넌트란?

컴포넌트(Component)란 프로그래밍에 있어 재사용이 가능한 각각의 독립된 모듈을 뜻한다.

그림에서 확인 할 수 있듯이 컴포넌트 기반 프로그래밍을 하면 마치 레고 블록처럼 이미 만들어진 컴포넌들을 조합하여 화면을 구성할 수 있다.

웹 컴포넌트는 이러한 컴포넌트 기반 프로그래밍을 웹에서도 적용할 수 있도록 W3C에서 새로 정한 규격이다. 웹 표준을 기반으로 구축되었으며, 최신 부라우저 및 모든 JavaScript 라이브러리, 프레임워크에서도 사용할 수 있다.

따라서 웹 컴포넌트를 이용하여 코드를 작성하면 Vue.js 나 React.js 와 같은 라이브러리, 프레임워크에 의존하지 않고 상호 운용이 가능하게끔 작성할 수 있다.