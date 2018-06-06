# 싱글턴 패턴 (Singleton Pattern)
* 싱글턴 패턴이란 인스턴스를 하나만 만들어 사용하기 위한 패턴입니다.
* 커넥션 풀, 스레드 풀, 디바이스 설정 객체 등과 같은 경우 인스턴스를 여러 개 만들게 되면 불필요한 자원을 사용하게 되고, 
또 프로그램이 예상치 못한 결과를 낳을 수 있습니다.
* 싱글턴 패턴은 오직 인스턴스를 하나만 만들고 그것을 계속해서 재사용합니다.
* 싱글턴 패턴을 적용할 경우 의미상 두 개의 객체가 존재할 수 없습니다.
* 이를 구현하려면 객체 생성을 위한 new에 제약을 걸어야 하고, 만들어진 단일 객체를 반환할 수 있는 메소드가 필요합니다.

* 따라서 다음과 같은 3가지 요소가 반드시 필요합니다.
    1. new를 실행할 수 없도록 생성자에 private 접근 제어자를 지정합니다.
    2. 유일한 단일 객체를 반환할 수 있는 정적 메소드가 필요합니다.
    3. 유일한 단일 객체를 참조할 정적 참조 변수가 필요합니다.
* 코드로 보도록 하겠습니다.
```
package singletonPattern;

public class Singleton {
    static Singleton singletonObject;   // 정적 참조 변수
    
    private Singleton() { };            // private 생성자
    
    // 객체 반환 정적 메소드
    public static Singleton getInstance() {
        if (singletonObject == null) {
            singletonObject = new Singleton();
        }
        return singletonObject;
    }
}
```

* getInstance() 정적 메소드를 보면 정적 참조 변수에 객체가 할당되어 있지 않은 경우에만 new를 통해 객체를 만들고 정적 참조 변수에 할당합니다.
* 그리고 정적 참조 변수에 할당되어 있는 유일한 객체의 참조를 반환합니다.
* 이를 사용하는 테스트 코드를 보겠습니다.
```
package singletonPattern;

public class Client {
    public static void main(String[] args) {
        // private 생성자이므로 new를 통해 인스턴스를 생성할 수 없습니다.
        // Singleton s = new Singleton();
        
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
        Singleton s3 = Singleton.getInstance();
        
        System.out.println(s1);
        System.out.println(s2);
        System.out.println(s3);
        
        s1 = null;
        s2 = null;
        s3 = null;
    }
}
```
* 4개의 참조 변수 (singletonObject, s1, s2, s3)가 하나의 단일 객체를 참조하게 됩니다.
* 단일 객체인 경우 결국 공유 객체로 사용되기 때문에 속성을 갖지 않게 하는 것이 정석입니다.
* 단일 객체가 속성을 갖게 되면 하나의 참조 변수가 변경한 단일 객체의 속성이 다른 참조 변수에도 영향을 미치기 때문입니다.
    > 이는 전역/공유 변수를 가능한 한 사용하지 말라는 지침과 일맥상통합니다.
* 다만 읽기 전용 속성을 갖는 것은 문제가 되지 않습니다.
* 이와 더불어 단일 객체가 다른 단일 객체에 대한 참조를 속성으로 갖는 것 또한 문제가 되지 않습니다.
    > 이는 스프링 싱글턴 빈이 가져야 할 제약조건이기도 합니다.
* 위 코드의 실행 결과 출력은 모두 같은 것을 확인할 수 있습니다.
