https://velog.io/@yachae1101/WIL-GDSC-OC-BE-STUDY-WEEK-8

8주차 WIL입니다.

## ✔️ IoC와 프레임워크, 라이브러리

### ▪️ 프레임워크 vs 라이브러리

`라이브러리`란, 개발에 필요한 것들을 미리 구현해 놓은 도구로, 미리 작성된 메서드, 클래스, 자료형, 값 등의 집합이다.
예를 들어, C++의 STL(Standard Template Library)를 통해, vector와 같은 컨테이너, sort와 같은 함수를 직접 구현하지 않고 손쉽게 가져다 사용할 수 있다.

`프레임워크` 또한, 필요한 것들을 미리 구현해 놓은 도구이다. 하지만, 프레임워크는 '제어할 수 있는 권한'을 가진다는 점에서 `라이브러리`와 다르다.

>`라이브러리` : 도서관(Library)에서 읽고 싶은 책만 골라 읽는 것과 같다.
`프레임워크` : 학교가 만든 커리큘럼 틀(Frame)을 따라가는 것과 같다.

`라이브러리`를 사용할 때는, 개발자가 직접 외부의 라이브러리 일부분을 가져와 프로그램에 활용하며 '직접 제어'한다.
`프레임워크`를 사용한다면, 역으로 개발자가 작성한 코드가 프레임워크의 일부분으로 동작하게 되어, 전체적인 흐름에 대한 '제어할 수 있는 권한을 프레임워크에 위임'하게 된다. 
이와 같이, 개발자가 작성한 객체나 메서드의 제어를 외부에 위임하는 것을 `IoC`(Inversion of Control / 제어의 역전)이라 한다.

### ▪️ IoC / DI
`IoC`를 실현하기 위해 필요로 하는 것이 `DI`(Dependency Injetion / 의존성 주입)이다.
예를 들어, `사람` 클래스가, `심장` 클래스에 **의존**한다면, 두 클래스는 **같은 생명 주기**를 가지게 된다. 따라서 프레임워크에 의해 클래스의 생명주기가 제어되는 것이 아니라, 이미 결합된 생명주기를 가지게 되어, IoC가 실현되지 못한다.
따라서, **의존성 주입(DI)**을 통해 각체간의 결합을 느슨하게 만들 필요가 있다.


## ✔️ 생성자를 통한 의존성 주입 vs @Autowired
```java
public class Car {
	Tire tire;
    
    public Car() {
    	// Car 에서 내부적으로 Tire 생산
        // new를 실행하는 Car 와 Tire 사이에서, Car 가 Tire 에 의존한다  
    	tire = new KoreaTire();
    }
    
    public String getTireBrand() {
    	return "장착된 타이어 : " + tire.getBrand();
    }
}
```
위의 `Car` 클래스는, 생성자에서 내부적으로 `new`를 사용하여 `KoreaTire`를 생성하고 있으므로, `Car` 클래스가 `KoreaTire` 클래스에 의존한다.
(+) `KoreaTier` 클래스는 `Tire` Interface를 구현한 클래스이다.

위 코드를 두가지 방법(생성자를 통한 vs @Autowired)을 통해, 의존성을 주입하도록 바꾸어보자.

### ▪️ 생성자를 통한 의존성 주입
기존의 코드처럼 Car 내부에서 타이어를 직접 생산하는 것이 아니라, **외부에서** 생산된 타이어를 Car에 장착시키는 방식, **주입**하는 방식으로 바꾸어보자.

```java
public class Car {
	Tire tire;
    
    public Car(Tire tire) {
    	// 생성자에 인자를 추가하므로써,
        // 직접적으로 의존하는 것이 아니라, 의존성을 주입받는 것으로 변경되었다.
    	this.tire = tire;
    }
    
    public String getTireBrand() {
    	return "장착된 타이어 : " + tire.getBrand();
    }
}
```
**의존성 주입**을 적용하였기 때문에, 그저 **Tire Interface**를 구현한 어떤 객체가 들어오더라도, 정상적으로 Car 클래스가 작동하게 된다. 이로써, 특정한 Tire에 의존하지 않고, 확장성 있는 Car 클래스가 만들어졌다.


### ▪️ @Autowired

```java
import org.springframework.beans.factory.annotation.Autowired;

public class Car {
	// @Autowired 을 통해 Car의 속성을 자동으로 엮어준다.
	@Autowired
	Tire tire;
    
    /*
    // @Autowired 에 의해 대체된 코드,,
    public void setTire(Tire tire) {
    	this.tire = tire;
    }
    */
    
    public String getTireBrand() {
    	return "장착된 타이어 : " + tire.getBrand();
    }
}
```

`@Autowired`는, 스프링 설정 파일을 보고, 자동으로 속성의 설정자 메서드 `setTire()`의 역할을 해주겠다는 의미이다. 따라서 자동으로 의존성 주입이 된 것이다.

스프링 설정파일에서 `Tire` 에 해당하는 **type**을 구현한 빈이 있는지 찾는다. 빈이 하나라면 해당 **빈을 속성에 할당**해준다.
만약 빈이 두개 이상이라면, 그 중 id가 일치하는 **빈을 찾아 속성에 할당**한다.


## ✔️ AOP (Aspect-Oriented Programming)

### ▪️ AOP❔
DI가 의존성(new)에 대한 주입이라면, `AOP`는 **로직(code)의 주입**이라고 할 수 있다.
프로그램에서 다수의 모듈에 공통적으로 나타나는 부분들이 존재하는데, 이것을 **횡단 관심사**라고 한다. 이렇게 반복적으로 등장하는 코드 기능을 따로 분리해 두고, 이 코드(로직)을 주입하여 사용하는 방법이다.

예를 들어, 학생과 아르바이트생의 아침을 묘사해보자.

- 학생의 아침
일어난다.
씻고 나갈 준비를 한다.
**학교에 간다.**

- 아르바이트생의 아침
일어난다.
씻고 나갈 준비를 한다.
**편의점에 간다.**

위의 두 의사 코드에서, 중복되는 부분을 **횡단 관심사**라고 할 수 있고, 진하게 표시된 부분(학교에, 편의점에 간다.)을 **핵심 관심사**라고 할 수 있다.


```java
public class Student {
	// 학생의 아침
	public void runSomething() {
    	// 횡단 관심사
    	System.out.println("일어난다.");
        System.out.println("씻고 나갈 준비를 한다.");
        // 핵심 관심사
        System.out.println("학교에 간다.");
    }
}

public class PartTimer {
	// 아르바이트생의 아침
	public void runSomething() {
    	// 횡단 관심사
    	System.out.println("일어난다.");
        System.out.println("씻고 나갈 준비를 한다.");
        // 핵심 관심사
        System.out.println("편의점에 간다.");
    }
}
```

**횡단 관심사**를 AOP를 적용하여 분리시켜보자.

```java
public interface Person {
	void runSomething();
}

public class Student implements Person {
	// 학생의 아침
	public void runSomething() {
        // 핵심 관심사
        System.out.println("학교에 간다.");
    }
}

public class PartTimer implements Person {
	// 아르바이트생의 아침
	public void runSomething() {
        // 핵심 관심사
        System.out.println("편의점에 간다.");
    }
}


@Aspect
public class MyAspect {
	@Before("execution(* runSomething())")
    public void before(JoinPoint joinPoint){
    	// 횡단 관심사
    	System.out.println("일어난다.");
        System.out.println("씻고 나갈 준비를 한다.");
    }
}
```

`@Aspect`는 이 클래스를 AOP에서 사용하겠다는 의미이다.
`@Before`은 대상 메서드 실행 전에, 이 **before 메서드**를 실행하겠다는 의미이다.
@Before로 만들어진 **before 메서드**(횡단 관심사 로직)가 런타임에 runSomething()에 **주입**된다.

`Student`와 `PartTimer` 클래스 코드에는 횡단 관심사는 사라지고, 오직 **핵심 관심사**만 남게 되어, 핵심이 무엇인지 단번에 파악할 수 있는 코드가 되었다.