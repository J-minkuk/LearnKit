# Map Interface
* Key와 Value의 쌍으로 저장되는 구조체이다. 그래서, 단일 객체만 저장되는 다른 Collection API들과는 다르게
따로 분리되어 있다.
* Map: Key와 Value의 쌍으로 구성된 객체의 집합을 처리하기 위한 인터페이스
    > 중복되는 Key를 허용하지 않습니다.
    * SortedMap: Key를 오름차순으로 정렬하는 Map 인터페이스

## Map Interface를 구현한 클래스
이름 | 내용
-----|-----
HashTable | 내부에서 관리하는 해시 테이블 객체가 동기화되어 있으므로, 동기화가 필요한 부분에서는 이 클래스를 사용하는 것이 좋습니다.
HashMap | HashTable 클래스와 다른 점은 null 값을 허용한다는 것과 동기화되어 있지 않다는 것입니다. 
TreeMap | red-black 트리에 데이터를 담습니다. TreeSet과 다른 점은 Key에 의해 순서가 정해진다는 점입니다.
LinkedHashMap | HashMap과 거의 동일하며 이중 연결 리스트라는 방식을 사용하여 데이터를 담는다는 점만 다릅니다.

## Sun에서 정리한, 각 인터페이스별 가장 일반적으로 사용되는 클래스
인터페이스 | 클래스
-----|-----
Map | HashMap