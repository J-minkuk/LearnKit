# Portable Service Abstraction - 일관성 있는 서비스 추상화
* 서비스 추상화의 예로 JDBC를 들 수 있습니다.

* JDBC라고 하는 표준 스펙이 있기에 Oracle을 사용하든, MySQL을 사용하든, MS-SQL을 사용하든<br/>
Connection, Statement, ResultSet을 이용해 공통된 방식으로 코드를 작성할 수 있는 것입니다.
    > DB 종류에 관계없이 같은 방식으로 제어할 수 있는 이유는 어댑터 패턴을 활용했기 때문입니다.<br/>
    이처럼 어댑터 패턴을 적용해 같은 일을 하는 다수의 기술을 공통의 인터페이스로 제어할 수 있게 한 것을<br/>
    서비스 추상화라고 합니다.
    
* 스프링 프레임워크에서는 서비스 추상화를 위해 다양한 어댑터를 제공합니다.

* 예를 들어, OXM(Object XML Mapping: 객체와 XML 매핑) 기술만 하더라도<br/>
Castor, JAXB, XMLBeans, JiBX, XStream 등 다양한 기술이 있는데, 이 기술들이 제공하는 API는 제각각입니다.

* 스프링은 제각각인 API를 위한 어댑터를 제공함으로써<br/>
실제로 어떤 OXM 기술을 사용하든 일관된 방식으로 코드를 작성할 수 있게 지원합니다.

* 또한, 하나의 OXM 기술에서 다른 OXM 기술로 변경할 때 큰 변화없이 세부 기술을 교체해서 사용할 수 있게 합니다.

* 스프링은 OXM 뿐만 아니라 ORM, 캐시, 트랜잭션 등 다양한 기술에 대한 PSA를 제공합니다.