# Kotlin - Board
코틀린을 익히고자 간단한 예제를 만들어본다.
아래는 기본 설명들을 적어볼 예정.

## variable
코틀린은 변수 타입을 자동 캐스팅하기 때문에 타입을 명시하지 않아도 됨, 하지만 명시할 수도 있음, 기본 타입에 ?를 붙이면 레퍼런스 타입이 됨
```kotlin
var number = 1
var a: Int = 1
var a: Int? = 1 // java의 Integer
```

## companion object
코틀린에는 static 키워드가 존재하지 않는다. 대신 companion object가 존재한다.
```kotlin
data class PostResponseVo(
    var title: String,
    var content: String,
    var author: String
) {
    companion object {
        fun from(post: Post): PostResponseVo {
            return PostResponseVo(post.title, post.content, post.author)
        }
    }
}
```

## fun
```kotlin
fun 함수명(인자1: 타입, 인자2: 타입 ...): 반환 타입 {
    return 
}
```
* 리턴 타입이 void인 경우 Unit 선언
* 리턴 타입을 생략해도 코틀린이 유추해서 자동 캐스팅 해준다.

인자의 기본값도 정의할 수 있다.
```kotlin
fun sum(num1: Int = 1, num2: Int = 10): Int {
    return num1 + num2
}

var sum = sum(num2 = 1)
println(sum)    // 2 출력
```

## interface
Java 8과 동일하게 메소드 구현이 가능하지만, 인스턴스 변수를 초기화 할 수 없고 자식 클래스에서 override 해야한다.

## class
* 클래스는 하나의 Primary Constructor와 Secondary Constructor를 가지는데 Primary Constructor는 클래스를 선언하면서 같이 선언한다.
* Secondary Constructor는 클래스의 코드 블럭 안에서 constructor 키워드를 사용하여 선언한다.

### Data Transfer Object
data 클래스는 getter만 제공한다. (setter는 제공하지 않음)
```kotlin
@Entity
data class Post(
    var title: String,
    var author: String,
    var content: String
) {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    var id: Long = 0
}
```

---

## Collections & Sequences
List의 개수가 적다면 Collections가 빠를 수 있지만, 많다면 Sequences가 성능적으로 유리할 수 있음.

### Java's Collections
* 자바의 컬렉션은 함수형 함수를 제공해주지 않아 Stream으로 map() 등의 Functional functions를 사용할 수 있다.
* Stream은 ```Lazy Evaluation```으로 동작한다. (가능한 코드의 수행을 미루고, 연산이 필요한 순간에 연산을 수행하는 방식)

### Kotlin's Collections
* 코틀린의 컬렉션은 Stream을 사용하지 않아도 언어 자체적으로 Functional functions을 제공한다. (다른 api의 도움없이 map() 등 사용 가능)
* 코틀린의 컬렉션은 ```Eager Evaluation```으로 동작한다.

### Kotlin's Sequences
* Java의 Stream처럼 ```Lazy Evaluation```으로 동작한다.

---


