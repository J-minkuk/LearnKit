# DB Connection, Connection Pool, DataSource

## DB Connection (DB 연결 수행 과정)
1. 드라이버를 로드합니다.
2. DB 서버의 IP와 ID, PW 등을 DriverManager 클래스의 getConnection 메소드를 사용해 Connection 객체로 만듭니다.
3. Connection으로부터 PreparedStatement 객체를 만듭니다.
4. executeQuery를 수행하여 그 결과로 ResultSet 객체를 받아 데이터를 처리합니다.
5. 모든 데이터를 처리한 후 finally 구문을 사용해 ResultSet, PreparedStatement, Connection 객체를 닫습니다.
    > 각 객체를 close 할 때 예외가 발생할 수 있으므로, 해당 메소드에서는 예외를 던지도록 처리해야 합니다.
    
* 위 과정에서 가장 느린 부분은 Connection 객체를 얻는 부분입니다.
    > DB와 WAS 사이에는 통신을 해야하기 때문입니다.
    > 사용자가 갑자기 증가하면 Connection 객체를 얻기 위한 시간이 많이 소요될 것이고, 많은 화면이 예외를 발생시킬 것입니다.

* 이렇게 Connection 객체를 생성하는 부분에서 발생하는 대기 시간을 줄이고,
네트워크의 부담을 줄이기 위해 사용하는 것이 **DB Connection Pool** 입니다.

## Connection Pool
지금은 모든 WAS에서 Connection Pool을 제공하고, DataSource를 사용하여 JNDI로 호출해 사용할 수 있습니다.
> JNDI (Java Naming and Directory Interface) : 디렉터리 서비스에서 제공하는 데이터 및 객체를 발견하고 참고하기 위한 자바 API

### DataSource와 Connection Pool의 차이
* DataSource는 JDK 1.4 버전부터 생긴 표준입니다.
* Connection Pool로 연결을 관리해야 하고, 트랜잭션 관리도 가능하도록 만들어야 합니다.
* DataSource가 Connection Pool을 포함한다고 생각하면 됩니다.
> 유의할 점: DB Connection Pool은 자바 표준으로 지정되어 있는 것이 없습니다.
> 따라서, WAS에 따라 사용법이 많이 다를 수 있습니다.
> 그러나, DataSource는 자바 표준이므로 WAS에 관계 없이 사용법이 동일합니다.

## PreparedStatement
다음과 같은 프로세스를 거칩니다.
1. 쿼리 문장 분석
2. 컴파일
3. 실행

* PreparedStatement는 처음 한 번만 위 세 단계를 거친 후 캐시에 담아서 재사용합니다.
* 동일한 쿼리를 반복적으로 수행한다면 DB에 적은 부하를 준다는 장점이 있고, 성능 또한 좋습니다.

## executeQuery(), executeUpdate(), execute() 메소드

메소드 이름 | 내용
------------|------------
executeQuery() | select 관련 쿼리를 수행합니다. 수행 결과로 요청한 데이터 값이 ResultSet 객체의 형태로 전달됩니다.
executeUpdate() | select와 관련된 쿼리를 제외한 DML(INSERT, UPDATE, DELETE 등) 및 DDL(CREATE TABLE, CREATE VIEW 등) 쿼리를 수행합니다. 결과는 int 형태로 리턴됩니다.
execute() | 쿼리의 종류와 상관없이 쿼리를 수행합니다. 수행 결과는 ResultSet이 아닌 boolean 형태의 데이터를 리턴합니다.

## DB Connection Pool 및 스레드 개수 설정
이 두 항목의 개수는 메모리와 관련이 있습니다. 많이 사용할수록 메모리를 많이 점유하게 됩니다.
그렇다고 메모리를 위해 DB Connection Pool과 스레드 개수를 적게 지정하면,
서버에서는 많은 요청을 처리하지 못하고 대기할 수 밖에 없습니다.

* 스레드는 입구, DB Connection Pool은 출구라고 생각하면 됩니다.
* DB Connection Pool은 보통 40~50개, 스레드 개수는 이보다 10개 정도 더 지정합니다.
    > 이렇게 지정하는 이유: 스레드의 개수가 DB Connection Pool의 개수보다 적으면
    적은 수만큼의 연결은 필요 없기 때문입니다.
    
### 스레드의 개수보다 DB Connection Pool의 개수가 많아야 하는 이유 ?
* 모든 애플리케이션이나 사용자가 DB에 접속하는 것은 아닙니다.
* 또한 관리자 콘솔을 사용하여 서버에 접속할 수도 있기 때문에, 보통 그만큼 여유분을 갖도록 지정하는 것입니다.

### 가장 적절한 DB Connection Pool과 스레드의 개수는 ?
* 서비스 및 서버의 상황에 맞게 값을 지정해야 합니다.
* 가장 좋은 방법은 성능 테스트를 통해 가장 적절한 값을 구하는 것입니다.

* 가정 Case 1) DB Connection Pool을 40개로 정했다고 가정해보겠습니다. 40개를 전부 사용하면서 DB의 CPU 사용량이 100%에 도달했다면 어떻게 해야 할까?
    * 이 경우 DB의 CPU를 점유하는 쿼리를 찾아 튜닝을 해야 합니다.
        > 인덱스가 없거나, 테이블을 풀 스캔하는 쿼리가 있는 것은 아닌지 확인해봐야 합니다.
    * 40개를 전부 사용한다고 해서 DB Connection Pool 개수를 80 ~ 200개로 늘리면, 결과는 모든 DB와의 연결을 전부 사용하고 응답 시간은 엄청나게 느려질 뿐입니다.
    
* 가정 Case 2) DB의 CPU 사용량은 50%도 되지 않는 상황에서 WAS의 CPU 사용량이 100%에 도달하고 있다. 이 때 사용하는 DB Connection Pool의 개수는 20개 정도 밖에 되지 않는다면 ?
    * 이 경우 WAS의 애플리케이션을 튜닝해야 합니다.
    * 이미 튜닝이 된 상태라면 이 서버의 DB Connection Pool의 개수를 25 ~ 30개로 여유롭게 지정하는 것이 좋습니다.
        > 단순히 서버의 대수를 늘리는 경우가 있는데, 서버를 늘리는 방안은 가장 마지막에 해야합니다.
        
### Connection Pool의 개수만큼이나 중요한 대기 시간(wait time)과 관련된 값
DB Connection Pool의 개수를 넘어 섰을 때 애플리케이션에서는 남는 Connection이 없는지 찾습니다. 이 때, 이 기다리는 시간이 대기 시간입니다.
* MyBatis에서는 poolTimeToWait이라는 값으로 이 대기 시간을 결정하며, 기본값은 20초입니다.
     > 하지만 무작정 이 대기 시간을 줄이는 것보다 시스템 상황에 맞게 설정해야만 예기치 못한 오류 페이지를 피할 수 있습니다.