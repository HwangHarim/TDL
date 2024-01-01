# Domain Name System

- DNS 서비스는 전 세계에 배포된 서비스로서, www.example.com과 같이 사람이 읽을 수 있는 이름을 192.0.2.1과 같은 숫자 IP 주소로 변환하여 컴퓨터가 서로 통신할 수 있도록 한다.
- 인터넷의 DNS 시스템은 이름과 숫자 간의 매핑을 관리하여 마치 전화번호부와 같은 기능.

**▶ DNS 서버의 특징**

**1) 호스트의 도메인 이름을 네트워크 주소로 바꾸거나 그 반대의 변환을 수행할 수 있도록 하기 위해 개발되었음.**

**2) 일반적으로 www.xxx.com 과 같은 도메인 주소를 입력하면, 192.168.0.100과 같은 IP 주소로 변환시켜주는 역할을 수행.**

**3) DNS 서버는 계층 구조로 이루어져 있고 루트 DNS 서버, 최상위 레벨 서버, 책임 DNS 서버로 나누고 추가로 로컬 DNS 서버가 존재.**

**4) 루트 DN 서버는 전 세계에 13개 ( A부터 M까지 ) 있음.**

**5) 최상위 레벨 서버는 com, org, net, kr, uk, fr, ca, jp와 같은 모든 국가의 상위 레벨 서버.**

**6) 책임 DNS 서버는 인터넷을 통해 서비스를 제공하능 모든 기관이 가지는 서버.**

**7) 로컬 DNS 서버는 사용자에게 직접적으로 도메인에 대한 질의를 받고 그에 대한 응답을 해주는 서버의 역할을 수행.**

# 예시

![https://velog.velcdn.com/images/rlarlxo6919/post/4e9d3229-f80e-48c0-bb49-181f684df663/image.png](https://velog.velcdn.com/images/rlarlxo6919/post/4e9d3229-f80e-48c0-bb49-181f684df663/image.png)

- 내 컴퓨터에서 www.naver.com에 접속하려 한다.

![https://velog.velcdn.com/images/rlarlxo6919/post/0e743dcc-cc55-4547-814c-1e102e97f007/image.png](https://velog.velcdn.com/images/rlarlxo6919/post/0e743dcc-cc55-4547-814c-1e102e97f007/image.png)

- 내 브라우저는 현재 www.naver.com의 ip를 모르기 때문에 PC에 설정된 로컬 DNS 서버(네임서버)에 해당 도메인과 ip가 있는지 요청.
- 로컬 DNS 서버는 통신사마다 지정된 곳에 위치. 따라서 사용자가 다른 위치에 있는 DNS 서버로 연결을 바꿀 수 있다.

![https://velog.velcdn.com/images/rlarlxo6919/post/805a5934-ee1d-405e-a740-c3e62d444ab1/image.png](https://velog.velcdn.com/images/rlarlxo6919/post/805a5934-ee1d-405e-a740-c3e62d444ab1/image.png)

- 로컬 DNS 서버에 해당 도메인이 있다면 바로 반환해준다.

![https://velog.velcdn.com/images/rlarlxo6919/post/cbcabf73-1472-462b-9dc0-4cb83c09c48f/image.png](https://velog.velcdn.com/images/rlarlxo6919/post/cbcabf73-1472-462b-9dc0-4cb83c09c48f/image.png)

- 로컬 DNS 서버에 없다면 Root 서버에 해당 도메인의 ip를 어디서 찾을 수 있는지 요청.

![https://velog.velcdn.com/images/rlarlxo6919/post/6f7c2f9c-76e7-4b13-88a8-2c7a8cfcdb8e/image.png](https://velog.velcdn.com/images/rlarlxo6919/post/6f7c2f9c-76e7-4b13-88a8-2c7a8cfcdb8e/image.png)

- Root 서버는 .com으로 끝나는 도메인들을 담당하는 서버 ip주소를 반환.

![https://velog.velcdn.com/images/rlarlxo6919/post/498fb81e-99ea-4173-abba-78e5e04aa493/image.png](https://velog.velcdn.com/images/rlarlxo6919/post/498fb81e-99ea-4173-abba-78e5e04aa493/image.png)

- .com 서버 ip로 요청을 하면 해당 도메인 서버는 naver.com의 도메인을 가진 DNS 서버 ip 주소를 반환.

![https://velog.velcdn.com/images/rlarlxo6919/post/69d00449-0ffd-4400-ba66-f1cd7f2bc7fd/image.png](https://velog.velcdn.com/images/rlarlxo6919/post/69d00449-0ffd-4400-ba66-f1cd7f2bc7fd/image.png)

- naver.com의 도메인을 가진 DNS 서버에서 www에 대한 ip를 받아서 로컬 DNS 서버는 브라우저에게 반환하고 브라우저는 www.naver.com에 접속.