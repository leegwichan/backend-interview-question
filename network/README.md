# 네트워크

- TCP vs UDP
  - TCP와 UDP의 차이점에 대해서 설명해보세요.
  - TCP 3, 4 way handshake에 대해서 설명해보세요.
  - OSI 7계층과 그 존재 이유, TCP/IP 4계층에 대해 설명해보세요.
    - 웹 서버 소프트웨어(Apache, Nginx)는 OSI 7계층 중 어디서 작동하는지 설명해보세요.
    - 웹 서버 소프트웨어(Apache, Nginx)의 서버 간 라우팅 기능은 OSI 7계층 중 어디서 작동하는지 설명해보세요.

- HTTP
  - HTTP의 문제점
  - 무상태성과 비연결성에 대해서 설명해주세요.
  - HTTP와 HTTPS의 차이점에 대해서 설명해보세요.
  - HTTPS에 대해서 설명하고 SSL Handshake에 대해서 설명해보세요.
  - SSL 인증서 암호화 기법인 대칭키 암호화 기법, 공개키 암호화 기법에 대해 설명해주세요.
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

### OSI 7계층
- [OSI 7 Layer](./osi_seven_layer.md)
  - L4 로드밸런서 vs L7 로드밸런서
- [TCP](./tcp.md)
  - TCP vs UDP
  - TCP 특징
  - TCP handshaking

### HTTP
- [HTTP의 정의 & 특징](./http.md)
  - HTTP의 문제점
  - HTTPS의 정의 & 특징
- [캐시 처리를 위한 HTTP Headers](./http_headers_cache.md)
- [HTTPS](./https.md)
- [REST API](./rest_api.md)
  - HTTP Method
  - 비멱등성 API 중복 호출 방지
