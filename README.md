# 메모장

## Contents
* [Java](#Java)
* [DataStructure](#DataStructure)
* [Design Pattern](#Design-Pattern)
* [Spring Framework](#Spring-Framework)
* [Cloud](#Cloud)
* [JPA](#JPA)
* [Web](#Web)
* [Database](#Database)
* [Network](#Network)
* [ETC](#ETC)

---

### Java
**Java 버전별 특징 정리**

version | description
--------|---------
5 | - generics<br>- enumeration<br>- annotation<br>- auto boxing/unboxing<br>- concurrency API<br>- static import<br>- 가변 파라미터
7 | - diamond operator<br>- switch-case 문자열 가능<br>- try-with-resources<br>- multi-catch
8 | - Lambda<br>- interface default method<br>- Optional<br>- 날짜와 시간 API(대표적인 예: LocalDateTime)<br>- Stream<br>- type, repeating annotation
  
* [Intro](Java/Intro.md)
* [Static](Java/Static.md)
* [Collection Interface](Java/Collection%20Interface.md)
* [Map Interface](Java/Interface/Map/Map%20Interface.md)
    * [HashTable](Java/Interface/Map/HashTable/1.%20HashTable.md)
        * [Chaining](Java/Interface/Map/HashTable/2.%20Chaining.md)
        * [Linear Probing](Java/Interface/Map/HashTable/3.%20Open%20Addressing%20-%20Linear%20Probing.md)
        * [Quadratic Probing](Java/Interface/Map/HashTable/4.%20Open%20Addressing%20-%20Quadratic%20Probing.md)
        * [Double Hashing](Java/Interface/Map/HashTable/5.%20Open%20Addressing%20-%20Double%20Hashing.md)
* **JVM**
    * [Java Class Loading Process](Java/JVM/1.%20클래스%20로딩%20절차.md)
    * [Java Compile](Java/JVM/2.%20Java%20Compile.md)
    * [HotSpot VM Structure](Java/JVM/3.%20HotSpot%20VM의%20구조.md)
        * [Garbage Collection](Java/JVM/GC/1.%20Garbage%20Collection.md)
        * [Java GC](Java/JVM/GC/2.%20Java%20GC의%20종류.md)
        * [Comprehensive GC Process](Java/JVM/GC/3.%20포괄적인%20GC%20과정.md)
        * [Young Generation Area GC](Java/JVM/GC/4.%20Young%20Generation%20영역의%20GC.md)
        * [Old Generation Area GC](Java/JVM/GC/5.%20Old%20generation%20영역의%20GC.md)
* **Object-Oriented**
    * [Access Modifier](Java/ObjectOriented/1.%20Access%20Modifier.md)
    * [Interface vs Abstract](Java/ObjectOriented/2.%20Interface%20vs%20Abstract.md)
    * [Four Basics of OOP](Java/ObjectOriented/3.%20OOP의%204대%20특성.md)
    * [Polymorphism](Java/ObjectOriented/4.%20Polymorphism.md)
    * [Five Basics of OOD](Java/ObjectOriented/5.%20OOD%205원칙.md)
    * [지바가 확장한 객체 지향](Java/ObjectOriented/6.%20확장한%20객체%20지향.md)
* [Wrapper Class](Java/Wrapper%20Class.md)
* [String & StringBuffer & StringBuilder](Java/String/String%20&%20StringBuffer%20&%20StringBuilder.md)
* [HashCode](Java/Method%20hashCode.md)
* [HashCode & Equals](Java/Method%20hashCode%20&%20equals.md)
* **Generic**
  * [Generic?](Java/Generic.md)
  * [과연 Deep Dive일까](https://github.com/Road-of-CODEr/we-hate-jvm/blob/master/Generic/README.md)
* [Reflection Class](Java/Reflection/Reflection%20Class.md)
* [System Class](Java/System%20Class.md)
* **Thread**
    * [Process & Thread](Java/Thread/1.%20Process%20&%20Thread.md)
    * [Thread Class & Runnable Interface](Java/Thread/2.%20Thread%20Class%20&%20Runnable%20Interface.md)
    * [Synchronized](Java/Thread/3.%20Synchronized.md)
    * [Thread Pool](Java/Thread/4.%20ThreadPool.md)
* [Error & Exception](Java/Error%20&%20Exception.md)
* [IO](Java/IO/IO.md)
    * [IO Model](Java/IO/IO%20Model.md)
* [Atomic](Java/AtomicReference.md)
* [ForkJoinPool](Java/ForkJoinPool.md)

---

### DataStructure
* [Array](DataStructure/Array.md)
* [ArrayList](DataStructure/ArrayList.md)
* [LinkedList](DataStructure/LinkedList.md)
* [Stack](DataStructure/Stack.md)
* [Queue](DataStructure/Queue.md)
* [B-Tree](DataStructure/B-Tree.md)

---

### Design Pattern
* [Transfer Object](DesignPattern/Template%20Callback%20Pattern.md)
* [Decorator](DesignPattern/Decorator%20Pattern.md)
* [Template Callback](DesignPattern/Template%20Callback%20Pattern.md)
* [Singleton](DesignPattern/Singleton%20Pattern.md)
* [Proxy](DesignPattern/Proxy%20Pattern.md)
* [Service Locator](DesignPattern/Service%20Locator.md)
* [Strategy](DesignPattern/Strategy%20Pattern.md)
* [Facade](DesignPattern/Facade%20Pattern.md)

---

### Spring Framework
* [Servlet](Spring%20Framework/Servlet.md)
* [Servlet Container](Spring%20Framework/Servlet%20Container.md)
* [JSP & Servlet의 기본 동작 원리](Spring%20Framework/JSP%20&%20Serlvet의%20기본적인%20동작%20원리.md)
* **IoC & DI**
    * [IoC & DI 간단 정리](Spring%20Framework/DI/IoC%20&%20DI.md)
    * [Java, XML](Spring%20Framework/DI/1.%20IoC%20&%20DI%20(Java,%20XML).md)
    * [@Autowired & @Resource](Spring%20Framework/DI/2.%20IoC%20&%20DI%20(@Autowired%20&%20@Resource).md)
* **AOP**
    * [AOP란](Spring%20Framework/AOP/1.%20AOP.md)
    * [POJO와 XML 기반 AOP](Spring%20Framework/AOP/2.%20POJO와%20XML%20기반%20AOP.md)
    * [AOP 용어](Spring%20Framework/AOP/3.%20AOP%20용어.md)
    * [AOP 기초 완성](Spring%20Framework/AOP/4.%20AOP%20기초%20완성.md)
* [PSA](Spring%20Framework/PSA/PSA.md)
* [Filter & Interceptor](Spring%20Framework/Filter%20&%20Interceptor.md)
* [RestController](Spring%20Framework/RestController.md)
* [EventListener](Spring%20Framework/EventListener.md)

### Cloud
* [Cloud & MSA](SpringCloud/1.Cloud%20&%20MSA.md)
* [Hystrix](SpringCloud/2.Hystrix.md)
* [Ribbon](SpringCloud/3.Ribbon.md)
* [Eureka](SpringCloud/4.Eureka.md)
* [Feign](SpringCloud/5.Feign.md)
* [Zuul](SpringCloud/6.Zuul.md)
* [Sleuth](SpringCloud/7.Sleuth.md)

---

### JPA
* [Intro](JPA/1.Intro.md)
* [Lock](JPA/Lock.md)

---

### Web
* [HTTP](Web/HTTP.md)
* [URL 분석](Web/URL_분석.md)
* [JSON](Web/JSON.md)
* [Rest API](Web/REST%20API.md)
* [Session & Cookie](Web/Session%20&%20Cookie.md)
* [OAuth](Web/OAuth/1.%20OAuth.md)
* [JWT](Web/OAuth/2.%20JWT.md)
* [MSA](Web/MSA.md)
* [Forward & Reverse Proxy](Web/Forward%20&%20Reverse%20Proxy.md)
* [웹 서비스 확장](Web/웹%20서비스를%20확장하려면.md)

---

### Database
**RDB**
* [DB Connection & Connection Pool & DataSource](Database/DB%20Connection%20&%20Connection%20Pool%20&%20DataSource.md) 
* [ACID](Database/RDB/ACID.md)
* [Transaction Isolation](Database/RDB/Transaction%20Isolation.md)
* [index](Database/RDB/1.%20Index.md)
* [index 활용 최적화](Database/RDB/2.%20Index%20활용%20최적화.md)
* [MySQL Engine (MyISAM & InnoDB)](Database/RDB/MySQL/MyISAM%20&%20InnoDB.md)
* **Query Example**
    * [MySQL Basic Query](Database/RDB/MySQL/1.%20Basic%20Query.md) 
    * [MySQL Join](Database/RDB/MySQL/2.%20JOIN.md)
    * [MySQL Group By & Having](Database/RDB/MySQL/3.%20GROUP%20BY%20&%20HAVING.md)
    
**NoSQL**
* [NoSQL 이론](Database/NoSQL/1.%20NoSQL%20이론.md)
* [NoSQL 개념 & 특징](Database/NoSQL/2.%20NoSQL%20개념과%20특징.md)
* [Redis](Database/NoSQL/간단한%20Redis%20설명.md)

---

### Network
* [3-Way-HandShake & 4-Way-HandShake](Network/3-Way-HandShake%20&%204-Way-HandShake.md)

---
### ETC
* [Kotlin](Kotlin/README.md)
* [Zookeeper](ETC/Zookeeper.md)
* [MDC](ETC/MDC.md)
* [RabbitMQ](ETC/RabbitMQ.md)
