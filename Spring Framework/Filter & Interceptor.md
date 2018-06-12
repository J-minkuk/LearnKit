# Filter & Interceptor

## 실행 시점
![Filter_Interceptor](./img/Filter%20&%20Interceptor.jpg)

* Filter와 Interceptor는 실행되는 시점이 다릅니다.
* Filter는 Web Application에 등록합니다.
* Interceptor는 Spring의 Context에 등록합니다.

---

## Filter & Interceptor 비교
**공통점**
* 둘 모두 요청에 대한 전후 처리라고 하는 역할을 수행합니다.
* 또한, URI 기반으로 언제 실행할 것인지를 조정할 수 있습니다.

**차이점**
* Filter에서 예외가 발생하면 Web Application에서 처리해야 합니다.
* Interceptor에서 예외가 발생하면 @ControllerAdvice에서 @ExceptionHandler를 사용하여 예외 처리를 할 수 있습니다.

### Interface 비교
**Filter**
```
public interface Filter {
    void doFilter(ServletRequest request, ServletResponse response, FilterChain chain);
}
```
**HandlerInterceptor**
```
public interface HandlerInterceptor {
    boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler);
    void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView mav);
    void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex);
}
```
* Filter는 Servlet에서 처리하기 전후를 다룰 수 있습니다.
* Interceptor는 Handler를 실행하기 전(preHandle), Handler를 실행한 후(postHandle), view를 렌더링한 후(afterCompletion) 등, 
Servlet 내에서도 메소드에 따라 실행 시점을 다르게 가져갑니다.

### Interceptor에서만 가능한 것
* AOP를 흉내낼 수 있습니다.<br/>
@RequestMapping 선언으로 요청에 대한 HandlerMethod(@Controller의 메소드)가 정해졌다면,<br/>
handler라는 이름으로 HandlerMethod가 들어옵니다.<br/>
HandlerMethod로 메소드 시그니처 등 추가적인 정보를 파악해 로직 실행 여부를 판단할 수 있습니다.

* View를 렌더링하기 전에 추가 작업을 할 수 있습니다.<br/>
예를 들어, 웹 페이지가 권한에 따라 GNB(Global Navigation Bar)의 항목이 다르게 노출되어야 하는 경우 등의 처리를 하기 좋습니다.

### Filter에서만 가능한 것
* ServletRequest와 ServletResponse를 교체할 수 있습니다.
```
public class CustomFilter implements Filter {
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) {
        chain.doFilter(new CustomServletRequest(), new CustomServletResponse());
    }
}
```
* HttpServletRequest는 body의 내용을 한 번만 읽을 수 있습니다.
* REST API Application을 작성할 때, 흔히 JSON 형식으로 요청을 받습니다.
* @Controller(Handler)에 요청이 들어오면 body를 한 번 읽게 됩니다.
* 때문에, Filter나 Interceptor에서는 body를 읽을 수 없습니다.
    > IO Exception이 발생합니다.
* body를 로깅하기 위해서는 HttpServletRequest를 감싸 여러 번 inputStream을 열 수 있도록<br/> 
커스터마이징된 ServletRequest를 쓸 수 밖에 업습니다.
```
public class CustomFilter implements Filter {
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) {
        chain.doFilter(new BodyCachedServletRequestWrapper(request), response);
    }
}
```