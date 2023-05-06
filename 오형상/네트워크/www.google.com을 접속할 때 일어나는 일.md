## 큰 흐름

1. 브라우저는 URL에 적힌 값을 Parsing하여 HTTP Request Message를 만들고 👉 OS에 전송 요청을 한다. 이 때, Domain으로 요청을 보낼 수 없기에 DNS Lookup 과정을 수행한다.

2. DNS Lookup 과정에서 크롬 브라우저의 경우 브라우저 👉 hosts 파일 👉 DNS cache 순서로 Domain에 매칭되는 IP를 찾는다. 일반적인 DNS Lookup 과정은 Root Domain Server 👉 Sub Domain Server 순서로 찾게 된다.

3. Domain으로의 요청은 Protocol Stack (OS에 내장된 네트워크 제어용 소프트웨어) 에 의해서 패킷에 담기고 👉 패킷에 제어 정보를 덧붙여 LAN Adapter에 전송한다. 👉 LAN Adapter는 이를 전기신호로 변환시켜 송출한다.

4. 패킷은 Switching Hub 등을 경유하여 👉 인터넷 접속용 Router에서 ISP로 전달되고 👉 인터넷으로 이동한다. Access 회선에 의해 통신사용 Router로 운반되고 👉 인터넷의 핵심부로 전달된다. 고속 Router들 사이로 목적지까지 패킷이 흘러들어간다.

5. 인터넷의 핵심부를 통과한 패킷은 목적지 LAN에 도착하고, 방화벽이 패킷을 검사한 후 Cache Server로 보내 Web Server에 갈 필요가 있는지 검사한다.

6. Web Server에 도착한 패킷을 Protocol Stack이 추출하여 메시지를 복원하고 Web Server Application에 넘긴다. Web Server Application은 요청에 대한 응답 데이터를 작성하여 클라이언트로 회송한다 (전달된 방식 그대로 전송된다).
