# 전략 패턴 (Strategy Pattern)
* **디자인 패턴의 꽃**
* 전략 패턴을 구성하는 **3가지 요소**
    1. 전략 메소드를 가진 전략 객체
    2. 전략 객체를 사용하는 컨텍스트(전략 객체의 사용자/소비자)
    3. 전략 객체를 생성해 컨텍스트에 주입하는 클라이언트(제3자, 전략 객체의 공급자)
* ```클라이언트```는 다양한 ```전략``` 중 하나를 선택해 생성한 후 ```컨텍스트```에 주입

---

### Example 
* 군인과 그 군인이 사용할 무기가 있다고 가정
* 보급 장교가 군인에게 무기를 지급하면 군인은 주어진 무기에 따라 전투를 수행
* 이 이야기를 전략 패턴에 따라 구분하면, <code>무기는 전략</code>이 되고, <code>군인은 컨텍스트</code>, <code>보급 장교는 제3자, 즉 클라이언트</code>가 된다.

```java
public interface Strategy {
    void runStrategy();
}
```
```java
public class StrategyGun implements Strategy {
    @Override
    public void runStrategy() {
        System.out.println("탕탕탕");
    }
}
```
```java
public class StrategySword implements Strategy {
    @Override
    public void runStrategy() {
        System.out.println("챙챙챙");
    }
}
```
```java
public class Soldier {
    void runContext(Strategy strategy) {
        System.out.println("전투 시작");
        strategy.runStrategy();
        System.out.println("전투 종료");
    }
}
```
```java
public class Client {
    public static void main(String[] args) {
        Strategy strategy = null;
        Soldier soldier = new Soldier();
        
        // 총을 soldier에게 전달하여 전투를 수행하게 합니다.
        strategy = new StrategyGun();
        soldier.runContext(strategy);
        
        // 검을 soldier에게 전달하여 전투를 수행하게 합니다.
        strategy = new StrategySword();
        soldier.runContext(strategy);
    }
}
```

---

## 전략 패턴 정리
* 클라이언트가 전략을 생성해 전략을 실행할 컨텍스트에 주입하는 패턴
* 개방 폐쇄 원칙(OCP)과 의존 역전 법칙(DIP)이 적용된 설계 패턴
