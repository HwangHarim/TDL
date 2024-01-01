# 접근제한자

---

![1234.png](https://i.imgur.com/4JazPgh.png)

---

# public

**`Public`**은 **package, Class가 동일하지 않아도 모든 접근이 가능**한 제한자이다.

*같은 package(O), 다른 package(O), 같은 클래스 (O),외부 클래스(O) 저부 허용*

# protected

**`Protected`**는 **같은 package에서만 접근을 허용**하고 **다른 package에서 접근하려면 해당 Class를 상속받을 시에만 접근이 가능**한 제한자이다.

*같은 Class내에서 접근 허용, 같은 package의 다른 Class에서 접근 허용, 다른 package의 상속받은 Class 접근 허용, **다른 package의 다른 Class 접근 불가***

# default

`default`는 **동일 package에서만 접근을 허용**하는 제한자로, **접근 제한자가 생략되어 있을경우엔 기본적으로 `default` 접근 제한자가 적용**된다.

*같은 class 내에서 허용, 같은 package 내의 다른 class에서 허용, **다른 package에서는 접근 불가***

`default`는 자동으로 선언되어 지므로 변수, 메소드 앞에 명시적으로 적어서는 안된다.

*아무것도 선언되지 않았을 경우 `default`, `friendly` 접근 제한자로 선언되었다. 표현*

# private

`private`는 **동일 package, 다른 package 모두 접근이 불가능**하고 **같은 Class 내에서만 접근을 허용**하는 제한자이다.

***같은 java 파일 안의 서로 다른 Class라도 접근 불가***

# 접근 제한자 별 사용 가능 범위

- **Class에 사용 가능**`public,` `default`
- **Construtor**`public`, `protected`, `default`, `private`
- **Member 변수**`public`, `protected`, `default`, `private`
- **Member method**`public`, `protected`, `default`, `private`
- **지역 변수**접근 제한자 사용 불가
---

## **생성자**

> new 연산자와 같이 사용되어 클래스로부터 객체를 생성할 때 호출되어 객체의 초기화를 담당한다.
>

**객체 초기화**

- 필드를 초기화하거나, 메소드를 호출해서 객체를 사용할 준비를 하는 것
- 생성자를 실행시키지 않고는 클래스로 부터 객체를 만들 수 없다.
- new 연산자에 의해 생성자가 성공적으로 실행되면, 힙 영역에 객체가 생성되고, 객체의 주소가 반환된다.
- 반환된 객체 주소는 클래스 타입 변수에 저장되어, 객체에 접근할 때 이용된다.
- 만약 생성자가 실행되지 않고 예외(에러)가 발생했다면, 객체는 생성되지 않는다.

### **기본 생성자**

- 모든 클래스는 생성자가 반드시 존재하며, 하나 이상을 가질 수 있다.
- 클래스 내부에 생성자 선언을 생략했다면, 컴파일러는 아래와 같이 중괄호 { } 블록 내용이 비어있는 기본 생성자(Default Constructor)를 바이트 코드에 자동 추가 시킨다.

바이트코드 내부

```java
[public] 클래스() { }
```

클래스가 public class 로 선언되면 기본 생성자에도 public 이 붙지만, **클래스가 public 없이 class 로만 선언되면, 기본 생성자에도 public 이 붙지 않는다.**

ex) Car 클래스를 설계할 때 생성자를 생략하면 아래와 같이 기본 생성자가 생성된다.

![https://blog.kakaocdn.net/dn/WMAx3/btqEconX4YQ/3W8zkK8udsM4Yh3DVz24j0/img.png](https://blog.kakaocdn.net/dn/WMAx3/btqEconX4YQ/3W8zkK8udsM4Yh3DVz24j0/img.png)

기본 생성자는 자동으로 생성된다. 따라서 클래스에 생성자를 선언하지 않아도, 아래와 같이 new 연산자 뒤에 기본 생성자를 호출해서 객체를 생성시킬 수 있다.

```java
Car myCar = new Car();// Car() : 기본 생성자
```

클래스에 명시적으로 선언한 생성자가 한 개라도 존재하면, 컴파일러는 기본 생성자를 추가하지 않는다. 명시적으로 생성자를 선언하는 이유는 **객체를 다양하게 초기화**하기 위해서이다.

---
# SOLID

# 1. 단일 책임 원칙 SRP(Single Responsibility Principle)

1. 한 클래스는 한가지의 역할을 갖어야한다.
2. 응집도를 높이고 결합도를 낮춘다.
3. 변경시 파급효과가 적다.

SRP를 지키지 않은 유형

```java
class 운동선수{
    final static boolean 태권도 = true;
    final static boolean 유도 = false;
    boolean 운동;

    void 훈련하기(){
      if(this.운동 == 태권도){
        //발차기
      }else{
        //굳히기
      }
    }
```

위 클래스는 void 훈련하기()에서 태권도, 유도 모두 구현하려고 해서 단일 책임 원칙을 위반하고 있는 것을 볼수있다.

```java
abstract class 운동선수{
	abstract void 훈련하기();
}

class 태권도 extends 운동선수{
	void 훈련하기{
		//발차기
	}
}

class 유도 extends 운동선수{
	void 훈련하기{
		//굳히기
	}
}

```

# 2. 개방폐쇠의 원칙 OCP (Open Close Principle)

1. 소프트웨어의 모든 구성 요소(클래스, 메스드, 모듈)변경에는 닫혀있고 자신의 확장에는 열려있다.

![화면 캡처 2022-02-16 105809.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7e52eb6b-3555-4a0c-8e32-97fc4c0fa8cd/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2022-02-16_105809.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220720%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220720T165228Z&X-Amz-Expires=86400&X-Amz-Signature=a83fd793bb4408b551f23e6bf144082c30bfd84e89f4c74cf081cb6c06e86e5a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22%25ED%2599%2594%25EB%25A9%25B4%2520%25EC%25BA%25A1%25EC%25B2%2598%25202022-02-16%2520105809.png%22&x-id=GetObject)

![화면 캡처 2022-02-16 105913.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b9d9498f-be28-4a6f-bb5c-029e1b7c355f/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2022-02-16_105913.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220720%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220720T165305Z&X-Amz-Expires=86400&X-Amz-Signature=75d46df7224bd67479aa762a53a7f8ab0df8d34b24c02b24ceb2e19f6c05b31b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22%25ED%2599%2594%25EB%25A9%25B4%2520%25EC%25BA%25A1%25EC%25B2%2598%25202022-02-16%2520105913.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d1301f1e-e813-425d-bdfb-f28a3ad60178/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220720%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220720T165319Z&X-Amz-Expires=86400&X-Amz-Signature=a063da119987220722238f4d297e6165a3f9267d1d5239366c2f0acb6c853470&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

# 3. 리스코브 치환의 원칙LSP(Liskov Substitution Principle)

1. 부모 클래스를 가리키는 포인터에 해당 클래스를 상속하는 자식 클래스를 할당하더라도 모든 기능이 정상적으로 작동해야 하며
2. 지키기위한 방법은 자식 클래스에서 Override를 사용하지 않는 것과 사용하더라도 기능을 추가하는 정도에서 부모클래스의 모든 기능이 수행가능하게 해야한다.
3.

> 서브 타입은 언제나 자신의 기반 타입으로 교체할 수 있어야 한다. - 로버트 C.마틴
>
- `하위 클래스 is a kind of 상위 클래스` - 하위 분류는 상위 분류의 한 종류다.
- `구현 클래스 is able to 인터페이스`: 구현 분류는 인터페이스할 수 있어야 한다.

위의 두 문장을 잘 지키고 있다면 이미 `리스코프 치환 원칙`을 잘 지키고 있다고 할 수 있습니다

리스코프 치환 원칙 위배

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/20203e15-b353-4083-9d68-4833b73b3391/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220720%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220720T165405Z&X-Amz-Expires=86400&X-Amz-Signature=9492101b4bb6fd78561c7917d23ca9fe5845d3af98e9622cf15cb3b0dd27f102&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

아들 is a kind of 할아버지는 성립이 되지 않는다.

리스코프 치환 원칙 만족

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8f6fa700-f01e-4bd7-b3ea-13a50f108106/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220720%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220720T165432Z&X-Amz-Expires=86400&X-Amz-Signature=b2bd2af06b38101a2340fd8e26776820d103d4de1228cd8a5ee9732504db130f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

즉, 하위 클래스의 인스턴스는 상위형 객체 참조 변수에 대입해 상위 클래스의 인스턴스 역할을 하는데 문제가 없어야 한다.

```java
class 동물 {
 void 울다(){
  //울음소리 출력
 }
}

class 조류 extends 동물{
	@Override
	public void 울다(){
		//울음소리 출력
	}
	
	public void 날개짓(){
		//날개짓
	}
}
class 펭귄 extends 죠류{
	@Override
	public void 울다(){
		//펭귄 울음소리 출력
	}
	@Override
	public void 날개짓(){
		//날개짓
	}
}
```

# 4. 인터페이스 분리 원칙 ISP(Interface Segregation Principle)

> 클라이언트는 자신이 사용하지 않는 메소드에 의존 관계를 맺으면 안 된다. - 로버트 C.마틴
>

1. 추상적인 인터페이스보다 새분화된 인터페이스가 더 좋음
2. ex> interface 복합기(인쇄, 복사, 팩스 송신, 팩스 수신)를 할 경우 인쇄와 복사만 필요한 구현체를 만들때 interface로 강제하게 되어 필요없는 기능도 추가되어 인터페이스는 새분화해서 정의하는게 좋다는 원칙

```java
interface 복합기{
  void 인쇄();
  
  void 복사();

  void 팩스보내기();

  void 패스받기();
}

class 인쇄기 implements 복합기{

  @Override
  public void 인쇄() {
    //인쇄하기
  }

  @Override
  public void 복사() {
    //복사하기
  }

  @Override
  public void 팩스보내기() {
    // 팩스보내기
  }

  @Override
  public void 팩스받기() {
    //팩스받기
  }
}
```

강제 적으로 모든 기능을 갖고 오게 됨. 필요없는 기능이 메서드에 의존관계를 갖게됨

```java
interface 인쇄 {

  void 인쇄(){...};
}

interface 복사 {

  void 복사(){...};
}

interface 팩스보내기 {

  void 팩스보내기(){...};
}

interface 팩스받기 {

  void 팩스받기(){...};
}

class 프린트기 implements 인쇄, 복사 {

	@Override
	public void 인쇄 (){
	//인쇄
	}

	@Override
	public void 복사 (){
		//인쇄
	}

}

```

# 5. 의존 역적의 원칙DIP(Dependency Inversion Principle)

> 고차원 모듈은 저차원 모듈에 의존하면 안 된다. 이 두 모듈 모두 다른 추상화된 것에 의존해야 한다. 추상화된 것은 구체적인 것에 의존하면 안된다. 구체적인 것이 추상화된 것에 의존해야 한다. 자주 변경되는 구체(concrete) 클래스에 의존하지 마라 - 로버트 C.마틴-
>

1. 구현체에서 추상체로 의존성이 역전하는 원칙

![화면 캡처 2022-02-16 105809.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7e52eb6b-3555-4a0c-8e32-97fc4c0fa8cd/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2022-02-16_105809.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220720%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220720T165228Z&X-Amz-Expires=86400&X-Amz-Signature=a83fd793bb4408b551f23e6bf144082c30bfd84e89f4c74cf081cb6c06e86e5a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22%25ED%2599%2594%25EB%25A9%25B4%2520%25EC%25BA%25A1%25EC%25B2%2598%25202022-02-16%2520105809.png%22&x-id=GetObject)

```java
class 직장인 extends 라때 주문{
		@Override
		public void 라때 주문(){
			...
		}
}

class 라때 주문{
	void 라때 주문(){
		...
	}
}
```

![화면 캡처 2022-02-16 105913.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b9d9498f-be28-4a6f-bb5c-029e1b7c355f/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2022-02-16_105913.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220720%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220720T165305Z&X-Amz-Expires=86400&X-Amz-Signature=75d46df7224bd67479aa762a53a7f8ab0df8d34b24c02b24ceb2e19f6c05b31b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22%25ED%2599%2594%25EB%25A9%25B4%2520%25EC%25BA%25A1%25EC%25B2%2598%25202022-02-16%2520105913.png%22&x-id=GetObject)

```java
class 직장인 implements 주문{
		public ride(){...}
}

interface 주문 extends ???{
...		
}

class 아메{
	...
	}

class 라떼{
	...
	}

class 녹차{
	...
	}
}
```

이처럼 자신보다 변하기 쉬운 것에 의존하던 것을 추상화된 인터페이스나 상위 클래스를 두어 변하기 쉬운 것의 변화에 영향받지 않게 하는 것이 의존 역전 원칙이다.

상위 클래스일수록, 인터페이스일수록, 추상 클래스일수록 변하지 않을 가능성이 높기에 하위 클래스나 구현체 클래스가 아닌 상위 클래스, 인터페이스, 추상 클래스를 통해 의존하라는 것이 바로 의존 역전 원칙이다.