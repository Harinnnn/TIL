<h2> 📍 구조 </h2>

![](https://blog.kakaocdn.net/dn/bMNEp4/btq4CrzE4tO/1VkXzKN22ygN75k606iIe0/img.png)

<br>

### 📍 JVM
- **자바가상머신(Java Virtual Machine)**의 약자
- 자바프로그램을 컴파일해서 나온 결과인 **바이트코드를 실행**시킨다.
	- ``가비지 컬렉터(GC)``를 통해 어플리케이션의 동적 메모리를 관리한다.

<br>

### 📍 JRE

- **자바런타임환경(Java Runtime Environment)**의 약자
- JVM을 동작하는 데 필요한 **자바 라이브러리들을 담음**

<br>

### 📍 JDK

- **자바개발키트(Java Development Kit)**의 약자
- 자바로 개발할 수 있도록 여러 기능들을 제공한다.
- 자바 언어를 바이트 코드로 컴파일해주는 ``자바 컴파일러(javac)``, 자바 클래스 파일을 해석해주는 ``어셈블리어(javap)``등이 있다.

<br>


---

<br>

## 📍 JVM 동작원리

<br>

![](https://blog.kakaocdn.net/dn/YPgAl/btq4ErMuE3y/aEUYDKZdu9L3gABwBcckb0/img.jpg)

- JVM은 위와 같은 절차로 자바를 실행시킨다.

<br>

>1. 자바를 통해 개발을 하고 실행하면, 자바 파일은 바이트코드(.class)파일로 컴파일 과정을 거치게 된다.
>2. 바이트코드로 변환된 파일들은 클래스로더를 통해 동적 로딩, 필요한 클래스를 로딩 및 링크하며 각 런타임데이터 영역에 할당한다.
>3. 클래스로더로부터 할당된 바이트코드는 익스큐션 엔진을 통해 명령어 단위로 하나씩 가져와 실행된다.

