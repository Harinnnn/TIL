이번 글에서는 객체지향의 5대 원칙 중, ``개방 폐쇄 원칙(OCP)``에 대해 알아봅니다!

다섯가지 원칙 **SOLID** 는 아래와 같습니다.

>1. **단일 책임 원칙** (Single Responsibility principle)
>2. **개방 폐쇄 원칙** (Open Close Principle)
>3. **리스코프 치환 원칙** (Liscov Substitution Principle)
>4. **인터페이스 분리 원칙** (Interface Sergregation Principle)
>5. **의존성 역전 원칙** (Dependency Inversion Principle)

---

## ✅ 개방 폐쇄 원칙 (OCP)

``Open Close Principle``

> _**"소프트웨어 엔티티(클래스, 모듈, 함수 등)는 확장에 대해서는 열려 있어야 하지만 변경에 대해서는 닫혀 있어야 한다."**_
	- 로버트 C 마틴
    
<br>

- `**객체의 확장은 개방적으로, 객체의 수정은 폐쇄적으로** 대해야 한다는 원칙
- **기능이 변하거나 확장되는 것은 가능하지만 그 과정에서 기존의 코드가 수정되지 않아야한다**

<br>

🤔 기능이 변하는 것과 확장은 가능한데, 어떻게 코드의 수정 없이 그것들을 가능하게 하는지 잘 와닿지 않을 수 있습니다.
대표적으로 프로그래밍시 사용하는 라이브러리를 생각해보겠습니다. 라이브러리를 사용하는 객체의 코드가 변경된다고 해서 라이브러리의 코드까지 변경하지는 않습니다.

<br>

이렇게 어떤 하나의 객체를 수정해야 하는 상황에서, 해당 객체에 의존하는 다른 객체들까지 줄줄이 수정해야한다면 좋은 설계라고 보기 힘들 것입니다.

<br>

💻 하지만 OCP를 코드에 적용하면, 

- 객체 간의 의존성을 최소화하여 코드 변경에 따른 영향력을 낮출 수 있습니다.

---

## 🤓 코드로 보는 개방 폐쇄 원칙

<br>

자동차를 운전하는 운전자에 관한 간단한 예제 코드를 보며 OCP를 이해해보겠습니다.

<br>

![](https://velog.velcdn.com/images/harinnnnn/post/10489f56-5d4a-4ba8-a134-8da46e88283c/image.png)


<br>

### 🎐 OCP를 위반한 코드

다음은 개방 폐쇄 원칙을 위반한 코드입니다.

```java

public class NOT_OCP운전자 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		소나타 운전자 = new 소나타();
		  운전자.drive();
		
		그랜저 운전자2 = new 그랜저();
		  운전자2.drive();
		
		BMW 운전자3 = new BMW();
		  운전자3.drive();
	}

}

class 소나타{	
	void drive() {
		System.out.println("나는 소나타를 운전한다.");
	}
}

class 그랜저{	
	void drive() {
		System.out.println("나는 그랜저를 운전한다.");
	}
}

class BMW{	
	void drive() {
		System.out.println("나는 BMW를 운전한다.");
	}
}

```

위 코드에서는 각각의 소나타, 그랜저, BMW 클래스에서 drive() 라는 메서드를 구현하고 있습니다. 이 코드에서는 운전자 객체가 생성될 때부터 각 차량 클래스에 과하게 의존하고 있습니다.

만약 운전자3의 차가 소나타로 바뀌면, 운전자3의 객체를 다시 생성해주어야 합니다. 코드 자체가 수정되는 상황은 **수정에 폐쇄적인 OCP를 위배**합니다.

자동차가 바뀌더라도 내가 운전하는 방식은 동일해야 합니다.

---

### 🎐 OCP를 적용한 코드

다음은 개방 폐쇄 원칙을 적용한 코드입니다.

각각의 그랜저, 소나타, BMW 클래스들은 더 추상적인 개념인 자동차 클래스를 상속 받고 있습니다. 이 코드에서의 drive() 메서드는 자동차가 바뀌더라도 변경되지 않습니다. 자동차의 변경과 확장에 대해서는 개방되어 있고, 어떤 차를 타도 운전 방법이 수정되지 않게 폐쇄되어있는 코드입니다.

<br>

```java

public class OCP운전자 {

	public static void main(String[] args) {
		
		자동차[] 운전자 = new 자동차[3];
		
		운전자[0] = new 소나타();
		운전자[1] = new 그랜저();
		운전자[2] = new BMW();
		
		for(int i=0; i<운전자.length; i++) {
			운전자[i].drive();
		}

	}

}

class 자동차{
	String myCar="자동차";
	void drive() {
		System.out.printf("나는 %s 를 운전할 수 있다. \n",  myCar);
	}
}

class 소나타 extends 자동차{
	public 소나타() {
		myCar = "소나타";
	}	
}

class 그랜저 extends 자동차{	
	public 그랜저() {
		myCar = "그랜저";
	}
}

class BMW extends 자동차{	
	public BMW() {
		myCar = "BMW";
	}
}

```

여기서 우리는 현대 자동차를 운전하는 운전자를 하나 더 만들어 코드를 확장하려고 합니다.

```java

    Class 현대 extends 자동차 {
        public 현대() {
            myCar = "현대";
        }
    }
    
```

라는 현대 클래스를 하나 추가하고, 다음과 같이 메인 메서드를 작성해주면 됩니다.

```java

	public static void main(String[] args) {
    
        운전자[3] = new 현대(); //추가
		운전자[3].drive();

	}
```

새로운 자동차를 하나 더 추가하는 상황에서도 기존 drive() 메서드나 자동차 클래스의 코드가 전혀 변경되지 않았음을 알 수 있습니다.

---

### ⭕️ 정리! 개방 폐쇄 원칙 (OCP)

> 확장에는 개방되어있고, 수정에는 폐쇄되어야 한다. 즉, 기능이 변하거나 확장되는 것은 가능하지만 그 과정에서 기존의 코드가 수정되지 않아야 한다는 원칙이었습니다.