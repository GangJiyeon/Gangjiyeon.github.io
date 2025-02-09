---
title: "[C언어] 제어문(조건문, 분기문, 반복문)"
tags:
    - C언어기초
date: "2024-12-08"
thumbnail: "/assets/img/thumbnail/book.jpg"
---
이번에는 C언어의 제어문(조건문, 분기문, 반복문)에 대해 알아보자.    


# **제어문(Control Statement)**
---

## **제어문이란**
**1) 제어문이란?** 순차적인 실행뿐만 아니라 선택과 반복 등 순차적인 실행을 변경하여 프로그램의 실행순서를 제어하는 문장     
<br>

**2) 제어문의 종류**
* **조건문(조건선택)** : 두 개 또는 여러 개 중의 하나를 선택하는 구조
* **반복문(반복)** : 반복 몸체인 여러문장을 반복하는 구조
* **분기분(분기처리)** : 정해진 장소로 이동하는 구조

<br>
<br>

# **조건문**
---

## **조건문이란?**
* 두 개 또는 여러 개 중에서 한 개를 선택하도록 지원하는 구문
* `if` `if else` `if else if` `switch` `nested if`

<br>
<br>

## **if문**
**1) if문 구조**

```c
if(cond)    //cond : 조건식
{
    stmt;
}

next;
```

* `cond 조건식`
    * 반드시 괄호 필요
    * `cond != 0(거짓)`이면 `stmt` 실행
* `stmt`
    * `cond`가 만족되면 실행되는 문장 
    * 여러문장이면 블록으로 구성, 들여쓰기 필수, 세미콜론으로 종료 

<br>

**2) if문 예시**

```c
//표준입력으로 받은 온도가 30도 이상이면 "폭염주의보를 발령합니다" 출력
//온도와 상관없이 항상 현재 온도 출력

#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main(void)
{
    double temp;

    printf("현재 온도를 입력하세요\n");
    scanf("%lf", &temp);

    if(temp >= 30.0)
        prtintf("폭엽주의보를 발령합니다.\n");

    printf("%현재온도는 lf 입니다.\n", temp);
    return 0;
}

```

<br>
<br>

## **if else문**
**1) if else문 구조**

```c
if(cond)
    stmt1;
else
    stmt2;

nest;
```

* `조건 cond`를 만족하면 `stmt1` 수행, 만족하지 않으면 `stmt2` 수행
* `cond 조건식` : 괄호 필수
* `stmt` : 실행문장이 여러줄이면 `{...}`

<br>

**2) if else문 예시**

```c
//표준입력으로 받은 정수가 짝수인지 홀수인지를 판별하는 프로그램
#define _CRT_SECURE_NO_WARNINGS
#inclue <stdio.h>

int main(void)
{
    int n;
    printf("정수를 입력하세요.");
    scanf("%d", &n);

    //if else문 이용
    if(n % 2)    //n % 2 != 0(홀수이면)
        printf("홀수\n");
    else
        printf("짝수\n");

    //조건연산자 이용
    (n % 2) ? printf("홀수\n"); : printf("짝수\n");
    return 0;
}
```

<br>
<br>

## **if else if문**

**1) if else if문 구조**

```c
if(cond1)
    stmt1;
else if(cond2)
    stmt2;
else if(cond3)
    stmt3;
else
    stmt4;

nest;
```

* 순서대로 조건을 충족하는지 확인하여, 조건을 충족하는 하나의 문장만 실행

<br>

**2) if else if문 예시**

```c
//평균 평점에 따른 적정 구문 출력

#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main()
{
    double gpa;

    printf("평균평점 입력");
    scanf("%lf", &gpa);

    if(gpa >= 4.3)
        printf("최우등\n");
    else if(gpa >= 3.8)
        printf("우등\n");
    else if(gpa >= 3.0)
        printf("우수\n");
    else
        prinft("3.0 미만");

    return 0;
}

```

<br>

## **중첩된 if**
**1) 중첩된 if문 이란**
* 중첩된 if문 : if문 내부에 if문이 존재하는 것

```c
if(type == 1)
{    //없어도 오류는 없지만, 소스 가독성을 위해 삽입
    if(point >= 70)
        printf("1종면허 합격\n");
    else
        printf("1종면허 불합격\n");
}
else if(type == 2)
{
    if(point >= 60)
        printf("2종면허 합격\n");
    else
        printf("2종면허 불합격\n");
}
```

<br>
<br>

## **switch문**
**1) switch문 구조**

```c
switch(exp){
    case value1 :
        stmt1;
        break;
    case value2 :
        stmt2;
        break;
    case value3 :
        stmt3;
        break;
    default :
        stmt4;
        break;    //생략가능
}
```

* `exp` 결과 중 `case`의 값과 일치하는 항목의 문장 `stmti`를 실행한 후 `break`를 만나 종료
* `exp` : 결과값은 반드시 문자나 정수
* `value` : 상수식(constant expression), 중복X, 변수X
* `defalut` : 선택적이므로 사용하지 않을 수 있음, 어디에든 위치 가능
* `break` : switch문 바로 종료, break문을 만날 때 까지 실행

<br>

**2) switch문 예시**

```c
swtich(op)    //int op
{
    case 1 :
        printf("1번");
    case 2 :
        printf("2번");
    case 3 :
        printf("3번");
    default :
        printf("복권 당첨돼서 놀고 먹고 싶다");
}
```

```c
//오류발생
switch(month)
{
    case 4 : case 5 : 
        printf("봄");
        break;
    case 6, 7 :        //오류
        printf("여름");
        break;
}
```

```c
//연산식의 활용과 default의 위치

#define _CRT_SECURE_NO_WARNINGS
#inclue <stdio.h>

int main()
{
    int score;

    printf("점수를 입력하세요 : ");
    scanf("%d", &score);

    switch(score/10)
    {
        default:              //생략가능, 위치제한 없음
            printf("F");
            break;            //마지막에서만 생략가능
        case 10: case 9:
            printf("A");
            break;
        case 8:
            printf("B";
            break;
    }
    return 0;
}
```



<br>
<br>
<br>


# **반복문**
---

## **반복문이란?**
**1) 반복문이란**
* 정해진 횟수나 조건을 만족하면 일정 영역의 문장을 여러 번 실행
* `while` `do while` `for`
<br>

**2) 반복문 개요**
* 반복(repetition) : 순환 = 루프, 같거나 비슷한 일을 여러 번 수행하는 작업
* 반복몸체(repetition body) : 반복조건을 만족하면 일정하게 반복되는 블록

<br>
<br>

## **while문**
**1) while문 구조**

```c
while(cond)
{
    반복몸체(loop body, stmt);
};
```

* 반복조건인 cond를 평가하여 0이 아니면(참이면) 반복몸체인 stmt 실행, cond가 거짓일 때까지 반복
    * `cond` : 반복조건, cond가 `0(거짓)`이 될 때까지 반복
    * `stmt` : 반복몸체, 필요(여러줄)하면 블록으로 구성 가능

<br>

**2) while문 예시**
```c
int count = 0;

while(count <= 3)    //제어변수 : 반복횟수를 제어하는 변수
{
    printf("제발 복권 당첨되게 해주세요\n");
    count++;        //count++가 없으면 무한반복(indefinite loop), Ctrl+C로 종료 가능
}

//표준입력으로 받은 실수가 0이 아니면 계속 더하는 while문
double number = 1;
while(number != 0.0)
{
    printf("실수입력");
    scanf("%lf", &number);
    sum += number;
}
```

<br>
<br>

## **do while문**
**1) do while문 구조**
* 반복몸체 수행 후에 반복 조건을 검사
* 반복 횟수가 정해지지 않고 입력 받은 자료 값에 따라 반복 수행의 여부를 결정하는 구분에 유용
* 센티널 값(sentinel value) 검사에 유용
* `stmt` : 가장 먼저 실행, 반복몸체가 여러 문장이거나 필요하면 블록으로 구성
* `cond` : 반복조건, stmt실행 후 cond를 평가하여 0(거짓)이 될 때까지 stmt 실행

> 센티널 값 : 반복의 종료를 알리는 특정한 자료 값

```c
do
{
    반복몸체(loop body, stmt);
}
while(cond);        //세미콜론 필수
```

<br>

**2) do while문 예시**

```c
int input;

do
{
    printf("| 0. 종료 | 1. 아메리카노 | 2. 카페라떼 | 3. 카푸치노 |\n");
    printf("주문할 커피 또는 종료(0) 입력");
    scanf("%d", &input);
}
while(input != 0)    //while(input)
```

<br>
<br>

## **for문**
**1) for문의 구조**
* `init` : 초기화(initialization), 단 한번만 수행
* `cond` : 반복조건(condition), cond가 0이면 반복 종료
* `inc` : 증감(increment), 반복을 결정하는 제어 변수의 증감 수행, stmt 실행후 inc 실행
* `stmt` : 반복몸체가 여러 문장이거나 필요하면 블록으로 구성

```c
for(init; cond; inc)
{
    반복몸체(loop body, stmt);
}

//세미콜론으로 구분되는 항목은 모두 생략 가능, 세미콜론은 필수
//무한반복
for(;;)    
{
    stmt;
}
```

<br>

**2) for문 예시**

```c
for(int i = 0; i <= MAX; i++)    //i처럼 반복의 횟수를 제어하는 변수를 제어변수
    printf("반복 %d", i + 1);

double celsius = 12.46;
for(int i = 0; i <= MAX; i++, celsius += 10) 
    printf("반복 %d", i + 1);
```


<br>
<br>

# **분기문**
---

## **분기문이란**
* `break` : 작업을 수행하는 도중 조건에 따라 반복이나 선택을 빠져나감
* `continue` : 일정 구문을 수행하지 않고 다음 반복을 실행
* `goto` : 지정된 위치로 이동
* `return` : 작업 수행을 마치고 이전 위치로 돌아가는 구문

<br>
<br>

## **break문**
**1) break문**
* 언제 : 반복 내부에서 반복을 종료하기 위해, switch문의 종료

```c
//for문
for(;;)
{
    ...
    break;    //1. break를 만나면
    ...       //   break 다음코드는 실행하지 않음
}
next;         //2. for문을 종료하고 다음 코드 실행


//while문
while(...)
{
    ...
    break;    //1. break를 만나면
    ...       //   break 다음 코드는 실행하지 않음
}
next;         //2. while문을 종료하고 다음 코드 실행


//do while
do
{
    ...
    break;    //1. break를 만나면
    ...       //   break 다음 코드는 실행하지 않음
}
while(...);
next;        //2. do while문을 종료하고 다음 코드 싷행
```

* 반복이 중첩된 경우 break를 포함하는 가장 근접한 내부 반복을 종료

```c
while(...)
{
    ...
    for(;;)
    {
        ...
        break;    //1. break를 만나면
        ...       //   가장 근접한 내부 반복을 종료
    }

    next;         //2. for문을 종료하고 다음 코드 실행
}
next;
```

<br>
<br>

**2) continue문**
* continue문이 위치한 이후 반복몸체의 나머지 부분을 실행하지 않고 다음 반복을 계속 유지하는 문장
    * while문과 do while문 : continue를 만나면 조건 검사로 이동하여 실행
    * for문 : 증감부분으로 이동
* 중첩된 반복에서 continue는 자신이 속한 가장 근접한 반복에서 다음 반복을 실행
 
```c
while(cond1)
{
    ...
    continue;    //cond1로 이동

    for(init; cond2; inc)
    {
        continue;    //cond2로 이동
        ...
    }
}
```

<br>
<br>

**3) goto문**
* lable이 위치한 다음 문장으로 실행순서를 이동하는 문장
* lable은 `콜론(:)`을 이용하여 지정

```c
int main(void)
{
    int count = 1;

loop:
    printf("%3d", count);
    if(++count <= 10)
        goto loop;

    printf("종료");

    return 0;
}
```


