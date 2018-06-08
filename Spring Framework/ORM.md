# ORM (Object Relational Mapping)
* 객체형 데이터(Java Object)와 관계형 데이터(RDB의 테이블) 사이에서 개념적으로 일치하지 않는 부분을 해결하기 위해
이 둘 사이를 Mapping하는 것을 의미합니다.
* 이 둘의 각 속성들을 Mapping 할 경우, 관계형 데이터를 객체형 데이터처럼 사용할 수 있습니다.
* 쉽게 말해, SQL 문 작성 없이 간단한 Mapping 설정으로 DB의 테이블 데이터를 Java 객체로 전달받을 수 있는 것입니다.
* Hibernate, iBatis, Spring JPA 등이 존재합니다.

## ORM의 장점

### 생산성 & 유지보수성 향상
* JSP를 이용해 프로젝트를 진행할 때, 중복된 JDBC 코드를 작성하지 않아도 됩니다.
    
### 독립성
* ORM은 DBMS에 종속적이지 않습니다.
* MySQL을 사용하든지 Oracle DB를 사용하든지 Mapping 설정 일부만 변경해주면 Java 코드를 수정할 필요가 없습니다. 

## JPA, MyBatis

### JPA
장점
* 간단한 CRUD는 자동으로 구현됩니다.
* 관계형 DB가 아닌 경우에도 적용할 수 있습니다.
단점
* 복잡한 기능을 구현하기에는 MyBatis가 더 편리합니다.
* 정렬을 위해 Sort 객체를 만들어야 합니다.

### MyBatis
장점
* 복잡한 SQL 문을 작성할 때 resultMap을 활용해 Java 코드로 구현할 양이 줄어듭니다.
* SQL 문을 직접 사용할 수 있습니다.
* MyBatis cache (태그 한줄만 추가하면 됩니다.)
단점
* 관게형 DB가 아니면 안 됩니다. (SQL 문을 사용하기 때문에 그렇습니다.)