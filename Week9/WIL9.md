https://velog.io/@yachae1101/WIL-GDSC-OC-BE-STUDY-WEEK-9

9주차 WIL입니다.

## ✔️ Lambda❔
**람다**란? 한 마디로 **코드 블록**이다. 기존의 코드 블록은 반드시 메서드 내에 존재해야 했고, 이 메서드는 클래스 내에 존재해야 했다. 이러한 불편함을 해결하기 위해, 코드 블록인 **람다를 메서드의 인자나 반환값으로 바로 사용할 수 있게** 만들었다. 즉, **코드 블록을 변수처럼 사용**할 수 있다는 것이다.

### ▪️ 기존 방식의 코드 블록 사용

```java
public class NotUsingLambda {
	public static void main(String[] args) {
    
    	MyTest = mt = new MyTest();
        
        Runnable r = mt;
        r.run();
    }
}

// 코드 블럭의 사용을 위해, 1. 클래스 생성
class MyTest implements Runnable {
	// 코드 블럭의 사용을 위해, 2. 메서드 생성
	public void run() {
    	// 사용하고 싶은 코드 블럭!! //
    	System.out.println("Hello Lambda!");
    }
}
```

### ▪️ 람다 방식의 코드 블록 사용

```java
public class UsingLambda {
	public static void main(String[] args) {
    
        Runnable r = () -> {
        	// 사용하고 싶은 코드 블럭!! //
        	System.out.println("Hello Lambda!");
        };
        
        r.run();
    }
}
```


## ✔️ 함수형 인터페이스
위의 코드 예시에서, `Runnable` 인터페이스를 사용하는 코드를 람다식으로 변경했다. `Runnable` 인터페이스는 `run()`이라는 추상 메서드 하나만을 가지는데, 이렇듯 **단 하나의 추상 메서드를 갖는 인터페이스**를 **함수형 인터페이스**라 한다. 이런 **함수형 인터페이스만**을 **람다식으로 변경**할 수 있다. **사용자 정의 함수형 인터페이스**를 직접 정의하여 사용할 수도 있다.

```java
public class UsingLambda {
	public static void main(String[] args) {
    
    	MyFunctionalInterface mfi = (int a) -> { return a * a; };
    
        int b = mfi.runSomething(5);
        System.out.println(b);
    }
}

@FunctionalInterface
interface MyFunctionalInterface {
	public abstract int runSomething(int count);
}
```



## ✔️ 컬렉션 스트림

람다는 다양한 용도로 사용되지만, 그 중 **컬렉션 스트림**을 위한 기능에 초점이 맞춰져 있다. 
스트림과 람다를 활용한 코드를 살펴보자.

### ▪️ 기존 방식의 코드
```java
// 미성년자 출입 제한 코드 by 기존 방식
public class BlockMinor {
	public static void main(String[] args) {
    
    	Integer[] ages = { 20, 25, 18, 27, 30, 21, 17, 19, 34, 28 };
        
        for (int i=0 ; i<ages.length ; i++) {
        	if (ages[i] < 20) {
         		System.out.format("Age %d!! Can't enter!!\n", ages[i]);   	
            }
        }
    }
}
```


### ▪️ 스트림과 람다를 활용한 코드
```java
// 미성년자 출입 제한 코드 using 스트림 & 람다
public class BlockMinor {
	public static void main(String[] args) {
    
    	Integer[] ages = { 20, 25, 18, 27, 30, 21, 17, 19, 34, 28 };
        
        // ages 배열의 stream 을 가져옴
        Arrays.stream(ages)
        	// age의 값이 20 미만이면 true를 반환하는 람다식을 filter()의 인자로 
            // 20세 미만인 경우를 선별(filter)해 주세요.
        	.filter(age -> age < 20)
            // 선별된 각 요소에 대해 입장이 불가하다고 해 주세요.
            .forEach(age -> System.out.format("Age %d!! Can't enter!!\n", age));
    }
}
```
스트림과 람다를 활용하여, 프로그램의 요구를 선언적으로 코딩할 수 있게 되었다. 요구사항 내용 자체가 그대로 코드로 구현되어, 해당 코드가 무슨 일을 하는지 한눈에 파악 할 수 있다는 장점이 있다.



## ✔️ Optional❔
개발에서 가장 흔히 발생하는 예외 중 하나가, null 값에 접근하려 할 때 발생하는 NPE(NullPointerException)이다. 이 NPE를 방지하기 위해서는, 코드 중간에 null 값을 체크하는 조건절이 들어가야 하기 때문에, 코드가 길어지고 가독성이 떨어진다. 이 NPE를 방지하고 처리를 도와주는 클래스가 `Optional` 이다.

### ▪️ 기존 방식의 코드

```java
// 랜덤 house를 받아서, house의 주인의 이름을 출력하는 코드
public class NameOfOwner {
	public static void main(String[] args) {
    
    	House house = getRandomHouse();
        
        // 1. house 가 null이 아닌지?
        // 2. house Owner 가 null이 아닌지?
        // 3. house Owner의 Name 이 null이 아닌지?
		if (house != null && house.getOwner() != null && house.getOwner().getName() != null) {
		    System.out.println("House owner : " + house.getOwner().getName());
		}
	}
}
```

### ▪️ Optional을 활용한 코드

```java
// 랜덤 house를 받아서, house의 주인의 이름을 출력하는 코드 using Optional & 람다
public class NameOfOwner {
	public static void main(String[] args) {
    
    	House house = getRandomHouse();
        
        Optional.of(house)
        	.map(House::getOwner)
        	.map(House::getName)
        	.ifPresent(n -> System.out.println("House owner : " + n));
	}
}
```
Optional과 람다를 활용하여, null 값에 대한 처리를 더욱 깔끔하게 할 수 있다. 이를 통해, 코드의 가독성을 향상시킬 수 있다.