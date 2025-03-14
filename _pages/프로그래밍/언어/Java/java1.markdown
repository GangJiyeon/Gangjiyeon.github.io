---
title: "[Java] 자바 기초 총정리"
tags:
    - Java기초
date: "2024-03-10"
thumbnail: "/assets/img/thumbnail/book.jpg"
---

이번에 학교에서 객체지향 프로그래밍 수업을 듣게되었는데,
자바개념을 다시 복습하는 것이 좋을 것 같아서 주요 개념을 몽땅 정리해보려고 한다

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



# **자료형**
---

|자료형 구분|종류|
|:---:|:---:|
|정수형|`byte(8bit)`, `short(16bit)`, `int(32bit)`, `long(64bit)`|
|실수형|`float(32bit)`, `double(64bit)`|
|문자형|`char(16bit)`|
|불리언형|`boolean(true, false)`|


<br>
<br>
<br>
