# JPA 더티 체킹

---

**더티체킹이 필요한 이유**
- jpa에서는 엔티티 매니저가 엔티티를 저장/조회/수정/삭제가 일어난다.
  - 저장 -> persist
  - 조회 ->find
  - 삭제->delete
  - 수정에 해당하는 매서드는 없다. 
    - 대신 더티체킹(Dirty Checking)을 지원한다. 
- 더티체킹은 Transaction 안에서 엔티티의 변경이 일어나면, 변역 내용을 자동으로 데이터베이스에 반영하는 jpa의 특징이다.
- 데이터베이스에서 변경 데이터를 저장하는 시점
  - Transaction commit 
  - EntityMannanger flush
  - JPQL 사용시점

### 더디체킹 대상
> 더티체킹을 진행하는 검사의 대상
> 
>영속성 컨텍스트가 관리하는 엔티티를 대상으로 한다.
> 
>       detach 된 엔티티 (준영속)
>
>       DB에 반영되기 전 처음 생성된 엔티티 (비영속)
>준영속/비영속 상태의 엔티티는 더티 체킹에 해당사항이 없다.
> 
>값을 변경해도 데이터베이스에 반영되지 않음.  


![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcokEKI%2FbtqygTOISLW%2FTrI5hAUoR9wiVP92OJlIJ0%2Fimg.png)

**더티체킹이 일어나는 환경은 두가지 조건이 충족되어야 한다.**

     1) 영속 상태 안에서 있는 엔티티인 경우
     2) Transaction 안에서 엔티티를 변경하는 경우

---

### 1) @Transaction을 사용하는 경우 

    @Service
    public class ExampleService {
        @Transactional
        public void updateInfo(Long id, String name) {
            User user = userRepository.findById(id);
            user.setName(name);
        }
    }


### 2) EntityTransaction을 이용해서 트랜잭션을 범위를 지정하고 사용하는 경우 

    @Service
    public class ExampleService {
        public void updateInfo(Long id, String name) {
            EntityManager em = entityManagerFactory.createEntityManager();
            EntityTransaction tx = em.getTransaction();
            // 1. 트랜잭션 시작
            tx.begin();
            // 2.User 엔티티를 조회 & User 스냅샷 생성
            User user = em.find(User.class, id);
            // 3.User 엔티티의 name을 변경
            user.setName(name);
            // 4. 트랜잭션
            // 5.User 스냅샷과 최종 user의 내용을 비교해서 Dirty를 Checking 해서 Update Query 발생
            tx.commit();
        }
    }

### 더티 체킹이 발생하면 어떤 절차가 진행될까요?

- 1번/2번에서 더티 체킹이 일어나면 다음과 같은 Query 문이 발생한 것을 볼 수 있다.
- 분명 user의 업데이트에 대한 메서드를 호출하지 않았음에도 불구하고 Query가 발생한다.(더티 체킹)
- **그리고 커밋 이후, 트랜잭션이 끝나는 시점에 모든 엔티티에 대한 정보를 DB에 방영 함**
  ![img.png](https://velog.velcdn.com/cloudflare/seungho1216/69f24fb7-a660-4e9d-84bc-35cd5164ae0b/1%EC%B0%A8%EC%BA%90%EC%8B%9C2.png)

### 트랜잭션이 아닌 상태에서 엔티티 내용이 변경하는 경우

    public void updateInfo() { 
        User user = userRepository.findById(2L)
         .orElseThrow(() -> new ErrorCodeException(ErrorType.USER_IS_NOT_EXISTING));
         user.setEmail("hello@gmail.com");
        System.out.println(userRepository.existsByEmail("hello@gmail.com"));
    }

**@Transactional를 걸어준 경우**

1. Table: User에서 PK id가 2인 user 엔티티 객체 조회
2. user의 email을 hello@gmail.com로 수정 (Dirty Checking 발동)
3. hello@gmail.com를 email로 가진 user 엔티티 유무 확인, 2번 과정에서 수정되었기에 true 출력


**@Transactional를 걸어주지 않은 경우**

1. Table: User에서 PK id가 2인 user 엔티티 객체 조회
2. user의 email을 hello@gmail.com로 수정 (Dirty Checking 발동)
3. hello@gmail.com를 email로 가진 user 엔티티 유무 확인, 2번 과정에서 수정되었기에 true 출력
4. 2번 과정에서 수정되지 못해서 false 출력

**Transaction을 사용하지 않아서 반영되지 못한 내용을 반영하고 싶은 경우,**

**원하는 시점에 save, saveAndFlush를 사용합니다.**

### update가 부담스러운 경우 EX> 만약 20개가 넘는 필드에서 하나만 고칠경우는??

---

> JPA는 전체 필드를 업데이트하는 방식을 기본값으로 사용한다.

update가 부담스러운 경우 (이런 경우 정규화가 잘못된 확률이 높다.)

**@DynamicUpdate로 변경 필드만 반영되도록 할 수 있다.**

    @Getter
    @NoArgsConstructor
    @Entity
    @DynamicUpdate // 변경한 필드만 대응
    public class Pay {

        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;

        private String tradeNo;
        private long amount;
    }


### 단점

> 위에서 설명한 것처럼 JPA의 구현체인 hibernate는 애플리케이션이 처음 로드될 때 entity 들을 모두 스캔하여 업데이트할 쿼리를 캐시 해놓고 사용 
> 
> 즉 DynamicUpdate를 사용하면 캐시 된 쿼리를 사용하지 못하고 새로 동적 쿼리를 생성하고, 이 과정에서 오버헤드가 발생해 오히려 성능이 떨어짐.
---
출처 : https://interconnection.tistory.com/121
