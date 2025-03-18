---
title: "[Java] 자바 기초 총정리 - 자바의 프로그램 구조, 기본 용어 정리"
tags:
    - Java기초
date: "2025-03-10"
thumbnail: "/assets/img/thumbnail/book.jpg"
---

저번 글에 이어서 자바의 프로그램 구조와 기본적인 용어를 정리해보도록 하자

<br>

# **자바의 프로그램 구조**
---

> 자바 프로그램은 클래스(Class) → 메서드(Method) → 문장(Statement) 으로 구성된다

```java
// 1. 패키지 선언 (필수는 아님)
package mypackage;

// 2. 클래스 선언
public class MyClass {

    // 3. main 메서드 (프로그램의 시작점)
    public static void main(String[] args) {
        
        // 4. 변수 선언 및 초기화
        int number = 10;  
        
        // 5. 메서드 호출
        printMessage(number);
    }

    // 6. 사용자 정의 메서드 (기능 정의)
    public static void printMessage(int num) {
        System.out.println("입력된 숫자: " + num);
    }
}
```

우선 여기선 이렇게 생겼다~ 만 봐두도록 하고 이후 개념을 추가적으로 정리하겠다

<br>
<br>
<br>

# **키워드와 예약어**
---

자바에서 `키워드(Keyword)`와 `예약어(Reserved Word)`는 종종 같은 의미로 사용되는데, 엄밀히 따지면 약간 차이가 있다

<br>

## **키워드란 VS 예약어**

|비교|키워드|예약어|
|:---:|:---:|:---:|
|정의|특정 기능을 수행하는 자바의 필수적인 단어|자바에서 미리 정의된 단어|
|변수/클래스/메서드명으로 사용|불가능|불가능|
|사용|모두 현재 사용|사용되고 있지 않은(미래에 사용될 수 있는) 단어도 존재|
|예시|`class`, `public` 등|키워드, `goto`, `const` 등 사용되지 않는 단어|

> 즉, 키워드는 `프로그래밍에 실제 사용되는 단어`이고, 예약어는 `단순히 예약된 단어 (키워드 + 현재 사용되지 않지만 미래를 위해 예약된 단어)`를 의미한다


<br>


## **키워드(예약어)의 종류**

|구분|키워드(예약어)|
|:---:|:---:|
|자료형|`byte`, `short`, `int`, `long`,`float`, `double`, `char`, `boolean`|
|제어문|`if`, `else`, `switch`, `case`, `default`, `while`, `do`, `for`, `break`, `continue`, `return`|
|접근제어자|`publice`, `private`, `protected`, `default(예약어X)`|
|클래스 및 객체|`class`, `interface`, `extends`, `implements`, `new`, `this`, `super`, `abstract`, `final`, `static`|
|예외 처리|`try`, `catch`, `finally`, `throw`, `throws`|
|패키지/임포트|`package`, `import`|
|예약어|`instanceof`, `enum`, `native`, `strictfp`, `transient`, `assert`|

<br> 
<br>
<br>

# **식(Expression)과 문장(Statement)**
---
## **식**
> 값을 생성하는 코드
변수를 포함한 연산자, 메서드 호출 등을 의미
항상 값으로 평가됨

<br>

## **문장**
> 하나의 완전한 실행(명령)의 단위
세미콜론(;)으로 끝남
선언문, 실행문, 제어문 등이 포함됨

|문장의 종류|설명|예시|
|:---:|:---:|:---:|
|선언문|변수선언|`int x;`|
|대입문|변수에 값 할당|`x = 10;`|
|제어문|흐름 제어 `(if, for, while)`|`if (x > 0) {}`|
|메서드 호출문|메서드 실행|`System.out.println(x);`|
|반환문|메서드 결과 반환|`return x;`|

<br>
<br>
<br>


