# synchronized 이해
하나의 객체에 여러 요청이 동시에 들어오면 원하는 처리를 하지 못하고 이상한 결과가 나올 수 있습니다.
* 그래서 synchronized를 사용하여 동기화를 하는 것입니다.
* 이 식별자를 사용하면 "천천히 하나씩 들어오세요."라고 해당 메소드나 블럭에서 제어하게 됩니다.

*코드 예제
```
public synchronized void sampleMethod() {
    ...
}

private Object obj = new Object();
public void sampleBlock() {
    synchronized(obj) {
        ...
    }
}
```
* 위 처럼 간단히 synchronized라는 식별자만 사용하면 동기화할 수 있습니다.

## 언제 동기화를 사용해야 할까 ?
* 하나의 객체를 여러 스레드에서 동시에 사용할 경우
* static으로 선언한 객체를 여러 스레드에서 동시에 사용할 경우

### 동일 객체 접근시
```
public class Contribution {
    private int amount = 0;
    public synchronized void donate() {
        amount++;
    }
    public int getTotal() {
        return amount;
    }
}
```
```
public class Contribution extends Thread {
    private Contribution myContribution;
    private String myName;
    
    public Contributor(Contribution contrubution, String name) {
        myContribution = contribution;
        myName = name;
    }
    
    public void run() {
        for (int loop = 0; loop < 1000; ++loop)
            myContribution.donate();
        System.out.format("%s total = %d\n", myName, myContribution.getTotal());
    }
}
```
```
public class ContributeTest {
    public static void main(String args[]) {
        Contributor[] crs = new Contributor[10];
        Contribution group = new Contribution();
        
        // 기부자와 기부 단체 초기화
        for (int loop = 0; loop < 10; ++loop)
            crs[loop] = new Contributor(group, " Contributor" + loop);
        
        // 기부 실행
        for (int loop = 0; loop < 10; ++loop)
            crs[loop].start();
    }
}
```

### static 사용시
```
public class Contribution {
    private static int amount = 0;
    public static synchronized void donate() {
        amount++;
    }
    public int getTotal() {
        return amount;
    }
}
```
```
public class Contribution extends Thread {
    private Contribution myContribution;
    private String myName;
    
    public Contributor(Contribution contrubution, String name) {
        myContribution = contribution;
        myName = name;
    }
    
    public void run() {
        for (int loop = 0; loop < 1000; ++loop)
            myContribution.donate();
        System.out.format("%s total = %d\n", myName, myContribution.getTotal());
    }
}
```
```
public class ContributeTest {
    public static void main(String args[]) {
        Contributor[] crs = new Contributor[10];
        
        // 기부자와 기부 단체 초기화
        for (int loop = 0; loop < 10; ++loop) {
            Contribution group = new Contribution();
            crs[loop] = new Contributor(group, " Contributor" + loop);
        }
        
        // 기부 실행
        for (int loop = 0; loop < 10; ++loop)
            crs[loop].start();
    }
}
```
* amount를 static으로 선언하면 객체의 변수가 아닌 클래스의 변수가 됩니다.
* 따라서, 각 단체에 따로 기부하는 것은 구현이 불가능합니다.
* synchronized는 각각의 객체에 대한 동기화를 하는 것이기 때문에, synchronized만 사용하면 amount에 대한 동기화는 되지 않습니다.
* 그래서 static synchronized로 구현했지만, 항상 변하는 값(amount)에 대해서 static으로 선언하는 것은 굉장히 위험하다는 것을 알아두시면 좋겠습니다.