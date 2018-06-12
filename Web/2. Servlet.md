# Servlet이란 무엇인가
* **원칙적으로 javax.servlet.Servlet 인터페이스를 구현한 것입니다.**
    >일반적으로 자바 독립 실행 프로그램은 <code>public static void main(String[] args)</code>메소드가 있어서,<br/>
    해당 메소드가 시작되면 프로그램을 시작하며 main 메소드가 끝나면 프로그램 역시 종료됩니다.
    
* 하지만, Servlet은 Servlet Container 내에 등록된 후, Servlet Container에 의해 생성, 호출, 소멸이 이뤄집니다.

* 다시 말해, Servlet은 독립적으로 실행되지 않고, main 메소드가 필요하지 않으며,<br/>
Servlet Container에 의해서 Servlet의 상태가 바뀝니다.

* 때때로, Servlet은 자신의 상태 변경 시점을 알아내 적절한 리소스 획득/반환 등의 처리를 해야 하므로<br/>
Servlet 인터페이스에 init/destroy 메소드가 정의됩니다.

* 즉, Servlet Container는 Servlet의 생명주기에 따라 Servlet의 상태를 변경하면서 Servlet 인터페이스에 정의된 각 메소드를 호출합니다.

* 사용자가 웹 브라우저를 통해 웹 사이트로 접근하면, 해당 요청이 웹 브라우저에 의해 HTTP 프로토콜로 변환되어<br/>
해당 사이트를 서비스하는 Servlet Container로 전달됩니다.

* 이 HTTP 프로토콜로 전달된 메시지는 Servlet Container에서 해석되고 재조합되어 웹 프로그래머가 작성한 Servlet으로<br/>
전달되는 과정을 거칩니다.

* 이때 해당 Servlet에 구현된, 매개변수로 <code>ServletRequest</code>와 <code>ServletResponse</code>를 가지는 service 메소드가 호출되며<br/>
클라이언트로부터 전달받은 메시지는 ServletRequest 인터페이스를 통해 전달됩니다.

---

## GenericServlet
* Servlet 인터페이스만 구현하면 Servlet Container가 Servlet의 생성, 소멸 등의 생명주기 관리 작업을 수행할 수 있습니다.

* 그런데, Servlet Container가 Servlet 관리를 하기 위해 필요한 기능은 Servlet 스펙에 모두 정의되어 있으므로<br/>
Servlet 명세는 Servlet에 필요한 구현을 미리 작성해 GenericServlet이란 이름으로 제공합니다.

* GenericServlet 클래스는 추상 클래스이지만 abstract void service(ServletRequest req, ServletResponse res)를 제외하고는<br/>
모두 구현된 일종의 Servlet을 위한 어댑터 역할을 제공합니다.

* 따라서, Servlet을 작성하는 프로그래머들은 반복적으로 동일한 Servlet 인터페이스를 구현하는 대신<br/>
GenericServlet을 상속받아 사용합니다.

---

## HttpServlet
* 일반적으로 Servlet이라 하면 거의 대부분 이 HttpServlet을 상속받은 Servlet을 의미합니다.

* HttpServlet은 GenericServlet을 상속받으며,<br/>
GenericServlet의 유일한 추상 메소드인 service를 HTTP 프로토콜 요청 메소드에 적합하게 재구현한 것입니다.

* HTTP 프로토콜의 요청 메소드인 Head, Get, Post, Put, Delete, Options, Trace를 처리하는 메소드가 모두 정의되어 있습니다.

* Servlet Container는 받은 요청에 대한 Servlet을 선택한 후 Servlet 인터페이스에 정의된<br/>
service(ServletRequest, ServletResponse)를 호출합니다.

* 그러면, 클래스 상속 위계에 따라 그 처리가 부모 클래스인 GenericServlet에서 자식 클래스인 HttpServlet으로 넘어옵니다.

* HttpServlet의 service 메소드 내에서는 HTTP 요청 메소드에 의해 여러 doXXX 메소드로 분기하여 처리합니다.

* HttpServlet을 상속받아 웹 프로그래머가 작성한 Servlet은 이 doXXX 메소드를 다시 Overriding하여 HTTP 메소드별로<br/>
서로 다른 처리를 수행합니다.

---

## 정리
* 웹 서비스란 Servlet Container가 전달받은 HTTP 메시지를 Servlet에 전달하고,<br/>
이 Servlet이 동작함으로써 결과가 클라이언트에 반환되는 과정을 말합니다.

* Servlet Container는 메시지 헤더의 첫 라인(시작 라인)을 HTTP 메소드, 요청 URL, HTTP 버전으로 다시 분리합니다.

* 그리고 요청 URL을 분석하여 자신이 유지관리하는 Servlet 중 하나를 선택한 후,<br/>
Servlet의 service 메소드를 호출해 HTTP 메시지를 처리하도록 위임합니다.

### 그렇다면 실제 Servlet에서 구현된 개별 doGet, doPost 메소드는 어떻게 구별하여 호출하는 것일까 ?
* doGet 메소드와 doPost 메소드의 구분은<br/>
Servlet의 바로 상위 클래스인 javax.servlet.HttpServlet에 구현된 내용에 따라 결정됩니다.

* **강조하자면, Servlet Container는 최상위 Servlet 인터페이스만 인식하고 해당 메소드의 service 메소드를 호출합니다.**

* 그러면 메소드 호출은 클래스의 상속 구조를 따라 해당 Servlet 인터페이스의 service 메소드,<br/>
GenericServlet 클래스의 service 메소드, HttpServlet 클래스의 service 메소드까지 내려갑니다.

* 그리고 전달받은 HTTP 요청의 메소드 종류에 따라 HttpServlet.doGet 또는 HttpServlet.doPost 등으로 분기되어<br/>
다시 위임됩니다.

* 따라서, 프로그래머가 작성한 Servlet이 HttpServlet 클래스를 상속받은 후 doGet 메소드를 Overriding 했다면,<br/>
프로그래머가 작성한 doGet으로 웹 브라우저가 전달한 HTTP 메시지가 전달됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       
