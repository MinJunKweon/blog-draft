###  확장함수<sup>Extension function</sup>란?

> 어떤 클래스의 멤버 메소드인 것처럼 호출할 수 있지만 그 클래스의 밖에 선언된 함수

* 하나의 클래스에 추가적인 메소드를 구현하고 싶을 때, 해당 클래스를 상속받은 새로운 클래스 없이 구현할 수 있는 기능
* 이를 통해 새로운 클래스를 만들 필요도 없어지고, 코드가 더욱 직관적이다.

### 예시

* `String` 객체에 추가적인 기능으로 **마지막 글자를 반환하는 `lastChar()` 메소드를 구현하려고 한다. **

#### 코틀린에서 구현

```kotlin
// StringUtils.kt
fun String.lastChar(): Char = this.get(this.length - 1)

// Application.kt
println("Hello World".lastChar()) // d
```

#### 자바에서 구현

```java
// StringUtils.java
public class StringUtils {
  public static Char lastChar(String str) {
    return str.get(str.length - 1);
  }
}

// Application.java
public class Application() {
  public static void main(String[] args) {
    System.out.println(StringUtils.lastChar("Hello World"));
  }
}
```



#### 설명

* 위 예시처럼 확장함수<sup>Extension function</sup>를 사용하면 **원래 해당 클래스에 있었던 메소드처럼 동작**시킬 수 있다.
  * 확장함수 내부에서도 마찬가지로 하나의 인스턴스의 메소드인 것처럼 `this` 키워드가 수신 객체<sup>Receiver object</sup>를 의미한다. 위 코드에서는 **"Hello World"의 값을 가진 String 객체**가 수신 객체<sup>Receiver object</sup>다.
* **실제로 코틀린 코드는 내부적으로는 위 자바 코드와 같이 정적 메소드<sup>Static Method</sup> 형태로 변환된다.**
  * 따라서, 자바 코드에서도 코틀린의 확장 함수를 사용할 수 있게 된다. *(호출형태는 일반 정적 메소드를 부르는 것처럼 생기겠지만)*
  * **이 개념을 확실히 알고 있으면 확장 함수를 잘못 사용할 확률이 매우 낮다.**

**자바에서 확장 함수<sup>Extension function</sup> 호출**

```java
// StringUtil.kt 파일에 선언되어 있는 경우 StringUtilKt에서 호출 
char c = StringUtilKt.lastchar()
```



### 확장함수 주의사항

* 확장 함수 또한 임포트를 정확히 해야 사용이 가능하다.
  * 만약 아래와 같이 `strings` 패키지로 정의된 메소드들을 사용하기 위해서는 `import` 문을 통해 패키지를 임포트 해야한다.
* Asterisk(`*`)를 사용해서 임포트를 해도 제대로 동작한다.

```kotlin
// StringUtils.kt
package strings
fun String.lastChar() = get(length - 1) // this는 생략 가능하다. (또한, this는 수신객체를 의미)

// OtherFile.kt
import strings.lastChar // import strings.* 또한 제대로 동작한다.
println("Hello World".lastChar()) // d
```

* 오버라이드<sup>Override</sup> 할 수 없다.
  * 확장 함수는 **클래스의 밖에 선언된다.** 따라서, 오버라이드할 수 없게되는 것이다.

#### 확장 함수<sup>Extension function</sup>는 **정적 타입에 의해 호출이 결정된다.**

* 즉, 부모 클래스 타입의 변수에 자식 클래스 객체가 들어가있더라도 부모 클래스의 확장 함수가 호출되는 것이다. 
* 예시 코드는 다음과 같다.

```kotlin
open class View { // open 키워드는 상속 및 오버라이딩이 가능하게 해주는 키워드. 나중에 자세히 설명함.
  open fun click() = println("View clicked")
}
class Button: View() {
  override fun clik() = println("Button clicked")
}

fun View.showOff() = println("I'm a view!")
fun Button.showOff() = println("I'm a button!")

val view: View = Button() // 부모 클래스(View) 변수 안에 자식 클래스(Button) 객체
view.showOff()
// I'm a view!
view.click()
// Button clicked
```

#### 왜 그럴까?

* 앞서 알아봤듯이 확장 함수<sup>Extension function</sup>는 정적 메소드<sup>Static Method</sup>로 변환된다.
  * 위 확장 함수들을 자바 코드로 표현하면 다음과 같다

```java
public class ExtensionUtils {
  
  public static void showOff(View view) { // View.showOff()
    System.out.println("I'm a view!");
  }
  
  public static void showOff(Button button) { // Button.showOff()
    System.out.println("I'm a button!");
  }
}
```

* 따라서, 실행시점에서 `view` 변수의 타입이 `View`이므로, `ExtensionUtils.showOff(view)`를 했을 때 `View.showOff()` 에 상응하는 메소드가 실행되는 것이다.



### 확장 프로퍼티<sup>Extension property</sup>

> 기존 클래스 객체에 대한 프로퍼티 형식의 구문으로 사용할 수 있는 API

```kotlin
val String.lastChar: Char
    get() = get(length - 1)
```

* 상태를 저장할 적절한 방법이 없기 때문에 실제로는 확장 프로퍼티에서는 **아무 상태도 가질 수 없다.**
  * 마치 원래부터 객체에 있던 필드인 것처럼 값을 대입하는 것이 불가능하다.
  * 하지만, Setter를 통해 기존에 가지고 있는 프로퍼티를 수정하는 것은 가능하다.

