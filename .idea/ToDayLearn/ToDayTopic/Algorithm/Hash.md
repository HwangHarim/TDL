# Hash

---

**Hash란?**
> 1. Key - Value로 데이터를 관리하는 자료구조 이다.
> 2. 순서가 정해지 않고 Key값으로 데이터를 관리한다.

![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FeHiqbk%2FbtqS1WeoGXA%2FfIo6eAPnZtGiY9Glrn8Zek%2Fimg.png)

### 해시테이블 구성
- **key**  
  - 고유한 값, hash function의 Input이 된다.
  - key값을 그대로 저장소의 색인으로 사용할 경우 key의 길이만큼의 정보를 저장해야한 공간도 따로 마련해야 하기 때문에(key의 길이가 제각각 일수 있다.), 고정된 길이의 해시로 변경한다.
  

- **hash function**
  - key를 고정된 길이의 hash로 변경해주는 역할을 한다.  
  - 서로 다른 key가 hashing 후 같은 hash값이 나오는 경우가 있다. 이를 해시충돌이라고 부른다. 해시 충돌 발생확률이 적을 수록 좋다.
  - 해시충돌이 균등하게 발생하도록 하는것도 중요하다. 모든 키가 같은 해시값이 나오게 되면 데이터 저장시 비효율성도 커지고 보안이 취약해져서 좋지 않다.


- **value**  
  - 저장소(버킷,슬롯)에 최종적으로 저장되는 값으로, hash와 매칭되어 저장되어진다.
  

- **hash table**
  - 해시함수를 사용하여 키를 해시값으로 매핑하고, 이 해시값을 주소또는 색인 삼아 데이터(value)를 key와 함께 저장하는 자료구조이다.  
  - 데이터가 저장되는 곳을 버킷, 슬롯이라고 한다.  

> ##### 해시는 색인 또는 인덱스, hash function은 key->hash로 만들어 주는 함수, 해시테이블은 hash를 주소로 삼아 데이터를 저장하는 자료구조이다.  

---
### 장점
> 해시테이블은 key-value가 1:1로 매핑되어 있기 때문에 삽입, 삭제, 검색의 과정에서 모두 평균적으로O(1)의 시간복잡도를 가지고 있다.

### 단점
> - 해시 충돌이 발생(개방 주소법, 체이닝 과 같은 기법으로 해결해 줘야 한다.)
> - 순서/관계가 있는 배열에는 어울리지 않는다.
> - 공간 효율성이 떨어진다. 데이터가 저장되기 전에 저장공간을 미리 만들어놔야한다. 공간을 만들었지만 공간에 채워지지 않는 경우가 발생한다.
> - hash function의 의존도가 높다. 해시함수가 복잡하다면 hash를 만들어 내는데 오래 걸릴 것이다
> ![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbjQM18%2FbtqTh0eKrgg%2F6elm4BkpGBazUNfyyQTTkk%2Fimg.png)

### Direct-address table

- 키의 전체 개수와 동일한 크기의 버킷을 가진 해시테이블을 Direct-address table이라고 한다. 
-  하지만 실제 사용하는 키는 명개 되지 않을 경우에는 전체 키의 갯수만큼의 테이블 크기를 유지하는 것은 메모리 낭비이다.

## 해쉬 충돌

---

### 해결 방법 1. Chaining

![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnMfgg%2FbtqS1WyRuWI%2F32LmJGOvrT9YTndHMvYW50%2Fimg.png)


>체이닝은 저장소(Bucket)에서 충돌이 일어나면 기존 값과 새로운 값을 연결리스트로 연결하는 방법이다.

#### 장점
> 미리 충돌을 대비해서 공간을 많이 잡아놓을 필요가 없다. 출돌이 나면 그때 공간을 만들어서 연결만 해주면 된다.

#### 단점
> 같은 hash에 자료들이 많이 연결되면 검색ㄴㄴ시 효율이 낮아진다.해결 방법


### 해결 방법 2. Open Addressing(개방주소법)개방 주소법


![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqT8Kh%2FbtqSZxlHJBv%2FOOV1zISHKWBVoJGRDiytDK%2Fimg.png)

> 충돌이 일어나면 비어있는 hash에 데이터를 저장하는 방법이다. 개방주소법의 해시 테이블은 hash와 value가 1:1관계를 유지한다


#### 탐색법

> - 선형탐색
> - 제곱탐색

---

## Java에서 HashMap

>HashTable이란 JDK 1.0부터 있던 Java의 API이고, HashMap은 Java2에서 처음 선보인 Java Collections Framework에 속한 API이다.
HashTable 또한 Map 인터페이스를 구현하고 있기때문에 HashMap과 HashTable이 제공하는 기능은 같다.

### 차이점

- 보조 해시 함수  
  HashMap은 보조 해시함수를 사용하기 때문에 보조 해시 함수를 사용하지 않는 HashTable에 비하여 해시 충동(hash collision)이 덜 발생할 수 있어 상대적으로 성능상 이점이 있다.


- 동기화  
HashMap의 경우 동기화를 지원하지 않는다. 그래서 Hash Table은 동기화 처리라는 비용때문에 HashMap에 비해 더 느리다고 한다. 프로그래밍상의 편의성 때문에 멀티쓰레드 환경에서도 HashTable을 쓰기보다는 HashMap을 다시 감싸서 Map m == Collections.syschronizedMap(new HashpMap()); 과 같은 형태가 더 선호된다.

### HashMap
> HashMap에서 사용하는 충돌기법 방식은 Seaparate Chaining 이다.
> 1. Open Addressing은 데이터를 삭제할 때 처리가 효율적이기 어려운데 HashMap에서 remove()메서드는 비번하게 호출될 수 있기 때문
> 2. 하나의 해시 버킷에 8개 이상의 키-값 쌍이 모이면 LinkedList를 Tree구조로 바꾼다. 그리고 버킷이 6개에 이르게 되면 다시 LinkedList 구조로 변경한다.
> 3. HashMap은 key-value 쌍 데이터 개수가 일정 개수 이상이 되면, 해시 버킷의 수를 두배로 늘린다. 해시 버킷의 수를 늘려서 해시 충돌의 확률을 줄일 수 있다.