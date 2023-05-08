## 3Hand Shake

### 개념

TCP/IP 프로토콜을 이용해서 통신을 하는 응용 프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다.

### 작동 과정

![Untitled](https://user-images.githubusercontent.com/110380812/236743731-8b28d95d-2c73-4067-870b-850838e8dab3.png)


- **Step 1 (SYN)**
    
    **클라이언트는 서버와 커넥션을 연결하기 위해 SYN을 보낸다. (seq : x)**
    
    - 송신자가 최초로 데이터를 전송할 때 Sequence Number를 임의의 랜덤 숫자로 지정하고, SYN 플래그 비트를 1로 설정한 세그먼트를 전송한다.
    - PORT 상태
        - Client : `CLOSED` `SYN_SENT` 로 변함
        - Server : `LISTEN`
- **Step 2 (SYN + ACK)**
    
    **서버가 SYN(x)을 받고, 클라이언트로 받았다는 신호인 ACK와 SYN 패킷을 보냄 (seq : y, ACK : x + 1)**
    
    - 접속요청을 받은 Q가 요청을 수락했으며, 접속 요청 프로세스인 P도 포트를 열어달라는 메세지를 전송 (SYN-ACK signal bits set)
    - ACK Number필드를 Sequence Number + 1 로 지정하고 SYN과 ACK 플래그 비트를 1로 설정한 새그먼트 전송 (`Seq=y, Ack=x+1, SYN, ACK`)
    - PORT 상태
        - Client : `CLOSED`
        - Server : `SYN_RCV`
- **Step 3 (ACK)**
    
    **클라이언트는 서버의 응답은 ACK(x+1)와 SYN(y) 패킷을 받고, ACK(y+1)를 서버로 보냄**
    
    - 마지막으로 접속 요청 프로세스 P가 수락 확인을 보내 연결을 맺음 (ACK)
    - 이때, 전송할 데이터가 있으면 이 단계에서 데이터를 전송할 수 있다.
    - PORT 상태
        - Client : `ESTABLISED`
        - Server : `SYN_RCV` ⇒ ACK ⇒ `ESTABLISED`

## 4 Hand Shake

### 개념

4-Way Handshake은 연결을 해제 (Connecntion Termination)하는 과정이다. 여기서는 FIN 플래그를 이용한다.

- `FIN` (finish) : 세션을 종료시키는데 사용되며, 더 이상 보낸 데이터가 없음을 나타낸다.

### 작동 과정

- Step 1

클라이언트가 연결을 종료하겠다는 FIN플래그를 전송한다.

- Step 2

서버는 일단 확인메시지를 보내고 자신의 통신이 끝날때까지 기다리는데 이 상태가 TIME_WAIT상태다.

- Step 3

서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN플래그를 전송한다.

- Step 4

클라이언트는 확인했다는 메시지를 보낸다.
