
# Autocommit

**Autocommit이란?**
* 각각의 SQL 문을 자동으로 transaction 처리해 주는 개념이다.
  * SQL 문이 성공적으로 실행되면 자동으로 commit 한다.
  * 실행 중에 문제가 있었다면 알아서 rollback 한다.
* MySQL에서는 default로 autocommit이 enabled 되어 있다.
* 다른 DBMS에서도 대부분 같은 기능을 제공한다.

</br>

**Autocommit 확인하기**

mysql에서는 default로 활성화 되어 있어서 1이 조회된다.
```sql
select @@ autocommit;
```

</br>

**Autocommit 설정하기**

활성화 시=1, 비활성화 시 =0을 입력하자.
```sql
set autocommit=0;
```

</br>

**자바/스프링에서 확인하기**
```java
public void transfer(String fromId, String toId, int amount) {
	try {
    	Connection connection = ...;
        connection.setAutoCommit(false);
        ...
        ...
        connection.commit();
    } catch (Exception e) {
    	...
        connection.rollback();
        ...
    } finally {
    	connection.setAutoCommit(true);
    }
}
```

자바/스프링에서는

1. DB 커넥션을 조회
2. autoCommit = false로 초기화(트랜잭션 시작)
3. 비즈니스 로직 수행
4. 성공적이라면 커밋
5. 실패면 롤백
6. autocommt = true로 다시 초기화

트랜잭션 관련된 부가적인 코드들 때문에 서비스 로직의 가독성이 저하된다. 우리가 흔히 사용하는 `@Transactional`을 통해 transaction 관련된 코드들을 함축시킬수 있다.  
```java
@Transactional
public void transfer(String fromId, String toId, int amount) {
	...
    ...
}
```
