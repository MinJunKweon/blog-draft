### 3중 따옴표 문자열<sup>Triple-quoted strings</sup>

* 코틀린에서는 따옴표(`"`)를 3번 사용하는 문자열을 만들 수 있다. 마치 Python과 같다.

```kotlin
val tripleQuotedString = """
												.Hello World!!
												.It's a triple-quoted string!
												"""

println(tripleQuotedString)
//
//												.Hello World!!
//												.It's a triple-quoted string!
//												
```

### 특징

* 여러 줄의 문자열을 간편하게 만들 수 있다

  * 자바에서 처럼 각 줄을 `+` 연산자를 통해 연결<sup>concatenate</sup>할 필요가 없이 한번에 처리 가능하다.

* **이스케이프 문자를 사용할 수 없다.**

  * 보이는대로 출력되기 때문에 직관적일 수 있지만 `$`를 표기하기 위해서는 `${'$'}`를 사용해서 출력해야한다.
  * `$` 뒤에 오는 이름이 변수명으로 취급되기 때문

* 문자열이 그대로 표현되기 때문에 들여쓰기<sup>Indentation</sup>이 전부 그대로 표현된다.

  * 따라서, 특별한 문자(ex. `.`)를 맨앞에 두고 `trimMargin()` 메소드를 사용해서 들여쓰기를 모두 제거한다.

    * ```kotlin
      println(tripleQuotedString.trimMargin("."))
      //
      // Hello World!!
      // It's a triple-qouted string!
      //
      ```

