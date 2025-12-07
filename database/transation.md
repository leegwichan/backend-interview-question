# 트랜잭션 (Transaction)
- 데이터베이스의 상태를 변화시키기 위해 수행하는 작업의 논리적인 단위

### 트랜젝션 특징 (ACID)
- 원자성 (Atomicity) : 전부 또는 전무(All or Nothing)
- 일관성 (Consistency) : 트랜잭션 실행 후에도 일관성(데이터 유효성) 유지
- 격리성 (Isolation) : 트랜잭션 실행 중 연산의 중간 결과에 다른 트랜잭션이 접근할 수 없음
- 영속성 (Durability) : 트랜잭션이 일단 성공적으로 실행되면 그 결과는 영속적

#### 원자성 (Atomicity)
- 부분 갱신 문제 해결 -> Undo Log (이전 상태 기록하여 롤백 지원)

#### 일관성 (Consistency)
- 데이터 무결성 위반 문제 해결 -> 제약 조건

#### 격리성 (Isolation)
- 동시성 문제 해결 (출금 예제) -> Lock, MVCC
  - MVCC (Multi Version Concurrency Control) : 하나의 데이터에 대해 여러 개의 버전을 동시에 관리
- Dirty Read, Non-Repeatable Read, Phantom Read -> 트랜잭션 격리 수준 설정

#### 영속성 (Durability)
- 시스템 장애로 인한 데이터 소실 문제 해결 -> Redo Log (WAL)
  - ARIES 알고리즘 : Redo Log 실행 (장애 직전까지 했던 모든 작업 실행) -> Undo Log 실행 (완료되지 못하고 끊긴 트랜잭션 롤백 실행)
  - WAL(Write-Ahead Logging) : 로그 먼저 남긴 후 응답, 추후 실제 데이터 파일에 반영
