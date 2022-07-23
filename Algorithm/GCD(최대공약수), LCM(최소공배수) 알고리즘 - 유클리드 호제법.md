<br>
백준 1934, 2609, 13241 최소 공배수 관련 문제를 풀면서 알게된 최대공약수(GCD)와 최소공배수(LCM) 알고리즘을 정리합니다.

<br>


## 🔖 최대 공약수(GCD) 구하기
최대 공약수(GCD, ``Greatest Common Divisor``)란 두 자연수의 공통된 약수 중에서 가장 큰 수이다.

- ex) GCD(8, 12) = 4

---

## ✏️ 유클리드 호제법 - GCD

기존의 무차별 대입으로 gcd를 구하는 방법보다 더 효율적인 알고리즘입니다.

>1. 큰 수를 작은 수로 나눈다.
>2. 나누는 수를 나머지로 계속 나눈다.
>3. 나머지가 0이 나오면, 나누는 수가 최대공약수이다.

- 유클리드 호제법을 ``코드``로 나타내면 다음과 같습니다.

```java
public static int gcd(int a, int b) {
		while(b!=0) {
            int r = a%b;
            a = b;
            b = r;
        }
        return a;
    }
```

---


## 🔖 최소 공배수(LCM) 구하기
최소 공배수(LCM, ``Least Common Muliple``)란 두 자연수의 공통된 배수 중 가장 작은 수이다.

- ex) LCM(8, 12) = 24

- 최소 공배수는 두 자연수의 곱을 최대 공약수로 나눈 몫입니다!
``LCM = a x b / GCD )``

- ``코드``로 나타내면 다음과 같습니다.
```java
public static int lcm(int a, int b, int gcd) {
  return (a * b) / gcd
}
```