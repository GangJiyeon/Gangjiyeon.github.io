---
title: "[Java기초] 총정리 3 - 자료형, 연산자, 제어문"
tags:
    - Java기초
date: "2025-03-11"
thumbnail: "/assets/img/thumbnail/book.jpg"
---

# **자료형**
---

## **자료형이란?**

> `자료형(Data Type)`은 `변수에 저장할 수 있는 값의 종류`를 정의하며, 크게 **기본 자료형(Primitive Type)**과 **참조 자료형(Reference Type)**으로 나뉜다

|구분|기본자료형|참조자료형|
|:---:|:---:|:---:|
|저장방식|값 자체를 저장|객체의 주소값 저장|
|크기|고정 크기|동적 크기 가능|
|메모리 저장영역|스택(stack)|힙(heap)|
|기본값|`0`, `false` 등|`null`|

<br>

## **기본자료형**
> 자바에서 직접 값을 저장하는 데이터 타입

|자료형 구분|종류|
|:---:|:---:|
|정수형|`byte`: 1byte, default 0, -128 ~ 127 <br>`short`: 2byte, default 0, -32,768 ~ 32,767 <br> `int`: 4byte, default 0, -2,147,483,648 ~ 2,147,483,647 <br>`long`: 8byte, default 0L, -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807|
|실수형|`float`: 4byte, default 0.0f, 32비트 부동소수점 (소수점 이하 약 7자리 정밀도) <br>`double`: 8byte, default 0.0d, 64비트 부동소수점 (소수점 이하 약 15자리 정밀도)|
|문자형|`char`: 2byte, default \u0000, 유니코드 문자 (0~65535)|
|불리언형|`boolean`: 1byte, default false, true, false|

<br>

## **참조자료형**
> 객체의 주소값을 저장하는 타입

(1) 배열 (array): 같은 타입의 데이터를 연속적(메모리상 연속된 공간에)으로 저장하는 자료구조
• 한 번 크기를 정하면 변경할 수 없음
• 배열 사용하기

```java
/* 배열 선언 후 초기화 */
// 배열 선언하기
int[] numbers;  // 권장
int numbers2[]; // 비권장, 하지만 가능

// 배열 초기화(Initialization) > 할당
int [] numbers = new int[5];    // java default값을 초기값으로 지정
````

```java
/* 배열 선언과 초기화를 동시에 */
// 방법 1: 배열 리터럴 사용
int[] numbers = {1, 2, 3, 4, 5};    // 명시적으로 초기화(할당)

// 방법 2: new 연산자 사용
int[] numbers2 = new int[]{10, 20, 30};

// 방법 3: 개별 값 할당
int[] numbers3 = new int[3];
numbers3[0] = 100;
numbers3[1] = 200;
numbers3[2] = 300;
```

• 2차원 배열 사용하기

```java
// 2차원 배열 선언 및 크기 지정
int[][] matrix = new int[3][3];  // 3x3 배열 (초기값: 0)

// 2차원 배열 초기화 (직접 할당)
int[][] matrix2 = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// 개별 요소 접근
matrix[0][0] = 10;  // 첫 번째 행, 첫 번째 열 값 변경

```

<br>


(2) 클래스(class): 사용자가 정의한 객체를 생성하는 데이터 타입

```java
class Person {
    String name;
    int age;
}
````

<br>

(3) 인터페이스(interface): 다형성을 구현하기 위해 사용하는 참조형 타입

```java
interface Animal {
    void makeSound();
}
````

<br>


(4) 문자열(string): 문자들의 집합이며, `String` 클래스의 객체로 취급됨

```java
String message = "Hello, Java!";
```

class, 인터페이스, 문자열은 이후의 글에서 더 알아보도록 하자

<br>
<br>
<br>

# **자바의 연산자(Operators)**
---
자바의 연산자는 **기능에 따라 6가지 유형**으로 나뉜다

<br>

## **산술 연산자 (Arithmetic Operators)**
> 숫자에 대한 기본적인 계산을 수행하는 연산자

|연산자|설명|예제|결과|
|:---:|:---:|:---:|:---:|
|`+`|덧셈|`5 + 3`|`8`|
|`-`|뺄셈|`5 - 3`|`2`|
|`*`|곱셈|`5 * 3`|`15`|
|`/`|나눗셈(몫)|`10 / 3`|`3`(정수 나눗셈, 소수점 이하 버림)|
|`%`|나머지|`10 % 3`|`1`|

<br>

## **대입 연산자 (Assignment Operators)**
> 변수에 값을 저장할 때 사용되는 연산자

|연산자|설명|예제|결과|
|:---:|:---:|:---:|:---:|
|`=`|값 할당|`x = 10;`|`x`가 `10`이 됨|
|`+=`|더한 후 할당|`x += 5;`|`x = x + 5`|
|`-=`|뺀 후 할당|`x -= 3;`|`x = x - 3`|
|`*=`|곱한 후 할당|`x *= 2;`|`x = x * 2`|
|`/=`|나눈 후 할당|`x /= 2;`|`x = x / 2`|
|`%=`|나머지 후 할당|`x %= 3;`|`x = x % 3`|


<br>

## **비교 연산자 (Comparison Operators)**
> 두 값을 비교하고 boolean 값(`true` 또는 `false`)을 반환

|연산자|설명|예제|결과|
|:---:|:---:|:---:|:---:|
| `==` | 두 값이 같은지 비교 | `5 == 3` | `false` |
| `!=` | 두 값이 다른지 비교 | `5 != 3` | `true` |
| `>` | 왼쪽이 큰지 비교 | `5 > 3` | `true` |
| `<` | 오른쪽이 큰지 비교 | `5 < 3` | `false` |
| `>=` | 왼쪽이 크거나 같은지 비교 | `5 >= 5` | `true` |
| `<=` | 오른쪽이 크거나 같은지 비교 | `5 <= 3` | `false` |

<br>

## **논리 연산자 (Logical Operators)**
> 조건문에서 주로 사용되며, **true 또는 false 값을 반환**

|연산자|설명|예제|결과|
|:---:|:---:|:---:|:---:|
| `&&` | AND (둘 다 `true`이면 `true`) | `(5 > 3) && (10 > 2)` | `true` |
| `||` | OR (하나라도 `true`이면 `true`) | `(5 > 3) || (10 < 2)` | `true` |
| `!` | NOT (반대값 반환) | `!(5 > 3)` | `false` |

<br>

## **비트 연산자 (Bitwise Operators)**
> **2진수 비트 단위**로 연산을 수행하는 연산자

|연산자|설명|예제(`a=5`, `b=3`)|결과|
|:---:|:---:|:---:|:---:|
| `&` | 비트 AND | `5 & 3` | `1` (0101 & 0011 = 0001) |
| `|` | 비트 OR | `5 | 3` | `7` (0101 | 0011 = 0111) |
| `^` | 비트 XOR | `5 ^ 3` | `6` (0101 ^ 0011 = 0110) |
| `~` | 비트 NOT | `~5` | `-6` (비트 반전) |
| `<<` | 왼쪽 시프트 | `5 << 2` | `20` (5 × 2²) |
| `>>` | 오른쪽 시프트 | `5 >> 1` | `2` (5 ÷ 2¹) |

<br>

## **증감 연산자 (Increment & Decrement)**
> **변수의 값을 1 증가 또는 감소시키는 연산자**

|연산자|설명|예제|결과|
|:---:|:---:|:---:|:---:|
| `++` | 1 증가 | `x++` 또는 `++x` | `x = x + 1` |
| `--` | 1 감소 | `x--` 또는 `--x` | `x = x - 1` |


<br>

## **삼항 연산자 (Ternary Operator)**
> **간단한 조건문 대체**

```java
조건 ? 참일 때 값 : 거짓일 때 값;
```


<br>
<br>
<br>

# **자바의 제어문**
---

**제어문이란?**

> 자바에서 제어문`Control Statement`은 프로그램의 흐름을 제어하는 문장으로 조건문, 반복문, 분기문으로 나뉜다

<br>

**제어문의 종류**
| 분류 | 종류 | 설명 |
|:---:|:---:|:---:|
| **조건문** | `if`, `if-else`, `switch` | 특정 조건에 따라 코드 실행 |
| **반복문** | `for`, `while`, `do-while` | 특정 조건 동안 반복 실행 |
| **분기문** | `break`, `continue`, `return` | 반복문 또는 메서드 실행 흐름 변경 |

<br>
<br>

## **조건문(Conditional Statements)**  
> 조건문은 **특정 조건을 만족할 때만 코드가 실행**되도록 한다

**(1) if 문**
• **조건이 `true`일 때 코드 블록 실행**
• 중괄호 `{}` 없이 단일 문장 실행 가능 (비추천)

```java
if (조건식) {
    // 실행될 코드
}
```

```java
int age = 20;
if (age >= 18) {
    System.out.println("성인입니다.");
}
```

<br>

**(2) if-else 문**
• **조건이 `true`이면 `if` 블록 실행, `false`이면 `else` 블록 실행**

```java
if (조건식) {
    // 참일 때 실행될 코드
} else {
    // 거짓일 때 실행될 코드
}
```

```java
int age = 16;
if (age >= 18) {
    System.out.println("성인입니다.");
} else {
    System.out.println("미성년자입니다.");
}
```

<br>

**(3) if-else if-else 문**
• 여러 개의 조건을 검사할 때 사용
• 위에서부터 차례대로 검사하며, 첫 번째 `true` 조건이 실행되면 나머지는 실행되지 않음

```java
if (조건1) {
    // 조건1이 참일 때 실행
} else if (조건2) {
    // 조건2가 참일 때 실행
} else {
    // 모든 조건이 거짓일 때 실행
}
```

```java
int score = 85;

if (score >= 90) {
    System.out.println("A 학점");
} else if (score >= 80) {
    System.out.println("B 학점");
} else if (score >= 70) {
    System.out.println("C 학점");
} else {
    System.out.println("F 학점");
}
```

<br>

**(4) switch 문**
• 여러 개의 조건을 비교할 때 사용 (`==` 비교만 가능)
• `case` 값과 비교하여 일치하는 경우 실행  
• `break`를 사용하여 실행 종료 (없으면 다음 `case`까지 실행됨)
• `default`는 모든 `case`가 일치하지 않을 때 실행

```java
switch (변수) {
    case 값1:
        // 실행될 코드
        break;
    case 값2:
        // 실행될 코드
        break;
    default:
        // 위 조건에 해당하지 않을 경우 실행
}
```

```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("월요일");
        break;
    case 2:
        System.out.println("화요일");
        break;
    case 3:
        System.out.println("수요일");
        break;
    default:
        System.out.println("기타 요일");
}

// 수요일 출력
```

---

## **반복문(Loop Statements)**
> 반복문은 특정 조건이 참인 동안 코드를 반복 실행한다

**(1) for 문**
• 반복 횟수가 정해진 경우 사용
• `초기식 → 조건식 → 실행 → 증감식` 순서로 실행

```java
for (초기식; 조건식; 증감식) {
    // 반복 실행될 코드
}
```

```java
for (int i = 1; i <= 5; i++) {
    System.out.println("Hello, Java! " + i);
}

/*
Hello, Java! 1
Hello, Java! 2
Hello, Java! 3
Hello, Java! 4
Hello, Java! 5
*/
```

<br>

**(2) while 문**
•  **조건이 `true`인 동안 계속 반복**
• 반복 횟수가 정해지지 않은 경우 사용

```java
while (조건식) {
    // 반복 실행될 코드
}
```

```java
int i = 1;
while (i <= 5) {
    System.out.println("반복 횟수: " + i);
    i++;
}
```

<br>

**(3) do-while 문**
• `while`과 동일하지만, **최소 1번은 실행됨** (조건 검사 전에 실행)

```java
do {
    // 최소 1회 실행될 코드
} while (조건식);
```

```java
int i = 1;
do {
    System.out.println("반복 횟수: " + i);
    i++;
} while (i <= 5);
```

<br>
<br>

## **분기문 (Break / Continue / Return)**
> 분기문은 **제어문의 흐름을 변경**하는 역할을 한다

**(1) break 문**
• 반복문을 즉시 종료하고 빠져나옴
• `switch` 문에서도 사용됨

```java
for (int i = 1; i <= 10; i++) {
    if (i == 5) {
        break;  // i가 5면 반복문 종료
    }
    System.out.println(i);
}
/*
1
2
3
4
*/
```

<br> 

**(2) continue 문**
• 현재 반복을 건너뛰고 다음 반복으로 이동

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue;  // i가 3이면 건너뛰고 다음 반복 실행
    }
    System.out.println(i);
}
/*
1
2
4
5
*/
```
<br>

**(3) return 문**
• 메서드를 즉시 종료하고 호출한 곳으로 돌아감
• 반환값이 있는 경우 `return 값;` 사용

```java
public static int add(int a, int b) {
    return a + b;  // 실행 후 결과 반환
}
```

