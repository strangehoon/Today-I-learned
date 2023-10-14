# Serializability
**schedule** : 다수의 transaction이 동시에 실행될 때 각 transaction에 속한 operation들의 실행 순서
* **serial schedule** : transaction들이 겹치지 않고 한 번에 하나씩 실행되는 schedule, 한 번에 하나의 transaction만 실행되기 때문에 좋은 성능을 낼 수 없고 현실적으로 사용할 수 없는 방식이다. 
* **nonserial schedule** : transaction들이 겹쳐서 실행되는 schedule, transaction들이 겹처서 실행되기 때문에 동시성이 높아져서 같은 시간 동안 더 많은 transaction들을 처리할 수 있다. 하지만 transaction들이 어떤 형태로 겹처서 실행되는지에 따라 이상한 결과가 나올 수 있다.


🤔 **고민거리** : 성능 때문에 여러 transaction들을 겹쳐서 실행할 수 있으면 좋다. 하지만 이상한 결과가 나오는 것은 싫다. </br>

💡 그렇다면 serial schedule과 동일한(equivalent) nonserial schedule을 실행하면 되겠구나!! 먼저 conflict에 대해 알아보자. 

**conflict** : 아래 3가지 조건을 모두 만족하면 conflict
1. 서로 다른 transaction 소속
2. 같은 데이터에 접근
3. 최소 하나는 write operation

 conflict 종류에는 read-write conflict, write-write conflict가 존재하는데 conflict operation은 순서가 바뀌면 결과도 바뀐다. 

**conflict equivalent** : 아래 두 조건 모두 만족하면 conflict eqivalent
1. 두 schedule은 같은 transaction들을 가진다.
2. 어떤 conflicting operations의 순서도 양쪽 schedule 모두 동일하다.

serial schedule과 conflict equivalent일 때 conflict serializable하다. 

💡 **고민거리의 해결책** : conflict serializable한 nonserial schedule을 허용하자 -> 여러 transaction을 동시에 실행해도 schedule이 conflict serializable 하도록 보장하는 프로토콜을 적용

</br>

# Recoverability
**unrecoveralbe schedule** : schedule 내에서 commit된 transaction이 rollback된 transaction이 write 했었던 데이터를 읽은 경우, rollback을 해도 이전 상태로 회복 불가능할 수 있기 때문에 이런 schedule은 DBMS가 허용하면 안된다. </br>

**recoveralbe schedule** : schedule 내에서 그 어떤 transaction도 자신이 읽은 데이터를 write한 transaction이 먼저 commit/rollback 전까지는 commit 하지 않는 경우, rollback할 때 이전 상태로 온전히 돌아갈 수 있기 때문에 DBMS는 이런 schedule만 허용해야 한다. 하나의 transaction이 rollback하면 의존성이 있는 다른 transaction도 rollback 해야 하는데 이를 cascading rollback이라고 한다.

하지만 여러 transaction의 rollback이 연쇄적으로 일어나면 처리하는 비용이 많이 든다. 이를 위한 개념이 cascadeless schedule과 strict schedule </br>
* **cascadeless schedule** : schedule 내에서 어떤(any) transaction도 commit 되지 않은 transaction들이 write한 데이터는 읽지 않는 경우 </br>
* **strict schedule** : schedule 내에서 어떤 transaction도 commit 되지 않은 transaction들이 write한 데이터는 쓰지도 읽지도 않는 경우 

<img src = "https://github.com/strangehoon/Today-I-learned/assets/117654450/0c8b7de5-010f-485b-9d07-fef00b159440" height = "250" width = "400" allign = "left">

> 참고 </br>
> [(1부) concurrency control 기초 : schedule과 serializability](https://www.youtube.com/watch?v=DwRN24nWbEc&list=PLcXyemr8ZeoREWGhhZi5FZs6cvymjIBVe&index=15) </br>
> [(2부) concurrency control 기초](https://www.youtube.com/watch?v=89TZbhmo8zk&list=PLcXyemr8ZeoREWGhhZi5FZs6cvymjIBVe&index=16)
