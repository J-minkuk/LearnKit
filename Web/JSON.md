# JSON (JavaScript Object Notation)
* 기본적으로 프로그래밍 언어가 아닙니다.
* JSON 데이터는 다음과 같은 2가지 구조를 기본으로 합니다.
    * name / value 형태의 쌍으로 collection 타입
    * 값의 순서가 있는 목록 타입
* XML에 비해 경량화된 데이터 교환 포맷입니다.
* 비동기 브라우저/서버 통신을 위해, XML을 대체할 수 있는 주요 데이터 포맷입니다.
* XML은 모두 String이지만, 그에 비해 JSON은 데이터 타입을 갖습니다.

## JSON과 Parser
* JSON도 많은 CPU와 메모리를 점유하며 응답 시간도 느립니다.
* 가장 많이 사용되는 JSON Parser로는 Jackson JSON과 google-gson 등이 있습니다.
* JSON 데이터는 Serialize와 Deserialize를 처리하는 성능이 좋지 않습니다.

## 데이터 전송을 빠르게 하는 라이브러리
* protobuf : 구글에서 제공하는 오픈 소스 라이브러리
* Thrift : 페이스북에서 만들어 Apache 프로젝트로 오픈된 라이브러리
