이번 글에서는 DI(의존성 주입, 의존관계 주입)에 대해 알아보겠습니다.
<br><br>
## DI(Dependency Injection)란 <br><br>
> **DI**는 ``Dependency : 의존성`` , ``Injection : 주입`` 즉 **dependency Injection**의 줄임말로, **의존성 주입**을 뜻합니다.

- 다시 말해 **클래스간의 의존성**을 **클래스 내부가 아닌 외부!!!!!에서 주입!**하는 것입니다.

아직까지는 DI가 너무 추상적으로 다가올 것입니다. 객체지향 프로그래밍에서의 ``의존성``과 ``주입``은 어떤 의미를 가지는지 자세하게 알아보겠습니다.

<br>

---
## 🫂 Dependency, 의존성이 뭘까 🤔
<br>

> A가 B를 의존한다.

여기서 의존대상 **B의 기능이 추가되거나 변경되면 그것이 A에 영향을 미치게 됩니다.**

다시 말해 의존성은 **함수에 필요한 클래스 또는 참조변수나 객체에 의존하는 것**이라고 볼 수 있습니다.
<br><br>

---

<br>

## 💉 Injection, 주입이란? 😲

- 보통 내부에서 필요한 내용(객체)을 생성하여, 참조와 사용을 **내부가 아니라 외부에서 객체를 생성해서 넣어주는 것**을 **주입한다**고 합니다.

주입은 개발자들이 객체를 생성하는 번거로움과 다양한 테스트 케이스를 고려하는 경우를 줄이고, 변수 사용과 개발에 더욱 집중할 수 있게 해주며 **클래스간의 결합도(coupling)를 낮추어 의존성을 줄입니다.**

<br>

---

### 🚧 잠깐! 클래스간의 결합도란...

<br>

- 소프트웨어의 코드의 요소가 **다른 것과 얼마나 강력하게 연결** 되어 있는지, 또한 **얼마나 의존적인지** 나타내는 정도입니다.

>😵‍💫 _**클래스간의 결합도가 높으면..**_ 🔗🔗🔗🔗🔗🔗🔗🔗🔗
- 연관된 클래스가 변경되면 더불어 함께 변경을 해주어야 하고,
- 수정하려는 클래스를 이해하기 위해 연관된 클래스를 함께 이해해야 하고,
- 클래스를 재사용하기 힘들어집니다.

따라서 ``클래스간의 결합도가 낮은 코드를 좋은 코드``라고 보고 있습니다.


---

다시 돌아와 **의존성 주입**을 정리하면 이렇습니다.

- 코드에서 두 모듈(프로그램의 기능을 독립적인 부품으로 분리한 것) 간의 연결
- A와 B가 의존 관계일 때, A는 어떤 용도를 위해 B를 사용함.
- 클래스간의 의존성이 줄어들면 유지보수시 매우 편함!

---

## 🍔 햄버거 가게 예제 코드
이제 햄버거 가게 예제 코드를 통해 DI를 더 깊게 이해해보겠습니다.

``햄버거 가게 요리사는 햄버거 레시피에 의존한다.``

햄버거 레시피가 변화되었을 때, 요리사는 햄버거 레시피에 따라 햄버거 만드는 방법을 수정해야 합니다.
레시피의 변화가 요리사의 행위에 영향을 미쳤기 때문에 **'요리사가 레시피에게 의존성을 갖는다 (요리사 -> 레시피)'** 고 할 수 있습니다.
🚧 이런 코드는 ``결합도가 높다``고 볼 수 있습니다. 레시피 클래스가 수정되면, 레시피의 의존성을 갖는 모든 클래스들도 함께 수정되어야 하기 때문입니다. 예제처럼 의존성을 갖는 클래스가 한 두개 뿐이라면 문제가 없지만, 규모가 큰 코드라면 **유지보수의 효율이 아주 엉망**이 될 것입니다! 해당 변경에 의존성을 갖는 한 코드라도 수정 되지 않은 곳이 있다면 오류를 발생시킬 것입니다.

코드로 표현한다면 다음과 같습니다.

```java
class BurgerChef {
    private HamBurgerRecipe hamBurgerRecipe; //햄버거 레시피

    public BurgerChef() { // 요리사는 햄버거 레시피에 의존하고 있습니다.
        hamBurgerRecipe = new HamBurgerRecipe();        
    }
}
```

---

### 의존관계를 인터페이스로 추상화하기!
<br>
이런 의존 관계는 인터페이스를 이용해 추상화할 수 있습니다.

위의 코드는 많은 레시피들 중 오직 HamBurgerRecipe만을 의존하는 구조였습니다. 그래서 아래의 코드에서는 BurgerRecipe 인터페이스를 만들어 햄버거 레시피를 더 큰 개념인 레시피로 추상화했습니다.

아래 코드에서 BurgerChef는 BurgerRecipe를 의존해 더 다양한 버거들의 레시피에 의존할 수 있습니다.
<br>


```java
class BurgerChef {
    private BurgerRecipe burgerRecipe;

// 이제 BurgerChef는 더 다양한 종류의 레시피에 의존하게 된다.
    public BurgerChef() {
        burgerRecipe = new HamBurgerRecipe();
        //burgerRecipe = new CheeseBurgerRecipe();
        //burgerRecipe = new ChickenBurgerRecipe();
    }
}

// 레시피의 개념으로 추상화한 BugerRecipe 인터페이스
interface BugerRecipe {
    newBurger();
    // 이외의 다양한 메소드
} 

//BurgerRecipe 인터페이스를 구현한 HambergerRecipe
class HamBurgerRecipe implements BurgerRecipe {
    public Burger newBurger() {
        return new HamBerger();
    }
    
    // ...
}
```
<br>

이렇게 의존관계를 인터페이스로 추상화하게 되면, 더 다양한 의존 관계를 맺을 수가 있습니다. 더 다양한 의존 관계를 맺는다는 것은 ``🔖 실제 구현 클래스와의 관계가 느슨해지고, 결합도가 낮아진다`` 는 의미를 갖습니다.

---

## 🍔🥸 이제 진짜 DI 구현하기!

지금까지의 구현에서는 **BurgerChef 클래스 내부적**으로 의존관계인 BurgerRecipe가 어떤 값을 가질지 직접 정하고 있습니다.

하지만 이제 우리는 내부가 아닌, **외부에서 의존성을 주입하는 DI**를 구현해보겠습니다.

**어떤 BurgerRecipe를 만들지를 버거 가게 사장님이 정하는 시나리오**를 써보겠습니다. 즉, BurgerChef가 의존하고 있는 BurgerRecipe를 요리사 스스로가 아닌, **외부**(사장님)에서 결정하고 주입하는 것입니다.

이런 관계가 바로 의존관계를 외부에서 결정하고 주입하는, DI(의존관계 주입)입니다.

---

코드로 구현해보겠습니다.

Burger 레스토랑 주인이 어떤 레시피를 주입하는지 결정하는 예시로 설명해보겠습니다.

### 생성자 이용

```java
class BurgerChef {
    private BurgerRecipe burgerRecipe;

    public BurgerChef(BurgerRecipe burgerRecipe) { //생성자
        this.burgerRecipe = burgerRecipe;
    }
}

class BurgerRestaurantOwner { //버거 가게 사장님 클래스! (외부)
    private BurgerChef burgerChef = new BurgerChef(new HamburgerRecipe());

    public void changeMenu() { //메뉴를 바꾸는 메서드
        burgerChef = new BurgerChef(new CheeseBurgerRecipe());
    	//사장 클래스가 각각의 요리사가 만들 레시피를 개별적으로 주입하고 있다.
        
    }
}

```

### 메소드 이용 (대표적으로 Setter 메서드)

```java
class BurgerChef {
    private BurgerRecipe burgerRecipe = new HamburgerRecipe();

    public void setBurgerRecipe(BurgerRecipe burgerRecipe) { //Setter
        this.burgerRecipe = burgerRecipe;
    }
}

class BurgerRestaurantOwner { //버거 가게 사장님 클래스! (외부)
    private BurgerChef burgerChef = new BurgerChef();

    public void changeMenu() { //메뉴를 바꾸는 메서드
        burgerChef.setBurgerRecipe(new CheeseBurgerRecipe());
        //사장 클래스가 각각의 요리사가 만들 레시피를 개별적으로 주입하고 있다.
    }
}
```

---

## 🍥 의존성 주입의 장점과 의의

의존 관계를 분리해, 외부에서 주입 받는 코드들은 다음과 같은 장점을 가집니다.

- 리팩토링(결과의 변경 없이 코드의 구조를 재조정)이 쉬워진다.
- 객체 간의 의존성을 줄이거나 없앨 수 있다.
- 객체 간의 결합도를 낮추며 유연한 코드 작성이 가능하다.
- 테스트하기 좋은 코드가 된다.
(BurgerRecipe의 테스트를 BurgerChef 테스트와 분리해 진행할 수 있습니다.)

---

<br>

[🍔 예제코드 참고 블로그](https://tecoble.techcourse.co.kr/post/2021-04-27-dependency-injection/)