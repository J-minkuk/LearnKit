## RDBMS의 한계
* Schema 문제: 빅 데이터를 RDB의 Schema에 맞춰 변경해서 넣으려면 매우 긴 시간의 Down Time이 발생합니다.
* Scale Up의 한계: RDBMS는 애초부터 Scale Out(분산 환경)을 염두에 두고 설계되지 않았습니다.

## NoSQL (Not Only SQL)
* 기본 RDBMS의 한계를 극복하기 위해 만들어진 새로운 형태의 DB입니다.
* 빅 데이터를 다룰 때, RDBMS로만 트래픽을 감당하기 어려워졌고, 이를 해결하기 위해 탄생했습니다.
* NoSQL은 분산 환경에서 대용량의 데이터를 빠르게 처리하기 위해 개발되었습니다.
* 핵심은 Horizontal Scalability(수평 확장)과 High Availability(고가용성)입니다.

## 특징과 장점
* 거대한 Map<String, Object>로서 Key-Value 형식을 지원합니다.
* 대용량 데이터를 저장합니다.
* 분산형 구조를 통해 여러 대의 서버에 분산하여 저장하고 상호 복제하여 데이터 유실이나 서비스 중지에 대비합니다.
* Schema-less
* 읽기 작업보다 쓰기 작업이 더 빠르며, 일반적으로 RDBMS에 비하여 쓰기와 읽기 성능이 빠릅니다.