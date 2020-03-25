### 함수<sup>Function</sup>와 변수<sup>Variable</sup>

* 함수를 선언할때 `fun` 키워드를 사용한다.

* 파라미터 이름 뒤에 타입을 쓴다.

  ```kotlin
  fun main(args: Array<String>) {
    // do something
  }
  ```

* 클래스 밖에 함수를 작성할 수 있다.

  * 대신 클래스의 일부가 아니므로 오버라이드 할 수 없다.

* 배열도 일반적인 클래스와 마찬가지로 취급한다. 배열 처리를 위한 문법이 따로 존재하지 않는다.

* `System.out.println()` 대신 `println()`으로 작성한다.

  * 여러가지 표준 자바 라이브러리 함수를 간결하게 사용할 수 있게 해주는 래퍼<sup>Wrapper</sup>를 제공한다.

* **세미콜론을 붙이지 않아도 된다.**

#### 함수<sup>Function</sup>

##### 블록이 본문인 함수<sup>Block body function</sup>

```kotlin
fun max(a: Int, b: Int): Int {
  return if (a > b) a else b
}
```

* fun <함수이름>(<파라미터 이름>: <파라미터 타입>, ...): <리턴값 타입> { <구현부> }` 와 같은 형태를 띈다.
* 코틀린 `if`는 문<sup>Statement</sup>가 아닌 **식<sup>Expression</sup>이다.**
  * 식<sup>Expression</sup>은 값을 만들어 내며 다른 식의 하위 요소로 계산에 참여할 수 있다.
  * 문<sup>Statement</sup>는 자신을 둘러싸고 있는 가장 안쪽 블록의 최상위 요소로 존재하며, 아무 값을 만들어내지 못한다.
* 자바에서는 대입문이 식<sup>Expression</sup>이었지만, 코틀린에서는 문<sup>Statement</sup>가 되었다.

##### 식이 본문인 함수<sup>Expression body function</sup>

```kotlin
fun max(a: Int, b: Int): Int = if (a > b) a else b
```

* 위 코드조각을 한줄로 간결하게 표현할 수 있다. 중괄호와 `return`을 제외하고 `=` 키워드를 통해 식<sup>Expression</sup>의 결과값을 반환하는 함수를 간결하게 표현한다.
* 게다가, 반환 타입까지 생략할 수 있다.
  * 타입 추론<sup>Type inference</sup>에 의해서 식<sup>Expression</sup>의 결과 값을 추론할 수 있기 때문
  * 단, **블록이 본문인 함수<sup>Block body function</sup>은 명시해줘야한다.**

#### 변수<sup>Variable</sup>

```kotlin
// 변수를 선언할 때, 타입 지정을 생략할 수 있다. 타입 추론(Type inference) 덕분.
val question = "삶, 우주, 그리고 모든 것에 대한 궁극적인 질문"
val answer = 42

// 타입을 명시해도 된다
val answer2: Int = 42

// 초기화문을 사용하지 않고 변수를 선언할 수 있다. 다만, 타입을 반드시 지정해줘야함.
val answer3: Int 
answer3 = 42
```

##### 변경 가능한<sup>mutable</sup> 변수와 변경 불가능한<sup>immutable</sup> 변수

* `val` 키워드 - 변경 불가능한<sup>immutable</sup> 참조.
  * 초기화와 동시에 값을 넣고, 이후에 재대입 불가.
  * 자바의 `final` 키워드를 사용한 변수
* `var` 키워드 - 변경 가능한<sup>mutable</sup> 참조.
  * 재대입 가능. 자바의 일반 변수

##### 변수의 올바른 용법

* 기본적으로 모든 변수는 `val` 키워드를 사용

  * 추후 꼭 필요할 때만 `var` 키워드 사용
  * 사이드 이펙트를 최대한 줄이기 위함.

* `val` 변수는 반드시 정확히 한 번만 초기화되어야한다.

* `var` 변수를 초기화하면서 넣은 값과 같은 타입의 값만 새로 재대입 가능하다.

  ```kotlin
  var answer = 42
  answer = "error" // error: type mismatch
  ```

#### 문자열 템플릿

```kotlin
fun main(args: Array<String>) {
  val name = if (args.size > 0) args[0] else "Kotlin"
  println("Hello, $name!") // Hello, Kotlin!
  println("I have \$25") // I have $25
  println("Argument size: ${args.size}") // Argument size: 0
}
```

* 문자열 리터럴<sup>String literal</sup> 안에서 `$` 키워드를 변수앞에 붙이면 해당 변수를 출력할 수 있다.
* 달러 기호(`$`)를 표기하고 싶으면 앞에 역슬래시(`\`)를 붙인다.
* 변수명이 아닌 식<sup>Expression</sup>의 결과를 출력하고 싶다면 중괄호(`{`, `}`)를 사용한다.
