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