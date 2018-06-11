# 조건문의 성능
* if 문 안에는 boolean 형태의 결과 값만 사용할 수 있습니다.
* switch 문은 byte, short, char, int, String 타입이 가능합니다. (JDK 7 부터 String이 포함되었습니다.)

## switch-case문에서는 주로 정수와 enum을 처리할 수 있었는데, 어떻게 JDK 7에서는 String을 비교할까 ?
* int(정수)를 리턴하는 Object 클래스의 <b>hashCode()</b>라는 메소드에 그 답이 있습니다.
* String에서 Overriding한 hashCode() 메소드는 문자열을 int 값으로 구분하여 switch-case 문에서 사용합니다.
* 즉, 컴파일하면서 case 문에 있는 각 값들을 hashCode로 변환하고,<br/>
그 값을 작은 것부터 정렬한 다음 String의 equals() 메소드를 사용하여 실제 값과 동일한 지 비교합니다.
* 여기서, 숫자들이 정렬되어 있다는 것을 꼭 기억해야 하는데<br/>
switch-case 문은 작은 숫자부터 큰 숫자를 비교하는 게 가장 빠릅니다.