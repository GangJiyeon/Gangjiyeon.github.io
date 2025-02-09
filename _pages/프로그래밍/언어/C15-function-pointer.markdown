---
title: "[C언어] 함수와 포인터 활용"
tags:
    - C언어기초
date: "2024-12-15"
thumbnail: "/assets/img/thumbnail/book.jpg"
---
이번에는 C언어의 함수와 포인터 활용에 대해 알아보자.    


## **함수의 인자전달 방식**
### **값에 의한 호출과 참조에 의한 호출**
**1) 함수에서 값의 전달**
* 값에 의한 호출(call by value)
	* 함수 호출 시 실인자의 값이 형식인자에 복사되어 저장
	* 함수 외부의 변수를 함수 내부에서 수정할 수 없음

<br>

**2) 함수에서 주소의 전달**
* 주소에 의한 호출(call by address)
	* 함수에서 주소를 전달해 호출하는 방식
	* 포인터를 매개변수로 사용하면 함수로 전달된 실인자의 주소를 이용해 해당 변수 참조 가능

<br>
<br>

### **배열의 전달**
**1) 배열의 전달**
* 함수의 매개변수로 배열 전달 
	* = 배열의 첫 원소의 주소를 매개변수로 전달(주소에 의한 호출)
	* 함수 내부에서 실인자로 전달된 배열의 배열크기를 알 수 없음(포인터 변수처럼 인식)

```c
//함수원형
double sum(double [], int i);	//배열 이름 생략 가능
double sum(double *, int i);	//포인터 이름 생략 가능
```

<br>

**2) 다양한 배열원소 참조 방법**

```c
int sum = 0;
int point[] = {95, 88. 76, 54, 85, 33};
int *address = point;
int aryLength = sizeof(point) / sizeof(int);

//배열 출력
for(int i = 0; i < aryLength; i++)
	sum += *(point+i);

for(int i = 0; i < aryLength; i++)
	sum += *(address++);

for(int i = 0; i < aryLength; i++)
	//error: point(배열이름)는 주소 상수
	//sum += *(point++);
```

<br>
<br>

### **가변인자**
**1) 가변인자가 있는 함수머리**
* `...` : 가변인자 매개변수
```c
//printf() 함수원형
int printf(const char *_Format, ...);	///... : 가변인자 매개변수
```

* 가변인자(variable argument) : 함수에서 인자의 수와 자료형이 결정되지 않은 함수 인자 방식
	* 처음(앞부분)의 매개변수는 정해져 있고, 중간 이후부터 마지막에 위치한 가변인자만 가능
	* `...` 첫 고정 매개변수 : 가변인자를 처리하는 데 필요한 정보를 지정
	
<br>

**2) 가변인자가 있는 함수 구현**
* 헤더파일 `stdadrg.h` 필요
* 4단계 : 가변인자 선언 > 가변인자 처리 시작 > 가변인자 얻기 > 가변인자 처리 종료
	* 가변인자 선언
	* 가변인자 처리 시작
	* 가변인자 얻기
	* 가변인자 처리 종료

```c
int sum(int numagrs, ...)
{
	//1. 가변인자 선언
	va_list argp;	//va_list로 변수 argp 선언
	
	//2. 가변인자 처리 시작
	va_start(argp, numagrs);

	//3. 가변인자 얻기
	...
	total += va_arg(argp, int);
	...
	
	//4. 가변인자 처리 종료
	va_end(argp);
};
```

<br>
<br>
<br>

---
## **포인터 전달과 반환**
### **함수 매개변수와 반환으로 포인터 사용**
**1) 주소연산자 &**
* 함수에서 매개변수를 포인터로 이용 : 주소에 의한 호출(call by address)

<br>

**2) 주소값 반환**
* 함수의 결과를 포인터로 반환
* 지역변수 주소값의 반환믄 문제가 발생할 수 있음

```c
int *add(int *psum, int a, int b)
{
	*psum = a + b;
	return psum;
}
```

<br>
<br>

### **상수를 위한 const 사용**
**1) 키워드 const**
* 수정을 원하지 않는 함수의 인자 앞에 키워드 `const` 삽입
* `const`의 위치

<br>
<br>

### **함수의 구조체 전달과 반환**
**1) 복소수를 위한 구조체**

```c
struct complex
{
	double real;	//실수
	double img;		//상수
};

typedef struct complex complex;
```

<br>

**2) 인자와 반환형으로 구조체 사용**
* 구조체도 자료형이므로 함수의 인자와 반환 값으로 이용 가능


<br>
<br>
<br>

---
## **함수 포인터와 void 포인터**
### **함수 포인터**
**1) 함수 주소 저장 변수**
* 포인터 : 하나의 포인터로 여러 변수를 참조하여 읽거나 쓰기 가능
* 함수 포인터(pointer to function) : 함수의 주소값을 저장하는 포인터 변수
	* 하나의 함수이름으로 필요에 따라 여러 함수를 사용가능
	* 반환형, 인자목록의 수와 각각의 자료형이 일치하는 함수의 주소를 저장할 수 있는 변수
	* 선언 시 함수원형에서 함수이름을 제외한 반환형과 인자목록의 정보 필요

```c
//함수 포인터 변수 선언
반환자료형 (*함수 포인터변수이름)(자료형1 매개변수명1, 자료형2 매개변수명2, ...);
반환자료형 (*함수 포인터변수이름)(자료형1, 자료형2, ...);

void add(double*, double, double);

//이름이 pf1인 함수 포인터 선언, add의 주소값 대입
//대입시 add, &add 가능, add() 불가능
void (*pf1)(double *z, double x, double y) = add;
```

<br>

**2) 함수 포인터를 이용한 함수 호출**


<br>
<br>

### **함수 포인터 배열**
**1) 함수 포인터 배열 개념**
* 함수포인터 배열(array of function pointer) : 함수 포인터가 원소인 배열

```c
int (*pfunary[3])(int, int);
//배열 pfunary가 가리키는 함수의 반환값은 int, 인자목록이 (int, int)
```

<br>

**2) 함수 포인터 배열 선언**

```c
반환자료형 (*배열이름[배열크기])(자료형1 매개변수명1, 자료형2 매개변수명2, ...);
반환자료형 (*배열이름[배열크기])(자료형1, 자료형2, ...);

void add(double*, double, double);
void subtract(double*, double, double);
void multiply(double*, double, double);
void devide(double*, double, double);

//1. 함수 포인터 배열 선언 후 초기화
void(*fpary[4])(double*, double, double);
fpary[0] = add;
fpary[1] = subtract;
fpary[2] = multiply;
fpary[3] = devide;

//2. 함수 포인터 배열 선언과 초기화를 동시에
void void(*fpary[4])(double*, double, double) = {add, subtract, multiply, devide};
```

<br>
<br>

### **void 포인터**
**1) void 포인터 개념**
* 포인터 : 가리키는 대상의 구제적인 자료형의 포인터로 사용하는 것이 일반적
	* 주소값 : 참조를 시작하는 주소에 불과, 자료형을 알아야 참조할 범위와 내용 해석 가능
* void 포인터 `(void *)`
	* 자료형을 무시하고 주소값만을 다루는 포인터
	* 대상에 상관없이 모든 자료형(일반변수, 배열, 구조체, 함수 등)의 주소를 저장 가능
	* 가리키는 변수를 참조하거나 수정이 불가능
	* 참조를 위해선 자료형 변환이 필요

```c
int m = 10;
double x = 3.98;

void *p = &m;
int n = *(int *)p;	//int *로 변환
n = *p				//오류

p = &x;				
int y = *(double *)p;	//double *로 변환
y = *p;					//오류
```
