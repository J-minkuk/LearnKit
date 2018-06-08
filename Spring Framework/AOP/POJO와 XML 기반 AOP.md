# POJO와 XML 기반 AOP
* 기존의 어노테이션 기반으로 작성한 AOP 예제를 POJO와 XML 기반으로 전환하기 위해 변경해야할 곳은 Aspect가 정의되어 있는 
MyAspect.java와 스프링 설정 정보 XML 파일입니다.

---
* @ 어노테이션 기반 코드
```
기존
@ 어노테이션 기반 - MyAspect.java가 스프링 프레임워크에 종속
package aop001;

import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.JoinPoint;

@Aspect
public class MyAspect {
    @Before("execution(* runSomething())")
    public void before(JoinPoint joinPoint) {
        System.out.println("얼굴 인식 확인: 문 개방");
    }
}
```
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    
    xsi:schemaLocation="
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop-3.1.xsd
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
        
    <aop:aspectj-autoproxy />
    
    <bean id="myAspect" class="aop001.MyAspect"></bean>
    <bean id="boy" class="aop001.Boy"></bean>
    <bean id="girl" class="aop001.Girl"></bean>
</beans>
```

---

* POJO & XML 기반 코드
```
변경
POJO & XML 기반 - 스프링 프레임워크에 종속되지 않음
package aop001;

import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.JoinPoint;

@Aspect
public class MyAspect {
    public void before(JoinPoint joinPoint) {
        System.out.println("얼굴 인식 확인: 문 개방");
    }
}
```
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    
    xsi:schemaLocation="
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop-3.1.xsd
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
        
    <aop:aspectj-autoproxy />
    
    <bean id="myAspect" class="aop001.MyAspect"></bean>
    <bean id="boy" class="aop001.Boy"></bean>
    <bean id="girl" class="aop001.Girl"></bean>
    
    <aop:config>
        <aop:aspect ref="myAspect">
            <aop:before method="before" pointcut="execution(* runSomething())" />
        </aop:aspect>
    </aop:config>
</beans>
```