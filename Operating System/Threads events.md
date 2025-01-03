### 36장.이벤트 기반의 병행성

<details>
  
  <summary><strong> 쓰레드 없이 병행 서버를 개발할 수 있는 방법이 있나요? </strong></summary>

<br>

  ### 이벤트 기반의 병행성

  - node js와 같은 서버 프레임워크에서 사용된다.
  - GUI 기반 프로그램이나 인터넷 서버에서는 쓰레드와 다른 스타일의 병행 프로그램으로 이벤트 기반 병행성이 사용된다.
  - 이벤트(사건)의 발생을 대기하고, 이벤트가 발생하면 종류를 파악한 후 I/O를 요청, 또는 다른 이벤트 발생 등의 작업을 한다.
  - 다음에 처리할 이벤트를 결정한다는 점이 스케줄링과 비슷한 효과를 낸다.

</details>

<details>
  
  <summary><strong> 비동기 I/O를 사용하는 이유는 무엇인가요? </strong></summary>

<br>

  ## 블로킹 시스템 콜

  메타 데이터가 필요하거나 데이터에 메모리가 없어서 여러 가지를 같은 장치에 요청을 보낸다면?

  #### 쓰레드 기반 서버

  - 한 쓰레드 대기, 다른 쓰레드 실행 = 서버는 지속적으로 동작
  - I/O 처리와 다른 연산이 자연스럽게 겹쳐지는 현상이 장점

  #### 이벤트 기반 서버

  - 이벤트 핸들러가 블로킹 콜을 호출하면, 그 일을 처리하기 위해 끝날 때까지 다른 것들을 차단
  - 이벤트 루프가 블록되면, 시스템이 유휴 상태가 되고, 심각한 자원 낭비가 발생한다.

  ## 비동기 I/O

  I/O 요청이 끝나기 전, 제어권을 즉시 다시 호출자에게 돌려주고, 여러 I/O들이 완료되었는지 판단할 수 있도록 한다.

</details>

<details>
  
  <summary><strong> 이벤트 기반 서버는 상태관리를 어떻게 하나요? </strong></summary>

<br>

  ## 수동 스텍 관리

  이벤트 핸들러가 비동기 I/O를 발생할 때, 완료 시 사용할 상태를 정리해놓아야 하기 때문에, 상태 관리 문제점이 대두된다.
  (쓰레드 기반 프로그램에서는 이미 같은 스택에 정보가 들어 있으므로 불필요)

  ### continuation

  - 이벤트를 종료하는데 필요한 자료들을 한 곳에 저장한다.
  - 이벤트가 발생하면 저장해둔 정보들을 활용하여 처리한다.  

</details>

<details>
  
  <summary><strong> 이벤트는 왜 사용이 어렵나요? </strong></summary>

<br>

  - 멀티 CPU에서는 이벤트 기반 접근법의 단순함이 없어진다.
    - 다수의 이벤트 핸들러를 병렬적으로 실행해야 하므로 동기화 문제가 발생
    - 동기화 문제가 되면 락 등을 사용할 수 밖에 없다.
- 페이징(paging)과 같은 특정 종류의 시스템과 맞지 않는다.
    - 페이지 폴트가 발생하면 이벤트 핸들러 동작이 중단, 서버는 처리 완료되기 전까지 진행할 수 없게 된다.
    - 자주 발생한다면, 심각한 성능 하락이 생긴다.
- 루틴 작동방식의 지속적 변화로, 이벤트 관리가 어려워진다.
    - 루틴을 두 버전으로 나누어야 한다. (차단방식, 비차단 방식)
    - API 문법이 변경되었는지 살펴야 한다.
- 비동기 디스크 I/O가 대부분 사용가능하지만, 아직까지 간단하고 일관성 있게 적용되지 않았다.

</details>