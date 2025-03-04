---
title: "[C언어] C언어의 변수"
tags:
    - C언어기초
date: "2024-12-02"
thumbnail: "/assets/img/thumbnail/book.jpg"
---
이번에는 C언어의 변수 선언, 변수 초기화에 대해 알아보자.    


<br>

# **변수**
---
## **변수(variables)란?**

**1) 변수란** 
> 프로그래밍에서 고유한 이름이 있는 자료 값을 저장하는 공간    
• 변수에는 고유한 이름이 붙여지고, 물리적으로는 기억장치인 메모리(ram)에 위치하게 됨
• 즉, 메모리 주소를 사용해서 변수에 데이터를 저장하고, 접근하여 저장된 데이터를 사용할 수 있다     

**2) 변수의 3요소** 
> 주요 정보인 `변수이름`, `변수의 자료형`, `변수 저장 값`     

```c
int num = 30;

// int: 변수 자료형, 그대로 유지
// num: 변수 이름, 그대로 유지
// 30: 변수 저장값, 저장값이 바뀔 수 있음 => 변수
```


**3) 변수의 특징**
• 자료형을 가짐 => 자료형에 따라 공간 크기, 자료값 범주 결정
• 저장되는 값 수정 가능, 마지막 값만 유지

**4) 변수의 사용** 👉 변수 선언 후 초기화

<br>
<br>
<br>

# **변수 선언(variables declaration)**
---
## **변수 선언이란?**
> 프로그램에서 변수를 사용하기 위해서는 원칙적으로 사용 전에 먼저 `변수 선언(variables declaration)` 과정이 반드시 필요하다.

**1) 변수 선언(variables declaration)**     
* 컴파일러에게 프로그램에서 사용할 저장공간에 `변수 (자료형, 변수이름)`를 알리는 것    
* 변수 선언을 하게 되면 `컴파일러`는 실제 변수 선언 문장에 맞는 저장 영역을 `메모리`에 확보     
* 프로그래머가 선언한 변수를 사용하겠다는 약속의 의미   
* 변수 선언 이후, 지정한 변수이름으로 값을 저장하거나 값을 참조 가능

  
<br>

**2) 변수 선언하기**

```c
/*변수 선언문 형태*/
자료형키워드 변수명;

/*변수 선언*/
double height; //double=>자료형, height=>변수명

/*같은 자료형, 여러 개 변수 선언*/
int math, eng, ko;
```

<br>

**3) 변수 이름 작성 규칙**    
* 사용 가능한 문자: `영어알파벳`, `숫자`, `밑줄(_)`로 구성
* **시작 문자**: `영어알파벳`, _`밑줄(_)`_ 
* **불가능**: `키워드` 사용 불가능, `공백` 불가능
* 누구나 이해할 수 있게 변수에 저장되는 값의 목적에 맞는 이름과 적당한 길이로 작성

> _`밑줄(_)`_: (라이브러리에서 밑줄로 시작하는 변수 이름을 종종 사용하기 때문에 밑줄로 시작하는 변수 이름을 선언하지 않는 것이 좋음)

<br>

**4) 위치제한**
* Ansi 99 이전: 변수 선언 후 다른 문장(블럭 도입부에 변수 선언)
* Ansi 99 이후: 변수 사용 전


<br>
<br>
<br>  
  
# **변수 초기화**
---

## **변수 초기화란?**
**1) 변수 초기화** 👉 변수를 선언한 이후에 값을 저장하는 것
* **변수선언 후 초기화**: 변수를 선언한 뒤에 변수명 이후에 `대입연산자 =` 을 사용해 변수 초기화를 한다

```c
int year;
year = 2024;
```

* **변수선언 및 초기화**: 변수를 선언하면서 변수명 이후에 `대입연산자 =` 을 사용해 변수 초기화를 한다

```c
int year = 2024;
```

<br>


**2) 대입연산자 '='**
* **대입연산자** : `=`
* **대입문(assignment statement)**: 대입 연산이 있는 문장
* `year <- 2024`의 의미

```c
int year = 2024;
```

> _`* 지역변수(local variables):`_ 
> • 함수 내부에서 선언된 변수    
> • 초기화하지 않으면 저장값 정의X(의미 없는 쓰레기값 저장) => 참조시 `c4700 컴파일 오류`


<br>
<br>
<br>

# **변수의 이용**
---
**1) 문장에서 변수의 의미**    
• 저장공간 자체
• 저장공간에 저장된 값

```c
int num = 3;

// num   => 저장공간 사용
// 3     => 저장공간에 저장된 값의 사용
```
 
<br>

**2) L-value와 R-value**

|L-value|R-value|
|:----|:----|
|left locate value, object local value|right locate value, value of and expression|
|메모리를 차지하고 있는 특정 데이터 객체(개체)|수정가능한 L-value에게 대입될 수 있는 값|
|R-value가 될 수 있음|L-value가 될 수 없음|
|(data)object 여야 함||

> _`* (data)object`_     
&nbsp;메모리에 있는 데이터들을 오브젝트 형태라고 부른다. 오브젝트 형태는 메모리에 자기 자리가 있다.

```c
const int TWO = 2;          // TWO => 수정가능한 L-value
int a, b, c;                // a, b, c => 수정가능한 L-value
a = 24;                     // 24 => R-value
b = a;
c = TWO * TWO (a + b);      // a + b => R-value
```
