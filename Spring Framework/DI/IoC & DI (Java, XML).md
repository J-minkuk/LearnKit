# Spring Framework
* 스프링을 이해하는 데는 POJO(Plain Old Java Object)를 기반으로 스프링 삼각형이라는 애칭을 가진 IoC/DI, AOP, PSA라고 하는 
스프링의 3대 프로그래밍 모델에 대한 이해가 필수입니다.
* 스프링 삼각형을 이해하지 않은 상태에서 스프링 프레임워크를 학습하는 것은 알파벳을 모르고 영어를 공부하는 것과 마찬가지입니다.

## IoC/DI - 제어의 역전/의존성 주입
* 스프링의 IoC(Inversion of Control / 제어의 역전)라고도 하는 DI(Dependency Injection / 의존성 주입)를 알아보기 전 프로그래밍에서 의존성이란 무엇인지 알아보겠습니다.
```
[ 의사 코드 ]
운전자가 자동차를 생산합니다.
자동차는 내부적으로 타이어를 생산합니다.

[ 자바로 표현 ]
new Car();
Car 객체 생성자에서 new Tire();

[ 그리고 의존성을 단순하게 정의하면 다음과 같습니다. ]
의존성은 new입니다.
new를 실행하는 Car와 Tire 사이에서 Car가 Tire에 의존합니다.
```
* 결론적으로 전체가 부분에 의존한다고 표현할 수 있습니다.
* 전체가 부분에 의존한다는 것과 '프로그래밍에서 의존 관계는 new로 표현된다!'를 기억하시면 됩니다.
* 더 깊이 들어가면 의존하는 객체(전체)와 의존되는 객체(부분) 사이에 집합 관계(Aggregation)와 구성 관계(Composition)로 구분할 수 있습니다.
```
집합 관계: 부분이 전체와 다른 생명 주기를 가질 수 있습니다.
예) 집 vs 냉장고

구성 관계: 부분은 전체와 같은 생명 주기를 갖습니다.
예) 사람 vs 심장
```

### 스프링을 적용하지 않은 기존 방식의 자바 코드
* 먼저 스프링을 적용하지 않은 기존 방식으로 자바 코드를 작성해보겠습니다.
```
package exampleJava;

interface Tire {
    String getBrand();
}
```
```
package exampleJava;

public class KoreaTire implements Tire {
    public String getBrand() {
        return "한국 타이어";
    }
}
```
```
package exampleJava;

public class AmericaTire implements Tire {
    public String getBrand() {
        return "미국 타이어";
    }
}
```
```
package exampleJava;

public class Car {
    Tire tire;
    
    public Car() {
        tire = new KoreaTire();         // 의존 관계가 일어나고 있는 부분
        // tire = new AmericaTire();
    }
    
    public String getTireBrand() {
        return "장착된 타이어: " + tire.getBrand();
    }
}
```
```
package exampleJava;

public class Driver {
    public static void main(String[] args) {
        Car car = new Car();
        System.out.println(car.getTireBrand());
    }
}
```

### 스프링 없이 의존성 주입하기 1 - 생성자를 통한 의존성 주입
```
[ 의사 코드 ]
운전자가 타이어를 생산합니다.
운전자가 자동차를 생산하면서 타이어를 장착합니다.

[ 자바로 표현 - 생성자 인자 이용 ]
Tire tire = new KoreaTire();
Car car = new Car(tire);
```
주입이란?
* 주입이란 말은 외부에서라는 뜻을 내포하고 있는 단어입니다.
* 결국 자동차 내부에서 타이어를 생산하는 것이 아니라 외부에서 생산된 타이어를 자동차에 장착하는 작업이 주입입니다.

```
package exampleJavaDI01;

interface Tire {
    String getBrand();
}
```
```
package exampleJavaDI01;

public class KoreaTire implements Tire {
    public String getBrand() {
        return "한국 타이어";
    }
}
```
```
package exampleJavaDI01;

public class AmericaTire implements Tire {
    public String getBrand() {
        return "미국 타이어";
    }
}
```
```
package exampleJavaDI01;

public class Car {
    Tire tire;
    
    // 생성자 부분이 위 예제와 다른 부분입니다.
    public Car(Tire tire) {
        this.tire = tire;
    }
    
    public String getTireBrand() {
        return "장착된 타이어: " + tire.getBrand();
    }
}
```
```
package exampleJavaDI01;

public class Driver {
    public static void main(String[] args) {
        Tire tire = new KoreaTire();
        // Tire tire = new AmericaTire();
        Car car = new Car(tire);
        
        System.out.println(car.getTireBrand());
    }
}
```
* 기존 방식이라면 Car는 KoreaTire, AmericaTire에 대해 정확히 알고 있어야만 그에 해당하는 객체를 생성할 수 있었습니다.
* 의존성 주입을 적용할 경우 Car는 그저 Tire 인터페이스를 구현한 어떤 객체가 들어오기만 하면 정상적으로 작동하게 됩니다.
* 의존성 주입을 하면 확장성도 좋아지는데, ChinaTire, SpainTire 등 새로운 타이어 브랜드가 생겨도 각 타이어 브랜드들이 Tire 인터페이스를 구현한다면 
Car.java 코드를 변경할 필요가 없습니다.
* 현실 세계의 표준 규격 준수 = 프로그래밍 세계의 인터페이스 구현

### 스프링 없이 의존성 주입하기 2 - 속성을 통한 의존성 주입
```
[ 의사 코드 ]
운전자가 타이어를 생산합니다.
운전자가 자동차를 생산합니다.
운전자가 자동차를 타이어에 장착합니다.

[ 자바로 표현 - 속성 접근자 메소드 사용 ]
Tire tire = new KoreaTire();
Car car = new Car();
car.setTire(tire);
``` 
* 앞서 생성자를 통해 의존성 주입을 하는 코드를 살펴봤습니다.
* 하지만, 생성자를 통해 의존성 주입을 하는 것을 현실 세계에 빗대어 생각해보면 자동차를 생산할 때 한번 타이어를 장착하면 더 이상 타이어를 교체할 수 없게 됩니다.
* 더 이상적인 방법은 운전자가 원할 때 Car의 Tire를 교체하는 것입니다.
* 자바에서 이를 구현하려면 생성자가 아닌 속성을 통한 의존성 주입이 필요합니다.
    > 스프링에서 Annotation(@)을 사용하는 경우 주로 속성 주입 방식을 사용하게 됩니다.
    
```
package exampleJavaDI02;

public class Car {
    Tire tire;
    
    public Tire getTire() {
        return tire;
    }
    
    public void setTire(Tire tire) {
        this.tire = tire;
    }
    
    public String getTireBrand() {
        return "장착된 타이어: " + tire.getBrand();
    }
}
```
* Car.java에서 생성자가 사라지고, tire 속성에 대한 getter, setter 메소드가 생겼습니다.
```
package exampleJavaDI02;

public class Driver {
    public static void main(String[] args) {
        Tire tire = new KoreaTire();
        Car car = new Car();
        car.setTire(tire);
        
        System.out.println(car.getTireBrand());
    }
}
```

### 스프링을 통한 의존성 주입 - XML 파일 사용
```
[ 의사 코드 ]
운전자가 종합 쇼핑몰에서 타이어를 구매합니다.
운전자가 종합 쇼핑몰에서 자동차를 구매합니다.
운전자가 자동차에 타이어를 장착합니다.

[ 자바로 표현 - 속성 메소드 사용 ]
ApplicationContext context = new ClassPathXmlApplicationContext("exampleSpringDI.xml", Driver.class);

Tire tire = (Tire)context.getBean("tire");

Car car = (Car)context.getBean("Car");
car.setTire(tire);
```

* 스프링 프레임워크를 반영한 코드
```
package exampleSpringDI;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Driver {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("exampleSpringDI/exampleSpringDI.xml");
        
        Car car = context.getBean("car", Car.class);
        
        Tire tire = context.getBean("tire", Tire.class);
        
        car.setTire(tire);
        
        System.out.println(car.getTireBrand());
    }
}
```
스프링 프레임워크에 대한 정보를 가지고 있는 패키지
* import org.springframework.context.ApplicationContext;
* import org.springframework.context.support.ClassPathXmlApplicationContext;


* XML 설정 파일
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
    
    <bean id="tire" class="exampleSpringDI.KoreaTire"></bean>
    <bean id="americaTire" class="exampleSpringDI.AmericaTire"></bean>
    <bean id="car" class="exampleSpringDI.Car"></bean>
</beans>
```

스프링을 도입해서 얻는 이득은 무엇일까?
* 가장 큰 이득은 자동차의 타이어 브랜드를 변경할 때 그 무엇도 재컴파일/재배포하지 않아도 XML파일만 수정하면 프로그램의 실행 결과를 바꿀 수 있다는 것입니다.

### 스프링을 통한 의존성 주입 - 스프링 설정 파일(XML)에서 속성 주입
```
[ 의사 코드 - 점점 더 현실 세계를 닮아가고 있습니다. ]
운전자가 종합 쇼핑몰에서 자동차를 구매 요청합니다.
종합 쇼핑몰은 자동차를 생산합니다.
종합 쇼핑몰은 타이어를 생산합니다.
종합 쇼핑몰은 자동차에 타이어를 장착합니다.
종합 쇼핑몰은 운전자에게 자동차를 전달합니다.

[ 자바로 표현 ]
AppicationContext context = new ClassPathXmlApplicationContext("exSpringDI/exSpringDI.xml");
Car car = context.getBean("car", Car.class);

[ XML로 표현 ]
<bean id="koreaTire" class="exSpringDI.KoreaTire></bean>
<bean id="americaTire" class="exSpringDI.AmericaTire></bean>
<bean id="car" class="exSpringDI.Car>
    <property name="tire" ref="koreaTire"></property>
</bean>
```

* 스프링 프레임워크를 반영한 코드
```
package exSpringDI;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Driver {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("exSpringDI/exSpringDI.xml");
        
        Car car = context.getBean("car", Car.class);
                
        System.out.println(car.getTireBrand());
    }
}
```
