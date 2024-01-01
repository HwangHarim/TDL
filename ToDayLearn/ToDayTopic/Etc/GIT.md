### **GIT이란 무엇인가?**

깃(Git)은 2005년에 리누스 토르발스에 의해 개발된 '**분산 버전관리 시스템**(Distributed Version Control Systems - DVCS)'으로, 컴퓨터 파일의 변경사항을 추적하고 여러명의 사용자들 간에 파일에 대한 작업을 조율하는데 사용된다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/faaf56b2-b997-4559-861c-2909449fe886/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220723%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220723T153305Z&X-Amz-Expires=86400&X-Amz-Signature=1a604ecd8a351b33906860868fe3f51bf69234298c735223f21ae9df0ee0cd4b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

즉, 주로 **여러명의 개발자**가 **하나의** 소프트웨어 개발 **프로젝트**에 참여할 때, **소스 코드를 관리**하는데 주로 사용된다.

### 

### **Git 기본 용어**

- **Repository**:

  **저장소**. 저장소는 히스토리, 태그, 소스의 가지치기 혹은 branch에 따라 버전을 저장. 작업자가 변경한 모든 히스토리를 확인 가능.


- **Working Tree** :

  저장소를 어느 한 시점을 바라보는 작업자의 현재 시점.


- **Staging Area** :

  저장소에 커밋하기 전에 **커밋을 준비하는 위치**.


- **Commit** :

  현재 **변경된 작업 상태를** 점검을 마치면 **확정하고 저장소에 저장**하는 작업.


- **Head** :

  현재 **작업중인 Branch**를 가리킨다.


- **Branch** :

  가지 또는 분기점. 작업을 할때에 **현재 상태를 복사**하여 **Branch에서 작업**을 한 후에 완전하다 싶을때 Merge를 하여 작업을 한다.


- **Merge** :

  다른 Branch의 내용을 현재 Branch로 가져와 합치는 작업을 의미한다.


### **Git 기본 명령어**

- **git help :**

  **도움말** 기능(가장 많이 사용하는 21개의 깃 명령어 출력). 사용법이 궁금한 명령어에 대해 'git help [궁금한 명령어]'를 타이핑시, 해당 깃 명령어의 설정과 사용에 대한 도움말 출력.

- **git init :**

  깃 저장소를 **초기화**. 저장소나 디렉토리 안에서 이 명령을 실행하기 전까지는 그냥 일반 폴더이다. **이 명령어를 입력한 후에야 추가적인 깃 명령어 입력 가능**.

- **git status :**

  저장소 **상태 체크.** 어떤 파일이 저장소 안에 있는지, 커밋이 필요한 변경사항이 있는지, 현재 저장소의 어떤 브랜치에서 작업하고 있는지 등의 상태정보 출력.

- **git branch :**

  **새로운 브랜치 생성.** 여러 협업자와 작업할 시, 이 명령어로 새로운 브랜치를 만들고, 자신만의 변경사항과 파일 추가 등의 커밋 타임라인을 생성, 완성 후 협업자의 branch 혹은 main과 merge.

- **git add :**

  '**staging 영역'에 변경내용 추가**. 다음 commit명령 전까지 변경분을 staging 영역에 보관하여 변동내역을 저장.