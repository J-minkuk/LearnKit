# Reflection 관련 클래스들

## Class 클래스
메소드 이름 | 내용
------------|------------
String getName() | 클래스의 이름을 리턴
Package getPackage() | 클래스의 패키지 정보를 패키지 클래스 타입으로 리턴
Field[] getFields() | public으로 선언된 변수 목록을 Field 클래스 배열 타입으로 리턴
Field getField(String name) | public으로 선언된 변수를 Field 클래스 타입으로 리턴
Field[] getDeclaredFields() | 해당 클래스에서 정의된 변수 목록을 Field 클래스 배열 타입으로 리턴
Field[] getDeclaredFiled(String name) | name과 동일한 이름으로 정의된 변수를 Field 클래스 타입으로 리턴
Method[] getMethods() | public으로 선언된 모든 메소드 목록을 Method 클래스 타입으로 리턴합니다. 해당 클래스에서 사용 가능한 상속받은 메소드도 포함됩니다.
Method getMethod(String name, Class... parameterTypes) | 지정된 이름과 매개변수 타입을 갖는 메소드를 Method 클래스 타입으로 리턴
Method[] getDeclaredMethods() | 해당 클래스에서 선언된 모든 메소드 정보를 리턴
Method getDeclaredMethod(String name, Class... parameterTypes) | 지정된 이름과 매개변수 타입을 갖는 해당 클래스에서 선언된 메소드를 Method 클래스 타입으로 리턴
Constructor[] getConstructors() | 해당 클래스에 선언된 모든 public 생성자의 정보를 Constructor 배열 타입으로 리턴
Constructor[] getDeclaredConstructors() | 해당 클래스에 선언된 모든 생성자의 정보를 Constructor 배열 타입으로 리턴
int getModifiers() | 해당 클래스의 접근자(modifier) 정보를 int 타입으로 리턴
String toString() | 해당 클래스 객체를 문자열로 리턴

* 현재 클래스의 이름이 알고 싶다면 다음과 같이 사용하면 됩니다.
```
[ 패키지 정보까지 포함 ]
String currentClassName = this.getClass().getName();

[ 클래스 이름만 필요한 경우 ]
String currentClassName = this.getClass().getSimpleName();
```

## Method 클래스
메소드 이름 | 내용
------------|------------
Class<?> getDeclaredClass() | 해당 메소드가 선언된 클래스 정보를 리턴
Class<?> getReturnType() | 해당 메소드의 리턴 타입을 리턴
Class<?>[] getParameterTypes() | 해당 메소드를 사용하기 위한 매개변수의 타입들을 리턴
String getName() | 해당 메소드의 이름을 리턴
int getModifiers() | 해당 메소드의 접근자 정보를 리턴
Class<?>[] getExceptionTypes() | 해당 메소드에 정의되어 있는 예외 타입들을 리턴
Object invoke(Object obj, Object... args) | 해당 메소드를 수행합니다.
String toGenericString() | 타입 매개변수를 포함한 해당 메소드의 정보를 리턴
String toString() | 해당 메소드의 정보를 리턴

## Field 클래스
메소드 이름 | 내용
------------|------------
int getModifiers() | 해당 변수의 접근자 정보를 리턴
String getName() | 해당 변수의 이름을 리턴
String toString() | 해당 변수의 정보를 리턴

## Reflection 클래스 활용
```
[ A 경우 ]
public String checkClass(Object obj) {
    if (obj.getClass().getName().equals("java.math.BigDecimal")) {
        ...
    }
}

[ B 경우 ]
public String checkClass(Object obj) {
    if (obj instanceof java.math.BigDecimal) {
        ...
    }
}
```
* reflection 클래스를 활용해야 한다면 A보다 B 경우를 사용하도록 하자. (성능상 B 경우가 6배 빠릅니다.)
> 추가적으로, 클래스의 메타 데이터 정보는 JVM의 Perm 영역에 저장됩니다.<br/>
만약 Class 클래스를 사용하여 많은 클래스를 동적으로 생성하는 일이 벌어지면<br/>
Perm 영역을 더 이상 사용할 수 없게 되어 OutofMemoryError가 발생할 수 있습니다.

