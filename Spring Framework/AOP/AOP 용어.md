# AOP 용어
용어 | 영한 사전
-----|-----------
Aspect | 관점, 측면, 양상
Advisor | 조언자, 고문
Advice | 조언, 충고
JoinPoint | 결합점
Pointcut | 자르는 점

## Pointcut - Aspect 적용 위치 지정자
* MyAspect.java
```
package aop001;

import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.JoinPoint;

@Aspect
public class MyAspect {
    @Before("execution(* runSomething())")
    public void before(JoinPoint joinPoint) {
        System.out.println("얼굴 인식 확인: 문 개방");
        // System.out.println("열쇠로 문을 열고 집에 들어간다.");
    }
}
```
* '* runSomething()'이 바로 Pointcut입니다
* public void before는 횡단 관심사를 실행하는 메소드가 됩니다.
* Pointcut을 메소드 선정 알고리즘이라고도 합니다.
* 타겟 메소드 지정자에는 정규식과 AspectJ 표현식 등을 사용할 수 있습니다.
    > [접근제한자패턴]리턴타입패턴[패키지&클래스패턴.]메소드이름패턴(파라미터패턴)[throws 예외패턴]<br/>
    대괄호 []는 생략이 가능합니다.<br/>
    리턴 타입 패턴, 메소드 이름 패턴, 파라미터 패턴은 필수 요소입니다.

```
* runSomething()
----------------
접근 제한자는 무엇이라도 좋으며(생략)
리턴 타입도 무엇이라도 좋으며(*)
모든 패키지 밑의(생략)
모든 클래스 안에(생략)
파라미터가 없으며(())
던져지는 에러가 있든 없든
이름이 runSomething인 메소드(들)를
Pointcut으로 지정합니다.
```

## JoinPoint - 연결 가능한 지점
* Pointcut은 JoinPoint의 부분 집합입니다.
* JoinPoint란 Aspect 적용이 가능한 모든 지점을 말합니다.

## Advice - 언제, 무엇을
* Pointcut에 적용할 메소드를 의미합니다.
* 여기에 더해 언제라는 개념까지 포함하고 있습니다.
* 결국 Advice란 Pointcut에 언제, 무엇을 적용할지 정의한 메소드입니다.
    > Advice를 타겟 객체의 타겟 메소드에 적용할 부가 기능이라고 표현한 책도 있습니다.
* 위 MyAspect.java 코드에서 Pointcut이 시작되기 전(@Before)에 before() 메소드를 실행하라고 되어 있음을 확인할 수 있습니다.

## Aspect - Advisor의 집합체
* AOP에서 Aspect는 여러 개의 Advice와 여러 개의 Pointcut의 결합체를 의미합니다.
    > Aspect = Advice들 + Pointcut들
* Advice는 [언제(when), 무엇을(what)]를 의미하는 것이고, Pointcut은 [어디에(where)]를 의미하는 것입니다.
* 결국 Aspect는 When + Where + What(언제, 어디에, 무엇을)이 됩니다.
* 위 MyAspect.java 코드를 기반으로 해석한다면 Pointcut 중 하나인 public void aop001.Boy.runSomething() 메소드가 시작되기 전(@Before)에 
before() 메소드를 실행하라고 되어 있는 것을 볼 수 있습니다.

## Advisor - 어디서, 언제, 무엇을
* <code>Advisor = 한 개의 Advice + 한 개의 Pointcut</code>와 같이 표현할 수 있습니다.
* Advisor는 스프링 AOP에서만 사용하는 용어입니다.
* 또 스프링 버전이 올라가면서 이제는 사용하지 말라고 권고하는 기능이기도 합니다.
* 왜냐하면 다수의 Advice와 다수의 Pointcut을 다양하게 조합해 사용할 수 있는 Aspect가 나왔기 때문입니다.