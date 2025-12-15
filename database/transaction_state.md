# 트렌젝션 상태

<center><img src="./image/transaction_states.png" width="50%"></center>

- Active State (활동 상태)
    - Transaction이 진행중인 상태
    - 읽기 또는 쓰기가 정상적으로 진행된 경우, “Partially Committed State”
    - 읽기 또는 쓰기가 실패한 경우, “Failed State”
- Partially Committed State (부분 완료 상태)
    - 모든 읽기 쓰기 데이터가 DB에 저장된 경우 “committed state”로 이동
    - DB에 저장이 실패한 경우, “Failed State”
- Failed State (실패 상태)
    - Transaction의 명령이 실패하거나 DB에 데이터 저장, 변경에 실패한 경우
- Aborted State (철회 상태)
    - local buffer 또는 main memory에 있는 변경 사항들을 지우거나 롤백함
- Committed State (완료 상태)
    - DB에 모든 내용이 저장된 상태
- Terminated State
    - 롤백이나 다른 커밋 상태가 없을 때
    - 이전에 있었던 transaction은 지우고 새로운 transaction에 대기하는 상태
