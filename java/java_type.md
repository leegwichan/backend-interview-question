# Java 타입

### 원시 타입 vs 참조 타입
- 원시 타입
  - 정수, 실수, 문자, 논리 리터럴 등 실제 데이터 값을 저장하는 타입
  - boolean, char, byte, short, int, long, float, double (8개)
  - 메모리 공간(스택 영역)에 실제 데이터 값이 저장되어 있다.
- 참조 타입
  - 기본 타입을 제외한 타입, 객체의 주소를 저장하는 타입
  - 문자열, 배열, 열거형 상수, 클래스, 인터페이스 등
  - 실제 객체는 JVM 힙 영역에 저장되며, 참조 타입 변수는 실제 객체의 주소를 JVM 스택 영역에 저장한다. 그리고 객체를 사용할 때마다 참조 변수에 저장된 객체의 주소를 불러와 사용하게 된다.

### 자바의 원시 타입
| 종류  |  데이터형 | 크기 | 표현 범위 |
|:---:|:---:|---|---|
| 논리형 | boolean | 1byte (8bit) | true 또는 false |
| 문자형 |  char   | 2byte | ‘\u0000’ ~ ‘uFFFF’ (16비트 유니코드 문자 데이터) |
| 정수형 |  byte   | 1byte | -128 ~ 127 |
| 정수형 |  short  | 2byte | -32768 ~ 32767 |
| 정수형 |   int   | 4byte | -21억 ~ +21억 |
| 정수형 |  long   | 8byte | -100경 ~ +100경 |
| 실수형 |  float  | 4byte | 1.4E-45 ~ 3.402E38 |
| 실수형 | double  | 8byte | 4.9E-324~1.79E308 |

### String
- Constant String Pool
  - 목적 : 동일한 문자열 리터럴이 이미 풀(Pool)에 있다면, 새로운 객체를 생성하지 않고 기존 객체의 참조(주소)를 재사용
  - 핵심 원리: String Pool은 내부적으로 HashMap 구조를 사용하여 중복된 문자열 저장을 방지 (위치 - Heap 영역)

- String의 특정
  - 불변성 : 같은 참조 값을 가지므로 가변적이면 안된다.
  - 해시코드 캐싱 : 문자열을 저장하거나 찾을 때 `hashCode()`를 사용하여 위치를 결정
  - 스레드 안전성 : 여러 스레드가 동시에 하나의 String 객체에 접근하더라도 Read-Only 상태가 유지
  - 빈번한 + 연산 시 성능 저하 : 덧셈 연산을 할 때마다 String Pool에 계속해서 새로운 객체를 만들고, 이전 객체는 버려진다.

- StringBuffer vs StringBuilder
  - 공통점 : String과 달리, 둘 다 크기가 유연하게 변하는 가변성을 갖는다. (`append()`)
    - 변하지 않는 문자열을 자주 사용할 경우 String 타입을 사용하는 것이 좋다
  - 차이점 : StringBuilder는 동기화를 지원하지 않는 반면, StringBuffer는 동기화를 지원한다
    - StringBuffer는 `synchronized`를 사용하므로 멀티 스레드 환경에서도 안전하게 동작할 수 있습니다.
    - StringBuilder는 `synchronized`를 사용하지 않으모로 단일 스르드 환경에서는 StringBuffer보다 더 빠르게 동작할 수 있다
