# Servlet이란 무엇인가
* 원칙적으로 javax.servlet.Servlet 인터페이스를 구현한 것입니다.
* 일반적으로 자바 독립 실행 프로그램은 <code>public static void main(String[] args)</code>메소드가 있어서,
해당 메소드가 시작되면 프로그램을 시작하며 main 메소드가 끝나면 프로그램 역시 종료됩니다.
* 하지만 서블릿은 서블릿 컨테이너 내에 등록된 후 서블릿 컨테이너에 의해 생성, 호출, 소멸이 이뤄집니다.
* 다시 말해, 서블릿은 독립적으로 실행되지 않고, main 메소드가 필요하지 않으며, 서블릿 컨테이너에 의해서 서블릿의 상태가 바뀝니다.
* 때때로 서블릿은 자신의 상태 변경 시점을 알아내 적절한 리소스 획득/반환 등의 처리를 해야 하므로 Servlet 인터페이스에 init/destroy 메소드가 정의됩니다.
* 즉, 서블릿 컨테이너는 서블릿의 생명주기에 따라 서블릿의 상태를 변경하면서 Servlet 인터페이스에 정의된 각 메소드를 호출합니다.
* 사용자가 웹 브라우저를 통해 웹 사이트로 접근하면 해당 요청이 웹 브라우저에 의해 HTTP 프로토콜로 변환돼 해당 사이트를 서비스하는 서블릿 컨테이너로 전달됩니다.
* 이 HTTP 프로토콜로 전달된 메시지는 서블릿 컨테이너에서 해석되고 재조합되어 웹 프로그래머가 작성한 서블릿으로 전달되는 과정을 거칩니다.
* 이때 해당 서블릿의 매개변수로 ServletRequest와 ServletResponse를 가지는 service 메소드가 호출되며 클라이언트로부터 전달받은 메시지는 ServletRequest 인터페이스를 통해 전달됩니다.

## GenericServlet
* 서블릿 인터페이스만 구현하면 서블릿 컨테이너가 생성, 소멸 등의 생명주기 관리 작업을 수행할 수 있습니다.
* 그런데 서블릿 컨테이너가 서블릿 관리를 위해 필요한 기능은 서블릿 스펙에 모두 정의되어 있으므로 서블릿 명세는 서블릿에 필요한 구현을 미리 작성해 GenericServlet이란 이름으로 제공합니다.
* 이 GenericServlet 클래스는 추상 클래스이ㅣ지만 abstract void service(ServletRequest req, ServletResponse res)를 제외하고는 모두 구현된 일종의 서블릿을 위한 어댑터 역할을 제공합니다.
* 따라서 서블릿을 작성하는 프로그래머들은 반복적으로 동일한 서블릿 인터페이스를 구현하는 대신 GenericServlet을 상속받아 사용합니다.

## HttpServlet
* 일반적으로 서블릿이라 하면 거의 대부분 이 HttpServlet을 상속받은 서블릿을 의미합니다.
* HttpServlet은 GenericServlet을 상속받으며, GenericServlet의 유일한 추상 메소드인 service를 HTTP 프로토콜 요청 메소드에 적합하게 재구현한 것입니다.
* HTTP 프로토콜의 요청 메소드인 Head, Get, Post, Put, Delete, Options, Trace를 처리하는 메소드가 모두 정의되어 있습니다.
* 서블릿 컨테이너는 받은 요청에 대해 서블릿을 선택한 후 Servlet 인터페이스에 정의된 service(ServletRequest, ServletResponse)를 호출합니다.
* 그러면 클래스 상속 위계에 따라 그 처리가 부모 클래스인 GenericServlet에서 자식 클래스인 HttpServlet으로 넘어옵니다.
* HttpServlet의 service 메소드 내에서는 HTTP 요청 메소드에 의해 여러 doXXX 메소드로 분기돼 처리합니다.
* HttpServlet을 상속받아 웹 프로그래머가 작성한 서블릿은 이 doXXX 메소드를 다시 Overriding하여 HTTP 메소드별로 서로 다른 처리를 수행합니다.

## 정리
* 웹 서비스란 서블릿 컨테이너가 전달받은 HTTP 메시지를 서블릿에 전달하고, 이 서블릿이 동작함으로써 결과가 클라이언트에 반환되는 과정을 말합니다.
* 서블릿 컨테이너는 메시지 헤더의 첫 라인(시작 라인)을 HTTP 메소드, 요청 URL, HTTP 버전으로 다시 분리합니다.
* 그리고 요청 URL을 분석하여 자신이 유지관리하는 서블릿 중 하나를 선택한 후, 서블릿의 service 메소드를 호출해 HTTP 메시지를 처리하도록 위임합니다.

### 그렇다면 실제 서블릿에서 구현된 개별 doGet, doPost 메소드는 어떻게 구별하여 호출하는 것일까 ?
* doGet 메소드와 doPost 메소드의 구분은 서블릿의 바로 상위 클래스인 javax.servlet.HttpServlet에 구현된 내용에 따라 결정됩니다.
* 강조하자면, 서블릿 컨테이너는 최상위 servlet 인터페이스만 인식하고 해당 메소드의 service 메소드를 호출합니다.
* 그러면 메소드 호출은 클래스의 상속 구조를 따라 해당 Servlet 인터페이스의 service 메소드, GenericServlet 클래스의 service 메소드, HttpServlet 클래스의 service 메소드까지 내려갑니다.
* 그리고 전달받은 HTTP 요청의 메소드 종류에 따라 HttpServlet.doGet 또는 HttpServlet.doPost 등으로 분기해 다시 위임됩니다.
* 따라서 프로그래머가 작성한 서블릿이 HttpServlet 클래스를 상속받은 후 doGet 메소드를 Overriding 했다면 프로그래머가 작성한 doGet으로 웹 브라우저가 전달한 HTTP 메시지가 전달됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       
