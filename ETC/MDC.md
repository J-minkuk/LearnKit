# Mapped Diagnostic Context

## Correlation ID
멀티스레드 환경에서 여러 스레드가 동시에 각각의 요청을 처리할 때 로그를 남기면 스레드들이 컨텍스트를 바꿔가며 실행되기 때문에 로그가 섞인다. 
이 문제를 해결하기 위해 로그를 기록할 때마다 고유 ID를 부여하여 로그를 기록하면 그 ID를 이용해 각 요청마다의 로그를 묶어서 볼 수 있다. 
이 ID를 ```Correlation ID```라고 한다.

## Correlation ID 구현 (feat. ThreadLocal)
요청을 최초 받은 곳에서 Correlation ID를 생성하고 인자로 매번 넘기는 방법은 너무 비효율적이다.
> 모든 곳에 파리미터로 ID가 추가되어야 하기 때문에

자바에서는 ThreadLocal 이라는 변수를 통해 해결할 수 있다. 
ThreadLocal은 스레드의 로컬 컨텍스트 변수로 해당 스레드가 존재하는 한 계속 남아있는 변수다.
> 즉, 스레드가 살아있는 동안 계속 유지되는 변수

## MDC
**slf4j, logback, log4j2 등의 자바 로그 프레임워크에서 위 기능을 MDC로 제공한다!**<br>
```java
public class Sample {
    private static Logger log = LoggerFactory.getLogger(Sample.class);
    
    public static void main(String[] args) {
        log.info("## START");

        MDC.put("memberNo", "9210");
        MDC.put("transactionId", "test-abcdfj");
        log.info("## ING");

        MDC.clear();
        log.info("## END");
    }
}
```
```json
{
  "timestamp" : "2021-01-07T10:30:19.018Z",
  "level" : "INFO",
  "thread" : "main",
  "logger" : "com.example.test.log.TestMDC",
  "message" : "## START",
  "context" : "default"
}
{
  "timestamp" : "2021-01-07T10:30:19.043Z",
  "level" : "INFO",
  "thread" : "main",
  "mdc" : {
    "memberNo" : "9210",
    "transactionId" : "test-abcdfj"
  },
  "logger" : "com.example.test.log.TestMDC",
  "message" : "## ING",
  "context" : "default"
}
{
  "timestamp" : "2021-01-07T10:30:19.046Z",
  "level" : "INFO",
  "thread" : "main",
  "logger" : "com.example.test.log.TestMDC",
  "message" : "## END",
  "context" : "default"
}
```
