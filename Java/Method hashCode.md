# Object.hashCode()
```
Returns a hash code value for the object.
This method is supported for the benefit of hash tables such as those provided by HashMap
```
* 객체의 해시 코드 값을 리턴합니다.
* 이 메소드는 HashMap에서 제공하는 것과 같은 HashTable의 이점을 위해 지원됩니다.

코드로 보겠습니다.
```
package com.study.hashcode.equals

public class LikeLion {
    private String name;
    private int age;
    
    public LikeLion(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
}
```
```
package com.study.hashcode.equals

public class Example01 {
    public static void main(String[] args) {
        Object obj = new Object();
        System.out.println("(1) 참조변수 obj 출력값: " + obj);
        System.out.println("(2) obj 객체의 hashcode 출력값: " + obj.hashCode());
        
        LikeLion lion = new LikeLion("아기사자", 20);
        System.out.println("(3) 참조변수 lion 출력값: " + lion);
        System.out.println("(4) lion 객체의 hashcode 출력값: " + lion.hashCode());
        
        String str1 = "멋사";
        System.out.println("(5) \"멋사\" 객체의 hashcode 출력값: " + str1.hashCode());
    
        String str2 = "멋사";
        System.out.println("(6) \"멋사\" 객체의 hashcode 출력값: " + str2.hashCode());
    }
}
```
출력 결과는 다음과 같습니다.
```
(1) 참조변수 obj 출력값: java.lang.Object@1540e19d
(2) obj 객체의 hashcode 출력값: 356573597
(3) 참조변수 lion 출력값: com.study.hashcode.equals.LikeLion@677327b6
(4) lion 객체의 hashcode 출력값: 1735600054
(5) "멋사" 객체의 hashcode 출력값: 1527745
```
* (1)은 16진수, (2)는 (1)을 10진수로 변환한 값입니다.
* 서로 다른 객체는 각각의 주소값을 갖기 때문에 다른 hashcode 값을 갖습니다.
* (3)도 16진수, (4)는 (3)을 10진수로 변환한 값입니다.
* 정리하면, Object.hashCode() 메소드는 각 객체에 대응되는 고유한 정수값을 리턴합니다.

---

## String을 살펴보자
* 위 예제의 hashCode() 메소드는 Object 클래스에 정의된 메소드입니다.
    > 객체의 주소값과 연관이 있습니다.
* String 클래스의 hashCode() 메소드는 Overriding을 통해 새롭게 정의됩니다.
* 이 새롭게 정의된 내용에 따르면, 같은 문자열은 같은 hashcode 값을 갖습니다.

### Why
* String 클래스에서 hashCode() 메소드를 Overriding하지 않으면,<br/>
String str1 = "멋사" 와 String str2 = "멋사" 의 hashcode는 서로 다른 값이어야 합니다.
* 그런데 String 클래스 입장에서 str1과 str2는 같은 문자열이기 때문에 같은 객체라고 생각할 수 있습니다.
* 같은 문자열을 같은 두 객체의 hashcode 값이 다르다면 hashcode의 의미가 없다고 생각할 수 있습니다.
* hashcode 값을 활용해 Map이나 Set에 저장된 Key 값을 찾아야 하는데,<br/>
같은 객체임에도 불구하고 hashcode 값이 다르니 제대로 찾을 수가 없을 것입니다.
* 그렇기 때문에, 인위적으로 hashCode() 메소드를 Overriding한 것입니다.