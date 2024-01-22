# 네트워크

- TCP vs UDP
  - TCP와 UDP의 차이점에 대해서 설명해보세요.
  - TCP 3, 4 way handshake에 대해서 설명해보세요.
  - OSI 7계층과 그 존재 이유, TCP/IP 4계층에 대해 설명해보세요.
    - 웹 서버 소프트웨어(Apache, Nginx)는 OSI 7계층 중 어디서 작동하는지 설명해보세요.
    - 웹 서버 소프트웨어(Apache, Nginx)의 서버 간 라우팅 기능은 OSI 7계층 중 어디서 작동하는지 설명해보세요.

- HTTP
  - HTTP의 문제점
  - HTTP와 HTTPS의 차이점에 대해서 설명해보세요.
  - HTTPS에 대해서 설명하고 SSL Handshake에 대해서 설명해보세요.
  - SSL 인증서 암호화 기법인 대칭키 암호화 기법, 공개키 암호화 기법에 대해 설명해주세요.
  - 무상태성과 비연결성에 대해서 설명해주세요.
  - Expires, Date, Age, If-Modified-Since의 차이점에 대해 설명해주세요.
  - If-Modified-Since와 If-None-Match의 차이점에 대해 설명해주세요.

- REST API
  - RESTful이란 무엇이며, 이것에 대해서 아는대로 설명해보세요.
  - HTTP 메서드와 이것이 하는 역할에 대해서 설명해보세요.
  - GET과 POST의 차이점에 대해서 설명해보세요.
  - PUT과 PATCH의 차이점에 대해서 설명해보세요.

- 기타
  - CORS(Cross-Origin Resource Sharing)는 무엇인가 왜 이러한 방법이 정의 되었으며, 본인이 코드를 작성하면서 CORS와 관련하여서 경험하였던 이슈는 무엇인가요?
    - same-origin 정책에 대해 설명해주세요.
  - 웹 통신의 큰 흐름: https://www.google.com/ 을 접속할 때 일어나는 일 (DNS round robin 방식)
  - OAuth에 대해서 간단히 설명해주세요.
  - 브라우저 저장소에 대해서 설명해주세요.
    - Session과 Cookie 그리고 Token의 차이에 대해 설명해주세요.
  - 프록시 서버가 필요한 이유

### TCP vs UDP

- 공통점 : OSI 7 Layer 중 전송 계층에서 사용되는 프로토콜

- TCP (Transmission Control Protocol)
  - 연결 위주 전송 방식 (Connection-Oriented)
  - 신뢰성을 보장하며 3-way handshaking 과정을 통해 연결
  - TCP 연결경로를 통하여 데이터를 전송하고 이에 대한 응답(ack)을 받음으로 써 그 데이터가 올바르게 전송되었음을 보장
  - 양방향 연결 (가상회선 연결방식)
  - ex)

- UDP (User Datagram Protocol)
  - datagram 기반의 전송 프로토콜
  - 비연결형 데이터 전송, 비신뢰성 프로토콜 (데이터가 목적 호스트에 도착한다는 보장을 하지 못한다)
  - TCP보다 속도가 빠르다
  - ex) 실시간 스트리밍 서비스

#### TCP handshaking

<center><img src="./image/tcp-handshake.png" width="40%"></center>

- TCP 3-way handshaking (서버와 클라이언트를 논리적으로 연결하는 과정)
  1. [클라이언트 -> 서버]
     랜덤으로 Sequence number(J)를 만들고, 자신의 `SYN(J)`를 서버에 보낸다
  2. [서버 -> 클라이언트]
     서버는 `SYN(J)`를 받고, 랜덤으로 Sequence number(K)를 만든다
     `SYN(J)`를 잘 받았다는 의미인 `ACK(J+1)`과 서버가 만든 `SYN(K)`를 클라이언트에게 보낸다
  3. [클라이언트 -> 서버]
     클라이언트는 `SYN(K)`를 잘 받았다는 의미로 `ACK(K+1)`을 서버로 보낸다

- TCP 4-way handshaking (클라이언트가 서버에 연결을 끊는 과정)
  1. [클라이언트 -> 서버]
     클라이언트는 내부적으로 `close()`를 호출하여 서버에게 연결을 종료한다는 `FIN(M)` 플래그를 보낸다
     (FIN 패킷 내에는 실질적으로 ACK도 포함되어 있다)
  2. [서버 -> 클라이언트]
     서버는 `FIN(M)`을 받고, 확인했다는 `ACK(M+1)`를 클라이언트에게 보내고 자신의 통신이 끝날때까지 기다린다 (TIME_WAIT 상태)
     아직 남은 데이터가 있다면 마저 전송을 마친 후에 내부적으로 `close()`를 호출한다
  3. [서버 -> 클라이언트]
     데이터를 모두 보냈다면, 서버는 연결이 종료에 합의 한다는 의미로 `FIN(N)` 패킷을 클라이언트에게 보낸다
     클라이언트가 신호를 보내줄 때까지 기다니는 LAST_ACK 상태로 들어간다
  4. [클라이언트 -> 서버]
     클라이언트는 `FIN(N)`을 받고, 확인했다는 `ACK(N+1)`를 서버에게 보낸다
     서버는 ACK를 받은 이후 소켓을 닫는다

### REST API

- REST (Representational State Transfer API)
  - HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시한다
  - HTTP Method를 통해 해당 자원(URI)에 대한 CRUD 기능을 적용한다.

- [REST의 특징](https://aws.amazon.com/ko/what-is/restful-api/)
  - Server-Client(서버-클라이언트 구조)
  - Stateless(무상태)
  - Cacheable(캐시 처리 가능)
  - Layered System(계층화)
  - Uniform Interface(인터페이스 일관성)

- REST API : REST 아키텍처의 제약 조건을 준수하는 애플리케이션 프로그래밍 인터페이스

#### HTTP Method

- HTTP Method
  - 해당 자원(URI)에 대한 CRUD 기능을 의미한다

- 종류
  - GET
  - POST
  - PUT
  - PATCH
  - DELETE

- GET vs POST
  - 

- PUT vs PATCH
  - 
