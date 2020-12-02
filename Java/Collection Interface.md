# Collection Interface 구성
* Collection: 가장 상위 인터페이스
    * Set: 중복을 허용하지 않는 집합을 처리하기 위한 인터페이스
        * SortedSet: 오름차순을 갖는 Set 인터페이스
    * List: 순서가 있는 집합을 처리하기 위한 인터페이스
        > 인덱스로 위치를 지정하여 값을 찾을 수 있습니다.<br/>
        중복을 허용하며, List 인터페이스를 상속받는 클래스 중 가장 많이 사용하는 것으로는 ArrayList가 있습니다.
    * Queue: 여러 개의 객체를 처리하기 전에 담아서 처리할 때 사용하기 위한 인터페이스
        > 기본적으로 FIFO를 따릅니다.
        
## Collection 관련 클래스의 동기화
* 동기화되지 않은 클래스
    > HashSet, TreeSet, LinkedHashSet, ArrayList, LinkedList
* 동기화되어 있는 클래스
    > Vector
    
## 인터페이스별 가장 일반적으로 사용되는 클래스
인터페이스 | 클래스
-----|-----
Set | HashSet
List | ArrayList
Queue | LinkedList

## Collection Interface Method
메소드 | 내용
-------|-------
boolean add(E e) | 객체 e를 내부 목록에 추가합니다.
boolean addAll(Collection<E> c) | 목록 객체 c에 들어있는 항목들을 전부 내부 목록에 추가합니다.
void clear() | 내부 목록에 들어있는 항목 전체를 제거합니다.
boolean contains(Object o) | 파라미터 o와 동일한 값이 들어있는지 확인합니다.<br/>equals 메소드를 호출해서 비교합니다.
boolean equals(Object o) | 객체 o와 this 객체의 equality를 비교합니다.<br/>equals 메소드를 호출해서 비교합니다.
int hashCode() | 내부 객체 목록까지 고려하여 hash code 값을 계산해 리턴합니다.
boolean isEmpty() | 목록이 비어있는지 확인합니다.
Iterator<E> iterator() | 내부 목록에 들어있는 항목을<br/>하나씩 탐색하기 위한 Iterator 객체를 생성하여 리턴합니다.
boolean remove(Object o) | 파라미터 o와 동일한 값(equals)을 목록에서 찾아 제거합니다.<br/>파라미터 값이 null이면 null을 찾아서 제거합니다.
boolean removeAll(Collection c) | 파라미터로 주어진 목록 객체 c에 들어있는 항목들을<br/>this 객체에서 찾아 전부 제거합니다.
boolean retainAll(Collection c) | 파라미터로 주어진 목록 객체 c에 들어있지 않은 항목들을<br/>this 객체에서 찾아 전부 제거합니다.<br/>c에 들어있는 항목들만 this 객체에 남습니다.
int size() | 내부 목록에 들어있는 항목의 수 리턴합니다.
Object[] toArray() | 목록 객체에 들어있는 항목들을 배열에 채워서 리턴합니다.<br/>리턴되는 배열의 타입은 Object[]입니다.
E[] toArray(E[] a) | 목록 객체에 들어있는 항목들을 배열에 채워서 리턴합니다.<br/>리턴되는 배열의 타입은 파라미터로 주어진 배열의 타입과 같습니다.

---

# List Interface
* 배열의 확장판이라고 생각하면 됩니다.
* 데이터의 개수를 확실히 알지 못할 때 유용하게 사용됩니다.

## List 인터페이스를 구현한 클래스
이름 | 내용
-----|-----
Vector | 객체 생성시에 크기를 지정할 필요가 없는 배열 클래스
ArrayList | Vector와 비슷하지만, 동기화 처리가 되어 있지 않습니다.
LinkedList | ArrayList와 동일하지만, Queue 인터페이스를 구현했기 때문에 FIFO 큐 작업을 수행합니다.

---

# Queue Interface
* 데이터를 담아 두었다가 먼저 들어온 데이터부터 처리하기 위해서 사용됩니다.
* 예를 들어, SMS와 같은 문자를 처리할 때 서버에서 들어오는 순서대로 처리하려면 이 Queue에 넣고,<br/>
  처음 요청 받은 데이터부터 처리하면 됩니다.

## List도 순서가 있고, Queue도 순서가 있는데 왜 굳이 Queue가 필요할까 ?
* List의 가장 큰 단점은 데이터가 많은 경우 처리 시간이 늘어난다는 점입니다.
* **ArrayList**의 경우 가장 앞에 있는 데이터(0번 데이터)를 지우면<br/>
  그 다음 1번 데이터부터 마지막 데이터까지 한 칸씩 옮기는 작업을 수행해야 하므로,<br/>
  데이터가 적을 때는 상관없지만, 데이터가 많아질수록 가장 앞에 있는 데이터를 지우는데 소요되는 시간이 증가됩니다.
* **LinkedList**의 경우 순차적으로 찾아가야 하기 때문에 가장 뒤에 있는 데이터를 지우는데 소요되는 시간이 증가합니다.

## Queue Interface를 구현한 클래스
* Queue 인터페이스를 구현한 클래스는 두 가지로 분류됩니다.
    * java.util 패키지에 속하는 LinkedList와 PriorityQueue: 일반적인 목적의 Queue 클래스
    * java.util.concurrent 패키지에 속하는 클래스

이름 | 내용
-----|------
PriorityQueue | 큐에 추가된 순서와 상관없이 우선 순위에 따라 나오도록 되어 있는 큐
LinkedBlockingQueue | 저장할 데이터의 크기를 선택적으로 정할 수 있는 FIFO 기반의 링크 노드를 사용하는 블로킹 큐
ArrayBlockingQueue | 저장되는 데이터의 크기가 정해져있는 FIFO 기반의 블로킹 큐
PriorityBlockingQueue | 저장되는 데이터의 크기가 정해져 있지 않고,<br/>객체의 우선 순위에 따라서 순서가 저장되는 블로킹 큐
DelayQueue | 큐가 대기하는 시간을 지정하여 처리하도록 되어 있는 큐
SynchronousQueue | put() 메소드를 호출하면,<br/>다른 스레드에서 take() 메소드가 호출될 때까지 대기하도록 되어 있는 큐,<br/>이 큐에는 저장되는 데이터가 없습니다.<br/>API에서 제공하는 대부분의 메소드는 0이나 null을 리턴합니다.

* 블로킹 큐(Blocking Queue)란 크기가 지정되어 있는 큐에 더 이상 공간이 없을 때,<br/>
  공간이 생길 때까지 대기하도록 만들어진 큐를 의미합니다.

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

* getPriorityQueue 메소드를 구현합니다.
* 이 메소드에서는 Person 객체를 생성하여 PriorityQueue에 넣고 해당 PriorityQueue를 반환합니다.
* Person 클래스에 Comparable 인터페이스를 구현하지 않고 PriorityQueue에 집어넣으면 어떻게 될까 ?
  > offer는 큐 한쪽 끝에 element를 저장하는데,<br/>
  이때 다형성을 이용하여 추가되는 element 객체를 Comparable 인터페이스로 Up Casting 합니다.<br/>
  하지만, Comparable 인터페이스를 구현한 객체가 아니라면 다음과 같은 에러 메시지를 볼 수 있습니다.
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

---

# Set Interface
* 중복이 없는 집합 객체를 만들 때 유용합니다.

## Set 인터페이스를 구현한 클래스
이름 | 내용
-----|-----
HashSet | 데이터를 해시 테이블에 담는 클래스로 순서 없이 저장됩니다.
TreeSet |red-black이라는 트리에 데이터를 담습니다.<br/>값에 따라 순서가 정해집니다.<br/>데이터를 담는 것과 동시에 정렬을 하기 때문에 HashSet보다 성능상 느립니다.
LinkedHashSet | 해시 테이블에 모든 데이터를 담는데, 저장된 순서에 따라 순서가 결정됩니다.
