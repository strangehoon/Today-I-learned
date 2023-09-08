# ACID

**ACID** : 데이터베이스 내에서 일어나는 하나의 transaction의 안전성을 보장하는데 필요한 성질이다.
* **Atomicity(원자성)** 

  * 시스템에서 한 transaction의 연산들이 모두 성공하거나, 반대로 모두 실패돼야 한다.
  * 작업이 모두 반영되거나 모두 반영되지 않음으로써 결과를 예측할 수 있어야 한다.

* **Consistency(일관성)**
  * 데이터베이스의 상태가 일관되어야 한다.
  * 하나의 transaction 이전과 이후, 데이터베이스의 상태는 이전과 같이 유효해야 한다.
  * 다시 말해, transaction이 일어난 이후의 데이터베이스는 데이터베이스의 제약이나 규칙을 만족해야 한다.


* **Isolation(격리성)**
  * 모든 transaction은 다른 transaction으로부터 독립되어야 한다.
  * concurrency control의 주된 목표가 isolation이다.

* **Durability(지속성)**
  * commit된 transaction은 DB에 영구적으로 저장한다.
  * 즉, DB system에 문제가 생겨도 commit된 transaction은 DB에 남아 있다.
  * '영구적으로 저장한다'라고 할 때는 일반적으로 '비휘발성 메모리(HDD, SSD)에 저장함'을 의미한다.
  * 기본적으로 transaction의 durability는 DBMS가 보장한다. 


 ACID 원칙을 strict 하게 지키려면 동시성이 매우 떨어져서 DBMS는 ACID 원칙을 희생하여 동시성을 얻을 수 있는 방법으로 isolation level을 제공한다. 
