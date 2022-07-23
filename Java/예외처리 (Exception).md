## ✏️ 예외처리(Exception)

>**정의**
프로그램 실행 시 발생할 수 있는 예외의 발생에 대비한 코드를 작성하는 것

>**목적**
프로그램의 비정상 종료를 막고, 정상적인 실행상태를 유지합니다.

- 예외는 error의 일종이며, 예외 발생시 **시스템 및 프로그램 불능상태**를 야기한다.
- 예외 처리를 통해 갑작스러운 예외가 발생하여도, 시스템 및 프로그램이 불능상태가 되지 않고 **정상 실행 상태를 유지**할 수 있다.

---

## 📍 Exception의 종류

> - **일반예외 (Exception)** : ``💻컴파일 시점에 발생하는 예외``
> - **실행예외 (RuntimeException)** : ``💻프로그램 실행시에 발생하는 예외``

- ``일반예외는 컴파일러가 체크해주지만, 실행예외는 컴파일러가 따로 체크해주지 못한다.`` 그러니 알아서 예외 처리 코드를 사용해야한다. 실행예외는 프로그램 실행 이후에 발생하는 예외이기 때문에, 따로 컴파일러가 예외 처리 코드를 강제하라고 하지 않는다. 온전히 개발자의 경험에 의해 예외 처리 코드를 사용해야 한다. 컴파일 시점에서 실행예외를 판단해 검사할 수가 없기 때문에, 개발자의 역량에 따라 실행 예외를 잘 막을 수도, 막지 못할수도 있다. 다른 의미에서는 ``일반예외보다 실행예외가 예외발생시 더 치명적``이다.

---

## 💻 java.lang.Exception

이 2가지 종류의 Exception 을 처리하기 위해 자바에서는 ``java.lang.Exception`` 이라는 ``최상위 부모 클래스``를 제공합니다. 따라서 모든 Exception 들의 조상은 결국  java.lang.Exception 입니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBiChk%2FbtqAVIydR4K%2FkfmFOLQqeVpEff5sVmNJbK%2Fimg.png)

파란색은 일반예외, 초록색은 런타임에러이다.

---

### 📍 예외처리 하기

예외처리는 ```try, catch 문```을 사용한다.

```java
try {
    ...
} catch(예외1) {
    ...
} catch(예외2) {
    ...
...
}
```
---

## 📍 try-catch문의 흐름

> **예외 처리 코드 Try - Catch - Finally**

1️⃣ try 블럭 내에서 ``예외가 발생``한 경우

1. 발생한 예외와 일치하는 catch블럭이 있는지 확인한다.
2. 일치하는 catch 블럭을 찾게 되면, 그 catch블럭 내의 문장들을 수행하고 전체 try-catch문을 빠져나가서 그 다음 문장을 계속해서 수행한다. (만일 일치하는 catch블럭을 찾지 못했다면 예외 처리되지 못한다. > 프로그램 비정상 종료)

2️⃣ try 블럭 내에서 ``예외가 발생하지 않은`` 경우

1. catch 블럭을 거치지 않고 전체 try-catch문을 빠져나가서 수행을 계속한다.

> - **Try 블록** : 실제 코드가 들어가는 곳으로써 예외 Exeption이 발생할 가능성이 있는 코드
> - **Catch 블록** : Try 블록에서 Exeption이 발생하면 코드 실행 순서가 Catch 쪽으로 오게됨. 즉 예외에 대한 후 처리 코드
> - **Finally 블록** : Try 블록에서의 Exeption과 발생 유무와 상관 없이 무조건 수행되는 코드 (옵션이라 생략이 가능)


---

## 💻 Exeption 미발생!

Try 블록 수행 -> Finally 블록 수행 (생략가능)

```java
package Exception;
//예외 발생 X
public class Ex_1 {
    public static void main(String[] args) {
        System.out.println(1);
        try {
            System.out.println(2);
            System.out.println(3);
        } catch (Exception e) {
            System.out.println(4);
        } //try-catch의 끝
        System.out.println(5);
    }
}
````

> 출력:
1
2
3
5

---

## 💻 Exeption 발생!

Try 블록 수행 -> Catch 블록 수행 -> Finally 블록 수행 (생략가능)

```java
package Exception;
// 예외 발생 O
public class Ex_2 {
    public static void main(String[] args) {
        System.out.println(1);
        try {
            System.out.println(0/0); //예외발생!
            System.out.println(2); //실행되지 않음
        } catch (ArithmeticException ae) {
            System.out.println(3);
        } //try-catch문의 끝
        System.out.println(4);
    } //main 메서드의 끝
}
```
> 출력:
1
3
4

- 예외가 발생한 후 바로 해당되는 catch문을 수행한다. 예외가 발생한 후 다음 실행문운 실행되지 않는다.
- catch문이 여러 개 있더라도 발생한 예외에 해당하는 catch 블럭 한 개만 수행된다.

---

## 💻 Exception



```java
package Exception;

public class Exception {
    public static void main(String[] args) {
        System.out.println(1);
        System.out.println(2);
        try {
            System.out.println(3);
            System.out.println(0/0);
            System.out.println(4);
        } catch (ArithmeticException ae) {
            if (ae instanceof ArithmeticException)
                System.out.println("true");
            System.out.println("ArithmeticException");
        } catch (Exception e) {
            System.out.println("Exception");
        }
        System.out.println(5);
    }
}
```

- ``Exception``이 선언된 catch 블럭은 **모든 예외 처리가 가능**하다. 따라서 catch문의 가장 마지막에 위치해야한다! (모든 예외처리가 가능해서 다른 catch문이 의미없어지기 때문)


