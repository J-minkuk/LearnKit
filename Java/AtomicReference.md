# AtomicReference
AtomicReference는 V 객체를 wrapping 하는 클래스이고, 멀티스레드 환경에서 동시성을 보장한다.

## get(), set(), getAndSet()
```java
public void example1() {
    AtomicReference<Integer> atomicInteger = new AtomicReference<>();
    System.out.println(atomicInteger.get());
    
    atomicInteger.set(92);
    System.out.println(atomicInteger.get());

    System.out.println(atomicInteger.getAndSet(30));
    System.out.println(atomicInteger.get());
}
```

## compareAndSet(expect, update)
현재 값이 expect와 같다면 update로 변경하고 true return, 아니라면 데이터 변경 없이 false return.
```java
public void example2() {
    int expected = 30;
    AtomicReference<Integer> atomicInteger = new AtomicReference<>(29);
    System.out.println(atomicInteger.compareAndSet(expected, 100));
    System.out.println(atomicInteger.get());
    
    atomicInteger.set(30);
    System.out.println(atomicInteger.compareAndSet(expected, 100));
    System.out.println(atomicInteger.get());
}
```

---

## 동시성 문제 해결
자바에서 동시성 문제를 해결하는 방법
**synchronized**<br>
동시성을 보장할 수 있지만, 비용이 크다.

**Atomic 클래스**<br>
CAS를 이용하여 동시성을 보장하고, 여러 스레드에서 동시에 데이터를 write해도 문제가 없다.

**참고**<br>
volatile은 A-thread에서 write, B-thread에서 read하는 경우에만 동시성을 보장한다. 2개의 스레드에서 write한다면 문제가 될 수 있다.