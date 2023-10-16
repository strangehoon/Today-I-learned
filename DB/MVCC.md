# MVCC
MVCC는 multiversion concurrency control의 약자로 데이터를 읽을 때 특정 시점을 기준으로 가장 최근에 commit 된 데이터를 읽는다. 
특정 시점 기준은 isolation level에 따라 다르다. 이전에 2PL protocol과 달리 select 문에 락이 걸리지 않아 read와 write는 서로를 block 하지 않는다. commit 한 다음에 락을 반환하며 이는 recoverability 때문이다. 반환은 RDBMS가 책임진다. 
오늘날 대부분 RDBMS는 대부분 MVCC로 동작한다. 

👇 **mysql 기준**
* **read uncommited** : MVCC는 commit 된 데이터를 읽기 때문에 이 level에서는 보통 MVCC가 적용되지 않는다. 
* **read commited** : read 하는 시간을 기준으로 그전에 commit 된 데이터를 읽는다. 
* **repeatable read** : 트랜잭션 시작 시간 기준으로 그전에 commit 된 데이터를 읽는다.
* **serializable** : 트랜잭션의 모든 평범한 select문은 암묵적으로 select ...for share처럼 동작한다.


Mysql에서는 read commited, repeatable에서 일어나는 이상 현상을 locking read로 해결한다. 
locking read에는 select...for update, select...for share가 있다.

