# JSON과 Parser
* JSON은 XML 다음으로 유명한 데이터 교환 형식 중 하나입니다.
* JSON 데이터는 다음과 같은 2가지 구조를 기본으로 합니다.
    * name / value 형태의 쌍으로 collection 타입
    * 값의 순서가 있는 목록 타입
* JSON도 많은 CPU와 메모리를 점유하며 응답 시간도 느립니다.
* 가장 많이 사용되는 JSON Parser로는 Jackson JSON과 google-gson 등이 있습니다.

* JSON 데이터는 Serialize와 Deserialize를 처리하는 성능이 좋지 않습니다.

## 데이터 전송을 빠르게 하는 라이브러리
* protobuf : 구글에서 제공하는 오픈 소스 라이브러리
* Thrift : 페이스북에서 만들어 Apache 프로젝트로 오픈된 라이브러리