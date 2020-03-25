### 선택 표현과 처리: enum과 when

#### enum 클래스 정의

```kotlin
enum class Color {
  RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET
}

enum class Color2(
	val r: Int, val g: Int, val b: Int
) {
  RED(255, 0, 0), ORANGE(255, 165, 0),
  YELLOW(255, 255, 0), GREEN(0, 255, 0), BLUE(0, 0, 255),
  INDIGO(75, 0, 130), VIOLET(238, 130, 238);
  
  fun rgb() = (r * 256 + g) * 256 + b
}
```

* `enum` 키워드를 통해 enum 클래스를 선언할 수 있다.
* `enum`은 **소프트 키워드<sup>Soft keyword</sup>**의 종류이다.
  * `class` 키워드 앞에 붙으면 enum 클래스로 선언되지만, 그 외의 경우 이름에 사용할 수 있다.
  * 반면, `class`는 키워드
* 자바와 마찬가지로 프로퍼티나 메소드를 선언할 수 있다.
  * 메소드를 선언하는 경우 enum 상수 목록 선언 끝에 `;`를 붙인다.

#### when으로 enum 클래스 처리

```kotlin
fun getMnemonic(color: Color) =
	when (color) {
    Color.RED -> "Richard"
    Color.ORANGE -> "Of"
    Color.YELLOW -> "York"
    Color.GREEN -> "Gave"
    Color.BLUE -> "Battle"
    Color.INDIGO -> "In"
    Color.VIOLET -> "Vain"
  }

println(getMnemonic(Color.BLUE)) // Battle

fun getWarmth(color: Color) =
	when(color) {
  	Color.RED, Color.ORANGE, Color.YELLOW -> "warm"
    Color.GREEN -> "neutral"
    Color.BLUE, Color.INDIGO, Color.VIOLET -> "cold"
	}
println(Color.RED) // warm
println(Color.YELLOW) // warm
```

* 코틀린에서는 `when` 식<sup>Expression</sup>을 자바의`switch` 문 대신 사용한다.
* 각 분기의 끝에 break를 넣지 않아도 된다.
* 여러 값을 매칭시키기 위해서는 `,` 를 사용해서 구분한다.

#### when 분기 조건에 여러 다른 객체 사용하기

```kotlin
fun minx(c1: Color, c2: Color) =
	when (setOf(c1, c2)) {
    setOf(RED, YELLOW) -> ORANGE
    setOf(YELLOW, BLUE) -> GREEN
    setOf(BLUE, VIOLET) -> INDIGO
    else -> throw Exception("Dirty color")
  }
```

* 코틀린 표준 라이브러리에 `setOf()`는 파라미터로 받은 객체들을 포함하는 집합인 `Set` 객체로 만드는 함수
* `else`를 통해 예외를 처리할 수 있다.

##### Tip) 코틀린 1.3부터는 when 대상<sup>Target</sup>을 변수에 대입할 수 있다.

```kotlin
// 코틀린 1.3 이전
fun Request.getBody(): ResponseBody { // Request의 확장 함수(Extension function).
  val response = executeRequest()
	return when (response) {
    is Success -> response.body
    is HttpError -> throw HttpException(response.status)
  }
}

// 코틀린 1.3 이후
fun Request.getBody() = // Request의 확장 함수(Extension function). 나중에 설명합니다.
	when (val response = executeRequest()) {
    is Success -> response.body
    is HttpError -> throw HttpException(response.status)
  }
```

* `when` 괄호 안에서 변수를 대입할 수 있다.
  * 밖의 네임스페이스가 더러워지는 일을 줄일 수 있다.



