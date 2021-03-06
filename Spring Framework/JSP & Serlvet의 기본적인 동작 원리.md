# JSP와 Servlet의 기본적인 동작 원리
* 일반적으로 JSP와 같은 웹 프론트단을 처리하는 부분에서 소요되는 시간은 많지 않습니다.

* JSP의 경우 가장 처음에 호출되는 경우만 시간이 소요되고,<br/>
그 이후의 시간에는 컴파일된 서블릿 클래스가 수행되기 때문입니다.

## JSP의 Life Cycle
1. JSP URL 호출
2. 페이지 번역
3. JSP 페이지 컴파일
4. 클래스 로드
5. 인스턴스 생성
6. jspInit 메소드 호출
7. _jspService 메소드 호출
8. jspDestroy 메소드 호출

* 여기서 해당 JSP 페이지가 이미 컴파일되어 있고, 클래스가 로드되어 있고, JSP 파일이 변경되지 않았다면,<br/>
가장 많은 시간이 소요되는 2~4 프로세스는 생략됩니다.

## Servlet의 Life Cycle
* WAS의 JVM이 시작한 후에는
    * Servlet 객체가 자동으로 생성되고 초기화 되거나,<br/>
    사용자가 해당 Servlet을 처음으로 호출했을 때 생성되고 초기화됩니다.
    * 그 다음 계속 '사용 가능' 상태로 대기합니다.<br/>
    그리고 중간에 예외가 발생하면 '사용 불가능' 상태로 빠졌다가 다시 '사용 가능' 상태로 변환되기도 합니다.<br/>
    그리고 나서, 더 이상 해당 Servlet이 필요없을 때는 '파기' 상태로 넘어간 후, JVM에서 제거됩니다.
    
### 기억해야할 점
* Servlet은 JVM에 여러 객체로 생성되지 않습니다.

* **다시 말해, WAS가 시작되고 '사용 가능' 상태가 된 이상 대부분의 Servlet은 JVM에 살아 있고,<br/>
여러 스레드에서 해당 Servlet의 service() 메소드를 호출하여 공유합니다.**