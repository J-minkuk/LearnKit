# List Interface
* 배열의 확장판이라고 생각하면 됩니다.
* 데이터의 개수를 확실히 알지 못할 때 유용하게 사용됩니다.

## List 인터페이스를 구현한 클래스
이름 | 내용
-----|-----
Vector | 객체 생성시에 크기를 지정할 필요가 없는 배열 클래스
ArrayList | Vector와 비슷하지만, 동기화 처리가 되어 있지 않습니다.
LinkedList | ArrayList와 동일하지만, Queue 인터페이스를 구현했기 때문에 FIFO 큐 작업을 수행합니다.