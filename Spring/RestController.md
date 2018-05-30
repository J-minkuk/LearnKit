# @RestController

## @RestController의 동작 방식
* @RestController는 @Controller 어노테이션과 @ResponseBody 어노테이션을 합쳐놓은 어노테이션입니다.
* 클래스 상단에 @RestController 어노테이션을 선언하면 아래의 코드와 동일하게 동작합니다.

```
@Controller
@RequestMapping("/rests")
public class JacksonController {
    @GetMapping("/text")
    @ResponseBody
    public String getPlainText() {
        return "Hello, World!";
    }
}
```

## @Controller와 @RestController의 차이
* Spring Framework는 일반적으로 view 이름을 리턴하여 사용자에게 뷰를 통해 출력되게 되어있습니다.
![controller_flow](./img/controller_flow.png)