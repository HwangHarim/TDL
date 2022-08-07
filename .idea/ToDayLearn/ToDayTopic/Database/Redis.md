![img.png](https://azderica.github.io/assets/static/RedisLogo.07cc2b7.8b577cf10f0d36b46fea48dfed2b30e2.png)

# Redis란?

---

    고성능의 키-값 데이터 구조 스토어입니다.

    여러 자료구조를 지원하며 크게 <String>, <Set>, <Sorted Set>, <Hash>, <List>등의 데이터형식을 지원

# Redis 특징

---

- 영속성을 지원하는 인메모리 데이터 저장속

    - 왜 영속성을 제공하는가?
      - ㅇ

- 읽기 성능 증대를 위한 서버 측 복제를 지원함
  - 전체 데이터베이스의 초기 복사본을 받는 마스터/슬레이브 복제를 지원합니다.
  - 마스터에서 쓰기가 순행되면 슬레이브 데이터 세트를 실시간으로 업데이트하기 위해 연결된 모든 슬레이브로 전송됩니다.


- 쓰기 성능 증대를 위한 클라이언트 측 샤딩(Sharding)을 지원합니다.
- <String>, <Set>, <Sorted Set>, <Hash>, <List>과 같은 다양한 데이터형을 지원합니다.

> **샤딩(Sharding)**
>

파티션과 동일하며, 같은 테이블 스키마를 가진 데이터를 다수의 데이터베이스에 분산하여 저장하는 방법을 의미한다.

나눈다는 이야기임

---

# Redis 특징

##Key-Value Store

![img.png](https://user-images.githubusercontent.com/42582516/133774329-00ddf3c0-a24e-40b0-9dd8-460616ea5400.png)

- Redis는 거대한 맵(Map) 데이터 저장소이다.
- Redis는 직관적이다. 그러나 데이터를 레디스 자체 내에서는 처리하기 어렵다.


# Persistence

![img.png](https://user-images.githubusercontent.com/42582516/133775761-c7644499-ae6f-4aa8-bd25-8208780c41e0.png)

- Redis는 영속성을 가집니다.

- Redis는 데이터를 disk에 저장할 수 있습니다. 따라서 Redis는 서버가 강제 종료되고 재시작하더라도 disk에 저장해놓은 데이터를 다시 읽어서 데이터가 유실되지 않습니다.

- redis의 데이터를 disk에 저장하는 방식은 snapshot, AOF 방식이 있습니다.

  - Snapshot : RDB와 비슷하게 어떤 특정 시점의 데이터를 Disk에 담는 방식을 뜻합니다. Blocking 방식의 SAVE와 Non-blocking 방식의 BGSAVE 방식이 있습니다.
  
  - AOF : Redis의 모든 write/update 연산 자체를 모두 log 파일에 기록하는 형태입니다. 서버가 재시작 시 write/update를 순차적으로 재실행하고 데이터를 복구합니다.
  
  - 가장 좋은 방식은 두 방법을 혼용해서 사용하는 방법으로 주기적으로 snapshot으로 백업을 하고 다음 snapshot까지의 저장을 AOF 방식으로 수행하는 방식입니다.

# 서버측 복제 및 샤딩 지원

- 읽기 성능 증대를 위해 서버 측 복제를 지원합니다.
- 쓰기 성능 증대를 위해 클라이언트 측 샤딩을 지원합니다.

# Redis의 장점

- 리스트, 배열과 같은 데이터를 처리하는데 유용합니다.
- Message Queue, Shared Memory, Remote Dictionary(RDBMS의 캐시 솔루션 / read 속도가 매우 빠릅니다.) 용도로 사용됩니다.
- 메모리를 활용하면서 데이터를 보존합니다.
- Redis Server는 1개의 싱글 쓰레드로 수행되며, 서버 하나에 여러개의 서버를 띄우는 것이 가능합니다.



