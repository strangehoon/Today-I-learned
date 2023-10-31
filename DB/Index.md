# Index
Index란 추가적인 쓰기 작업과 저장 공간을 활용하여 데이터베이스 테이블의 검색 속도를 향상시키기 위한 자료구조이다. 
## Index를 쓰는 이유
조건을 만족하는 튜플(들)을 빠르게 조회하기 위해
빠르게 정렬(order by)하거나 그룹핑(group by)하기 위

## DB index로 B tree 계열이 사용되는 이유

* **B tree(B+ tree, B\* tree)**

| case | 조회 | 삽입 | 삭제 |
| :- | :- | :- | :- |
| avg case | O(logN) | O(logN) | O(logN) |
| worst case | O(logN) | O(logN) | O(logN) | 

  
* **self-balancing BST(AVL tree, Red-Black tree)**

| case | 조회 | 삽입 | 삭제 |
| :- | :- | :- | :- |
| avg case | O(logN) | O(logN) | O(logN) |
| worst case | O(logN) | O(logN) | O(logN) | 


하지만 Btree, self-balancing BST 모두 O(logN)이다. 그렇다면 왜 DB index로 B tree가 사용될까?

DB secondary storage에 저장된다. DB에서 데이터를 조회할 때 secondary storage에 최대한 적게 접근하는 것이 성능 면에서 좋다. 
block 단위로 읽고 쓰기 때문에 연관된 데이터를 모아서 저장하면 더 효율적으로 읽고 쓸 수 있다. 

B tree는 각 노드가 가질 수 있는 자녀 노드 수가 AVL tree보다 많기 때문에 데이터를 찾을 때 탐색 범위를 빠르게 좁힐 수 있다.
따라서 Btree가 secondary storage에 접근하는 수가 더 적기 때문에 성능이 더 좋다.  또한 Btree는 한 노드당 AVL tree보다 데이터를 더 많이 가진디. 따라서
secondary stoage로 부터 데이터를 가져올 때 block을 단위로 데이터를 조회하는데 B tree는 훨씬 사용될 데이터를 읽어서 효율적이다. -> Block 단위에 대한 저장 공간 활용도가 더 좋 다.


DB는 기본적으로 secondary storage에 저장된다.
Btree index는 self-balancing BST에 비해 secondary storage 접근을 적게 한다.
B tree 노드는 block 단위의 저장 공간을 알차게 사용할 수 있다. 


hash index를 쓰는건?
hash index는 삽입/삭제/조회의 시간복잡도가 O(1)
하지만 equality(=) 조회만 가능하고 범위 기반 검색이나 정렬에는 사용될 수 없다는 단점이 있다.

 





