# Facade Pattern
여러 인터페이스에 대한 통합된 인터페이스를 제공한다. facade에서 고수준 인터페이스를 정의하기 때문에 서브 모듈을 더 쉽게 활용할 수 있다.

## Example

### 음식 Service Layer
```java
public interface FoodService {
    
    void prepare();
    
    void takeout();
    
}
```
```java
public class FoodServiceImpl implements FoodService {
    
    @Override
    public void prepare() {
        System.out.println("음식 준비");
    }
    
    @Override
    public void takeout() {
        System.out.println("음식 주기");
    }
    
}
```

### 영화 Service Layer
```java
public interface MovieService {
    
    void prepare();
    
    void turnOn();
    
    void turnOff();
    
}
```
```java
public class MovieServiceImpl implements MovieService {
    
    @Override
    public void prepare() {
        System.out.println("영화 준비");
    }
    
    @Override
    public void turnOn() {
        System.out.println("영화 On");
    }
    
    @Override
    public void turnOff() {
        System.out.println("영화 Off");
    }
    
}
```

### 영화 Facade
영화, 음식 interface를 하나의 인터페이스로 구성함으로써 서브 시스템들이 더 용이하게 사용할 수 있도록 한다.
```java
public interface MovieFacade {
    
    void prepareWatch();
    
    void startMovie();
    
    void endMovie();
    
}
```
```java
public class MovieFacadeImpl implements MovieFacade {
    
    private final FoodService foodService;
    private final MovieService movieService;
    
    public MovieFacadeImpl(FoodService foodService,
                           MovieService movieService) {
        this.foodService = foodService;
        this.movieService = movieService;
    }
    
    @Override
    public void prepareWatch() {
        foodService.prepare();
        foodService.takeout();
        movieService.prepare();
    }
    
    @Override
    public void startMovie() {
        movieService.turnOn();
    }
    
    @Override
    public void endMovie() {
        movieService.endMovie();
    }
    
}
```