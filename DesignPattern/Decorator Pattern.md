# 데코레이터 패턴 (Decorator Pattern)
* 데코레이터 패턴은 원본에 장식을 더하는 패턴이라는 것이 이름에 잘 드러나 있습니다.
* 데코레이터 패턴은 프록시 패턴과 구현 방법이 같습니다.
* 다만 프록시 패턴은 클라이언트가 최종적으로 돌려 받는 반환값을 조작하지 않고 그대로 전달하는 반면 
데코레이터 패턴은 클라이언트가 받는 반환값에 장식을 더합니다.

## 프록시 패턴과 데코레이터 패턴 비교
프록시 패턴
* 제어의 흐름을 변경하거나 별도의 로직 처리를 목적으로 합니다.
* 클라이언트가 받는 반환값을 특별한 경우가 아니면 변경하지 않습니다.

데코레이터 패턴
* 클라이언트가 받는 반환값에 장식을 더합니다.

### 코드
```
package decoratorPattern;

public interface IService {
    public abstract String runSomething();
}
```
```
package decoratorPattern;

public class Service implements IService {
    public String runSomething() {
        return "서비스";
    }
}
```
```
package decoratorPattern;

public class Decorator implements IService {
    IService service;
    
    public String runSomething() {
        service = new Service();
        return "장식" + service.runSomething();
    }
}
```
```
package decoratorPattern;

public class ClientWithDecorator {
    public static void main(String[] args) {
        IService decoratro = new Decorator();
        System.out.println(decorator.runSomething());
    }
}
```

## 데코레이터 패턴의 중요 포인트
* 장식자는 실제 서비스와 같은 이름의 메소드를 구현하는데, 이때 인터페이스를 사용합니다.
* 장식자는 실제 서비스에 대한 참조 변수를 갖습니다.
* 장식자는 실제 서비스와 같은 이름의 메소드를 호출하고, 그 반환값에 장식을 더해 클라이언트에게 반환합니다.
* 장식자는 실제 서비스의 메소드 호출 전후에 별도의 로직을 수행할 수도 있습니다.

## 데코레이터 패턴 정리
* 메소드 호출의 반환값에 변화를 주기 위해 중간에 장식자를 두는 패턴입니다.
* 프록시 패턴과 동일한 구조를 갖기 때문에 데코레이터 패턴도 개방 폐쇄 원칙(OCP)과 의존 역전 법칙(DIP)이 적용된 설계 패턴입니다.
