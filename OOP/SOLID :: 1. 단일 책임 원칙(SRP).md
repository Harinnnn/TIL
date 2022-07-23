이번 글에서는 객체지향의 5대 원칙 중, ``단일 책임 원칙(SRP)``에 대해 알아봅니다!

다섯가지 원칙 **SOLID** 는 아래와 같습니다.

>1. **단일 책임 원칙** (Single Responsibility principle)
>2. **개방 폐쇄 원칙** (Open Close Principle)
>3. **리스코프 치환 원칙** (Liscov Substitution Principle)
>4. **인터페이스 분리 원칙** (Interface Sergregation Principle)
>5. **의존성 역전 원칙** (Dependency Inversion Principle)

<br>

---

## ✅ 단일 책임 원칙(SRP)
``Single Responsibility Principle``

> _**"어떤 클래스를 변경 해야 하는 이유는 오직 하나뿐 이어야 한다"**_
	- 로버트 C 마틴 -

<br>

- 단일 책임 원칙이란 **하나의 객체는 반드시 하나의 기능만을 수행하는 책임을 갖는다**는 원칙입니다. 이는 **클래스를 변경하는 이유는 오직 하나뿐이어야 한다**는 것과 같은 의미입니다.

객체가 담당하는 동작, 즉 책임이 많아질 수록 그 객체의 변경에 따른 영향도의 양과 범위가 매우 커지게 됩니다!

<br>

💻 하지만 SRP를 코드에 적용하면,

- 책임 영역이 확실해져 한 책임의 변경에서 다른 책임의 변경의 연쇄작용에서 자유로울 수 있습니다. 즉, 코드의 의존성과 결합도를 줄입니다.


단일 책임 원칙은 특정 객체의 책임 의존성 과중을 지양하기 위한 중요하고 기본적인 원칙입니다.

---

<br>

## 🤓 코드로 보는 단일 책임 원칙

간단한 예제 코드를 통해 SRP를 알아보겠습니다.

<br>

### 🎐 SRP를 위반한 코드

다음의 코드는 단일 책임 원칙을 위반하고 있습니다.

```java
public class Animal {

    private String animal;

    public void setAnimal(String animal) {
        this.animal = animal;
    }

    public void cry () {

        if(animal == "Dog") { // 강아지
            System.out.println("bark!");
        }
        else if(animal == "Cat") { // 고양이
            System.out.println("meow..");
        }
    }

}
```
다음의 Animal 클래스에서는 동물의 울음소리를 출력하는 cry() 메서드를 구현하고 있습니다. cry() 메서드는 Animal의 값이 "Cat"이면 고양이 울음소리를, "Dog"면 강아지 울음 소리를 출력합니다. 즉, 두 기능이 분리되어 있지 않고 **하나의 메서드가 두 기능을 모두 가지고 있으므로 단일 책임 원칙을 위반하고 있습니다.**

---

### 🎐 SRP를 적용한 코드

다음 코드에서는 단일 책임 원칙 위반 문제를 해결하기 위해 추상 클래스를 만들어 각각의 하위 클래스에서 메서드를 상속 받아 사용하고 있습니다.


```java
abstract class Animal {
    abstract void cry();
}

class Dog extends Animal {
    @Override
    void cry() {
        System.out.println("bark!!!");
    }
}

class Cat extends Animal {
    @Override
    void cry() {
        System.out.println("Meow...");
    }
}

```

위의 코드에서는 공통기능인 추상 메서드 cry()를 가진 추상 클래스 Animal을 만들었습니다.

그리고 각각의 Dog, Cat 클래스를 만들어 Animal을 상속 받아 각자의 클래스에 자신의 울음소리만을 구현했습니다. 즉, 하나의 클래스에 하나의 기능을 가지고 있는 것입니다.

---

### ⭕️ 정리! 단일 책임 원칙 (SRP)
>작성된 클래스는 하나의 기능만을 가지며, 클래스가 제공하는 모든 서비스는 그 하나의 책임을 수행하는 데 집중되어 있어야 한다.

