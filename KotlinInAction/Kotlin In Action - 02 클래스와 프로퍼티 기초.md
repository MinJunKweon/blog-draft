### 클래스<sup>Class</sup>와 프로퍼티<sup>Property</sup>

* 자바로 작성한 `Person` 클래스

```java
public class Person {
  private fianl String name; // 'name'이라는 Property
  
  public Person(String name) {
    this.name = name;
  }
  
  public String getName() {
    return name;
  }
}
```

* 코틀린으로 변환한 `Person` 클래스

```kotlin
class Person(val name: String)
```

* 코드가 없이 데이터만 저장하는 클래스를 **값 객체<sup>value object</sup>**라고 부른다.
* 코틀린은 가시성 변경자<sup>Visibility modifier</sup>가 `public`이므로 생략해도 된다.

#### 프로퍼티<sup>Property</sup>

> 자바의 멤버 필드<sup>Field</sup>와 접근자<sup>Accessor</sup>를 한데 묶어 코틀린에서는 **프로퍼티<sup>Property</sup>**라고 부른다.

* 클래스의 목적은 데이터를 캡슐화<sup>encapsulate</sup>하고 데이터를 다루는 코드를 한 주체 아래에 가두는 것
* 자바에서는 데이터를 필드<sup>Field</sup>에 저장, 멤버 필드의 가시성은 보통 `private`
* `private` 데이터를 접근하기 위해 **접근자 메소드<sup>accessor method</sup>**를 사용
  * Getter, Setter 등

* `val` 키워드를 사용하면 **읽기 전용(Getter)**, `var` 키워드를 사용하면 **변경 가능(Getter, Setter)**
  * 기본 접근자 메소드를 지원하여 위 코틀린 클래스는 위 자바 클래스와 같이 구현된다.
* 프로퍼티를 **뒷받침하는 필드<sup>Backing fleld</sup>**는 커스텀 Getter를 통해 구현할 수 있다.
  * 다른 프로퍼티의 값들로부터 계산된 값을 도출하는 필드가 필요한 경우 커스텀 Getter를 정의할 수 있다.

##### 커스텀 접근자<sup>Custom accessor</sup>

```kotlin
class Rectangle(val height: Int, val width: Int) {
  val isSquare: Boolean
  	get() { // 프로퍼티 Getter
      return height == width
    }
}

val rectangle = Rectangle(41, 43)
println(rectangle.isSquare) // false
```

#### 디렉토리<sup>Directory</sup>와 패키지<sup>Package</sup>

* 코틀린 파일의 맨 앞에 `package` 문을 사용할 수 있다.
  * 같은 파일 안에 모든 선언*(클래스, 함수, 프로퍼티 등)*이 모두 해당 패키지에 들어간다.
* 다른 패키지에 정의된 선언을 사용하려면 `import`를 해야한다.
  * 자바와 마찬가지로 `import` 문은 맨앞에 와야한다.
* 클래스 내부에 정의되지 않은 함수 또한 `import` 문을 통해 임포트 할 수 있다.
* 자바에서는 **패키지명과 디렉토리를 일치시켜야한다.** 하지만, 코틀린에서는 **어느 디렉토리에 파일을 위치시키든 관계 없다.**
  * 하지만, 자바 클래스를 코틀린 클래스로 마이그레이션<sup>Migration</sup>할 때 문제가 생길 수 있다.
