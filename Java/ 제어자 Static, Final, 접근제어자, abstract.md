## ✏️ 제어자(modifier)
- 클래스, 변수, 메서드의 선언부에 사용되어 부가적인 의미를 부여한다.
- 하나의 대상에 여러 개의 제어자를 조합해서 사용할 수 있으나, 접근제어자는 단 하나만 사용할 수 있다.

---


## ✏️ Static

>``정적``이라는 의미로, ``고정된``이란 뜻을 가짐.

- Static 키워드를 이용해 Static 변수와 Static 메소드를 만들 수 있다.
이 둘을 정적 멤버, 클래스 멤버라고도 한다.
- 정적 멤버는 인스턴스에 소속된 멤버가 아니라 클래스에 고정된 멤버다.

Static 영역에 할당된 메모리는 모든 객체가 공유하여, 하나의 멤버를 어디서든 참조할 수 있는 장점을 가집니다.
하지만 Garbage Collector의 관리 영역 밖에 존재하기 때문에 프로그램 종료시까지 메모리가 할당된 채로 존재합니다. 시스템 성능에 악영향을 줄 수도 있습니다.

### 📍 정적(Static) 멤버 선언

공용로 사용하고 싶은 필드나 메소드에 static 키워드를 붙여 선언합니다.
```java
static int num = 0; //타입 필드 = 초기값
public static void static_method(){} //static 리턴 타입 메소드 {}
```

### 📍 정적(Static) 필드 사용 예시

```java
lass Number{
    static int num = 0; //클래스 필드
    int num2 = 0; //인스턴스 필드
}

public class Static_ex {
	
    public static void main(String[] args) {
    	Number number1 = new Number(); //첫번째 number
    	Number number2 = new Number(); //두번쨰 number
    	
    	number1.num++; //클래스 필드 num을 1증가시킴
    	number1.num2++; //인스턴스 필드 num을 1증가시킴
    	System.out.println(number2.num); //두번째 number의 클래스 필드 출력
    	System.out.println(number2.num2); //두번째 number의 인스턴스 필드 출력
    }
}
```
>1<br>0

---

### 📍 정적(Static) 메소드 사용 예시

```java
class Name{
    static void print() { //클래스 메소드
	System.out.println("내 이름은 이하린입니다.");
    }

    void print2() { //인스턴스 메소드
	System.out.println("내 이름은 사밀이입니다.");
    }
}

public class Static_ex {
	
    public static void main(String[] args) {
        Name.print(); //인스턴스를 생성하지 않아도 호출이 가능
    	
        Name name = new Name(); //인스턴스 생성
        name.print2(); //인스턴스를 생성하여야만 호출이 가능
    }
}
```
>내 이름은 이하린입니다.
내 이름은 사밀이입니다.

---

## ✏️ Final

변수에 ``Final`` 을 붙이면 시간이 지나도 처음 정의된 상태가 변하지 않는것을 보장한다는 의미입니다.

```java
final String hello = "Hello world";
```

```java
final String hello = "Hello world";
hello = "See you around" // 에러 발생

```

### 📍 클래스 생성자에서 초기화
```java
class AAA {
    final String hello;
    AAA() {
        hello = "hello world";
    }
}
```

### 📍 final 클래스
```java
final class AAA {
    final String hello;
    AAA() {
        hello = "hello world";
    }
}
```

### 📍 final 메소드

```java
class AAA {
    final String hello = "hello world";

    final String getHello() {
        return hello;
    }
}
```

- final variables, arguments : 값이 변경되지 않도록 만든다
- final class : 클래스를 상속하지 못하도록 만든다
- final method : 메소드가 오버라이드되지 못하도록 만든다

---

## ✏️ Abstract(추상)
>abstract- '추상의' 또는 '미완성의' 의미를 가지고 있다.

- 메서드의 선언부만 작성하고 실제 수행 내용은 구현하지 않은 추상메서드를 선언하는데 사용한다.
- abstract 클래스
	- 클래스 내에 추상메서드가 선언되어 있음을 의미한다.
    - abstract 메서드- 선언부만 작성하고 구현부는 작성하지 않은 추상메서드임을 알린다.

---

## ✏️ 접근 제어자

| 접근 제어자 | 설명 |
|---|---|
|public|외부 클래스 어디서나 접근할 수 있다.|
|protected|같은 패키지 내부와 상속 관계의 클래스에서만 접근할 수 있고 그 외 클래스에서는 접근할 수 없다.|
|default| 같은 패키지 내부에서만 접근할 수 있다.|
|private|같은 클래스 내부에서만 접근할 수 있다.|