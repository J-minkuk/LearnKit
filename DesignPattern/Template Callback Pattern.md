# 템플릿 콜백 패턴 (Template Callback Pattern)
* 템플릿 콜백 패턴은 전략 패턴의 변형
* 스프링 3대 프로그래밍 모델 중 하나인 DI(의존성 주입)에서 사용하는 특별한 형태의 전략 패턴
* 템플릿 콜백 패턴은 전략 패턴과 모든 것이 동일한데 전략을 익명 내부 클래스로 정의해서 사용한다는 특징이 있다.
* [전략 패턴 예제 코드](/DesignPattern/Strategy%20Pattern.md)를 템플릿 콜백 패턴으로 바꿔보자.

### 기본 예제 코드
```java
public interface Strategy {
    void runStrategy();
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
        Soldier soldier = new Soldier();
        
        soldier.runContext(new Strategy() {
            @Override
            public void runStrategy() {
                System.out.println("탕탕탕");
            }
        });
        
        soldier.runContext(new Strategy() {
            @Override
            public void runStrategy() {
                System.out.println("챙챙챙");
            }
        });
    }
}
```
* 위 코드를 보면 중복된 코드를 볼 수 있다.

---

### 리팩토링 예제 코드
```java
public interface Strategy {
    void runStrategy();
}
```
```java
public class Soldier {
    void runContext(String weaponSound) {
        System.out.println("전투 시작");
        executeWeapon(weaponSound).runStrategy();
        System.out.println("전투 종료");
    }
    
    private Strategy executeWeapon(final String weaponSound) {
        return new Strategy() {
            @Override
            public void runStrategy() {
                System.out.println(weaponSound);
            }
        };
    }
}
```
```java
public class Client {
    public static void main(String[] args) {
        Soldier soldier = new Soldier();
        
        soldier.runContext("탕탕탕");
        soldier.runContext("챙챙챙");
    }
}
```
* 스프링은 이런 형식으로 리팩터링된 템플릿 콜백 패턴을 DI에 적극 활용하고 있다.

---

## 템플릿 콜백 패턴 정리
* 전략을 익명 내부 클래스로 구현한 전략 패턴
* 템플릿 콜백 패턴은 전략 패턴의 일종이므로 당연히 개방 폐쇄 원칙(OCP)과 의존 역전 법칙(DIP)이 적용된 설계 패턴
