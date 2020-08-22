# MySQL Storage Engine

## MyISAM
ISAM(Indexed Sequantial Access Method)<br>
**장점**
* 전체적인 속도가 InnoDB 보다 빠르다.
    > 특히 SELECT 가 빠르므로 읽기 작업에 적합하다.
* Full-Text 인덱싱이 가능하여 검색하고자 하는 내용에 대한 복합 검색이 가능하다.

**단점**
* 데이터 무결성이 보장되지 않는다.
* 트랜잭션에 대한 지원이 없기 때문에 작업 도중 문제가 생겨도 이미 작성된 내용들은 DB로 들어간다.
* Table-Level Lock 을 사용하기 때문에 쓰기 작업(INSERT, UPDATE)가 느리다.
    > 변경을 많이 요하는 작업이라면 MyISAM의 사용을 권하지 않는다.
    
## InnoDB
트랜잭션을 지원하므로 트랜잭션-세이프 스토리지 엔진이다.<br>
**장점**
* 데이터 무결성 보장
    > 제약조건, 외래키 생성 가능, 동시성 제어 가능
* Row-Level Lock(행 단위 Lock)을 사용하기 때문에 변경 작업(CUD)가 빠르다.

**단점**
* 여러 기능을 제공하다보니 데이터 모델 디자인에 많은 시간이 필요하다.
* 시스템 자원을 많이 사용한다.
* Full-Text 인덱싱이 불가능하다.
