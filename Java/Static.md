# Static
* 자바 프로그래밍에서 성능을 향상시키는 방법은 여러가지가 있습니다.
* 그 중에서 한가지는 static을 사용하는 것입니다.

## static의 특징
* 자바에서 static으로 지정했다면, 해당 메소드나 변수는 정적입니다. (반대말은 dynamic)
* static으로 선언한 변수는 클래스 변수입니다.
* 하나의 JVM이나 WAS 인스턴스에서는 같은 주소에 존재하는 값을 참조합니다.
* GC의 대상이 되지 않습니다.

## static 활용
* 자주 사용하고 절대 변하지 않는 변수는 final static으로 선언하자.

* 설장 파일 정보도 static으로 관리하자.
    > 클래스의 객체를 생성할 때마다 설정 파일을 로딩하면 엄청난 성능 저하가 발생합니다. 이럴 때 반드시 static으로 데이터를 읽어서 관리해야 합니다.

* 코드성 데이터는 DB에서 한 번만 읽자.
    > 쇼핑몰의 상품 코드처럼 양이 많고 자주 바뀔 확률이 높은 데이터를 제외하고, 
    건수가 그리 많지 않되 조회 빈도가 높은 코드성 데이터는 DB에서 한 번만 읽어서 관리하는 것이 성능 측면에서 좋습니다.
    
## static의 잘못된 활용 예제
```
import java.util.HashMap;

public class BadQueryManager {
    
    private static String queryURL = null;
    
    public BadQueryManager(String badUrl) {
        queryURL = badUrl;
    }
    
    public static String getSql(String idSql) {
        try {
            FileReader reader = new FileReader();
            HashMap<String, String> doc = reader.read(queryURL);
            return doc.get(idSql);
        } catch (Exception e) {
            System.out.println(e);
        }
        return null;
    }
}
```
* queryURL 이라는 문자열을 static으로 지정했습니다.
* 문자열이 있는 생성자로 이 클래스 객체를 생성하면 쿼리 파일이 지정됩니다.

> 어떤 사용자가 BadQueryManager의 생성자를 통해 queryURL을 설정하고 getSql() 메소드를 호출 하기 전, 다른 queryURL을 사용하는 사용자의 스레드에서 BadQueryManager의 생성자를 호출하면 어떻게 될까 ?
* 먼저 호출한 사용자는 생성자를 호출했을 때의 URL을 유지하고 있을 거라고 생각하고 getSql() 메소드를 호출하겠지만, 이미 그 값은 변경되고 난 이후입니다. 그러므로 시스템 오류가 발생합니다.
* getSql() 메소드와 queryURL을 static으로 선언한 것이 잘못된 부분입니다.
* 웹 환경이기 때문에 여러 사용자가 호출할 경우 queryURL은 그때 그때 변경됩니다.
* 다시 말하면, queryURL은 static으로 선언됐기 떄문에 클래스의 변수이지 객체의 변수가 아닙니다.
* 모든 스레드에서 동일한 주소를 가리키게 되어 문제가 발생한 것입니다.