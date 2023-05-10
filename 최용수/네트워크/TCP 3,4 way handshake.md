# TCP란
연결 지향형 프로토콜로 연속성 있는 데이터 패킷을 주고 받을 떄 사용한다.
## TCP 특징
* 전송되는 데이터의 신뢰성 보장 ( 흐름제어, 혼잡제어, 오류제어 ) 
* 파일전송에 주로 사용
* 가상 회선을 만들어 신뢰성을 보장

# TCP 3way handshake
연결하고자 하는 두 장치 간의 논리적 접속을 성립하기 위해 사용하는 연결 확인 방식으로 3번의 확인 과정을 거친다.  

간단 예시  
A -> B : 들려?  
B -> A : 물론, 나도 들려?  
A -> B : 너도 들려!  

SYN ( synchronize sequence numbers ) : 연결 확인을 위해 보내는 무작위 숫자값
ACK ( acknowledgements ) : Client 혹은 Server로부터 받은 SYN에 1을 더해 송신측에 되돌려준다.
ISN (Initial sequence numbers) : Client와 Server가 각각 처음으로 생성한 SYN

|상태|설명|
|---|------|
|CLOSED|연결 수립을 시작하기 전의 기본 상태(연결없음)|
|LISTEN|포트가 열린 상태로 연결 요청 대기중|
|SYN-SENT|SYN 요청을 한 상태|
|SYN-RECEIVED|SYN 요청을 받고 상대방의 응답을 기다리는 중|
|ESTABLISEHD|연결의 수립이 완료된 상태, 서로 데이터를 교환할 수 있다.|

# TCP 4 way handshake
3 way handshake와 반대로 가상 회선 연결을 해제할 때 주고 받는 확인 작업이다.  
이 역시 4번의 확인 과정을 거친다.



간단 예시  
A -> B : 다 보넀어, 이제 끊자!  
B -> A : 오케이 잠시만.  
B -> A : 나도 끊을게!  
A -> B : 알곘어!  

|상태|설명|
|---|------|
|CLOSED|연결 수립을 시작하기 전의 기본 상태(연결없음)|
|ESTABLISEHD|연결의 수립이 완료된 상태, 서로 데이터를 교환할 수 있다.|
|CLOSE-WAIT|상대방의 FIN(종료요청)을 받은 상태. 상대방 FIN에 대한 ACK를 보내고 애플리케이션에 종료를 알린다.|
|LAST-ACK|CLOSE-WAIT상태를 처리 후 자신의 FIN요청을 보낸 후 FIN에 대한 ACK를 기다리는 상태|
|FIN-WAIT-1|자신이 보낸 FIN에 대한 ACK를 기다리거나 상대방의 FIN을 기다린다.|
|FIN-WAIT-2|자신이 보낸 FIN에 대한 ACK를 받았고 상대방의 FIN을 기다린다.|
|CLOSING|상대방의 FIN에 ACK를 보냈지만 자신의 FIN에 대한 ACK를 못받은 상태|
|TIME-WAIT|모든 FIN에 대한 ACK를 받고 연결 종료가 완료된 상태. 새 연결과 겹치지 않도록 일정시간 대기후 CLOSED로 전이된다.|

### TIME-WAIT ? 
먼저 연결을 끊는 (active closer) 쪽에 생성되는 소캣으로, 혹시 모를 패킷 전송 실패에 대비하기 위하여 존재하는 소켓
### TIME-WATI이 없다면 ?
패킷의 손실이 발 생하거나 통신자 간 연결 해제가 제대로 이루어지지 않을 수 있다.

