![](https://velog.velcdn.com/images/harinnnnn/post/82402102-b3bd-44f2-97eb-98437254994d/image.png)

<br>

## μμνλ©°...ππ»ββοΈ
π μλ°μμλ λͺ¨λ  λ³μμ νμμ μ μνκ³  μμΌλ©°, λ³μκ° κ°μ§λ νμμ λ°λΌ λ΄μ μ μλ κ°μ μ’λ₯κ° λ¬λΌμ§λλ€. λ³μ νμκ³Ό κ°μ μλ‘μκ² μνΈλ³΄μμ μΈ μμμλλ€. ```μλ§μ νμ κ°μ μ λ¬ν΄μΌλ§ κ°μ μ μμ μΌλ‘ μ μ₯ν  μ μκ² λ©λλ€!```

π λ³μ νμμ ν¬κ² **κΈ°λ³Έν(primitive)**, **μ°Έμ‘°ν(Reference type)** μΌλ‘ κ΅¬λΆν  μ μμ΅λλ€. 

---

<br>

## π κΈ°λ³Έν(Primitive type)

<br>

κΈ°λ³Ένμ μ€μ  κ°(λ°μ΄ν°)λ₯Ό λ΄μ μ μλ λ³μμ νμμλλ€. κΈ°λ³Ένμ κ°μλ μ΄ 8κ°λ‘ κ΅¬λΆνλ©° ν¬κ²λ λΌλ¦¬ν, λ¬Έμν, μ μν, μ€μνμΌλ‘ κ΅¬λΆν  μ μμ΅λλ€.

<br>


>- **λΌλ¦¬** : boolean
>- **λ¬Έμ** : char
>- **μ«μ** : **μ μ**(byte, short, int, long
>- **μ€μ**(float, double)

**π¦· λΌλ¦¬ν λ³μ νμ (boolean)**
: λΌλ¦¬μ μ°Έκ³Ό κ±°μ§μ μλ―Έν©λλ€. ```true```, ```false``` μ€ νλμ κ°μ μ μ₯ν©λλ€.

**π¦· λ¬Έμν λ³μ νμ (char)**
: λ¬Έμ(charCharacter)λ₯Ό μ μ₯ν©λλ€.


**π¦· μ μν λ³μ νμ (byte, short, int, long)**
: μ μ(Integer)λ‘ ννλλ μ«μλ₯Ό μ μ₯ν©λλ€.

**π¦· μ€μν λ³μ νμ (double, float)**
: μ€μ(Floating point)λ‘ ννλλ μ«μλ₯Ό μ μ₯ν©λλ€.

---

<br>

### π κΈ°λ³Έν λ³μμ ν¬κΈ°

<br>

|λΆλ₯,ν¬κΈ°|1|2|4|8
|---|---|---|---|---|
λΌλ¦¬ν|boolean
λ¬Έμν||char
μ μν|byte|short|int|long
μ€μν|||float|double

---

<br>

## π νλ³ν(Casting)

<br>

π Javaμμ μ°μ°μ "2(byte) + 3(byte)"μ κ°μ΄ λμΌν λ°μ΄ν° νμμμ κ°λ₯ν©λλ€.

νμ§λ§, νλ‘κ·Έλ¨μ λ§λ€λ€ λ³΄λ©΄ "2(byte) + 3.5(double)"κ³Ό κ°μ΄ μλ‘ λ€λ₯Έ λ°μ΄ν° νμλΌλ¦¬μ μ°μ°μ΄ νμν  λκ° μμ΅λλ€. μ΄λ΄κ²½μ° λ³μμ λ°μ΄ν° νμμ λ°κΏμ£Όλ μμμ΄ νμνλ°, μ΄κ²μ΄ ```λ°μ΄ν° νμμ νλ³ν(νμλ³ν)```μλλ€.

π νλ³νμ μν©μ λ°λΌμ, νΉμ νμμ λ°λΌμ ```μλ£ν(data type)μ΄ λ€λ₯Έ κ²μΌλ‘ λ³νλλ κ²```μ λ§ν©λλ€. νΉλ³ν κ²½μ°μ **μλμ **μΌλ‘ λ°μνκΈ°λ νλ©°, **κ°μ **λ‘ κ°λ°μκ° λ³νμν¬ μλ μμ΅λλ€.

### π μλνλ³ν (Promotion, μλ¬΅μ  νλ³ν)
- λ°μ΄ν° μμ€μ΄ μλ νμμ μλμΌλ‘ νλ³νλ¨.
- μμ λ©λͺ¨λ¦¬ ν¬κΈ°μ νμμ ν° λ©λͺ¨λ¦¬ ν¬κΈ°μ νμμΌλ‘ λ³νν¨
(λ¨, λ©λͺ¨λ¦¬ ν¬κΈ°μ κ΄κ³ μμ΄ μ μλ λͺ¨λ  μ€μ λ°μ΄ν° νμμ μλμ μΌλ‘ νλ³νμ΄ κ°λ₯νλ€.)
- μλ νλ³νμ΄ μ΄λ£¨μ΄μ§λ μμ
	- byte(1) < short(2) < int(4) < long(8) < float(4) < double(8)

---

<br>

### π κ°μ νλ³ν(Casting)

<br>

>λ©λͺ¨λ¦¬ ν¬κΈ°κ° ν° λ³μ μμ λ³ννκ³ μ νλ λ°μ΄ν° νμμ κ΄νΈμ κ°μΈ μ λλ€

<br>

- **μμ ν¬κΈ° νμ = (μμ ν¬κΈ° νμ) ν° ν¬κΈ° νμ**


---

<br>

## π μ°μ°μ

<br>

### π μ£Όμ μ°μ°μ
---

### π μ°μ  μ°μ°μ(arithmetic operator)

μ°μ  μ°μ°μλ μ¬μΉ μ°μ°μ λ€λ£¨λ μ°μ°μλ‘, κ°μ₯ κΈ°λ³Έμ μ΄κ³  λ§μ΄ μ¬μ©λλ μ°μ°μμλλ€. νΌμ°μ°μλ€μ κ²°ν© λ°©ν₯μ μΌμͺ½μμ μ€λ₯Έμͺ½μλλ€.

|μ°μ μ°μ°μ|μ€λͺ|
|---|---|
+|λνκΈ°
-|λΉΌκΈ°
*|κ³±νκΈ°
/|λλ λͺ«
%|λλ λλ¨Έμ§

---

### π λλ¨Έμ§ μ£Όμ μ°μ°μ

|μ°μ°μ|μμ|
---|---
λμ|=, +=, -=, *=, /=, ^= λ±
μ¦κ°|++,--
λΉκ΅|==, !=, >, <, <=, >= λ±
λΌλ¦¬| !, &, && λ±
λΉνΈ| ~, &, ^
μ¬ννΈ| <<, >>, >>>
μΌν­μ°μ°μ|(μ‘°κ±΄μ) ? A:B

---

### π instanceof μ°μ°μ

κ°μ²΄ νμμ νμΈνλ μ°μ°μμ΄λ€. νλ³ν μ¬λΆλ₯Ό νμΈνλ©°, true, falseλ‘ κ²°κ³Όλ₯Ό λ°ννλ€. μ½κ² λ§ν΄, **ν΄λΉ ν΄λμ€κ° μκΈ° μ§μ΄ λ§λμ§ νμΈ**ν΄μ£Όλ μ°μ°μμ΄λ€.

``κ°μ²΄ instanceof ν΄λμ€``λ₯Ό μ μΈν΄ μ¬μ©νλ€!