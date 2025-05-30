<details>
  
<summary>
  <strong>TCP에서 '지연 ACK(Delayed ACK)' 메커니즘이란 무엇이며, 특징을 설명해주세요.</strong>
</summary>

<br>

지연 ACK(Delayed ACK)는 TCP 프로토콜에서 네트워크 트래픽을 줄이고 효율성을 높이기 위해 사용되는 메커니즘입니다.

<br>

동작 방식:

1. 순서에 맞는 세그먼트가 도착한 경우: 
  - TCP는 ACK를 즉시 보내지 않고 최대 500ms까지 대기합니다. 이 대기 시간 동안 추가 데이터 세그먼트가 도착할 가능성을 확인합니다.
    -  추가 데이터 세그먼트가 도착하면 두 세그먼트를 합쳐 하나의 누적된 ACK를 반환합니다.
    -  추가 데이터가 도착하지 않으면 대기 시간 이후 ACK를 보냅니다.
2. 이미 ACK를 대기 중인 세그먼트가 있는 상태에서 또 하나의 세그먼트가 도착한 경우:
  - TCP는 즉시 누적된 ACK를 보내 두 세그먼트를 모두 확인 응답합니다. 

<br>

장점:
- 네트워크 트래픽 감소: ACK의 빈도를 줄여 전송 효율성을 높입니다.
- 성능 최적화: 네트워크 자원을 보다 효과적으로 활용할 수 있습니다.
  
<br>
</details>
  
<br>

<details>
<summary><strong>TCP의 특징을 GBN 프로토콜, SR 프로토콜과 비교하여 설명해주세요.</strong></summary>

<br>

### 1. TCP의 기본 동작 (GBN 프로토콜 기반)  
TCP는 기본적으로 **누적 ACK** 방식을 사용합니다.

- **누적 ACK:** 수신자는 순서대로 도착한 가장 마지막 세그먼트에 대한 ACK만 송신자에게 보냅니다.
- **중복 ACK:** 순서가 틀린 세그먼트가 도착하면 즉시 중복 ACK(Duplicate ACK)를 송신합니다. 이 중복 ACK는 수신자가 기대하는 데이터의 순서 번호를 포함합니다.

<br>

### 2. TCP의 효율화 (SR 프로토콜 요소 포함)  
TCP는 GBN과 SR의 장점을 조합하여 효율성을 높였습니다.

- **재전송 최적화:** TCP는 일부 구현에서 순서가 틀린 데이터를 임시로 저장할 수 있습니다(이는 SR의 특징).
- **Selective Acknowledgment (SACK) 옵션:**  
  SACK을 통해 송신자는 정확히 손실된 데이터만 재전송함으로써 네트워크 자원을 효율적으로 사용합니다.  
  - GBN처럼 모든 데이터를 재전송하지 않아 불필요한 트래픽을 줄입니다.

<br>

### 3. 비교 요약

| 특징                   | GBN                      | SR                     | TCP                              |
|------------------------|--------------------------|------------------------|----------------------------------|
| ACK 방식               | 누적 ACK                 | 선택적 ACK             | 기본 누적 ACK, 선택적 ACK(SACK) |
| 손실 시 재전송 방식     | 손실 이후 모든 세그먼트 재전송 | 손실된 세그먼트만 재전송 | SACK 사용 시 손실된 데이터만 재전송 |
| 순서가 틀린 데이터 처리 | 무시                     | 버퍼에 저장            | 일부 구현에서 버퍼에 저장 가능  |

<br>

</details>
