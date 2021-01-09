# EventListener
이벤트 리스너를 알아보기 전에 ```ApplicationEventPublisher```를 먼저 간단하게 알아보자.

## ApplicationEventPublisher
ApplicationEventPublisher는 Spring의 ApplicationContext가 상속하는 interface 중 하나다. 
옵저버 패턴의 구현체로 이벤트 프로그래밍에 필요한 기능을 제공한다.

### Code
```java
@Getter
class SampleEvent extends ApplicationEvent {
    private String name;
    
    public SampleEvent(Object source, String name) {
        super(source);
        this.name = name;
    }
}
```
* Spring 4.2 미만에서 이벤트를 만들려면 ```ApplicationEvent```를 상속해야 한다.
* Spring에서 이벤트는 Bean으로 등록하지 않는다.

```java
@Component
class AppRunner implements ApplicationRunner {
    
    private final ApplicationEventPublisher eventPublisher;
    
    public AppRunner(ApplicationEventPublisher eventPublisher) {
        this.eventPublisher = eventPublisher;
    }
    
    @Override
    public void run(ApplicationArguments args) throws Exception {
        eventPublisher.publishEvent(new SampleEvent(this, "Hardy"));
    }
    
}
```
```java
@Slf4j
@Component
class SampleEventHandler implements ApplicationListener<SampleEvent> {
    @Override
    public void onApplicationEvent(SampleEvent event) {
        log.info("{}", event.getName());
    }
}
```
* 발생한 이벤트를 spring이 어디로 전달해야 되는지 알아야 하기 때문에 Bean으로 등록한다.
* Spring 4.2 미만에서 이벤트 핸들러를 만들려면 ```ApplicationListener```를 상속하여 구현해야 한다.
* 애플리케이션을 구동하면 ```ApplicationRunner```에서 호출한 ```eventPublisher.publishEvent()```로 이벤트가 발생하고, 
Spring IoC에 등록되어 있는 Bean중 이 이벤트를 처리할 Handler Bean이 이벤트를 처리한다.
  
---

## EventListener
Spring 4.2부터는 ```@EventListener``` 어노테이션을 통해 구현이 가능하다.

### Code
```java
@Getter
public class SignUpEvent {
    private String userId;

    public SignUpEvent(String userId) {
        this.userId = userId;
    }
}
```
```java
@Slf4j
@Component
public class SmsEventHandler {
    
    @Order(1)
    @EventListener
    public void sendCongratulationSms(SignUpEvent event) {
        log.info("{} 회원에게 가입 축하 메시지 발송 완료", event.getUserId());
    }

    @Order(2)
    @EventListener
    public void sendCouponSms(SignUpEvent event) {
        log.info("{} 회원에게 쿠폰 발송 완료", event.getUserId());
    }

    @Order(Ordered.HIGHEST_PRECEDENCE)
    @EventListener
    public void sendMostImportantSms(SignUpEvent event) {
        log.info("{} HIGHEST_PRECEDENCE", event.getUserId());
    }

    @Async
    @EventListener
    public void sendAsyncSms(SignUpEvent event) {
        log.info("{} async", event.getUserId());
    }
    
}
```
* ApplicationEvent, ApplicationListener를 구현하지 않아도 된다.
> 소스 코드에 Spring 코드가 노출되지 않도록 하는 Spring의 비침투성 사상이 반영됐다.
* 위 예제에서는 Event가 발생한 순서를 ```@Order``` 어노테이션을 사용해 지정했다.
* ```@Async``` 어노테이션으로 비동기도 지원한다.

```java
@Slf4j
@RequiredArgsConstructor
@Service
public class MemberService {

    private final ApplicationEventPublisher eventPublisher;

    public void signUp(String userId) {
        log.info("회원 가입 완료");
        eventPublisher.publishEvent(new SignUpEvent(userId));
    }

}
```
```java
@RequiredArgsConstructor
@RestController
public class MemberTestController {

    private final MemberService memberService;

    @PostMapping("/sign-up")
    public void signUp(@RequestParam("userId") String userId) {
        memberService.signUp(userId);
    }

}
```
애플리케이션을 구동하여 api call 후 찍히는 로그를 보면 다음과 같다.
> logback을 적용했다.
```
2021-01-10 02:57:08,351 | [http-nio-8080-exec-8] INFO  - 회원 가입 완료
2021-01-10 02:57:08,351 | [http-nio-8080-exec-8] INFO  - test HIGHEST_PRECEDENCE
2021-01-10 02:57:08,351 | [asyncTaskExecutor-2] INFO  - test async
2021-01-10 02:57:08,352 | [http-nio-8080-exec-8] INFO  - test 회원에게 가입 축하 메시지 발송 완료
2021-01-10 02:57:08,352 | [http-nio-8080-exec-8] INFO  - test 회원에게 쿠폰 발송 완료
```
* @Order로 지정해준 순서대로 찍힌 것을 확인할 수 있고, async를 제외하면 모두 같은 thread가 찍힌 것을 확인할 수 있다. 
> async는 @Order에 상관없이 찍힌다.

---

## Spring 제공 이벤트
Spring에서 기본적으로 제공하는 이벤트도 있다.

종류 | 설명
----|----
ContextRefreshedEvent | ApplicationContext를 초기화하거나 refresh할 때 발생
ContextStartedEvent | ApplicationContext를 start()하여 라이프 사이클 빈들이 시작 신호를 받은 시점에 발생
ContextStoppedEvent | ApplicationContext를 stop()하여 라이프 사이클 빈들이 정지 신호를 받은 시점에 발생
ContextClosedEvent | ApplicationContext를 close()하여 빈이 소멸되는 시점에 발생
RequestHandledEvent | HTTP 요청을 처리했을 때 발생

위 항목 중 ContextRefreshedEvent, ContextClosedEvent, RequestHandledEvent를 적용해보겠다.

### Code
```java
@Slf4j
@Component
public class ContextEventHandler {

    @EventListener
    public void onContextRefreshedEvent(ContextRefreshedEvent event) {
        log.info("## ContextRefreshedEvent");
    }

    @EventListener
    public void onContextClosedEvent(ContextClosedEvent event) {
        log.info("## ContextClosedEvent");
    }

    @EventListener
    public void onRequestHandledEvent(RequestHandledEvent event) {
        log.info("## RequestHandledEvent {} / {}", event.getDescription(), event.getFailureCause());
    }

}
```
바로 위에서 봤던 예제에 위 Handler만 추가해서 다시 서버를 구동해보면 로그는 다음과 같다.
```
2021-01-10 02:57:00,875 | [main] INFO  - ## ContextRefreshedEvent
2021-01-10 02:57:08,351 | [http-nio-8080-exec-8] INFO  - 회원 가입 완료
2021-01-10 02:57:08,351 | [http-nio-8080-exec-8] INFO  - test HIGHEST_PRECEDENCE
2021-01-10 02:57:08,351 | [mojitoAsyncTaskExecutor-2] INFO  - test async
2021-01-10 02:57:08,352 | [http-nio-8080-exec-8] INFO  - test 회원에게 가입 축하 메시지 발송 완료
2021-01-10 02:57:08,352 | [http-nio-8080-exec-8] INFO  - test 회원에게 쿠폰 발송 완료
2021-01-10 02:57:08,353 | [http-nio-8080-exec-8] INFO  - ## RequestHandledEvent url=[/sign-up]; client=[0:0:0:0:0:0:0:1]; method=[POST]; servlet=[dispatcherServlet]; session=[null]; user=[null]; time=[2ms]; status=[OK] / null
2021-01-10 02:58:15,163 | [Thread-18] INFO  - ## ContextClosedEvent
```
