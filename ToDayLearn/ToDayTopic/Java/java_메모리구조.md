# 자바 메모리 구조

---

## 자바의 프로그램 실행 구조

![img.png](https://velog.velcdn.com/images%2Fshin_stealer%2Fpost%2F2b05aec3-0719-482f-a6f0-e4e1ae92f7f1%2Fimage.png)


## JIT(Just In Time) 컴파일러

> C나 C++에서 하는 것처럼 프로그램을 실행하기 전에 처음 한 번 컴파일하는 대신, 프로그램을 실행하는 시점에서 필요한 부분을 즉석에서 컴파일하는 방식을 말한다.

### JIT가 필요한 이유

자바는 바이트코드로 한번 컴파일 하는 과정과, 바이트코드를 인터프리터 하는 방식 2가지를 진행하기 때문인데, 가뜩이나 인터프리터 방식은 소스코드를 런타임시에 한줄 한줄 읽어 들여야 하는 방식 때문에, 컴파일 방식보다 느리다.

(1) 컴파일 방식 : 소스코드를 한꺼번에 컴퓨터가 읽을 수 있는 native machine (기계)어로 변환

(2) 인터프리터 방식 : 소스코드를 빌드시에 암것도 하지 않다가, 런타임시에 한줄 한줄 읽어가며 변환

![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdoANQP%2FbtqM639PEix%2Fu7FZUSbwnlW5sizN1GyBh1%2Fimg.png)

>이런식으로 저장소에 저장을 한다는 개념이다. 첫 컨파일 때는 실행되지 않는다.
> 
> 정확히는 반복되는 코드를 모두 컴파일러로 컴파일 시키는거다.
> 
>그래서 인터프리터의 역학을 보조? 해준다고 생각하면 되는데, 인터프리터는 읽을 때,
> 
>반복되는 코드로 컴파일된 코드를 바로 사용 할 수 있다.
> 
> 반복되는 메서드를 컨파일한 것을 저장했다가 다시 사용 할 때 전송하므로 빨라진다.

## JVM의 전체적인 구조

![img.png](https://velog.velcdn.com/images%2Fshin_stealer%2Fpost%2F8e500340-258e-4150-85c0-455921663229%2Fimage.png)

> - (.java) 파일을 Java Compiler를 통해서 Byte Code(.Class)파일로 변환한다.
> - Byte Code로 변환된 파일을 JVM의 Class Loader로 보낸다.
> - Class Loader는 말 그대로 Class 파일을 부러와서 메모리에 저장하는 역할을 한다.
> - Execution Engine은 Class Loader에 저장된 Byte Code를 명령어 단위로 분류하여 하나씩 실행하게 하는 엔진이다.
> - Garbage Collector는 사용하지 않거나 필요없는 객체들을 메모리에서 소멸시키는 역할을 한다.
> - Runtime Date Area는 jvm이 프로그램을 수행하기위해 운영체제로부터 할당 받은 메모리 공간이다.
---
## Memory Area 의 구조

![img.png](https://velog.velcdn.com/images%2Fshin_stealer%2Fpost%2F024b42b8-85fa-4393-9668-6ef15227a0d0%2Fimage.png)

1) Method Area

   - JVM이 실행되면서 생기는 공간이다.
   - Class 정보, 전역변수 정보, Static 변수 정보가 저장되는 공간이다.
   - Runtime Constant Pool 에는 말 그대로 '상수' 정보가 저장되는 공간이다.
   - 모든 스레드에서 정보가 공유된다.
   

2) Heap

   - new 연산자로 생성된 객체, Array와 같은 동적으로 생성된 데이터가 저장되는 공간
   - Heap에 저장된 데이터는 Garbage Collector 가 처리하지 않는한 소멸되지 않는다.
   - Reference Type 의 데이터가 저장되는 공간
   - 모든 스레드에서 정보가 공유된다.
   

3) Stack

    - 지역변수, 메소드의 매개변수와 같이 잠시 사용되고 필요가 없어지는 데이터가 저장되는 공간
    - Last In First Out, 나중에 들어온 데이터가 먼저 나간다
    - 만약, 지역변수 이지만 Reference Type일 경우에는 Heap 에 저장된 데이터의 주소값을 Stack 에 저장해서 사용하게 된다.
    - 스레드마다 하나씩 존재한다.


4) PC Register

   - 스레드가 생성되면서 생기는 공간
   - 스레드가 어느 명령어를 처리하고 있는지 그 주소를 등록한다.
   - JVM이 실행하고 있는 현재 위치를 저장하는 역할


5) Native Method Stack
   - Java 가 아닌 다른 언어 (C, C++) 로 구성된 메소드를 실행이 필요할 때 사용되는 공간