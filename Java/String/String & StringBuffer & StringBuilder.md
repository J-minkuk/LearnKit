# String & StringBuffer & StringBuilder

## String
* String은 문자열을 처리하는 자바의 대표적인 클래스입니다.
* String 객체는 한번 생성되면 변경이 불가능한 immutable한 성격을 갖고 있습니다.
* String 객체가 **immutable**한 이유는 변경이 적고 참조만 많은 경우 또는 여러 개의 스레드에서 공유하는 문자열일 경우,<br/>
별다른 동기화를 구현하지 않고 안전하게 공유될 수 있다는 장점이 있기 때문입니다.
* 하지만, 문자열을 변형이 잦은 경우 매번 새로운 String 객체가 생성되기 때문에 메모리와 속도 측면에서 비효율적입니다.
* 따라서, String 클래스는 변경이 적고 단순 참조만 많은 경우 사용합니다.

## StringBuffer & StringBuilder
* StringBuffer 클래스와 StringBuilder 클래스는 새로운 객체를 생성하지 않고 기존 문자열을 변경합니다.
* 단, StringBuilder는 스레드의 동기화를 지원하지 않기 때문에 스레드에서 사용하기 위해서는<br/>
StringBuffer 클래스를 이용해야 합니다.
* 하지만, 동기화 처리를 하지 않는 경우 StringBuilder 클래스가 StringBuffer 클래스보다 빠르기 때문에<br/>
스레드를 사용하지 않는 환경에서는 StringBuilder 클래스를 사용하는 것이 유리합니다.
