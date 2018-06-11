# Session & Cookie

## Session
* 사용자가 웹 브라우저를 통해 웹서버에 접속한 시점부터 웹 브라우저를 종료하기 전까지 필요한 정보를 저장하거나<br/>
어떠한 상태를 유지시키기 위한 공간입니다.

### Session의 동작 과정
* 웹 브라우저가 서버에 request를 전달합니다.
* 서버는 request-header의 필드인 cookie를 통해 session-id를 검색합니다.
* session-id가 존재하지 않으면 session을 생성해 response-header에 session-id를 추가한 다음 리턴합니다.
* 웹 브라우저가 종료되거나 session이 만료되지 않는 이상 session-id를 통해 session에 접근합니다.

## Cookie
* cookie는 session과 반대로 사용자의 하드에 데이터를 저장하는 방식입니다.
* 만료 시간을 과거로 설정하면 cookie는 저장되지 않고 바로 삭제됩니다.
* session과 달리 영구적으로 저장할 수 있기 때문에 보안성이 낮습니다.

## Local Storage
* 사용자의 정보를 사용자의 하드에 저장한다는 점은 cookie와 동일하지만 용도가 다릅니다.
* cookie는 클라이언트와 서버 측에서 데이터를 사용하기 위한 저장소인 반면,
* local storage는 클라이언트 측에서만 동작합니다.
* 데이터를 서버와 클라이언트가 같이 사용해야 한다면 cookie가 적합하며,
* 클라이언트만 데이터를 사용한다면 local storage가 적합합니다.