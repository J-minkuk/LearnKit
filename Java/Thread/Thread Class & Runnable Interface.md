# Thread 클래스 상속과 Runnable 인터페이스 구현
* 스레드의 구현은 Thread 클래스를 상속받는 것과 Runnable 인터페이스를 구현하는 2가지 방법이 있습니다.
* Thread 클래스는 Runnable 인터페이스를 구현한 것이기 때문에 어느 것을 사용해도 상관은 없지만, Runnable 인터페이스를 구현하면 원하는 기능을 추가할 수 있습니다.
    > 이것은 장점이 될 수도 있지만, 해당 클래스를 수행할 때 별도의 스레드 객체를 생성해야 한다는 단점이 있을 수 있습니다. 또한 자바는 다중 상속을 허락하지 않습니다.
    따라서 스레드를 사용할 때 이미 상속받은 클래스가 있다면 Runnable 인터페이스를 구현해야 합니다.

* Runnable 인터페이스를 구현한 클래스    
```
public class RunnableImpl implements Runnable {
    public void run() {
        System.out.println("This is RunnableImpl.");
    }
}
```

* Thread 클래스를 상속받아 구현한 클래스
```
public class ThreadExtends extends Thread {
    public void run() {
        System.out.println("This is ThreadExtends.");
    }
}
```
## 이 클래스들을 어떻게 실행해야 할까 ?
* Thread 클래스를 상속받은 경우에는 start() 메소드를 호출하면 실행
* Runnable 인터페이스를 구현한 경우에는 Thread 클래스의 Runnable 인터페이스를 매개변수로 받는 생성자를 사용해
Thread 클래스를 만든후 start() 메소드를 호출해야 합니다.

* 실행 소스 코드
```
public class RunThreads {
    public static void main(String[] args) {
        RunnableImpl runnableImpl = new RunnableImpl();
        ThreadExtends threadExtends = new ThreadExtends();
        
        new Thread(runnableImpl).start();
        threadExtends.start();
    }
}
```

---

## sleep(), wait(), join() 메소드
현재 진행 중인 스레드를 대기하도록 하기 위해서 위 3가지 메소드를 사용하는 방법이 있습니다.
* 위 3가지 메소드는 모두 예외를 던지도록 되어 있어 사용할 때는 반드시 예외 처리를 해줘야 합니다.

### wait() 메소드
* 모든 클래스의 부모 클래스인 Object 클래스에 선언되어 있으므로 어떤 클래스에서든 사용할 수 있습니다.
* sleep()과 마찬가지로 명시된 시간만큼 해당 스레드를 대기시킵니다. sleep()과 다른 점은 매개변수인데, 만약 아무런 매개변수를 지정하지 않았다면
notify() 또는 notifyAll() 메소드가 호출될 때까지 대기합니다.

### sleep() 메소드
* 명시된 시간만큼 해당 스레드를 대기시킵니다.
    * sleep(long millis) : 명시된 ms만큼 해당 스레드가 대기합니다. static 메소드이기 때문에 스레드 객체를 통하지 않아도 사용할 수 있습니다.
    * sleep(long millis, int nanos) : 명시된 ms + 명시된 나노 시간만큼 해당 스레드가 대기합니다. 여기서 나노 시간은 0~999999까지 사용할 수 있습니다. (이것도 마찬가지로 static)

### join() 메소드
* 명시된 시간만큼 해당 스레드가 죽기를 기다립니다.
* 아무런 매개변수를 지정하지 않으면 죽을 때까지 계속 대기합니다.

## interrupt(), notify(), notifyAll() 메소드
* isAlive()라는 메소드도 있는데, 이것은 해당 스레드가 살아있는지 확인하는 메소드입니다.
    * 스레드가 살아있다면 true, 아니라면 false를 리턴합니다. 

### interrupt() 메소드
* 앞서 명시한 sleep(), wait(), join() 메소드를 모두 멈출 수 있는 유일한 메소드는 interrupt() 메소드입니다.
    * 하지만 interrupt() 메소드가 절대적인 것은 아닙니다.
    * 간단하게 설명하자면, interrupt() 메소드는 해당 스레드가 block되거나 특정 상태에서만 작동합니다.
* interrupt() 메소드가 호출되면 중지된 스레드는 InterruptedException이 발생합니다.
* 제대로 수행되었는지 확인하려면 interrupted() 메소드를 호출하거나 isInterrupted() 메소드를 호출하면 됩니다.
    * interrupted() 메소드는 스레드의 상태를 변경시킵니다.
    * isInterrupted() 메소드는 단지 스레드의 상태만을 리턴합니다.

### notify(), notifyAll() 메소드
* 위 두 메소드 모두 wait() 메소드를 멈추기 위한 메소드입니다.
* 위 두 메소드는 Object 클래스에 정의되어 있는데, wait() 메소드가 호출된 후 대기 상태로 바뀐 스레드를 깨웁니다.
    * notify() 메소드는 객체의 모니터와 관련 있는 단일 스레드를 깨웁니다.
    * notifyAll() 메소드는 객체의 모니터와 관련 있는 모든 스레드를 깨웁니다.
   
* 대기 메소드와 중단 메소드의 사용법 
```
public class Sleep extends Thread {
    public void run() {
        try {
            Thread.sleep(10000);    // 10초간 대기한 후 종료합니다.
        } catch (InterruptedException e) {
            System.out.println("Somebody stopped me.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    
    public static void main(String args[]) {
        Sleep sleep = new Sleep();
        sleep.start();  // 스레드를 시작합니다.
        
        try {
            int count = 0;
            while (count < 5) {
                sleep.join(1000);   // 1초씩 기다립니다.
                count++;
                System.out.format("%d second waited\n", count);    
            }
            if (sleep.isAlive()) {  // 스레드가 살아있는지 확인합니다.
                sleep.interrupt();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

