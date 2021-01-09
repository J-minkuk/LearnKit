# Optimistic & Pessimistic
JPA는 DB 트랜잭션 isolation level을 ```READ COMMITTED``` 정도로 가정한다. 로직에서 더 높은 level의 격리가 필요하다면 
낙관적 락과 비관적 락 중 하나를 선택해 사용하면 된다.

## Optimistic Lock (낙관적 락)
* 동시성 처리를 위해 JPA에서 제공
* Version 정보를 통해 업데이트를 처리하는 방법
* Version 정보로 사용할 컬럼(int, Integer, long, Long, short, Short, timestamp)에 ```@Version``` 어노테이션을 사용
> entity에는 하나의 버전 속성만 있어야 하고, 맵핑된 entity의 경우 기본 테이블에 배치되어야 한다.

```java
import javax.annotation.processing.Generated;

@Entity
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @Version
    private Integer version;
}
```

### Mode
* NONE: Lock 옵션을 적용하지 않아도 Entity에 @Version이 적용된 필드가 있다면 낙관적 락을 건다.
* OPTIMISTIC(READ): @Version만 적용했을 경우 Entity를 수정해야 Version을 체크하지만 이 옵션의 경우 조회할 때도 체크한다. 
즉, 조회 트랜잭션이 끝나기 전까지 다른 트랜잭션에서 변경할 수 없다.
> dirty read, non-repeatable read 방지
* OPTIMISTIC_FORCE_INCREMENT(WRITE): 버전 정보를 강제로 증가시킨다.

```java
entityManager.find(Student.class, studentId, LockModeType.OPTIMISTIC);
```
```java
Query query = entityManeger.createQuery("from Student where id = :id")
query.setParameter("id", studentId);
query.setLockMode(LockModeType.OPTIMISTIC_INCREMENT);
query.getResultList();
```
```java
@NamedQuery(
        name = "optimisticLock",
        query = "SELECT stu FROM Student stu WHERE stu.id LIKE :id",
        lockMode = WRITE
)
```

### Exception
* OptimisticLockException: 버전 정보가 맞지 않을 경우 예외
> persistence provider가 entity의의 optimistic lock 충돌을 감지하면 해당 예외가 발생하고 롤백시킨다.

---

## Pessimistic Lock (비관적 락)
트랜잭션의 충돌이 발생한다고 가정하고 우선 Lock을 건다. DB 수준에서 entity 잠금을 포함한다.

### Mode
* PESSIMISTIC_READ: dirty read가 발생하지 않을 때마다 Shared Lock을 획득하고 데이터가 수정, 삭제되는 것을 방지
* PESSIMISTIC_WRITE: Exclusive Lock을 획득하고 데이터를 다른 트랜잭션에서 Read, Update, Delete 하는 것을 방지
* PESSIMISTIC_FORCE_INCREMENT: PESSIMISTIC_WRITE와 유사하지만 @Version 어노테이션이 지정된 entity와의 상호작용을 위해 도입되어 
PESSIMISTIC_FORCE_INCREMENT 잠금을 획득할 시 Version이 업데이트된다.

### Exception
* PessimisticLockException: Lock은 Shared Lock과 Exclusive Lock 중 하나만 획득할 수 있으며 Lock 획득에 실패할 경우 발생하는 예외
* LockTimeoutException: Lock을 대기하다 설정한 wait time이 초과되었을 때 발생하는 예외
* PersistenceException: NoResultException, NonUniqueResultException, LockTimeoutException, QueryTimeoutException을 
제외한 PersistenceException 예외에 대해 트랜잭션 롤백을 마킹

### Lock Scope
* NORMAL: 기본값으로 해당 entity만 잠금 설정
* EXTENDED: @OneToOne, @OneToMany, @ElementCollection 등 연관된 entity도 잠금 설정

---

## Implicit Lock (암시적 잠금)
JPA에서는 entity에 @Version이 붙은 필드가 존재하거나 @OptimisticLocking이 설정되어 있을 경우 자동으로 충돌 감지를 위한 잠금이 실행된다. 
그리고 추가로 삭제 쿼리가 발생할 시 암시적으로 해당 row에 대한 Row Exclusive Lock을 제공한다.

## Explicit Lock (명시적 잠금)
의도적으로 잠금을 실행하는 것. EntityManager를 통해 LockMode를 지정하거나 select for update를 통해 직접 잠금을 지정할 수 있다.
```java
Student student = entityManeger.find(Student.class, id);
entityManager.lock(student, LockModeType.OPTIMISTIC);
```