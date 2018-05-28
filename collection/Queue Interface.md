# Queue Interface
* 데이터를 담아 두었다가 먼저 들어온 데이터부터 처리하기 위해서 사용됩니다.
* 예를 들어, SMS와 같은 문자를 처리할 때 서버에서 들어오는 순서대로 처리해 주려면 이 Queue에 던져 주고,
처음에 요청한 데이터부터 처리하면 됩니다.

## List도 순서가 있고, Queue도 순서가 있는데 왜 굳이 Queue가 필요할까 ?
* List의 가장 큰 단점은 데이터가 많은 경우 처리 시간이 늘어난다는 점입니다.
* 가장 앞에 있는 데이터(0번 데이터)를 지우면 그 다음 1번 데이터부터 마지막 데이터까지 한 칸씩 옮기는 작업을
수행해야 하므로, 데이터가 적을 때는 상관없지만, 데이터가 많으면 많을수록 가장 앞에 있는 데이터를 지우는데 소요되는
시간이 증가됩니다.

## Queue Interface를 구현한 클래스
* Queue 인터페이스를 구현한 클래스는 두 가지로 분류됩니다.
    * java.util 패키지에 속하는 LinkedList와 PriorityQueue: 일반적인 목적의 Queue 클래스
    * java.util.concurrent 패키지에 속하는 클래스

이름 | 내용
-----|------
PriorityQueue | 큐에 추가된 순서와 상관없이 우선 순위에 따라 나오도록 되어 있는 큐
LinkedBlockingQueue | 저장할 데이터의 크기를 선택적으로 정할 수 있는 FIFO 기반의 링크 노드를 사용하는 블로킹 큐
ArrayBlockingQueue | 저장되는 데이터의 크기가 정해져있는 FIFO 기반의 블로킹 큐
PriorityBlockingQueue | 저장되는 데이터의 크기가 정해져 있지 않고, 객체의 우선 순위에 따라서 순서가 저장되는 블로킹 큐
DelayQueue | 큐가 대기하는 시간을 지정하여 처리하도록 되어 있는 큐
SynchronousQueue | put() 메소드를 호출하면, 다른 스레드에서 take() 메소드가 호출될 때까지 대기하도록 되어 있는 큐, 이 큐에는 저장되는 데이터가 없습니다. API에서 제공하는 대부분의 메소드는 0이나 null을 리턴합니다.

* 블로킹 큐(Blocking Queue)란 크기가 지정되어 있는 큐에 더 이상 공간이 없을 때, 공간이 생길 때까지 대기하도록 만들어진 큐를 의미합니다.

### PriorityQueue 예제
* 가중치가 낮은 Person 객체를 먼저 꺼내기 위해 compareTo 메소드를 오름차순으로 정렬되도록 구현합니다.
```
class Person implements Comparable<Person> {
    String name;
    int weight;
    
    public Person(String name, int weight) {
        super();
        this.name = name;
        this.weght = weight;        
    }
    
    @Override
    public int compareTo(Person person) {
        if (this.weight > person.weight) return 1;
        else if (this.weight < person.weight) return -1;
        else return 0;
    }
}
```

* getPriorityQueue 메소드를 구현합니다. 이 메소드에서는 Person 객체를 생성하여 PriorityQueue에 넣고 해당 PriorityQueue를 반환합니다.
* Person 클래스에 Comparable 인터페이스를 구현하지 않고 PriorityQueue에 집어넣으면 어떻게 될까 ?
    > offer는 큐 한쪽 끝에 element를 저장하는데, 이때 다형성을 이용하여 추가되는 element 객체를 Comparable 인터페이스로
    Up Casting 합니다. 하지만, Comparable 인터페이스를 구현한 객체가 아니라면 다음과 같은 에러 메시지를 볼 수 있습니다.
    ```
    Exception in thread "main" java.lang.ClassCastException: Person cannot be cast to java.lang.Comparable
    ```
```
private static PriorityQueue<Person> getPriorityQueue() {

    Person person1 = new Person("Jo", 3);
    Person person2 = new Person("Min", 100);
    Person person3 = new Person("Kuk", 14);
    Person person4 = new Person("Super", 10);
    Person person5 = new Person("Man", 1);
    
    PriorityQueue<Person> priorityQueue = new Priority<>();
    
    priorityQueue.offer(person1);
    priorityQueue.offer(person2);
    priorityQueue.offer(person3);
    priorityQueue.offer(person4);
    priorityQueue.offer(person5);
    
    return priorityQueue;
}
```

```
public static void main(String[] args) {

    PriorityQueue<Person> priorityQueue = getPriorityQueue();
    
    while (!priorityQueue.isEmpty()) {
        Person person = priorityQueue.poll();
        System.out.println(person.name);
    }
}
```
* 다음과 같은 출력 결과를 볼 수 있습니다.
```
Man
Jo
Super
Kuk
Min
```

