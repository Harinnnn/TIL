## ✏️ Map

맵은 ``키(Key)``와 ``값(Value)`` 두 쌍으로 데이터를 보관하는 자료구조다. 키는 맵에 오직 유일하게 있어야합니다.

---


## ✏️ HashMap

- HashMap은 Map 인터페이스를 구현한 대표적인 Map 컬렉션이다. Map 인터페이스를 상속하고 있기에 Map의 성질을 그대로 가지고 있다.
- 많은 양의 데이터를 검색하는 데 있어서 뛰어난 성능을 보인다.
- 값은 중복 저장될 수 있지만 키는 중복 저장될 수 없다. 만약 기존에 저장된 키와 동일한 키로 값을 저장하면 기존의 값은 없어지고 새로운 값으로 대치된다. 

---

## 📍 HashMap 선언 방법

```java
HashMap<String,String> map1 = new HashMap<String,String>();//HashMap생성
HashMap<String,String> map2 = new HashMap<>();//new에서 타입 파라미터 생략가능

HashMap<String,String> map4 = new HashMap<>(10);//초기 용량(capacity)지정
HashMap<String,String> map6 = new HashMap<String,String>(){{//초기값 지정
    put("a","b");
}};
```

HashMap을 생성하려면 키 타입과 값 타입을 파라미터로 주고, 기본생성자를 호출하면 된다.
- HashMap은 저장공간보다 값이 추가로 들어오면 List처럼 저장공간을 추가로 늘리는데 List처럼 저장공간을 한 칸씩 늘리지 않고 약 두배로 늘린다.  여기서 과부하가 많이 발생하기 때문에 초기에 저장할 데이터 개수를 알고 있다면 Map의 초기 용량을 지정해주는 것이 좋다.

---

## 📍 HashMap 값 추가

```java
HashMap<Integer,String> map = new HashMap<>();//new에서 타입 파라미터 생략가능
map.put(1,"사과"); //값 추가
map.put(2,"바나나");
map.put(3,"포도");
```

HashMap에 값을 추가하려면 **put(key,value)** 메소드를 사용한다. **선언 시 HashMap에 설정해준 타입과 같은 타입의 Key와 Value값**을 넣어야 하며 만약 입력되는 키 값이 HashMap 내부에 존재한다면 기존의 값은 새로 입력되는 값으로 대치됩니다. (키 값은 중복 선언 불가)

---
## 📍 HashMap 값 삭제

```java 
HashMap<Integer,String> map = new HashMap<Integer,String>(){{//초기값 지정
    put(1,"사과");
    put(2,"바나나");
    put(3,"포도");
}};
map.remove(1); //key값 1 제거
map.clear(); //모든 값 제거

```

remove() 메소드를 사용하면 오직 key 값으로만 Map의 요소를 삭제할 수 있다.

---

## 📍 HashMap 값 출력

```java
//KeySet() 활용
for(Integer i : map.keySet()){ //저장된 key값 확인
    System.out.println("[Key]:" + i + " [Value]:" + map.get(i));
}
//[Key]:1 [Value]:사과
//[Key]:2 [Value]:바나나
//[Key]:3 [Value]:포도
```