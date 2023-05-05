https://velog.io/@yachae1101/WIL-GDSC-OC-BE-STUDY-WEEK-4

4주차 WIL입니다.

## ✔️ 절차 지향 프로그래밍 vs 객체 지향 프로그래밍

### ▪️ 절차 지향 프로그래밍
`절차 지향 프로그래밍(Procedural Programming)`은 프로그램을 명령어들의 `연속적인 실행 흐름`으로 구성하는 프로그래밍 방식이다. 이 방식에서는 프로그램을 일련의 `절차`나 `함수`로 나누고, 이들 함수를 `순차적`으로 호출하여 실행한다.

`절차 지향 프로그래밍`에서는 코드가 실행되는 컴퓨터의 하드웨어적인 특성에 직접적으로 맞추어 작성된다. 이러한 특성으로 인해 절차 지향 프로그래밍은 하드웨어 제어 및 입출력 처리와 같은 `저수준 기능을 수행하는 데에 유리`하다.

### ▪️ 객체 지향 프로그래밍
`객체 지향 프로그래밍(Object-Oriented Programming, OOP)`은 `객체`를 중심으로 프로그래밍하는 방식이다. `객체`는 `속성(attribute)`과 `행위(behavior)`로 구성되며, 이를 `클래스(class)`라는 틀에 따라 정의한다. 객체는 클래스의 인스턴스(instance)로서, 클래스에서 정의한 속성과 행위를 가지게 된다.

`객체 지향 프로그래밍`에서는 코드의 `재사용성`과 `유지보수성`을 높이기 위해 `상속(inheritance)`, `다형성(polymorphism)`, `캡슐화(encapsulation)` 등의 개념을 활용한다. 문제를 객체로 분해하고, 객체 간의 관계를 설계함으로써 `유연하고 확장 가능한 소프트웨어`를 만드는 데에 적합하다.


## ✔️ JVM의 역할과 가비지컬렉션(GC)

### ▪️ JVM
`JVM(Java Virtual Machine)`은 자바 프로그램을 실행하기 위한 `가상 머신`이다. `JVM`은 `자바 언어`와 `바이트 코드`를 이해하고 `해석`하여 `실행`하는 역할을 한다. 이를 통해 자바는 `OS에 독립적인 특징`을 가지며, 한 번의 컴파일로 `여러 운영체제에서 실행 가능`한 이점을 가진다.

![](https://velog.velcdn.com/images/yachae1101/post/0795eaf2-f8b7-4b43-9519-b03979ba1160/image.png)

### ▪️ 가비지컬렉션(GC)
`가비지 컬렉션(Garbage Collection)`은 메모리 관리를 자동으로 해주는 기능으로, 더 이상 `사용하지 않는 메모리 영역(쓰레기 객체)`을 찾아서 `해제`시켜주는 작업을 말한다.

`Java`에서는 가비지 컬렉션 기능이 `JVM에 내장`되어 있어서, 개발자가 메모리 해제를 명시적으로 처리하지 않아도 `자동으로 해제`된다.

가비지 컬렉션이 수행되는 시점은 `JVM이 메모리 상태를 체크`해서, 더 이상 `사용되지 않는 객체를 확인`하고, 해당 객체가 차지하고 있는 `메모리를 해제`하는 작업을 진행한다.


## ✔️ JVM의 메소드, 힙, 스택 영역

- `메소드 영역 (Method Area 또는 Code Area)`
	- `클래스 정보`와 `static 변수`가 저장
	- 프로그램 실행 중 `변하지 않는 공유 데이터`가 저장
	- JVM이 시작될 때 생성되며, JVM이 종료될 때까지 유지

- `힙 영역 (Heap Area)`
	- `new` 연산자를 사용하여 `동적으로 생성된 객체와 배열`이 저장
	- `GC(Garbage Collector)`가 참조하지 않는 객체를 수거하여 메모리를 해제
	- JVM이 시작될 때 생성되며, JVM이 종료될 때까지 유지

- `스택 영역 (Stack Area)`
	- `지역 변수`와 `메소드 호출 정보`가 저장
	- `스택 프레임(Stack Frame)`이라는 단위로 저장
	- 메소드 호출 시 생성되며, 메소드가 종료되면 함께 소멸


## ✔️ “클래스는 붕어빵 틀이고 객체는 붕어빵이다.”

클래스와 객체의 관계를 비유한 것.
 
### ▪️ 클래스
`클래스`는 붕어빵을 만들기 위한 `붕어빵 틀`과 같은 것이다. 붕어빵 틀은 붕어빵을 만들기 위한 규격이나 기본적인 형태를 정의해 놓은 것이며, 클래스도 마찬가지로 객체를 만들기 위한 기본적인 `형태와 속성`, `메서드` 등을 `정의`해 놓은 것이다.

### ▪️ 객체
`객체`는 붕어빵 틀을 바탕으로 `만들어진 실제 붕어빵`이라고 생각할 수 있다. 붕어빵 틀을 사용하여 여러 개의 붕어빵을 찍어내듯이, 클래스를 사용하여 `여러 개의 객체`를 생성할 수 있다. 각 객체는 `서로 다른 속성 값`을 가질 수 있으며, `각자 독립적으로 동작`할 수 있다.