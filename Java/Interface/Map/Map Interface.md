# Map Interface
* Key와 Value의 쌍으로 저장되는 구조체입니다. 그래서, 단일 객체만 저장되는 다른 Collection API들과는 다르게 따로 분리되어 있습니다.
* Map: Key와 Value의 쌍으로 구성된 객체의 집합을 처리하기 위한 인터페이스입니다.
    > 중복되는 Key를 허용하지 않습니다.
    * SortedMap: Key를 오름차순으로 정렬하는 Map 인터페이스

## Map Interface를 구현한 클래스
이름 | 내용
-----|-----
HashTable | 내부에서 관리하는 해시 테이블 객체가 동기화되어 있으므로, 동기화가 필요한 부분에서는 이 클래스를 사용하는 것이 좋습니다.
HashMap | HashTable 클래스와 다른 점은 null 값을 허용한다는 것과 동기화되어 있지 않다는 것입니다. 
TreeMap | red-black 트리에 데이터를 담습니다. TreeSet과 다른 점은 Key에 의해 순서가 정해진다는 점입니다.
LinkedHashMap | HashMap과 거의 동일하며 이중 연결 리스트라는 방식을 사용하여 데이터를 담는다는 점만 다릅니다.

## Map 관련 클래스의 동기화
* 동기화되지 않은 클래스
    > HashMap, TreeMap, LinkedHashMap
* 동기화되어 있는 클래스
    > HashTable

## 각 인터페이스별 가장 일반적으로 사용되는 클래스
인터페이스 | 클래스
-----|-----
Map | HashMap

## Map<K,V> Interface Method
메소드 | 내용
-------|-------
void clear() | 내부 목록에 들어있는 항목 전체를 제거합니다.
boolean containsKey(Object k) | 등록된 key 목록 중 k가 포함되어 있는지 확인합니다.
boolean containsValue(Object v) | 등록된 value 목록 중 v가 포함되어 있는지 확인합니다.
V get(Object k) | (Key: k)로 등록된 value를 리턴합니다.
V put(K k, V v) | (Key: k, Value: v)를 등록합니다.<br/>(Key: k)로 이미 등록되어 있던 value가 있다면 v로 치환됩니다.<br/>리턴 값은 (Key: k)로 이미 등록되어 있는 value이고, 등록되어 있던 value가 없을 경우 null을 리턴합니다.
void putAll(Map map) | map에 등록되어 있는 데이터 항목들을 전부 this에 등록합니다.
boolean isEmpty() | 등록된 데이터가 0개이면 true를 리턴합니다.
Set<K> keySet() | 등록된 Key 목록을 Set 타입으로 리턴합니다.
Set<Map, Entry<K, V>> entrySet() | 등록된 데이터 항목들의 목록을 Set 컬렉션 타입으로 리턴합니다.<br/>Key의 타입은 K이고, Value의 타입은 V입니다.<br/>데이터 항목 1개의 타입은 Map.Entry<K, V>입니다.<br/>리턴되는 데이터 항목의 목록 타입은 Set<Map.Entry<K, V>>입니다.
V remove(K k) | (Key: k)로 등록되어 있던 데이터를 제거합니다.<br/>리턴 값은 (Key: k)로 이미 등록되어 있던 value입니다.<br/>등록되어 있던 value가 없으면 null을 리턴합니다.
int size() | 등록된 데이터 항목의 수를 리턴합니다.
Collection<V> values() | 등록된 value 목록을 Collection 타입으로 리턴합니다.
