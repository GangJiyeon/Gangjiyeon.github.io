---
title: "[Java기초] 총정리 2 - 프로그램 구조, 메모리 영역, 기본 용어 "
tags:
    - Java기초
date: "2025-03-10"
thumbnail: "/assets/img/thumbnail/book.jpg"
---

저번 글에 이어서 자바의 프로그램 구조와 메모리 영역, 기본적인 용어를 정리해보도록 하자

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

우선 여기선 이렇게 생겼다~ 만 봐두도록 하고 이후 객체지향의 개념과 함께 추가적으로 정리하겠다


<br>
<br>
<br>

# **JVM의 메모리 영역(Java Virtual Machine Memory Area)**  

> JVM(Java Virtual Machine)은 자바 프로그램을 실행하기 위해 여러 개의 메모리 영역(5개)을 관리한다  
•  **메서드(Method) 영역 (또는 클래스 영역)**
•  **힙(Heap) 영역**
•  **스택(Stack) 영역**
•  **PC 레지스터(Program Counter Register)**
•  **네이티브 메서드 스택(Native Method Stack)**  

<br>


## JVM 메모리 영역의 종류

**메서드 영역 (Method Area)**
> **클래스 메타데이터를 저장하는 공간**

• JVM이 로드한 **클래스 정보, 정적(static) 변수, 상수, 메서드 코드, 인터페이스 정보** 등이 저장됨  
• 모든 스레드(Thread)가 공유하는 영역  
• **런타임 상수 풀(Runtime Constant Pool)** 포함 → 상수(리터럴, 상수 문자열) 저장  


```java
class Example {
    static int staticVar = 10; // 메서드 영역에 저장
}
```

<br>

**힙 영역 (Heap Area)**
> **객체(인스턴스)와 배열이 저장되는 공간**  

• `new` 키워드를 사용해 생성한 객체가 저장됨  
•  **가비지 컬렉션(GC, Garbage Collection)**에 의해 관리됨
•  모든 스레드가 공유하는 영역  

```java
class Example {
    int instanceVar = 20; // 힙 영역에 저장
}

public class Main {
    public static void main(String[] args) {
        Example obj = new Example(); // obj는 힙 영역에 저장
    }
}
```

<br>

**스택(Stack) 영역**
> **각 메서드 호출 시 생성되는 메모리 영역**

• 메서드 실행에 필요한 **지역 변수, 매개변수, 연산 중간값, 리턴 값** 등이 저장됨  
• 메서드 호출 시 **새로운 스택 프레임(Stack Frame)이 생성되고**, 메서드가 종료되면 제거됨  
• **스레드별로 개별적으로 존재 (스레드마다 하나의 스택을 가짐)**  


```java
public class Main {
    public static void main(String[] args) {
        int num = 10; // 스택 영역에 저장
        add(num); // add 메서드 호출 -> 새로운 스택 프레임 생성
    }

    public static void add(int x) {
        int result = x + 5; // 스택 영역에 저장
    }
}
```

<br>

**PC 레지스터 (Program Counter Register)**
> **JVM이 실행 중인 명령어 주소(현재 실행 중인 바이트코드 위치)를 저장하는 공간** 

• 스레드마다 하나씩 존재 → 각 스레드가 실행할 명령어의 위치를 추적  
• **자바 바이트코드 명령어를 순차적으로 실행할 때 사용됨**  

<br>

**네이티브 메서드 스택 (Native Method Stack)**
> **C, C++과 같은 네이티브 코드(C언어 기반 라이브러리)를 실행할 때 사용되는 스택**  

• `JNI(Java Native Interface)`를 통해 실행되는 네이티브 메서드 호출 시 사용됨  
•  예를 들어, **JNI를 사용하여 C++ 메서드를 호출할 때 사용됨**  


```java
public class Example {
    public native void nativeMethod(); // 네이티브 메서드 선언
}
```

<br>
<br>

## **JVM 메모리 구조 요약**
| 메모리 영역 | 역할 | 특징 |
|:---:|:---:|:---:|
| **메서드 영역 (Method Area)** | 클래스 정보, `static` 변수, 메서드 코드 저장 | 모든 스레드가 공유 |
| **힙 영역 (Heap Area)** | `new`로 생성한 객체 저장 | 모든 스레드가 공유, GC 관리 |
| **스택 영역 (Stack Area)** | 지역 변수, 메서드 호출 정보 저장 | 스레드별 개별 생성 |
| **PC 레지스터 (PC Register)** | 현재 실행 중인 명령어 주소 저장 | 스레드별 개별 존재 |
| **네이티브 메서드 스택 (Native Stack)** | 네이티브 코드(C, C++) 실행 | JNI 호출 시 사용 |

<br>
<br>

## **JVM 메모리 관리 - 가비지 컬렉션(GC)**
•  JVM은 **힙 영역의 불필요한 객체를 자동으로 제거(Garbage Collection)**  
•  GC는 더 이상 참조되지 않는 객체를 탐색하여 메모리를 해제  
•  `System.gc();`를 호출하여 GC 실행 요청 가능하지만, 보장되지 않음  

```java
Example obj1 = new Example();
Example obj2 = new Example();
obj1 = null; // obj1이 참조하는 객체는 GC 대상
```



<br>
<br>
<br>

# **키워드와 예약어**
---

자바에서 `키워드(Keyword)`와 `예약어(Reserved Word)`는 종종 같은 의미로 사용되는데, 엄밀히 따지면 약간 차이가 있다

<br>

## **키워드 VS 예약어**

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
> • 값을 생성하는 코드
• 변수를 포함한 연산자, 메서드 호출 등을 의미
• 항상 값으로 평가됨

<br>

## **문장**
> • 하나의 완전한 실행(명령)의 단위
• 세미콜론(;)으로 끝남
• 선언문, 실행문, 제어문 등이 포함됨

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




