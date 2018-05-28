# Collection Interface 구성
* Collection: 가장 상위 인터페이스
    * Set: 중복을 허용하지 않는 집합을 처리하기 위한 인터페이스
        * SortedSet: 오름차순을 갖는 Set 인터페이스
    * List: 순서가 있는 집합을 처리하기 위한 인터페이스
        > 인덱스로 위치를 지정하여 값을 찾을 수 있습니다.<br/>
        중복을 허용하며, List 인터페이스를 상속받는 클래스 중 가장 많이 사용하는 것으로
        ArrayList가 있습니다.
    * Queue: 여러 개의 객체를 처리하기 전에 담아서 처리할 때 사용하기 위한 인터페이스
        > 기본적으로 FIFO를 따릅니다.
        
## Collection 관련 클래스의 동기화
* 동기화되지 않은 클래스
    > HashSet, TreeSet, LinkedHashSet, ArrayList, LinkedList, HashMap, TreeMap, LinkedHashMap
* 동기화되어 있는 클래스
    > Vector, HashTable
    
## Sun에서 정리한, 각 인터페이스별 가장 일반적으로 사용되는 클래스
인터페이스 | 클래스
-----|-----
Set | HashSet
List | ArrayList
Queue | LinkedList
