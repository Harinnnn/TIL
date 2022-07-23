## ✏️ ArrayList

ArrayList는 자바에서 기본적으로 많이 사용되는 클래스입니다. 일반 배열과 동일하게 ``연속된 메모리 공간을 사용``하며 ``인덱스는 0부터`` 시작합니다.

배열과의 차이점은 배열의 크기는 고정인 반면 ArrayList는 **크기가 가변적으로 변하는 동적 배열**입니다.

내부적으로 저장이 가능한 메모리 용량(Capacity)이 있으며 현재 사용 중인 공간의 크기(Size)가 있습니다. 만약 가용량 이상을 저장하려고 하면, 더 큰 공간의 메모리를 새롭게 할당한다.

---

## 📍 ArrayList 생성

- ArrayList를 사용하기 위해서는 먼저 import 해야 합니다.
```java
import java.utill.ArrayList;
```
```java
ArrayList<Integer> arr = new ArrayList<>();
```
---

## 📍 함께 사용하는 메서드

- **add()** : 엘리먼트 추가
- **set()** : 기존에 추가된 값 변경
- **remove()** : 추가했던 값 삭제
- **clear()** : ArrayList 안의 내용 전체 삭제

```java
변수명.add(0, "LG"); // 1번째에l LG라는 값을 추가한다

변수명.set(1, "Apple"); // 2번째 값을 Apple로 변경한다

변수명.remove(3) //4번째 값 삭제
변수명.remove("Samsung") // Samsung이라는 값 삭제

변수명.clear(); 모든 값 삭제.

```

>**🌏 ArrayList에서 값이 삭제되면, 삭제된 자리가 비지 않고 가변적으로 뒤의 요소들이 밀려서 들어가게 된다. (동적배열이기 때문)**
<br>**ex)** [ 1,2,3,4,5 ] 에서 4를 삭제하면, [ 1,2,3,null,5 ] 가 아니라 [ 1,2,3,5 ]가 된다.

---

## 📍 ArrayList 전체 값 확인

ArrayList의 모든 값들을 순회해서 출력하고 싶은 경우 다양한 방법을 사용할 수 있다.

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Iterator;
import java.util.ListIterator;

public class ArrayListTest {
    public static void main(String[] args) {
        ArrayList<String> colors = new ArrayList<>(Arrays.asList("Black", "White", "Green", "Red"));
        
        // for-each loop
        for (String color : colors) {
            System.out.print(color + "  ");
        }
        System.out.println();

        // for loop
        for (int i = 0; i < colors.size(); ++i) {
            System.out.print(colors.get(i) + "  ");
        }
        System.out.println();

        // using iterator
        Iterator<String> iterator = colors.iterator();
        while (iterator.hasNext()) {
            System.out.print(iterator.next() + "  ");
        }
        System.out.println();

        // using listIterator
        ListIterator<String> listIterator = colors.listIterator(colors.size());
        while (listIterator.hasPrevious()) {
            System.out.print(listIterator.previous() + "  ");
        }
        System.out.println();
    }
}

```

listIterator의 경우 생성 시 ArrayList의 크기를 입력해주고 역방향으로 출력한다.

---

## 📍 값 존재 유무 확인

>- 값이 존재하는지 알고 싶은 경우 ``contains()``를 사용합니다.
<br>contains()는 값이 있는 경우 true를, 값이 없는 경우 false를 리턴합니다.

>- 값이 존재할 때, 어느 위치에 존재하는지 알고 싶은 경우 ``indexOf()``를 사용할 수 있습니다.
<br>indexOf()는 값이 존재하는 경우 해당 엘리먼트의 인덱스를 리턴합니다.

