# 프록시 패턴 (Proxy Pattern)
* 프록시는 대리자, 대변인이라는 뜻을 가진 단어입니다.
* 대리자/대변인이라고 하면 다른 누군가를 대신해 그 역할을 수행하는 존재를 말합니다.
* 먼저 프록시 패턴이 적용되지 않은 코드를 보도록 하겠습니다.
```
package proxyPattern;

public class Service {
    public String runSomething() {
        return "서비스";
    }
}
```
```
package proxyPattern;

public class ClientWithNoProxy {
    public static void main(String[] args) {
        // 프록시를 이용하지 않은 호출
        Service service = new Service();
        System.out.println(Service.runSomething());
    }
}
```

---

* 이번에는 프록시 패턴이 적용된 코드를 보도록 하겠습니다.
* 프록시 패턴의 경우 실제 서비스 객체가 가진 메소드와 같은 이름의 메소드를 사용하는데,<br/>
이를 위해 인터페이스를 사용합니다.
* 인터페이스를 사용하면 서비스 객체가 들어갈 자리에 대리자 객체를 대신 투입해<br/> 
클라이언트 쪽에서는 실제 서비스 객체를 통해 메소드를 호출하고 반환값을 받는지,<br/> 
대리자 객체를 통해 메소드를 호출하고 반환값을 받는지 전혀 모르게 처리할 수도 있습니다.
```
package proxyPattern;

public interface IService {
    String runSomething();
}
```
```
package proxyPattern;

public class Service implements IService {
    @Override
    public String runSomething() {
        return "서비스";
    }
}
```
```
package proxyPattern;

public class Proxy implements IService {
    IService service1;
    
    @Override
    public String runSomething() {
        service1 = new Service();
        return service1.runSomething();
    }
}
```
```
package proxyPattern;

public class ClientWithProxy {
    public static void main(String[] args) {
        // 프록시를 이용한 호출
        IService proxy = new Proxy();
        System.out.println(proxy.runSomething());
    }
}
```

---

## 프록시 패턴의 중요 포인트
* 대리자는 실제 서비스와 같은 이름의 메소드를 구현하는데, 이때 인터페이스를 사용합니다.
* 대리자는 실제 서비스에 대한 참조 변수를 갖습니다.
* 대리자는 실제 서비스의 같은 이름을 가진 메소드를 호출하고 그 값을 클라이언트에게 반환합니다.
* 대리자는 실제 서비스의 메소드 호출 전후에 별도의 로직을 수행할 수도 있습니다.

## 프록시 패턴 정리
* 제어 흐름을 조정하기 위한 목적으로 중간에 대리자를 두는 패턴입니다.
* 개방 폐쇄 원칙(OCP)과 의존 역전 법칙(DIP)이 적용된 설계 패턴입니다.
