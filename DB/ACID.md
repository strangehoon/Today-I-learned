# ACID

**Transaction** : transaction이란 여러 개의 작업을 하나로 묶은 실행 유닛으로 데이터베이스의 상태를 변환시키는 기능을 수행하기 위한 하나 이상의 쿼리를 모아 놓은 하나의 작업 단위를 말한다.

**ACID** : 데이터베이스 내에서 일어나는 하나의 transaction의 안전성을 보장하기 위해 필요한 성질이다.
* **Atomicity(원자성)** 

  * Atomicity이란 시스템에서 한 transaction의 연산들이 모두 성공하거나, 반대로 모두 실패되는 성질을 말한다.
  * Atomicity는 작업이 모두 반영되거나 모두 반영되지 않음으로서 결과를 예측할 수 있어야 한다.

* **Consistency(일관성)**
  * 일관성은 데이터베이스의 상태가 일관되어야 한다는 성질이다.
  * 일관성은 하나의 transaction 이전과 이후, 데이터베이스의 상태는 이전과 같이 유효해야 한다.
  * 다시 말해, transaction이 일어난 이후의 데이터베이스는 데이터베이스의 제약이나 규칙을 만족해야 한다는 뜻이다.


* **Isolation(격리성)**
  * 격리성은 모든 transaction은 다른 transaction으로부터 독립되어야 한다는 뜻이다.
  * DBMS는 여러 종류의 isolation level을 제공한다.
  * 개발자는 isolation level 중에 어떤 level로 transaction을 동작시킬지 설정할 수 있다.
  * concurrency control의 주된 목표가 isolation이다.

* **Durability(지속성)**
  * commit된 transaction은 DB에 영구적으로 저장한다.
  * 즉, DB system에 문제가 생겨도 commit된 transaction은 DB에 남아 있다.
  * '영구적으로 저장한다'라고 할 때는 일반적으로 '비휘발성 메모리(HDD,SSD)에 저장함'을 의미한다.
  * 기본적으로 transaction의 durability는 DBMS가 보장한다. 
