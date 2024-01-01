# 동시성이란?

---

먼저 동시성(Concurrency)의 사전적 정의에 대해서 살펴보자

- 사전적 의미 : 하나의 CPU 코어에서 시간분할(Time sharing)을 통하여 여러 일을 처리하는 것 처럼 보여지게 하는 기법

- 대중적 의미 : 여러 요청이 하나의 자원(data)에 접근하여 수정(변경, 삭제)하려는 상황.


---

# Spring에서의 동시성

spring을 공부하면서, 지금까지 마주한 동시성 문제의 상황은 아래 두 가지다.

- Singleton 객체 내부의 필드를 관리할 때의 동시성 Issue
- Database의 데이터에 접근해서 Update, Delete할 때의 동시성 Issue

여기에서는 Singleton 객체의 경우를 살펴보자

### - Singleton

스프링에서는 스프링 컨테이너가 등록된 Bean들을 싱글톤으로 관리해준다.   
싱글톤으로 관리된다는 말은, 하나의 객체가 호출될때마다 생성되는 것이 아닌,  
처음에 생성된 객체 하나를 모든 요청들이 같이 사용한다고 생각하면 된다.  
그렇기 때문에 A라는 사람이 싱글톤 객체(S)를 사용하고 있다고 하더라도, B라는 사람의 요청이 들어올 수 있고,  
이 과정에서 S를 동시에 사용하게 되는 것'처럼' 번갈아서 사용하게 된다.  
S를 아래와 같이 가정하자.

```java
@Getter @Setter	// getter, setter가 있다고 가정
public class S{
...
private String name;
...

}
```
- A가 S에 접근해서 setName("A") 후 getName() 한다.
- B도 S에 접근해서 setName("B") 후 getName() 한다.

만약 A의 setName과 getName의 과정 사이에서 B의 setName이 동작하게 되면 어떻게 될까?
A가 getName을 할때, 원하는 "A"가 아니라 "B"가 반환되게 된다.

이 모든것은 CPU가 concurrency를 사용해서, 하나의 코어가 여러개의 Task를 번갈아가면서 처리하기 때문에 일어난다.
동시에 많은 요청이 들어오면, CPU는 여러 개의 Task를 오가면서 처리한다.(Context Switching)

![img.png](https://velog.velcdn.com/images/noakafka/post/96012fe5-7e41-4ae3-9721-57cbf4a33359/image.png)

이 과정에서 Task가 바뀌어도 싱글톤 객체 내부 필드는 공유가 되고,
기대하지 않는 값이 반환되는 경우들이 생기는 것이다.

일반적으로 트래픽이 작은 시스템에서는 이러한 문제점을 발견하기 어렵다.
하지만 하나의 Task가 끝나기도 전에 다른 Task가 밀려들어오는 대규모 트래픽에서는 빈번하게 발생하는 문제라고 한다.

---

### 해결책: ThreadLocal

동시성 문제에서 잡아줘야 할 것은 Task(Thread)가 다른 Task의 공간에 침범하지도, 침범당하지도 않도록 하는 것이다. 이를 위해서는 싱글톤으로 공통으로 사용하고 있는 필드를 각 Task마다 고유의 저장공간에 저장해주면 된다.
ThreadLocal이 그 기능을 해준다. ThreadLocal 변수를 생성하면, 해당 변수는 Thread의 Id를 보고 별도의 저장공간을 배정해준다.
즉, 요청 A와 요청 B가 들어오면, 각각의 요청에 해당하는 Thread에 각각 분리된 저장소를 제공한다.


### 사용법

ThreadLocal은 Set, Get, Remove를 통해서 관리할 수 있다.
Set을 통해서 데이터를 저장소에 집어넣고, Get을 통해서 불러올 수 있다.
Remove를 통해서 저장소를 Clear할 수 있는데, 주의할 점이 있다.

ThreadLocal을 사용하면 각 Thread마다 별도의 내부 저장소를 제공합니다.
![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxHW4U%2FbtrzLIThkZO%2FTNt9B1lMOC5g8UxbjYa49K%2Fimg.png)

Thread A가 userA라는 정보를 저장하게 되면 ThreadLocal은 Thread A 저장 보관소에 보관하게 됩니다.
![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd3wS5v%2FbtrzOHUlMBn%2FbbhDFcHW5oKI1ON2xTjlfK%2Fimg.png)

마찬가지로 hread B가 userB라는 정보를 저장하게 되면 ThreadLocal은 Thread B 저장 보관소에 보관하게 됩니다.
![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FebWDam%2FbtrzRVDw1MB%2FXhupmFWicgzWJ2GxYmgYE0%2Fimg.png)

ThreadLocal을 통해서 데이터를 조회할 경우에도 각각 저장한 데이터를 반환해줍니다.

자바에서 ThreadLocal을 지원해주기 위해서
```java
import java.lang.ThreadLocal;
```
을 제공한다.

### ThreadLocal 사용법

```java
private ThreadLocal<String> a = new ThreadLocal<>();

a.set(String) -> 값 저장
a.get() -> 값 조회
a.remove() -> 값 삭제
```
### 주의할 점

Thread를 사용하고 난 뒤, 제거하는 경우에는 문제가 되지 않는다.
하지만 Thread Pool처럼 초기에 여러개의 Thread를 생성한 후 계속해서 재활용하는 구조에서는,
저장공간이 그대로 각각의 Thread에 매핑되어서 유지된다.
그렇기 때문에, Thread를 다 사용하고 나서 다음 요청에 대비해서 ThreadLocal을 반드시 Remove해주어야 한다.
---

- https://applepick.tistory.com/157
- https://velog.io/@noakafka/Spring-%EB%8F%99%EC%8B%9C%EC%84%B1-%EB%AC%B8%EC%A0%9C