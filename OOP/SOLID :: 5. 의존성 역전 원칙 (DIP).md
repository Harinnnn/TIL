이번 글에서는 객체지향의 5대 원칙 중, ``의존성 역전 원칙(DIP)``에 대해 알아봅니다!

다섯가지 원칙 **SOLID** 는 아래와 같습니다.

>1. **단일 책임 원칙** (Single Responsibility principle)
>2. **개방 폐쇄 원칙** (Open Closed Principle)
>3. **리스코프 치환 원칙** (Liscov Substitution Principle)
>4. **인터페이스 분리 원칙** (Interface Sergregation Principle)
>5. **의존성 역전 원칙** (Dependency Inversion Principle)

---


## ✅ 의존성 역전 원칙 (DIP)

``Dependency Injectoin Principle``

의존관계 역전 원칙이란 **"추상화에 의존해야지, 구체화에 의존하면 안 된다"** 는 원칙입니다.

---

<br>

이게 도대체 무슨 말인지 더 자세히 알아보겠습니다.

다시 말하자면, **고수준 모듈은 저수준 모듈의 구현에 의존해서는 안 됩니다.
대신 저수준 모듈이 고수준 모듈에서 정의한 ``추상 타입``에 의존해야 합니다.**

<br>

![](https://velog.velcdn.com/images/harinnnnn/post/5217fd08-c236-414a-812f-1b5977cda612/image.png)

<br>

> 🤔 고수준 모듈은 뭐고, 저수준 모듈은 또 뭘까?
>- **고수준 모듈** : 어떤 의미 있는 단일 기능을 제공하는 모듈 (interface, 추상 클래스)
>- **저수준 모듈** : 고수준 모듈의 기능을 구현하기 위해 필요한 하위 기능의 실제 구현 (메인클래스, 객체)

<br>

사실 고수준 클래스가 저수준 클래스를 사용하므로 고수준 클래스가 저수준 클래스에 의존하는 것이 자연스러워 보일 수 있습니다. 하지만 저수준 클래스는 빈번하게 변경되고, 새로운 것이 추가될 때마다 고수준 클래스가 영향을 받기 쉬우므로 의존관계를 역전시켜야 합니다.

<br>

---


## 🤓 코드로 보는 개방 폐쇄 원칙

아이가 장난감을 가지고 노는 상황을 예시로 코드를 구현해보겠습니다.

<br>

### 🎐 DIP를 위반한 코드

![](https://velog.velcdn.com/images/harinnnnn/post/fc82625e-321c-4bfd-9d4a-629406d748f4/image.png)

<br>


```java
public class Kid {
    private Robot toy;

    public void setToy(Robot toy) {
        this.toy = toy;
    }

    public void play() {
        System.out.println(toy.toString());
    }
}
```

```java
public class Main{
    public static void main(String[] args) {
        Robot robot = new Robot();
        Kid k = new Kid();
        k.setToy(robot);
        k.play();
    }
}
```

위 상황에서, ``Kid`` 는 ``robot``이라는 구체적인 객체에 의존하고 있습니다. 이런 경우 아이가 가지고 노는 장난감의 종류가 변경될 때, 다음과 같이 ``Kid`` 클래스를 수정해야 합니다.

<br>

```java
public class Kid {

    private Robot toy;
    private Lego toy; //레고 추가
    
    // 아이가 가지고 노는 장난감의 종류만큼 Kid 클래스 내에 메서드가 존재해야함.
    public void setToy(Robot toy) {
        this.toy = toy;
    }
    public void setToy(Lego toy) {
        this.toy = toy;
    }

    public void play() {
        System.out.println(toy.toString());
    }
    
}
```

이렇게 아이라는 고수준 모듈이, 변하기 쉬운 장난감이라는 저수준 모듈에게 의존하면 영향에 직접적으로 노출됩니다. 장난감을 하나 더 추가하기 위해 ``Kid`` 클래스에 수정까지 일어나기 때문입니다.

---

<br>

### 🎐 DIP를 적용한 코드

<br>

이 위태로운 설계에 **의존성 역전 원칙**을 적용해보겠습니다.

DIP는 의존 관계를 맺을 때 **자신보다 변화하기 쉬운 것을 의존해서는 안 되고, 거의 변화가 없는 개념에 의존해야 한다**고 말합니다.

- 아이가 장난감을 가지고 노는데 어떤 경우에는 로봇을, 어떤 경우에는 레고를 가지고 놀 것입니다. 이 경우에서 변하기 쉬운 것은 로봇, 레고, 모형 자동차입니다. 

- 하지만 아이가 장난감을 가지고 논다는 사실은 변하기 어려운 개념입니다.


<br>

![](https://velog.velcdn.com/images/harinnnnn/post/c607b934-0641-470d-8a80-7235c2c17f5c/image.png)

<br>

이제는 아이가 구체적인 객체들(로봇, 레고, 모형 자동차 등)을 직접 의존하지 않고 장난감이라는 추상 클래스와 의존 관계를 맺도록 설계했습니다. 로봇,레고,모형 자동차같은 구체적인 객체들도 상위 개념인 장난감 클래스에 의존하고 있습니다.

이런 설계에서는 장난감의 종류가 아무리 추가되고 변경되어도 아이 객체에 영향을 미치지 않습니다.

<br>

코드로 구현하면 다음과 같습니다.

```java
public class Kid {
    private Toy toy;

    public void setToy(Toy toy) {
        this.toy = toy;
    }

    public void play() {
        System.out.println(toy.toString());
    }
```
더이상 ``Kid`` 클래스 내에서 구체적인 장난감 객체들을 생성하지 않습니다. 이제 ``Kid`` 클래스는 장난감이라는 큰 개념의 클래스를 의존하고 있습니다. setToy() 메서드로 가지고 노는 장난감을 바꿀 수 있습니다.

<br>

만약 로봇을 가지고 놀고 싶다면, ``Toy``라는 추상 클래스를 상속 받아 다음과 같이 ``Robot`` 객체를 구현합니다.

```java
public class Robot extends Toy {
    public String toString() {
        return "Robot";
    }
}
```

```java
public class Main{
    public static void main(String[] args) {
        Toy robot = new Robot();
        Kid k = new Kid();
        k.setToy(robot);
        k.play();
    }
}
```

<br>

만약 레고를 가지고 싶다면 다음과 같이 ``Toy`` 클래스를 상속 받는 ``Lego`` 클래스를 구현해주면 됩니다. 

```java
public class Lego extends Toy {
    public String toString() {
        return "Lego";
    }
}
```

```java
public class Main{
    public static void main(String[] args) {
        Toy lego = new Lego();
        Kid k = new Kid();
        k.setToy(lego);
        k.play();
    }
}
```

새로운 장난감을 추가했지만 ``Kid`` 클래스의 코드에는 어떠한 변화도 일어나지 않고, 어떠한 영향도 미치지 않습니다. DIP를 만족했기 때문에 변화에 유연한 시스템이 된 것입니다.

---

<br>

### ⭕️ 정리! 의존성 역전 원칙 (DIP)

<br>

> 의존성 역전 원칙이란 **객체는 구체적인 객체가 아닌 추상화에 의존해야 한다는 법칙**입니다. 자신보다 변하기 쉬운 것에 의존해서는 안됩니다.

DIP를 만족하면, 의존성 주입(DI)라는 기술로 변화를 쉽게 수용할 수 있는 코드를 작성할 수 있습니다.