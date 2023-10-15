# Lock을 활용한 Concurrency control

**Write-lock(exclusive lock)**
* read/write(insert, update, delete) 할 때 사용
* 다른 트랜잭션이 같은 데이터를 read/write 하는 것을 허용하지 않는다.



**Read-lock(shared lock)**
* read 할 때 사용
* 다른 트랜잭션이 같은 데이터를 read 하는 것은 허용한다.



**Lock 호환성**
|  | Read-lock | Write-lock |
| :- | :- | :- |
| Read-lock	| O | X |
| Write-lock | X | X |

> 📌 **하지만 락을 써도 이상 현상이 발생할 수 있다.. 해결책으로는 2PL(two phase locking)**

</br>

**2PL protocol** : 트랜잭션에서 모든 locking operation이 최초의 unlock operation보다 먼저 수행되도록 하는 것
* expanding phase : lock을 취득하기만 하고 반환하지는 않는 phase
* shrinking phase : lock을 반환만 하고 취득하지는 않는 phase

> 📌**이러한 2PL protocol은 serializability를 보장하지만, deadlock이 발생할 수 있다.**

그 외의 2PL protocol의 종류는 아래와 같다.

Conservative 2PL : 모든 lock을 취득한 뒤 트랜잭션 시작
* deadlock-free
* 실용적이지 않다

Strict 2PL(S2PL)
* Strict-schedule을 보장하는 2PL
* recoverability 보장
* write-lock을 commit/rollback 될 때 반환

Strong strict 2PL(SS2PL)
* strict schedule을 보장하는 2PL
* recoverability 보장
* read-lock, write-lock 모두 commit, rollback 될 때 반환
* S2pl보다 구현이 쉬움

> 📌**S2PL, SS2PL은 초창기 RDBMS에서 가장 많이 사용되었던 구현방식이다. 하지만 2pl은 read-read를 제외하고는 한 쪽이 block 되니까 전체 처리량이 좋지 않다. read write가 서로를 block 하는 것만이라도 해결해보려고 나온 것이 MVCC이다. 오늘날 많은 RDBMS가 락과 MVCC를 혼용해서 사용한다.**
