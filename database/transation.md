# 트랜잭션 (Transaction)
- 데이터베이스의 상태를 변화시키기 위해 수행하는 작업의 논리적인 단위
- 주의할 점 : 트랜잭션의 범위를 최소화하여 사용해야 한다.

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

- Double Write Buffer (이중 쓰기 버퍼) : 운영체제나 시스템 크래시로 인해 Dirty Page가 버퍼 풀에서 데이터 파일로 기록될 때, 페이지의 내용이 일부만 기록되는 현상을 방지
  - Partial Page Write (Torn Page) : nnoDB의 버퍼 풀에 있는 Dirty Page를 디스크의 데이터 파일로 Flush(기록)하는 도중에, 예상치 못한 시스템 장애(서버 크래시, 전원 공급 중단, OS 문제 등)가 발생하여 페이지의 일부 내용만 디스크에 기록되고 나머지 부분은 기록되지 못한 상태

- Double Write Buffer vs Redo Log
  | 구분 | Double Write Buffer | Redo Log |
  | :--- | :--- | :--- |
  | 주요 목적 | 데이터 페이지의 무결성 보장 (Partial Page Write 방지) | 트랜잭션의 영속성 보장 (크래시 복구) |
  | 기록 대상 | Flush 되는 전체 데이터 페이지 | 페이지 내의 변경 내용만 (Log Record) |
  | 작동 원리 | 데이터 파일에 쓰기 전에 페이지 사본을 한 번 더 저장 (2단계 쓰기) | 변경 내용을 먼저 로그에 기록 후, 나중에 데이터 파일에 적용 (WAL) |
  | 위치 | 시스템 테이블스페이스 내의 디스크 영역 | 디스크의 Redo Log 파일 |
  | 복구 역할 | 손상된 페이지 자체를 복구함 | 커밋된 트랜잭션의 변경 사항을 재반영함 |
