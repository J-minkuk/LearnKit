# Call By Value
```
public class CallByValue {
    public static void main(String[] args) {
        int a = 10;
        int b = a;
        
        b = 20;
        
        System.out.println(a);  // 10
        System.out.println(b);  // 20
    }
}
```
# Call By Reference

```
public class CallByValue {
    public static void main(String[] args) {
        Animal refA = new Animal();
        Animal refB = refA;
        
        refA.age = 10;
        refB.age = 20;
        
        System.out.println(refA.age);  // 20
        System.out.println(refB.age);  // 20
    }
}

class Animal {
    public int age;
}
```

---

# 조건문의 성능
* if 문 안에는 boolean 형태의 결과 값만 사용 가능
* switch 문은 byte, short, char, int, String 타입이 가능. (JDK 7 부터 String 포함)

**switch-case문에서는 주로 정수와 enum을 처리할 수 있었는데,<br/>어떻게 JDK 7에서는 String을 비교할까?**
**int(정수)를 리턴하는 Object 클래스의 hashCode()라는 메소드에 그 답이 있다..!**<br>
String에서 오버라이딩한 hashCode() 메소드는 문자열을 int 값으로 구분하여 switch-case 문에서 사용한다.<br>
즉, **컴파일하면서 case 문에 있는 각 값들을 hashCode로 변환하고,<br/>
 그 값을 작은 것부터 정렬한 다음 String의 equals() 메소드를 사용하여 실제 값과 동일한 지 비교합니다.*<br>
*여기서, 숫자들이 정렬되어 있다는 것을 꼭 기억해야 하는데<br/>
 **switch-case 문은 작은 숫자부터 큰 숫자를 비교하는 게 가장 빠르다.**

---

# 반복문의 성능
* 일반적으로 for 문을 많이 사용합니다.
* while 문은 잘못하면 무한 루프에 빠질 수 있으므로 되도록 for 문 사용을 권장합니다.

## for 문 활용 비교 (A, B, C)
```
[ A 경우 ]
for (int  i = 0; i < list.size(); ++i)

[ B 경우 ]
int listSize = list.size();
for (int i = 0; i < listSize; ++i)
```
* A의 경우 매번 반복하면서 list.size() 메소드를 호출하기 때문에 B 경우와 같이 수정하는 것이 성능에 좋습니다.

```
[ C 경우 ]
for (String str : list)
```
* C와 같은 구문을 For-Each 문이라고 부릅니다.
* For-Each 문을 사용하면 별도로 형변환하거나 get() 메소드 또는 elementAt() 메소드를 호출할 필요 없이<br/>
  순서에 따라 String 객체를 for 문 안에서 사용할 수 있으므로 매우 편리합니다.
* 단, 이 방식은 데이터의 첫 번째부터 마지막 값까지 처리해야 할 경우에만 유용합니다.
* 만약 순서를 거꾸로 돌리거나 특정 값부터 데이터를 탐색하는 경우에는 적절하지 않습니다.

## loop 구문에서의 필요 없는 반복
```
public void sample(DataVO data, String key) {
    TreeSet treeSet2 = null;
    treeSet2 = (TreeSet) data.get(key);
    if (treeSet2 != null) {
        for (int i = 0; i < treeSet2.size(); ++i) {
            DataVO2 data2 = (DataVO2) treeSet2.toArray()[i];
            ...
        }
    }
}
```
* 이 소스 코드의 문제는 toArray() 메소드를 반복해서 호출한다는 것입니다.
* 그러므로, toArray() 메소드가 반복되지 않도록 아래와 같이 for 문 밖으로 옮기는 것이 좋습니다.

```
public void sample(DataVO data, String key) {
    TreeSet treeSet2 = null;
    treeSet2 = (TreeSet) data.get(key);
    if (treeSet2 != null) {
        
        DataVO2[] dataVO2 = (DataVO2) treeSet2.toArray();
        int treeSet2Size = treeSet2.size();
        
        for (int i = 0; i < treeSet2Size; ++i) {
            DataVO2 data2 = dataVO2[i];
            ...
        }
    }
}
```