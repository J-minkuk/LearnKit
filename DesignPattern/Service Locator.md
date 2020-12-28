# Service Locator 패턴
* EJB의 EJB Home 객체나 DB의 DataSource를 찾을 때 소요되는 응답 속도를 감소시키기 위해서 사용

## 예시
cache라는 Map 객체에 home 객체를 찾은 결과를 보관하고 있다가, 누군가 그 객체를 필요로 할 때 Map에서 찾아 제공하도록 한다. 만약 해당 객체가 cache라는 Map에 없으면 메모리에서 찾는다.