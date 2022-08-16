# 트랜잭션(Transaction)
### 트렌잭션이란?
> 데이터베이스의 상태를 변화시키기 위해 수행하는 작업 단위


상태를 변화시킨다는 것 -> SQL질의어를 통해 DB에 접근하는 것

- SELECT
- INSERT
- DELETE
- UPDATE

작업 단위 -> 많은 SQL 명령문들을 사람이 정하는 기준에 따라 정하는 것

    예시> 사용자 A가 사용자 B에게 만원을 송금한다.

    이때 DB작업
        -1. 사용자 A계좌에서 만원을 차감 : UPDATE 문을 사용
        -2. 사용자 B계좌에서 만원을 추가 : UPDATE 문을 사용
    
    현재 작업 단위 : 출금 UPDATE문 + 입금 UPDATE문
        -> 이를 하나의 트랜잭션이라고 한다.
    - 위 두 쿼리문 모두 성공적으로 완료되어야만 "하나의 작업"이 완료되는 것이다 'commit'
    - 작업 단위에 속하는 쿼리 중 하나라도 실패하면 모든 쿼리문을 취소하고 이전 상태로 돌려좋아야한다. 'Rolback'

### 트랜잭션 특징

- 원자성(Atomicity)
    > 트랜 잭션이 모두 성공 or 모두 실패
  
  만약 긴 트랜젝션 범위 내에서 대부분의 로직이 성공적으로 수행됐는데 마지막에 문제가 생겨서 롤백이 된다고 생각해보자. 문제가 발생하지 않은 영역까지 반복적으로 수행해야 하는건 손해이기 때문에 성공적인 지점 까지는 savePoint를 설정할 수 있다.

  ### savePoint

  savePoint는 트랜젝션 내부에서 사용자가 지정할 수 있는 세부 작업 단위라고 생각할 수 있다. 아래의 그림처럼 특정 지점에 savePoint를 설정 한 후 'Rollback to savePoint1' 을 통해 해당 지점으로 롤백을 할 수 있다.

  기억해야할 점은 아래 그림에서 SP1으로 롤백을 한 뒤에는 미래 시점인 SP2의 savePoint는 삭제 된다는 것이다.

  ![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbZAlvz%2Fbtrpgzeqiin%2FgbfmebyddSKi9hKGRSeJR1%2Fimg.png)
- 일관성(Consistency)
    > 트랜잭션의 작업 처리 결과는 항상 같아야한다.

- 독립성(Isolation)
  > 둘 이상의 트랜잭션이 동시에 병행 실행되고 있을 때, 어떤 트랜잭션도 다른 트랜잭션 연사에 끼어들 수 없다.

- 지속성(Durability)
  > 트랜잭션이 성공적으로 완료되었으면, 결과는 영구적으로 반영되어야 한다.

### Commit
  > 하나의 트랜잭션이 선ㅇ공적으로 끝났고, DB가 일관성있는 상태일 때 이를 알려주기 위해 사용하는 연산

### Rolback
  > 하나의 트랜잭션이 처리가 비정상적으로 종료되어 트랜잭션 원자성이 깨진 경우
  > 
  > transaction이 정상적으로 종료되지 않았을 때, last consistent state -> transaction의 시작 상태로 rollback 할 수 있다.
  >

### 트랜잭션의 상태

![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F999C55345B6D2ED308)

활동(Active) : 트랜잭션이 실행중인 상태

실패(Failed) : 트랜잭션 실행에 오류가 발생하여 중단된 상태

철회(Aborted) : 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태

부분 완료(Partially Committed) : 트랜잭션의 마지막 연산까지 실행했지만, Commit 연산이 실행되기 직전의 상태

완료(Committed) : 트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태

## Transaction 관리를 위한 DBMS의 전략
  
  ###1. DBMS의 구조
  > 크게 2가지 : Query Processor (질의 처리기), Storage System(저장 시스템)
  > 
> 입출력 단위 : 고정 길이의 page 단위로 disk에 읽거나 쓴다
  >
> 저장 공간 : 비휘발성 저장 장치인 disk에 저장, 일부분을 Main Memory에 저장
>
![img.png](https://d2.naver.com/content/images/2015/06/helloworld-407507-1.png)

  ###2. Page Buffer Manager or Buffer Manager
  
DBMS의 storage System에 속하는 모듈 중 하나로, Main Memory에 유지하는 페이지를 관리하는 모듈
> Buffer 관리 정책에 따라, UNDO 복구와 REDO 복구가 요구되거나 그렇지 않게 되므로,
> 
>transaction 관리에 매우 중요한 결정을 가져온다.

### UNDO, REDO
    REDO는 "다시 하다."라는 뜻을 가지고 UNDO는  "원상태로 돌리다" 라는 뜻을 가지고 있다.

    즉 REDO는 무언가를 다시 하는 것이고 UNDO는 무언가를 되돌리는 것이다.


REDO는 기본적으로 복구의 역할을 합니다.

 - 오라클 서버에 무슨 작업을 하든지 모두 REDO에 기록이 됩니다. (UNDO 포함)

 - UNDO는 작업 롤백과, 읽기 일관성, 복구한다.

 - REDO와UNDO의 공통점은 복구를 한다는 것이다.

하지만 둘의 **복구 방법은 차이**가 있습니다.

REDO는 복구를 할때 사용자가 했던 작업을 그대로 다시 하지만 UNDO는 사용자가 했던 작업을 반대로 진행한다.

즉 사용자의 작업을 원상태로 돌린다.
>  ### 예를 들어 아래와 같은 작업을 했을때 세션이 비정상 종료 되었다고 가정
>
> 만일 세션이 비정상 종료가 되기전 COMMIT을 하지 않았다면 UNDO를 이용하여 아래와 같은 작업을 이어서 하게된다.
> 
> 결국 시스템 장애시 REDO 데이터를 이용해서 마지막 CHECK POINT부터 장애까지의 DB BUFFER CACHE 를 복구하게 된다.
> 
> 이게 완료가 되면 UNDO를 이용하여 COMMIT되지 않은 데이터를 모두 ROLLBACK 함으로써 복구를 완료하게 된다.
> 
> **결국 REDO가 UNDO를 복구하고 최종적으로 UNDO가 복구를 하게 된다**