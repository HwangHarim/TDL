#  [오픈소스] 메시지큐(Message Queue)

---

- 메시지 지향 미들웨어(Meesage Oriented Middleware: MOM)은 비동기 메시지를 사용하는 다른 응용 프로그램 사이에서 데이터 송수신을 의미
- 프로그래밍에서 MQ는 프로세스 또는 프로그램 인스턴스가 데이터를 서로 교환할때 사용하는 방법

![img.png](https://user-images.githubusercontent.com/50273712/133918874-2664898b-a080-4df6-bd21-fad7a204029d.png)

### 메시지 큐의 장점

- 비동기(Asynchronous): Queue에 넣기 때문에 나중에 처리할 수 있습니다.

- 비동조(Decoupling): 애플리케이션과 분리할 수 있습니다.

- 탄력성(Resilience): 일부가 실패 시 전체에 영향을 받지 않습니다.

- 과잉(Redundancy): 실패할 경우 재실행 가능합니다.

- 보증(Guarantees): 작업이 처리된걸 확인할 수 있습니다.

- 확장성(Scalable): 다수의 프로세스들이 큐에 메시지를 보낼 수 있습니다.

---

### 메시지 큐 사용처

- 다른 곳의 API로 부터 데이터 송수신이 가능합니다.

- 다양한 애플리케이션에서 비동기 통신을 할 수 있습니다.

- 이메일 발송 및 문서 업로드가 가능합니다.

- 많은 양의 프로세스들을 처리할 수 있습니다.

---

## 오픈 소스 메시지 큐

RabbitMQ

- AMQT 프로토콜을 구현해 놓은 프로그램입니다.

- 신뢰성, 안정성과 성능을 충족할 수 있도록 다양한 기능을 제공합니다.

- 유연한 라우팅: Message Queue가 도착하기 전에 라우팅 되며 플러그인을 통해 더 복잡한 라우팅도 가능합니다.

- 클러스터링: 로컬네트워크에 있는 여러 RabbitMQ 서버를 논리적으로 클러스터링할 수 있고 논리적인 브로커도 가능합니다.

- 관리 UI가 있어 편하게 관리 가능합니다.

- 거의 모든 언어와 운영체제를 지원합니다.

- 오픈소스로 상업적 지원이 가능합니다.

![img.png](https://img1.daumcdn.net/thumb/R1280x0.fpng/?fname=http://t1.daumcdn.net/brunch/service/user/2MrI/image/e1se1orFfMGK7QNzVZlPpUqFnl8.png)

---
![img.png](https://velog.velcdn.com/images%2Fyyong3519%2Fpost%2F01f0806b-6be9-4c91-808e-07b593e615c3%2FScreen%20Shot%202022-02-23%20at%203.35.35%20AM.png)


