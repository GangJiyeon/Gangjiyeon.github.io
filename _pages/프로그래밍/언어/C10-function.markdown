---
title: "[C언어] 함수(function)"
tags:
    - C언어기초
date: "2024-12-10"
thumbnail: "/assets/img/thumbnail/book.jpg"
---
이번에는 C언어의 함수(function)에 대해 알아보자.    



## **함수**
### **함수란**
**1) 함수란(function)**
* 특정한 작업을 처리하도록 작성한 프로그램 단위
* 필요한 입력을 받아 원하는 어떤 기능을 수행한 후 결과를 반환(return)하는 프로그램

<br>

**2) 함수의 종류**
* 라이브러리 함수(library function) 
	* 표준함수(standard function) 
	* 이미 개발환경에 포함되어 있는 함수
	* 함수 내부 구현 방법을 몰라도 입력값과 반환값만 이해하면 쉽게 사용 가능
* 사용자 정의 함수(user defined function)
	*  필요에 의해 개발자가 직접 개발하는 함수

<br>
<br>
<br>

---
## **사용자 정의함수**
### **함수정의와 호출**
**1) 사용자 정의함수 사용하기**
* 사용자 정의 함수를 사용하기 위해선 아래 3가지가 필요하다
	* `함수선언(function declaration)`
	* `함수호출(function call)`
	* `함수정의(function definition)`

```c
#include <stdio.h>

//함수선언
void massage();	//함수 원형
void cacao();	//함수 원형

int main(void)
{
	put("main function start");	//라이브러리 함수 호출
	massage();					//사용자 정의 함수 호출
	cacao();					//사용자 정의 함수 호출
	put("main function finish");
}

//함수정의
void massage()
{
	puts("\t메시지다!!!");
}

//함수정의
void cacao()
{
	puts("\t카톡!카톡!");
}
```

<br>
<br>


### **함수선언(function definition)**
**1) 함수선언의 필요성** 
* 정의된 함수를 호출하기 전, 함수를 선언하는 `함수원형(function prototype)`이 필요
* 함수의 사용을 미리 컴파일러에게 알림
* 프로그램을 이해하기 쉽게 도와 줌


**2) 함수선언 방법**  👉 `함수원형(function prototype)` 이용
* 함수원형: 함수를 선언하는 문장
* `반환형 함수이름(매개변수 목록);`
* 변수이름 생략가능

<br>
<br>

### **함수정의(function definition)**
**1) 함수정의란?** 함수머리(function header)와 함수몸체(function body)로 구성
* 함수머리(function header) : 반환형, 함수이름, 매개변수 목록으로 구성
	* 반환형: 함수 결과값의 자료형, 반환값이 없으면 `void`
	* 함수이름: 식별자 생성규칙을 따름
	* 매개변수 목록: `자료형 변수이름`의 쌍, `콤마(,)`로 구분
* 함수몸체(function body)
	* `{...}` 중괄호로 시작하여 중괄호로 종료
	* 함수가 수행해야할 문장을로 구성
	* 마지막은 대부분 결과값을 반환하는 return문장으로 종료(생략가능)

```c
//function header
//반환형 반환값이 없으면 void
반환형 함수이름(매개변수 목록)
{//function body
	stmt;

	//retuna 1;
	//return (a+b);
	//return ;
	//return 'a';
	return (반환연산식);
}
```

<br>
<br>

### **함수호출(function call)**
**1) 정해진 함수를 실행(호출)하려면** 
* 함수 호출(function call)이 필요
* 호출 시 괄호 안에 적절한 매개변수가 필요

```c
int max = findMax(a, b);
```







<br>
<br>
<br>

---
## **매개변수**
### **매개변수란**
**1) 매개변수(parameter)의 종류**
* 형식매개변수(formal parameters)
	* 함수 정의에서 기술되는 매개변수
	* 함수 내부에서만 사용될 수 있다
	> 함수호출 시 메모리에 형식인자변수가 메모리에 할당(allocation)되고, 함수가 종료되면 메모리에서 자동으로 제거(free, deallocation)
* 실매개변수(real marameter) = 실인자(real argument) = 인자(argument)
	

<br>

**2) 매개변수로 배열 사용하기** 👉 배열과 배열의 크기를 함께 전달
* 형식매개변수에서 배열 자차에 배열 크기를 기술하는 것은 의미가 없으므로 생략
* 함수내부에서 배열의 크기를 알 수 없으므로 배열의 크기를 하나의 인자로 사용

```c
//함수원형
int sumary(int array[], int n);

//함수정의
int sumary(int array[], int SIZE)
{

}

//함수호출
int i = sumary(data, 5);
```

<br>

**3) 매개변수로 2차원 배열 사용하기**
* 다차원 배열을 인자로 이용: 함수원형과 함수정의의 헤더에서 첫 번재 대괄호 내부의  크기를 제외한 다른 모든 크기를 반드시 기술

```c
//함수원형
double sum(double data[][3], int, int);

//함수정의
double sum(double data[][3], int rowsize, int colsize)
{

}

//함수호출
double sum_value = sum(x, rowsize, colsize);
```

<br>
<br>
<br>

---
## **라이브러리 함수**
### **라이브러리 함수와 헤더파일**
* c언에에는 라이브러리 함수를 위한 함수원형, 상수, 매크로가 헤더파일에 저장되어 있음

|헤더파일|처리작업|
|---|---|
|`stdio.h`|표준 입출력 작업|
|`math.h`|수학 관련 작업|
|`string.h`|문자열 작업|
|`time.h`|시간 작업|
|`ctype.h`|문자 관련 작업|
|`stdlib.h`|여러 유틸리티(텍스트를 수로 변환, 난수, 메모리 할당 등)함수

<br>
<br>

### **난수 라이브러리 함수**
* *난수(random number)란*    
> 특정한 나열 순서나 규칙을 가지지 않는 연속적인 임의의 수

<br>

**1) 함수 `rand()`**
* 함수원형 정의 : <stdlib.h>
* 0에서 32767사이의 정수 중에서 임의로 하나의 정수 반환

<br>
<br>

### **수학 관련 라이브러리 함수**
* `double sin(double x)` : 삼각함수 sin
*

<br>
<br>
<br>

