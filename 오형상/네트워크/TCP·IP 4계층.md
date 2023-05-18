<img src="https://github.com/kj-cs-study/CS-Study/assets/110380812/e722e3a5-f6de-489d-8c0e-643ba97267bb.png"  width="600" height="400"/>

### OSI 7계층
> 통신 접속에서 완료까지의 과정을 네트워크 통신을 구성하는 요소들에 따라 7단계로 정의한 국제 통신 표준 규약

[OSI 7계층 자세히 보기](https://github.com/Songwonseok/CS-Study/blob/main/Network/OSI%207%EA%B3%84%EC%B8%B5.md)

📌 실제로 우리가 사용하는 네트워크는 TCP/IP 4계층이다.

## TCP/IP 4계층

- 현재 수많은 프로그램들이 인터넷으로 통신하는데 있어 가장 기반이 되는 프로토콜로 실제 대다수 프로그램은 TCP와 IP로 통신

### 4️⃣ 응용 계층(Application Layer)

**데이타 단위**: Data/Message

- 사용자와 가장 가까운 계층으로 사용자가 소프트웨어 application과 소통할 수 있게 해준다
- 응용프로그램(application)들이 데이터를 교환하기 위해 사용되는 프로토콜
- 사용자 응용프로그램 인터페이스를 담당

**예시** : 파일 전송, 이메일, FTP, HTTP, SSH, Telnet, DNS, SMTP 등

### 3️⃣ 전송 계층(Transport Layer)

**데이타 단위**: Segment

**전송 주소**: Port

- 통신 노드 간의 연결 제어 및 자료 송수신을 담당
- 애플리케이션 계층의 세션과 데이터그램 통신서비스 제공
- 세그먼트 (Segment)단위의 데이타 구성
    - 실질적인 데이터 전송을 위해 데이타를 일정 크기로 나눈 것. 발신, 수신, 포트주소, 오류검출코드가 붙게된다

**예시** : TCP, UDP, RTP, RTCP 등

### 2️⃣ 인터넷 계층(Internet Layer)

**데이타 단위**: 패킷

**전송 주소**: IP

- 네트워크상 최종 목적지까지 정확하게 연결되도록 연결성을 제공
- 단말을 구분하기위해 논리적인 주소(Logical Address) IP를 할당
    - 출발지와 목적지의 논리적 주소가 담겨있는 IP datagram이라는 패킷으로 데이타를 변경
    - 데이터 전송을 위한 주소 지정
- 라우팅(Routing) 기능을 처리
    - 경로 설정
- 최종 목적지까지 정확하게 연결되도록 연경성 제공
- 패킷단위의 데이타 구성
    - 세그먼트를 목적지까지 전송하기 위해 시작 주소와 목적지의 논리적 주소를 붙인 단위. 데이타 + IP Header

**예시 :** IP, ARP, ICMP, RARP, OSPF

### 1️⃣ 네트워크 연결 계층(Network Access Layer/Network Interface Layer)

**데이타 단위**: 프레임

**전송 주소**: MAC

- 물리적으로 데이타가 네트워크를 통해 어떻게 전송되는지를 정의
    - 논리주소(IP주소 등)이 아닌 물리주소(예. MAC주소(Media Access Control Address))을 참조해 장비간 전송
    - MAC주소란 컴퓨터의 하드웨워 주소
- 기본적으로 에러검출/패킷의 프레임화 담당
- 프레임(Frame)단위의 데이타 구성
    - 최종적으로 데이타 전송을 하기 전 패킷헤더에 MAC주소와 오류 검출을 위한 부분을 첨부

**예시 :** MAC, LAN, 패킷망 등에 사용되는 것 예) Ethernet, PPP, Token Ring 등
