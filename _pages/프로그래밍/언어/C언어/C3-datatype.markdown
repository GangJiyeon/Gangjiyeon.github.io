---
title: "[C언어] C언어의 자료형"
tags:
    - C언어기초
date: "2024-12-03"
thumbnail: "/assets/img/thumbnail/book.jpg"
---
이번에는 C언어의 자료형(기본자료형)에 대해 알아보자.    


# 자료형(data type)
---

## 자료형이란? 

**1) 자료형이란** 
> 변수의 범위를 지정하는 키워드, 프로그래밍에서 자료를 식별하는 종류    

**2) 자료형의 종류** 

|자료형 구분|설명 및 종류|
|:---:|:---|
|기본자료형<br>(basic data type)|기본이 되는 자료형<br>▫️ 정수형 `short` `int` `long`  <br>▫️ 실수형 `float` `double` `long double`<br>▫️ 문자형 `char`  =>컴퓨터는 문자를 정수로 처리해 정수형 취급하기도 함<br>▫️ 무치형 `void`|
|유도형<br>(deprived data type)|기본형에서 나온 자료형 <br>`array; 배열` `pointer 포인터` `function 함수`|
|사용자정의형<br>(user defined data type)|기본형, 유도형을 이용해 사용자가 만드는 자료형<br>`enumiration 열거형` `structure 구조체` `union 공용체`|

👉 간혹 기본형, 유도형, 사용자정의형의 구분 방법 대신 기본형과 파생형(유도형, 사용자정의형)으로 구분하기도 함


<br>
<br>


## 정수형(integer types)


**1) 키워드** : `short` ≤ `int` ≤ `long`
* `int`: 기본 키워드
* `short`, `long`: 파생 키워드

> 왜 `short`, `int`, `long` 로 구분하여 사용할까?     
> * 다양한 범위의 정수를 저장하기 위해
> * 메모리 낭비를 줄이고, 저장이 되지 않는 것을 방지하기 위해    
> _(일반적으로 자료형의 사이즈가 크면 느려지고, 메모리 낭비가 생길 수 있음)_

<br>

**2) 부호**
* `signed` : _[부호가 있는]_, 양수 / 0 / 음수
* `unsigned` : 양수 / 0

<br>

**3) 특징**: 8진수, 10진수, 16진수 저장가능

||범위|C언어 표현법|예시|
|:---:|:---:|:---:|:---:|
|2진수|0, 1|없음|`0b11`|
|8진수|0-7|`%o`|`0101`|
|10진수|0-9|`&d`|`23456`|
|16진수|0-9, A-F|`%x`|`0x41`|

<br>

**4) 정수 자료형 정리**

|정수자료형|저장공간|내부표현|표현범위|
|:---:|:---:|:---:|:---:|
|signed short int|2byte|없음|-2^15 ~ 2^15-1|
|singed int|4byt|`%o`|-2^31 ~ 2^31-1|
|signed long int|4byt|`&d`|-2^31 ~ 2^31-1|
|unsigned short int|2byt|`%x`|0 ~ 2^16-1|
|unsigned int|4byt|`&d`|0 ~ 2^32-1|
|unsigned long int|4byt|`%x`|0 ~ 2^32-1|

> 참고
> * `signed short int` = `short int` = `int`
> * `signed int` = `int` = `signed`
> * `signed long int` = `long int` = `int`
> * `unsigned short int` = `unsigned short`
> * `unsigned int` = `unsigned`
> * `unsigned long int` = `unsigned long`

<br>
<br>
<br>


## 실수형(부동소수형, floating number data type)
**1) 실수형이란** 
> 실수를 표현하는 자료형
• `float` ≤ `double` ≤ `long double`
• 내부적으로 부동소수점 표현법을 사용 => `부동소수점수 (=부동소수)`
• 이진수로 인식
• 정수에 비해 더 큰 범위의 숫자 사용 가능

👉 부동소수란? 소수점 위치가 정해져 있지 않고 떠다니는 것

<br>

**2) 과학적 표기법(scientific notification)**
> 믿을 수 있는 숫자의 갯수

<br>

**3) 유효숫자란**
> 믿을 수 있는 숫자의 갯수

<br>

**4) 실수 자료형 정리**
• 메모리 내부 구성
• 실수 자료형 정리

|정수자료형|저장공간|내부표현|정수 유효자리수|
|:---:|:---:|:---:|:---:|
|float|4byte|없음|6-7|
|double|8byte|`%o`|15-16|
|long double|8byte|`&d`|15-16|

<br>
<br>
<br>


## 문자형(char)
**1) 문자형이란** 
> charater(문자)의 약자)


