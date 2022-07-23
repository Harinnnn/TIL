이번 글에서는 객체지향의 5대 원칙 중, ``인터페이스 분리 원칙 (ISP)`` 에 대해 알아봅니다!

다섯가지 원칙 **SOLID** 는 아래와 같습니다.

>1. **단일 책임 원칙** (Single Responsibility Principle)
>2. **개방 폐쇄 원칙** (Open Closed Principle)
>3. **리스코프 치환 원칙** (Liscov Substitution Principle)
>4. **인터페이스 분리 원칙** (Interface Sergregation Principle)
>5. **의존성 역전 원칙** (Dependency Inversion Principle)

---

## ✅ 인터페이스 분리 원칙 (ISP)

``Interface Segregation Principle``

- 인터페이스 분리 원칙이란 **객체는 자신이 사용하는 메서드에만 의존해야 한다**는 법칙입니다. 객체가 사용하지 않는 메서드를 의존해서는 안 된다는 뜻이기도 합니다.


인터페이스는 지나치게 광범위하거나 지나치게 많은 기능을 구현해서는 안 되고, 그 인터페이스를 사용하는 객체를 기준으로 잘게 분리되어야 한다는 의미입니다.

<br>

### 🤕 인터페이스 분리 원칙 위반 설계

다음 그림을 보면서 확실하게 이해해보겠습니다!

![](https://velog.velcdn.com/images/harinnnnn/post/f56cf080-bd64-4714-86fa-05c2ed3dda33/image.png)

위의 그림에서는 ``User1``, ``User2``, ``User3`` 객체들이 OPS를 상속 받고 있습니다. 이 때 ``User1``은 오직 op1 메서드만을, ``User2``는 오직 op2 메서드만을, ``User3``는 오직 op3 메서드만을 사용한다고 가정해보겠습니다.

이 상황에서 ``User1``은 OPS 전체를 상속 받았기 때문에 op1, op2, op3 메서드를 모두 사용할 수 있지만, 정작 op1 메서드만을 필요로 합니다. ``User1``은 op2를 사용하지 않음에도 불구하고 만약 op2 메서드에 변경이 일어나면, 함께 변경되어 재컴파일 & 재배포 과정을 거쳐야하는 문제가 생깁니다.

**상속 받은 OPS 객체의 규모가 필요보다 크기 때문에 발생한 문제입니다.**

<br>

### 🤓 인터페이스 분리 원칙을 준수한 설계!

이런 경우, 설계에 인터페이스 분리 원칙을 적용해 문제상황을 해결할 수 있습니다.

![](https://velog.velcdn.com/images/harinnnnn/post/f4c05e79-6559-4d32-a41e-57a0785be03f/image.png)

**OPS는 OPS를 상속 받는 U1Ops, U2Ops, U3Ops로 잘게 분리 되었습니다.** 이렇게 분리되면, 각각의 객체들은 오직 자신이 필요한 메서드만을 사용할 수 있는 구조가 됩니다.

이 경우에는 op2 메서드의 변경이 일어나더라도 ``User1`` 객체에는 전혀 영향이 가지 않습니다. ISP를 준수한 바람직한 설계 구조라고 볼 수 있습니다.

<br>

---

## 🤓 코드로 보는 인터페이스 분리 원칙

자동차와 배 객체를 구현해보겠습니다. 

<br>

### 🎐 LSP를 위반한 예제 코드

먼저 두 객체를 구현하기 위해 큰 개념인 교통수단 추상 클래스를 만들었습니다. Transportation 클래스에는 두 객체의 공통 개념인 boarding() 메서드와 자동차에 관한 관한 메서드, 배에 관한 메서드가 있습니다.

```java

abstract public class Transportation {

    public void boarding() {
        System.out.println("탑승합니다.");
    }

	//Car
    public void drive() {
        System.out.println("운전합니다.");
    }
    public void driveLeft() {
        System.out.println("왼쪽으로 운전합니다.");
    }
    public void driveRight() {
        System.out.println("오른쪽으로 운전합니다.");
    };

	//Ship
    public void steer() {
        System.out.println("조종합니다.");
    };
    public void steerLeft() {
        System.out.println("왼쪽으로 조종합니다.");
    };
    public void steerRight() {
        System.out.println("오른쪽으로 조종합니다.");
    };
}
```

---

🚘 Transportation 클래스를 상속 받은 ``Car`` 객체입니다.

자동차에 필요한 메서드들을 오버라이드했습니다.

```java
//Car 객체
public class Car extends Transportation{

    @Override
    public void boarding() {
    	//구현...
    }

    @Override
    public void drive() {
    	//구현...
    }
    @Override
    public void driveLeft() {
    	//구현...
    }
    @Override
    public void driveRight() {
    	//구현...
    }


    @Override
    public void steer() {
        System.out.println("불필요");
    }

    @Override
    public void steerLeft() {
        System.out.println("불필요");
    }

    @Override
    public void steerRight() {
        System.out.println("불필요");
    }

}

```

하지만 ``Car`` 객체에서는 배를 조종할 때 필요한 steer(), steerLeft(), steerRight() 메서드들이 전혀 필요하지 않습니다.

---

⛴ Car와 같이 Transportation 클래스를 상속 받은 ``Ship`` 객체입니다.

배에 필요한 메서드들을 오버라이드했습니다.

```java
//Ship 객체
public class Ship extends Transportation{

    @Override
    public void boarding() {
    	//구현...
    }
    
    @Override
    public void drive() {
        System.out.println("불필요");
    }
    @Override
    public void driveLeft() {
        System.out.println("불필요");
    }
    @Override
    public void driveRight() {
        System.out.println("불필요");
    }


    @Override
    public void steer() {
    	//구현...
    }

    @Override
    public void steerLeft() {
    	//구현...
    }

    @Override
    public void steerRight() {
    	//구현...
    }
    
}
```

하지만 ``Ship`` 객체에서는 자동차를 운전할 때 필요한 drive(), driveLeft(), driveRight() 메서드들이 전혀 필요하지 않습니다. 그럼에도 불구하고 Transportation 클래스를 상속받았기 때문에 해당 기능의 메소드를 강제로 상속받게 됩니다.

이러한 상속의 특징은 부모 객체의 규모가 커질수록 개발의 편의성을 저하시킵니다. 필요하지도 않은 수십개의 메서드를 일일히 오버라이딩해 적절히 처리해야하기 때문입니다.

---

<br>

### 🎐 ISP를 적용한 코드

이런 문제 상황에 인터페이스 분리 원칙을 적용한 예제 코드입니다.

- **원래 Transportation 클래스의 메서드였던 기능들을 각각 인터페이스로 분리해주었습니다.**

이를 통해 각각의 ``Car``, ``Ship`` 객체는 필요한 인터페이스만을 선택적으로 구현할 수 있을 것입니다.

```java
public interface boarding {
    public void boarding();
}

public interface drive {
    public void dive();
}

public interface driveLeft {
    public void driveLeft();
}

public interface driveRight {
	public void driveRight();
}

public interface steer {
    public void steer();
}

public interface steerLeft {
    public void steerLeft();
}

public interface steerRight {
	public void steerRight();
}
```
---

이제, 필요한 기능을 가진 인터페이스만을 구현하는 ``Car`` 객체입니다. 더이상 필요하지 않은 배에 관련한 메서드들을 강제로 구현하지 않아도 됩니다.

```java
public class Car implements boarding,drive,driveLeft,driveRight{

    @Override
    public void boarding() {
        // 구현...
    }
    
    @Override
    public void dive() {
        System.out.println("운전합니다.");
    }

    @Override
    public void driveLeft() {
        System.out.println("왼쪽으로 운전합니다.");
    }
    
    @Override
    public void driveRight() {
        System.out.println("오른쪽으로 운전합니다.");
    }
    
}
```

인터페이스 분리 원칙을 적용한 설계이기 때문에, ``Ship`` 객체도 위와 같이 자신에게 필요한 메서드들만 구현하여 사용할 수 있습니다.

인터페이스는 다중 상속을 지원하므로, 필요한 기능을 인터페이스로 나누면 해당 기능만을 상속 받을 수 있습니다. 만약 추후 업데이트 되는 새로운 기능이 생긴다고 해도 기존의 코드 변경 없이 새 기능을 가지는 인터페이스를 설계해 객체 내에 구현해주면 됩니다!

---

<br>

### ⭕️ 정리! 인터페이스 분리 원칙 (ISP)

<br>

> 인터페이스 분리 원칙이란 **반드시 객체가 자신에게 필요한 기능만을 가지도록 제한**하는 원칙입니다. 불필요한 상속과 구현을 최대한 방지함으로써 객체의 불필요한 책임을 제거합니다.

위의 예제와 같이 필요보다 큰 규모의 객체는 인터페이스로 잘게 나누어 확장성을 향상시킬 수 있습니다.

객체를 상속할 때는 불필요한 의존 관계가 맺어지지 않는지 잘 판단하여 올바르게 상속해야합니다!