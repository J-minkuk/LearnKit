## HTTP (Hypertext Transfer Protocol)란?
* HTTP는 서버와 클라이언트가 인터넷 상에서 데이터를 주고받기 위한 프로토콜입니다.
* HTTP는 계속 발전하여 HTTP/2까지 등장한 상태입니다.

## HTTP 작동 방식
* HTTP는 서버/클라이언트 모델을 따릅니다.
* 장점
  * 불특정 다수를 대상으로 하는 서비스에 적합합니다.
  * 클라이언트와 서버가 계속 연결된 형태가 아니기 때문에 클라이언트와 서버 간의 최대 연결 수보다 훨씬 많은 요청과 응답 처리가 가능합니다.

* 단점
  * 연결을 끊어버리기 때문에 클라이언트의 이전 상황을 알 수 없습니다.
  * 이러한 특징을 무상태(Stateless)라고 합니다.
  * 이러한 특징 때문에 정보를 유지하기 위해 Cookie와 같은 기술이 등장했습니다.

## URL (Uniform Resource Locator)
* 인터넷 상의 자원의 위치입니다.
* 특정 웹 서버의 특정 파일에 접근하기 위한 경로 혹은 주소입니다.

## URI (Uniform Resource Identifier)
* URL을 포함하는 더 큰 개념입니다.
* https://www.naver.com/search -> URL
* https://www.naver.com/search?q=mingood -> URI이지만 URL은 아닙니다.

## HTTPS (Hypertext Transfer Protocol over Secure Sockets Layer)
* HTTP처럼 TCP 소켓으로 바로 사용하지 않고 SSL 소켓으로 내려보냅니다.
* 인터넷 상에서 데이터를 주고 받을 때 보안이 되는 프로토콜입니다.