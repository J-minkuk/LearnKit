# 상태 코드

코드 | 내용
-----|-----
2XX 리턴 코드 | 정상적인 경우의 리턴 코드 (200 코드가 대부분입니다.)
3XX 리턴 코드 | Redirection이 필요한 경우의 리턴 코드 (대부분 302 또는 304 코드입니다. 만약 브라우저의 캐시를 사용하여 이미지나 CSS, JS 파일 등을 다시 서버에 요청하지 않는 경우에 이 코드가 리턴됩니다.)
4XX 리턴 코드 | 클라이언트 오류가 있을 경우의 리턴 코드입니다. (대부분 404 코드가 많습니다. 만약 서버에 존재하지 않는 주소를 요청하면 이 코드가 리턴됩니다.)
5XX 리턴 코드 | 서버에 오류가 있을 경우의 리턴 코드입니다. (서버에서 Exception이 발생했을 때 오류 페이지 처리를 하지 않으면 500 코드를 주로 리턴합니다.)

## 상세 코드 내용
* 2XX 리턴 코드

코드 | 내용
-----|-----
200 | OK, 에러없이 전송 성공
201 | Created, POST 명령 실행 및 성공
202 | Accepted, 서버가 클라이언트 명령을 받음
203 | Non-authoritative information, 서버가 클라이언트 요구 중 일부만 전송
204 | No content, 클라이언트 요구를 처리했으나 전송할 데이터가 없음
205 | Reset content
206 | Partial content

* 3XX 리턴 코드

코드 | 내용
-----|-----
300 | Multiple choices, 최근에 옮겨진 데이터를 요청
301 | Moved permanently, 요구한 데이터를 변경된 임시 URL에서 찾았음
302 | Moved temporarily, 요구한 데이터가 변경된 URL에 있음을 명시
303 | See other, 요구한 데이터를 변경하지 않았기 때문에 문제가 있음
304 | Not modified
305 | Use proxy

* 4XX 리턴 코드

코드 | 내용
-----|-----
400 | Bad request, 클라이언트의 잘못된 요청으로 처리할 수 없음
401 | Unauthorized, 클라이언트의 인증 실패
402 | Payment required, 예약됨
403 | Forbidden, 접근이 거부된 문서를 요청함
404 | Not found, 문서를 찾을 수 없음
405 | Method not allowed, 리소스를 허용하지 않음
406 | Not acceptable, 허용할 수 없음
407 | Proxy authentication required, 프록시 인증 필요
408 | Request timeout, 요청 시간을 초과함
409 | Conflict
410 | Gone, 영구적으로 사용할 수 없음
411 | Length required
412 | Precondition failed, 전체 조건 실패
413 | Request entity too large
414 | Request-URI too long, URL이 너무 김
415 | Unsupported media type

* 5XX 리턴 코드

코드 | 내용
-----|-----
500 | Internal server error, 내부 서버 오류 (잘못된 스크립트 실행시)
501 | Not implemented, 클라이언트에서 서버가 수행할 수 없는 행동을 요구함
502 | Bad gateway, 서버의 과부하 상태
503 | Service unavailable, 외부 서비스가 죽었거나 현재 멈춤 상태
504 | Gateway timeout
505 | HTTP version not supported