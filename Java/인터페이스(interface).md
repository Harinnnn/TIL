## ✏️ 인터페이스(interface)

**인터페이스(interface)** 란 객체를 어떻게 구성해야 하는지 정리한 설계도이다.

- 극단적으로 **동일한 목적** 하에 **동일한 기능을 수행** 하게끔 강제한다.
- 자바에서는 인터페이스를 통해 **다중 상속**을 지원한다. (클래스를 통한 다중상속은 지원하지 x)
- 추상 클래스와 달리 인터페이스는 오로지 **추상 메소드**와 **상수**만을 포함할 수 있다.

---

## 📍 인터페이스의 장점

1. 대규모 프로젝트 개발 시 일관되고 정형화된 개발을 위한 표준화가 가능합니다. (정해진 틀 안에서 일관된 협업이 가능하다.)

2. 클래스의 작성과 인터페이스의 구현을 동시에 진행할 수 있으므로, 개발 시간을 단축할 수 있습니다.

---

## 💻 인터페이스의 선언

```java
접근제어자 interface 인터페이스이름 {
    public static final 타입 상수이름 = 값;
    ...
    public abstract 메소드이름(매개변수목록);
    ...
}
```

- 인터페이스의 모든 필드는 ``public static final``이어야 하며, 모든 메소드는 ``public abstract``이어야 한다.

---

## 💻 인터페이스의 구현

인터페이스는 자신이 직접 인스턴스를 생성할 수 없습니다. 따라서 인터페이스가 포함하고 있는 추상 메소드를 구현해 줄 클래스를 작성해야만 합니다.

```java
class 클래스이름 implements 인터페이스이름 { ... }
```


---



## 📍 인터페이스의 다중 상속

아래 예제에서 Cat 클래스와 Dog 클래스는 각각 Animal과 Pet이라는 두 개의 인터페이스를 동시에 구현하고 있습니다.

```java
interface Animal { public abstract void cry(); }

interface Pet { public abstract void play(); }

 

class Cat implements Animal, Pet {

    public void cry() {

        System.out.println("냐옹");

    }

    public void play() {

        System.out.println("쥐 잡기 놀이");

    }

}

 

class Dog implements Animal, Pet {

    public void cry() {

        System.out.println("멍멍");

    }

    public void play() {

        System.out.println("산책");

    }

}
```

---

## ✏️ default 메소드

인터페이스는 일반적으로 하나 혹은 여러 개의 구현 클래스들을 가지고 있는데, 만약 인터페이스에 새로운 메소드가 추가된다면 그 추가된 수 만큼 구현 클래스들은 강제적으로 구현을 해야만하는 문제점이 있다.

인터페이스의 default 메소드는 이 이슈를 효율적으로 해결할 수 있습니다. 그것들은 인터페이스에 새로운 메소드가 추가되면 자동적으로 구현 클래스에서도 사용할 수 있게 됩니다. 즉, 구현 클래스들을 수정할 필요가 없어집니다.

이렇게 구현 클래스를 수정하지 않고 깔끔하게 하위 호환(backward compatibility)이 가능하게 합니다.

- 디폴트 메서드는 인스턴스 메서드이다.(인터페이스 원칙을 예외적으로 위반한다.)

```java
    public interface Calculator {
        public int plus(int i, int j);
        public int multiple(int i, int j);
        default int exec(int i, int j){
        //default로 선언해, 메소드를 구현할 수 있다.
            return i + j;
        }
    }

    //Calculator인터페이스를 구현한 MyCalculator클래스
    public class MyCalculator implements Calculator {

        @Override
        public int plus(int i, int j) {
            return i + j;
        }

        @Override
        public int multiple(int i, int j) {
            return i * j;
        }
    }

    public class MyCalculatorExam {
        public static void main(String[] args){
            Calculator cal = new MyCalculator();
            int value = cal.exec(5, 10);
            System.out.println(value);
        }
    }
    
```

인터페이스가 default키워드로 선언되면 메소드가 구현될 수 있다. 또한 이를 구현하는 클래스는 default 메소드를 오버라이딩 할 수 있다.
