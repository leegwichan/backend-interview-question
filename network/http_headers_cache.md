# 캐시 처리를 위한 HTTP Headers

### 캐시 유효 기간 설정
- Cache-Control: max-age
  - 문서가 처음 생성된 이후부터, 제공하기엔 더 이상 유효하지 않다고 간주될 때까지 경과한 시간을 지정
  - ex. Cache-Control: max-age=484200 (484,200초 동안 유효함) 
- Expires
  - 문서가 유효한 절대 유효시간을 명시
  - ex. Expires: Fri, 05 Jul 2002, 05:00:00 GMT (해당 날짜 이전까지만 유효함)

### 서버 재검사 
- 캐시 유효기간이 지났을 때, 클라이언트는 서버에게 정보를 다시 요청한다
- 응답이 기존과 다를 경우 응답 데이터를 보내지만, 동일할 경우 '304 Not Modified'를 Status line에 담아 응답한다
- If-Modified-Since (IMS 요청)
  - 서버에게 리소스가 특정 날따 이후로 변경에 따른 조건부 요청
  - 가장 흔히 사용되는 캐시 재검사 헤더이다
  - ex) `If-Modified-Since : Fri, 05 Jul 2002, 05:00:00 GMT`
- If-None-Match
  - 요청한 엔터티의 태그 변경에 따른 조건부 요청
  - ex) `If-None-Match : "v2.4", "v2.5", "v2.6"`

### `Expires`, `Date`, `Age`, `If-Modified-Since`의 차이점
- Expires : 응답이 더 이상 유효하지 않게 되는 일시를 알려준다
  - ex) `Expires: Fri, 05 Jul 2002, 05:00:00 GMT`
- Date : 메시지가 생성된 날짜와 시간을 알려준다
  - ex) `Date: Fri, 05 Jul 2002, 05:00:00 GMT`
- Age : 수신자에게 응답이 얼마나 오래되었는지 말해준다
  - ex) `Age : 60 (초 단위)`
- If-Modified-Since : 마지막으로 요청이 있었을 때를 기준으로, 변경이 있었을 때만 응답을 받음 (조건부 요청)
  - 변경이 없었을 경우, '304 Not Modified'로 응답한다
  - ex) `If-Modified-Since : Fri, 05 Jul 2002, 05:00:00 GMT`
