# 자료 구조 & 알고리즘

- [선형 구조](#선형-구조)
  - 배열과 링크드 리스트(Linked List)의 차이를 설명해주세요.
  - List와 Set의 차이에 대해서 설명해주세요.
  - Stack, Queue에 대해서 설명해주세요.
- Map 구조
  - Hash Function, HashTable에 대해서 설명해주세요.
  - 해시 충돌 및 해결 방법에 대해서 설명해주세요.
- Tree 구조
  - Tree, Binary Tree, BST, AVL Tree에 대해서 설명해주세요.
      - Full Binary Tree, Complete Binary Tree
      - Red-Black Tree
  - Heap, Priority Queue에 대해서 설명해주세요.
    - Binary Heap
  - [Database] B 트리, B+ 트리
  - BST의 최악의 경우의 예와 시간복잡도에 대해서 설명해주세요.
- Graph 구조
  - Graph 용어 정리, Graph 구현
  - DFS, BFS에 대해서 설명해주세요.

- 알고리즘
  - 피보나치 수열을 코드로 구현하는 방법에 대해서 설명해주세요.
  - Prime Number Algorithm
- 정렬, 탐색
  - 정렬, 탐색에 대해 설명해주세요.
  - 버블 정렬, 선택 정렬, 삽입 정렬, 병합 정렬, 퀵 정렬, 힙 정렬
  - 순차 탐색 vs 이진 탐색

### 선형 구조

#### Array vs Linked List
- Array
  - 같은 타입의 여러 변수를 하나의 묶음으로 다루는 자료구조
  - **연속적인 메모리 공간**에 데이터가 저장되며, 크기가 고정되어 있다
  - 크기를 동적으로 변경하기 어려움, 동적 배열을 사용할 수 있으나 가득 차면 배열을 2배로 늘려서 공간을 확보해야 한다
- Linked List
  - 데이터 요소들이 순서대로 연결되어 있는 선형 자료 구조
  - 원소가 추가될 때마다 공간을 할당받아 **비연속적인 메모리 공간에 추가**
  - 크기가 동적으로 조정 가능해서 공간 효율적
  - 각 요소(Node)는 데이터와 다음 요소를 가리키는 포인터(주소)로 이루어진다.
    - Node의 구성에 따라 Singly Linked List, Doubly Linked List가 될 수 있다

- Linked List의 순환 여부 판단 (Floyd's Cycle Detection Algorithm)
  - 빠른 포인터(hare)와 느린 포인터(tortoise)를 구성
  - 빠른 포인터는 두 개의 노드를 건너뛰고, 느린 포인터는 한 번에 하나의 노드를 건너뛴다
  - 만약 Linked List에 사이클이 없다면, 빠른 포인터가 끝에 도달하게 된다
  - 만약 Linked List에 사이클이 있다면, 빠른 포인터와 느린 포인터가 같은 노드를 가리키게 된다

#### List vs Set
- List
  - 같은 타입의 여러 변수를 **순서있게** 다루는 자료구조
  - 순서가 존재하기 때문에 같은 값을 중복으로 가질 수 있다
- Set
  - 같은 타입의 여러 변수를 **순서없이** 다루는 자료구조
  - 같은 값을 중복으로 허용하지 않는다
  - `contains()`와 같은 탐색이 필요하다면 Set을 고려하는 것이 좋음 (HashSet - O(1))

#### Stack vs Queue
- Stack
  - LIFO (Last In First Out, 후입선출) 원칙에 기반한 선형 자료구조
  - ex) 최근 작업 순서로 되돌아가기, 프로그램의 함수 호출 관리, 웹 브라우저 뒤로 가기
  - 배열이나 링크드 리스트를 통해 구현
- Queue
  - FIFO (First In First Out, 선입선출) 원칙을 따르는 선형 자료구조
  - ex) CPU 스케줄링, 프린터 대기열, 주문 처리 시스템
  - Circular Queue : 배열로 Queue를 구현했을 때 원소가 들어오고 나감에 따라 빈공간이 생기는 것을 방지하기 위해, `(rear + 1) % n`을 통해 다음 위치를 찾도록 하여 배열을 원형으로 사용하도록 함
    - 배열의 값들을 전부 옮겨야 하는 작업이 없어지면서, 시간이 줄어든다