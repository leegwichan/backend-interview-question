# Database

- RDBMS vs NoSQL에 대해서 설명해주세요.
    - RDBMS 정의
    - NoSQL 정의, 저장 방식에 따른 분류
- 데이터 베이스 성능의 중요 요소에 대해 설명해주세요.
- Index
    - Index란 무엇인가요?
    - 데이터베이스에서 인덱스를 사용하는 이유 및 장단점에 대해 설명해주세요.
    - Index 자료구조
    - Primary index vs Secondary index, Composite index
    - Index의 성능과 고려해야할 사항
- 트랜잭션
    - 트랜잭션에 대해서 설명해주세요.
    - 정의, Lock, 특성, 상태, 주의할 점
    - 트랜잭션 격리 수준(Transaction Isolation Levels)에 대해서 설명해주세요.
    - cf) [DBMS 는 어떻게 트랜잭션을 관리할까?](https://d2.naver.com/helloworld/407507)
- 정규화
    - 정규화에 대해서 설명해주세요.
    - 탄생 배경, 정의, 종류, 장단점
- ACID에 대해서 설명해주세요.
- JOIN에 대해서 설명해주세요.
- Statement vs PreparedStatement
- Redis에 대해서 간단히 설명해주세요.
- CAP 이론과, Eventual Consistency에 대해서 설명해주세요.
- Redis와 Memcached의 차이에 대해서 설명해주세요.
- Elastic Search에 대해서 간단히 설명해주세요.
    - Elastic Search의 인덱스 구조와 RDBMS의 인덱스 구조의 차이에 대해 설명해주세요.
    - Elastic Search의 키워드 검색과 RDBMS의 LIKE 검색의 차이에 대해 설명해주세요.
- MongoDB에 대해서 간단히 설명해주세요.

### RDBMS vs NoSQL

#### RDBMS (Relational Database Management System)

- DBMS : 응용 프로그램과 데이터 사이의 중재자로서 모든 응용 프로그램(사용자)들이 데이터베이스를 **공용할 수 있게 관리**해 주는 범용 소프트웨어 시스템
    - 논리적 데이터 독립성 : 응용 프로그램에 영향을 주지 않고 논리적 데이터 구조의 변경이 가능
    - 물리적 데이터 독립성 : 응용 프로그램과 논리적 데이터 구조에 영향을 주지 않고 물리적 데이타 구조의 변경이 가능
- RDBMS : 관계형 데이터베이스를 관리하는 DBMS
    - 관계형 모델
        - 수학에서의 릴레이션(relation)과 집합(set) 이론에 기초, 일반 사용자는 테이블(table) 형태로 생각
        - 데이터가 하나 이상의 열과 행의 테이블(또는 '관계')에 저장되어 서로 다른 데이터 구조가 어떻게 관련되어 있는지 쉽게 파악하고 이해할 수 있도록 사전 정의된 관계

#### NoSQL (Not only SQL)

- NoSQL : 관계형 모델이 아닌 데이터베이스를 관리하는 DBMS
- NoSQL의 종류
    - Key-Value Model : key-value pair로 데이터를 저장함, key는 unique identifier로도 사용됨 ex) Redis, DynamoDB
    - Document Model : JSON, XML 등 자유로운 형태로 데이터를 저장함 ex) MongoDB
    - Graph Model : 데이터를 graph의 형태로 저장, 각 항목이 node로 이루어져있고 node간의 관계는 edge를 사용해서 나타냄 ex) Neo4J, OrientDB

#### RDBMS vs NoSQL

| 구분             | RDBMS (관계형 DB)                                                      | NoSQL (비관계형 DB)                                                                |
|----------------|---------------------------------------------------------------------|--------------------------------------------------------------------------------|
| Data Modeling  | - 스키마에 맞춰서 관리하기 때문에 데이터 **정합성 보장** </br> - 관계를 맺고있는 데이터가 자주 변경되는 경우 | - 자유롭게 데이터를 관리할 수 있다 </br> - 데이터 구조를 정확히 알 수 없는 경우 </br> - 데이터가 변경/확장될 수 있는 경우 |
| Scalability    | Scale Up </br> 각 단일 서버의 성능을 증가시켜서 더 많은 요청을 처리 (한계가 존재함)             | Scale Out </br> 요청량이 증가하더라도 동일하거나 비슷한 사양의 새로운 하드웨어를 추가                         |
| Query Language | SQL(Structured Query Language)                                      | DB마다 문법이 다름                                                                    |
| Consistency    | STRONG                                                              | eventual consistency </br> - may take time to be consistent                    |
| flexibility    | 상대적으로 떨어짐                                                           | 매우 유연함                                                                         |

### 데이터베이스 성능 중요 요소

- 데이터베이스의 성능 향상의 초점은 디스크 (랜덤) 접근 횟수(I/O)의 최소화 
    - **인덱스 최적화**와 **SQL 최적화**의 우선순위가 높다.
    - 인덱스를 통해 정렬되어 있는 자료에서 찾으므로써 디스크 접근 횟수를 줄일 수 있다.
    - SQL 최적화를 통해 메인 메모리를 거치는 횟수를 줄일 수 있다.
        - SQL을 트리 구조로 바꾸어 내부에서 다룬다.
        - 연산 비용이 큰 Join 전에 데이터의 크기를 줄이는 연산을 먼저 함으로써 Join 연산을 최소한의 데이터로 진행한다.

### 인덱스 (Index)

#### 인덱스란?

#### 인덱스 사용 이유 & 장단점

#### Index의 자료 구조
