# Java System 클래스
* 모든 System 클래스의 메소드는 static으로 되어 있습니다.
* 그 안에서 생성된 in, out, err과 같은 객체들도 static입니다.
* 생성자(Constructor)도 없습니다.

> 결론적으로, 우리는 System 객체를 생성할 수 없으며,<br/>
> System.XXX와 같은 방식을 사용해야 합니다.

### 알아두면 유용한 System 클래스 메소드
* static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)
> 특정 배열을 복사할 때 사용합니다.<br/>
> src: 복사 원본 배열<br/>
> dest: 복사한 값이 들어갈 배열<br/>
> srcPos: 원본의 시작 위치<br/>
> destPos: 복사본의 시작 위치<br/>
> length: 복사하는 개수<br/>

### 절대로 사용해서는 안되는 코드
* static void gc()
* static void exit(int status)
* static void runFinalization()