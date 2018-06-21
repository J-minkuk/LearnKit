# hashCode() 와 equals

## Case 1: Object
```
package com.study.hashcode.equals;

public class Example02 {
  public static void main(String[] args) {
    Object obj1 = new Object();
    Object obj2 = new Object();
    Object obj3 = new Object();

    System.out.println("obj1.equals(obj2) : " + obj1.equals(obj2));
    System.out.println("obj1.equals(obj3) : " + obj1.equals(obj3));
    System.out.println("obj2.equals(obj3) : " + obj1.equals(obj3));
    System.out.println("obj1.hashCode() : " + obj1.hashCode());
    System.out.println("obj2.hashCode() : " + obj2.hashCode());
    System.out.println("obj3.hashCode() : " + obj3.hashCode());
  }
}
```
출력 결과
```
obj1.equals(obj2) : false
obj1.equals(obj3) : false
obj2.equals(obj3) : false
obj1.hashCode() : 356573597
obj2.hashCode() : 1735600054
obj3.hashCode() : 21685669
```
* 3개의 객체를 모두 비교했을 때 모두 false를 리턴합니다.
    > 즉, 세 객체 모두 다른 객체라는 뜻입니다.
    
## Case 2: String
```
package com.study.hashcode.equals;

public class Example02 {
  public static void main(String[] args) {
    String str1 = "멋사";
    String str2 = "멋사";
    String str3 = "멋사";
    
    System.out.println("str1.equals(str2) : " + str1.equals(str2));
    System.out.println("str1.equals(str3) : " + str1.equals(str3));
    System.out.println("str2.equals(str3) : " + str2.equals(str3));
    System.out.println("str1.hashCode() : " + str1.hashCode());
    System.out.println("str2.hashCode() : " + str2.hashCode());
    System.out.println("str3.hashCode() : " + str3.hashCode());
  }
}
```
출력 결과
```
str1.equals(str2) : true
str1.equals(str3) : true
str2.equals(str3) : true
str1.hashCode() : 1527745
str2.hashCode() : 1527745
str3.hashCode() : 1527745
```
* [Method hashCode.md](Method%20hashCode.md)에서 설명했던 것과 같이<br/>
String 클래스의 hashCode() 메소드는 Overriding 되어 있기 때문에 모두 true를 리턴하고 hashcode 값도 모두 같습니다.

## Case 3: 새롭게 정의된 클래스
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
package com.study.hashcode.equals;

public class Example03 {
  public static void main(String[] args) {
    LikeLion lion1 = new LikeLion("아기사자", 20);
    LikeLion lion2 = new LikeLion("아기사자", 20);

    System.out.println("lion1.equals(lion2) : " + lion1.equals(lion2));
  }
}
```
출력 결과
```
lion1.equals(lion2) : false
```
* 두 객체는 다르다는 결과를 볼 수 있습니다.
* 즉, 새롭게 정의한 클래스에서는 두 객체가 같은 객체임을 의미하는 equals 메소드를 Overriding 해야하는 것입니다.

### equals 메소드 재정의
```
package com.study.hashcode.equals;

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

  @Override
  public boolean equals(Object obj) {
    if (obj instanceof LikeLion) {
      LikeLion likeLion = (LikeLion) obj;
      return (this.age == likeLion.getAge()) && (this.name.equals(likeLion.getName()));
    }
    else return false;
  }
}
```
출력 결과
```
lion1.equals(lion2) : true
lion1.hashCode() : 356573597
lion2.hashCode() : 1735600054
```
* equals 메소드를 재정의하여 true 라는 결과를 얻을 수 있습니다.
* 하지만, 두 객체의 hashcode 값이 다른 것을 볼 수 있습니다.
* 우리는 지금까지 Object에 정의된 hashCode() 메소드를 사용한 것이고,<br/>
equals 메소드를 재정의하기 전에는 false가 나온 두 객체의 hashcode 값이 다르다는 것을 알고 있습니다.
* 그러므로, 지금 이 결과는 hashcode의 의미를 해치고 있는 것이라고 할 수 있습니다.
* 두 LikeLion 객체는 같은 객체이므로 hashcode 값이 같아야만 hashcode가 의미를 갖는 것입니다.
* 그러므로 hashCode() 메소드도 재정의하도록 하겠습니다.

### hashCode() 메소드까지 재정의
```
package com.study.hashcode.equals;

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

  @Override
  public boolean equals(Object obj) {
    if (obj instanceof LikeLion) {
      LikeLion likeLion = (LikeLion) obj;
      return (this.age == likeLion.getAge()) && (this.name.equals(likeLion.getName()));
    }
    else return false;
  }

  @Override
  public int hashCode() {
    return this.age + this.name.hashCode();
  }
}
```
출력 결과
```
lion1.equals(lion2) : true
lion1.hashCode() : 1548878564
lion2.hashCode() : 1548878564
```

## 자바에서 제시하는 hashcode 규약
* equals 메소드의 리턴 값이 true이면, 두 객체의 hashcode 값은 같아야 합니다.
* equals 메소드의 리턴 값이 false이면, 두 객체의 hashcode 값이 꼭 다를 필요는 없습니다.
* 하지만, 서로 다른 hashcode 값을 갖는다면 HashTable의 성능이 향상될 수 있다는 것을 이해하고 있어야 합니다.