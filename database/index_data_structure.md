# 인덱스 자료구조

### B+ Tree


### Hash Index


### 기타 자료구조
- Bitmap Index : 데이터의 값을 0과 1의 비트(Bit) 배열로 변환하여 저장하는 방식, 비트 연산(AND, OR, NOT)을 사용하므로 대량의 데이터 처리 속도가 매우 빠르다.
- R-Tree (Spatial Index) : 공간 데이터(2차원 이상의 데이터)를 효율적으로 검색하기 위한 구조
- LSM Tree (Log-Structured Merge Tree) : 주로 쓰기(Write) 성능이 중요한 NoSQL 데이터베이스에서 많이 사용하는 구조, 데이터를 메모리에 쓰고 다 차면 디스크에 순차적으로 플러시