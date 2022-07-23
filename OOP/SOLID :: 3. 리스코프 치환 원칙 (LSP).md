이번 글에서는 객체지향의 5대 원칙 중, ``리스코프 치환 원칙 (LSP)``에 대해 알아봅니다!

다섯가지 원칙 **SOLID** 는 아래와 같습니다.

>1. **단일 책임 원칙** (Single Responsibility Principle)
>2. **개방 폐쇄 원칙** (Open Close Principle)
>3. **리스코프 치환 원칙** (Liscov Substitution Principle)
>4. **인터페이스 분리 원칙** (Interface Sergregation Principle)
>5. **의존성 역전 원칙** (Dependency Inversion Principle)

<br>

---

## ✅ 리스코프 치환 원칙 (LSP)

``Liscov Substitution Principle``

- 리스코프 치환 원칙이란 부모 객체와 자식 객체가 있을 때 **부모 객체를 호출하는 동작에서 자식 객체가 부모 객체를 완전히 대체할 수 있다**는 원칙이다.

<br>

객체 지향 프로그래밍에서 상속이 일어나면, 하위 타입인 자식 객체는 상위 타입인 부모 객체의 특성을 가지며, 그 특성을 토대로 확장할 수 있습니다.

![](https://velog.velcdn.com/images/harinnnnn/post/2f2c6e85-553f-4afa-83c1-2d2abf722cea/image.png)

리스코프 치환 원칙은 **올바른 상속**을 위해, **자식 객체의 확장이 부모 객체의 방향을 온전히 따르도록 권고**하는 원칙입니다!

---

## 🤓 코드로 보는 단일 책임 원칙

리스코프 치환 원칙 설명시에 많이 사용되는 예제인 직사각형, 정사각형 관계를 코드로 나타내보겠습니다.

<br>

### 🎐 LSP를 위반한 예제 코드

다음은 직사각형 ``Rectangle``을 구현한 클래스입니다. 너비와 높이 값을 지정, 반환 할 수 있으며 넓이를 계산할 수 있습니다. 

```java
public class Rectangle {

    public int width;
    public int height;

    // 너비 반환, Width Getter
    public int getWidth() {
        return width;
    }
    // 너비 할당, Width Setter
    public void setWidth(int width) {
        this.width = width;
    }

    // 높이 반환, Height Getter
    public int getHeight() {
        return height;
    }
    // 높이 할당, Height Setter
    public void setHeight(int height) {
        this.height = height;
    }
    
    //직사각형 넓이 반환 함수
    public int getArea() {
    	return width * height;
    }
}
```

---

**정사각형은 직사각형의 범주에 포함됩니다. 그렇다면 직사각형을 상속하여 정사각형 객체를 만들면 정상적으로 작동할까요?** 직사각형 클래스를 상속 받아 정사각형 객체를 구현해보겠습니다.

```java
public class Square extends Rectangle{
    
    @Override
    public void setWidth(int Width) {
        super.setWidth(width);
        super.setHeight(getWidth());
    }
    
    @Override
    public void setHeight(int height) {
        super.setHeight(height);
        super.setWidth(getHeight());
    }
    
}
```

위 코드처럼 ``Rectangle`` 객체를 상속 받은 ``Square`` 클래스에서는 정사각형의 너비와 높이가 같다는 특징을 구현했습니다. 너비와 높이 둘 중 하나를 입력해도 나머지 값이 일치되도록 메서드를 오버라이드 해주었습니다.

---

이제 직사각형과 정사각형 클래스를 모두 구현해주었으니, 정상적으로 잘 작동하는지 확인해보겠습니다!

```java
public class Main {
    public static void main(String[] args) {

        Rectangle rectangle = new Rectangle();
        rectangle.setHeight(5);
        rectangle.setWidth(10);

        System.out.println(rectangle.getArea());

    }
}
```

> 50

먼저 ``Rectangle`` 클래스입니다. 높이 5 x 너비 10으로 직사각형의 길이가 정상적으로 잘 구해진 것을 확인해볼 수 있습니다.

---

이번에는 ``Square`` 클래스를 테스트해보겠습니다.
테스트에 앞서, **리스코프 치환 원칙**은 _부모 객체를 호출하는 동작에서 자식 객체가 부모 객체를 **완전히** 대체_ 할 수 있다는 원칙이었습니다!

그렇다면, ``Rectangle`` 클래스에서의 테스트와 같은 값을 할당했을 때, 당연히 완전히 같은 결과를 반환해야 합니다. 확인해보겠습니다!

```java
public class Main {
    public static void main(String[] args) {

        Rectangle square = new Square();
        
        square.setWidth(10);
        square.setHeight(5);


        System.out.println(square.getArea());
        
    }
}

```

>25

어째서인지, 50이 아니라 25가 반환되었습니다. 가장 마지막에 수행된 ``setHeight(5)``가 객체의 너비와 높이르 모두 5로 할당했기 때문입니다. 그러니 당연히 넓이도 25로 출력되었습니다.

---

<br>

### 🤕 어떻게 된 일일까요!

<br>

사실 프로그램 자체는 우리가 계획한대로, ``정사각형의 넓이``가 잘 구현되었습니다. 하지만 ``Rectangle`` 클래스의 동작과 그를 상속 받은 ``Square`` 클래스의 동작이 전혀 다르다는 사실을 알 수 있습니다.

<br>

>이는 바로 정사각형이 직사각형을 상속 받는 것이 **올바른 상속 관계가 아니라는 것**을 의미합니다! **자식 객체가 부모 객체의 역할을 완전히 대체하지 못한다는 의미**죠.

<br>

이렇게 잘못된 객체를 상속하거나 올바르게 확장하지 못할 경우, 겉으로 보기엔 정상적이지만 올바른 객체라고 할 수는 없습니다.

바로 이런 코드가 리스코프 치환 원칙을 위배하는 코드입니다.

---

### 🎐 LSP를 준수한 코드

그렇다면 이 코드를 어떻게 리스코프 치환 원칙에 부합하게끔 구현할 수 있을까요?

바로 **올바르게 성립하는 상속 관계를 구현**해야합니다. 

앞에서 우리는 직사각형과 정사각형은 바람직한 상속 관계가 성립될 수 없다는 것을 알게 됐습니다. 그렇다면, 직사각형과 정사각형 객체가, 더 큰 범주의 ``사각형 객체``를 상속받을 수 있도록 구현해보겠습니다.

- ``Shape 클래스`` 구현
```java
public class Shape {

    public int width;
    public int height;

    // 너비 반환, Width Getter
    public int getWidth() {
        return width;
    }
    // 너비 할당, Width Setter
    public void setWidth(int width) {
        this.width = width;
    }

    // 높이 반환, Height Getter
    public int getHeight() {
        return height;
    }
    // 높이 할당, Height Setter
    public void setHeight(int height) {
        this.height = height;
    }

    // 사각형 넓이 반환
    public int getArea() {
        return width * height;
    }
}
```

```java

//직사각형 클래스
public class Rectangle extends Shape {

    public Rectangle(int width, int height) {
        setWidth(width);
        setHeight(height);
    }

}

//정사각형 클래스
public class Square extends Shape{
    
    public Square(int length) {
        setWidth(length);
        setHeight(length);
    }
    
}
```

``Shape`` 클래스를 상속 받는 ``Rectangle`` 클래스와 ``Square`` 클래스입니다. 
```java
public class Main {
    public static void main(String[] args) {
    
        Shape rectangle = new Rectangle(10, 5);
        Shape square = new Square(5);
        
        System.out.println(rectangle.getArea());
        System.out.println(square.getArea());
    }
}
```

> 50 <br>
25

<br>

메인 메서드에서 테스트해보면, 값이 잘 나오는 것을 확인할 수 있습니다.
더이상 ``Rectangle`` 객체와 ``Square`` 객체는 상속 관계가 아니므로, 리스코프 치환 원칙을 준수합니다.

---

### ⭕️ 정리! 리스코프 치환 법칙 (LSP)

> 리스코프 치환 원칙은 상속되는 객체는 반드시 부모 객체를 완전히 대체할 수 있어야한다고 권고한다.

첫번째의 직사각형 클래스를 상속받은 정사각형 객체 예제처럼, 올바르지 못한 상속관계는 제거하고 부모 객체의 동작을 완벽히 대체할 수 있는 관계만 상속하도록 코드를 설계해야합니다!