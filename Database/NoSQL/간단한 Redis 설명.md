## Redis (In Memory)
* Key에 대한 단위 연산이 빠릅니다.
* 하지만 여러 Key에 대한 연산은 느릴 수 있습니다.
* 메모리를 저장소로 쓰는 경우, 아주 빠른 Get과 Put을 지원합니다.

## 장점
* Sharding / Replication 이 용이합니다.
* Speed (간단한 데이터 200만건을 1.28초에 저장합니다.)
* In-Memory
* 데이터 TTL(Time to Live), Expire

## 단점
* Sharding을 클라이언트에서 잘 지정할 필요가 있습니다.
* Replication시 blocking (2.4 버전부터 non-blocking하면서 속도를 개선했습니다.)