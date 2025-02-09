---
title: "[C언어] 문자열"
tags:
    - C언어기초
date: "2024-12-13"
thumbnail: "/assets/img/thumbnail/book.jpg"
---
이번에는 C언어의 문자열에 대해 알아보자.    


## **문자와 문자열**
### **문자와 문자열 선언**
**1) 문자와 문자열의 개념**
* 문자
	* 표기 : 영어의 알파벳이나 한글의 한 글자를 `작은따옴표(single quote)`로 둘러싸서 표현
	* ex : `'A'`
	* 저장공간의 크기가 1바이트인 자료형 `char`
	* `문자상수` : 작은따옴표에 의해 표기된 문자
	* `'hi'` : 오류발생, 문자 아님
* 문자열(string)
	* 문자열 : 문자의 모임, 일련의 문자열
	* 표기 : 일련의 문자 앞 뒤로 `큰 따옴표(double quote)`로 둘러싸서 표현
	* ex : `"java"`, `"k"`

<br>

**2) 문자와 문자열의 선언**
* 문자의 선언
	* `char`형 변수에 문자 저장
* 문자열 선언
	* 문자배열 사용
	* 문자포인터사용

```c
/* 1. 문자배열을 사용한 문자열 선언
- 문자열의 마지막을 의미하는 NULL문자('\0')을 마지막에 저장
- 배열의 크기 : 저장될 문자 수 + 1, 배열크기를 생략하는 것이 편리 */
//방법 1
char csharp[3] = {'C', '#', '\0'};
char java[] = {'J', 'A', 'V', 'A', '\0'};	

//방법 2
char c[] = "C language";					
char python[7] = "python";
char go[5] = "go";		//크기가 (문자+1)보다 크면 나머지는 '\0' 저장

/* 출력 */
printf("%c", 'a');
printf("%s", "문자열 출력");
```

<br>

```c
/* 2. 포인터를 이용한 문자열 선언 
- 저장된 값은 상수이므로 수정이 불가능함 */
char *java = "JAVA";

/* 출력 */
//방법 1. printf
printf("%s", java);

//방법 2. 문자 포인터가 가리키는 문자를 배열형식으로 직접 참조해 출력
int i = 0;
while(java[i] != '\0')	//java[i] != '\0' == java[i]
	printf("%c", java[i++]);
print("\n");

while(java[i] != '\0')	//java[i] != '\0' == java[i]
	printf("%c", *(java + i++));
print("\n");
```

<br>

**3) `'\0'`문자에 의한 문자열 분리**
* `printf()`에서 `%s` : 문자 포인터가 가리키는 위치에서 `NULL문자`까지를 하나의 문자열로 인식

```c
char c[] = "c c++ java";
char[5] = '\0';

printf("%s\n%s\n",c, c+6);	
/* 출력
c c++
java
*/
```

<br>
<br>


### **다양한 문자 입출력**
**`getchar()` & `putchar()`**
* getchar() : 문자의 입력에 사용, `라인버퍼링(line buffering) 방식` 사용, 입력문자 수정 가능
* putchar() : 문자의 출력에 사용

> 라인버퍼링(line buffering) 방식 
> 1) 키보드 표준입력 : `enter`키를 누르기 전까지 입력자료의 편집이 가능하며 버퍼에 저장
> 2) 버퍼에 저장 : 임시기억장소인 버퍼에 저장되었다가 `enter`키를 만나면 프로그램으로 입력이 시작
> 3) 입력처리 : 버퍼자료를 이용하여 getchar() 수행

> 버퍼(buffer)
> * 속도 차이가 있는 장치들을 위한 임시 데이터 저장소
> * 입출력이 다른 처리에 비해 처리속도가 느리지만 효율적인 입출력을 위해 사용하기도 함

<br>

**`_getche()`**
* 버퍼를 사용하지 않고 문자를 바로바로 입력할 수 있는 함수
* 문자 하나를 입력하면 바로 함수 _getche() 실행
* 입력된 문자는 바로 모니터에 나타남
	* `_getche()`의 e는 `echo`
 	* 한 문자가 두번씩 나옴(표준입력, 표준출력)
* 헤더파일 `conio.h` 삽입
* 입력문자 수정 불가능

<br>

**`_getch()`**
* 버퍼를 사용하지 않는 문자 입력 함수
* 입력한 문자가 화면에 보이지 않음
* 헤더파일 `conio.h` 삽입
* 입력문자 수정 불가능

<br>
<br>

### **문자열 입력**
**scanf()**
* 공백으로 구분되는 하나의 문자열을 입력받을 수 있음
	* 입력 받은 문자열이 저장될 충분한 공간인 문자 배열 선언(문자포인터 불가능)
* 입력문자 수정 가능 

```c
char str[50]  =  "";
scanf("%s", str);
printf("%s", str);
```
<br>

**gets()와 puts()**

```c
/* 
gets(), puts(), gets_s() 
- 헤더파일 stdio.h 삽입 
*/

char * gets(char *buffer)
//한 행의 문자열 입력에 유용한 함수
//문자열을 입력 받아 buffer에 저장하고, 입력 받은 첫 문자의 주소값 반환
//표준입력으로 [enter]키를 누를 때까지 공백을 포함한 한 행의 모든 문자열을 입력 받음
//입력된 문자열에서 마지막 [enter]키를 '\0' 문자로 대체하여 저장

char * gets_s(char *buffer, size_t sizebuffer);
//두번째 인자인 sizebuffer는 정수형으로, buffer의 크기를 입력
//gets()대신 gets_s()를 사용하는 것을 권장

int puts(const char *str);
//한 행에 문자열을 출력하는 함수
//인자인 문자열 str에서 마지막 '\0' 문자를 개행문자인 '\n' 으로 대체하여 출력
//일반적으로 0인 정수를 반환하고, 오류 발생 시 EOF 반환
```

> EOF(End Of File) : 파일의 끝이라는 의미, 헤더파일에 정수 -1로 정의

<br>
<br>
<br>

---
## **문자열 관련 함수**
### **문자열 관련 라이브러리 함수**
**1) 문자열 배열에 관한 다양한 함수** 👉 <string.h> 정의

```c
size_t strlen(const char *str)
//포인터 src 위치에서 NULL 문자를 제외한 문자열의 길이 반환

void *memcpy(void *dest, const void *src, size_t n)
//포인트 src 위치에서 dest에 n바이트를 복사한 후 dest 위치 반환

void *memchr(const void *str, int c, size_t n)
//메모리 str에서 n바이트까지 문자 c를 찾아 그 위치를 반환

int memcmp(const void *str1, const void *str2, size_t, n)
//메모리 str1과 str2를 첫 n바이트를 비교 검색하여 같으면 0, 음수 또는 양수 반환

void *memmove(void *dest, const void *src, size_t n)
//포인터 src 위치에서 dest에 n바이트를 복사한 후 dest 위치 반환

void *memset(void *str, int c, size_t n)
//포인터 src위치에서부터 n바이트까지 문자 c를 지정한 후 src 위치 반환
```

<br>

**2) 두 문자열을 비교하는 함수** 👉 <string.h> 정의

```c
int strcmp(const char *s1, const char *s2);
//두 인자인 문자열에서 같은 위치의 문자를 앞에서부터 다를 때까지 비교
//같으면 0, 앞이 크면 양수, 뒤가 크면 음수 반환
//비교기준은 아스키코드 값

int strncmp(const char *s1, const char *s2, size_t maxn);
//두 인자 문자열을 같은 위치의 문자를 앞에서부터 다를 때까지 비교
//최대 n까지만 비교하여 같으면 0, 앞이크면 양수, 뒤가 크면 음수 반환
```

<br>

**3) 문자열을 복사하는 함수**

```c
char *strcpy(cha *dest, const char *source);
//1. 앞 문자열 dest에 뒤 문자열 null 문자를 포함한 soure를 복사하여
//	 복사된 문자열 반환
//2. 앞 문자열 수정가능, 뒤 문자열 수정 불가능

char *strncpy(char *dest, const char *source, size_t maxn);
//1. 앞 문자열 dest의 처음에 뒤 문자열 source애서 n개의 문자를 복사하여 
//	 복사된 문자열 반환
//2. maxn이 source보다 길면 나머지는 null문자 복사
//3. 앞 문자열 수정가능, 뒤 문자열 수정 불가능

errno_t strcpy_s(char *dest, size_t sizedest, const char *source);
errno_t strncoy_s(char *dest, size_t sizedest, const char *source, size_t maxn);
//두 번째 인자인 sizedest : 정수형, dest의 크기를 입력
//반환형 errno_t : 정수형, 오류번호, 성공하면 0반환
//
```

<br>

**4) 문자열을 연결하는 함수**

```c
char *strcat(char *dest, const char *source);
//앞 문자열 dest에 뒤 문자열 source 연결(concaternate)해 저장
//연결된 문자열을 반환, 뒤 문자열 수정 불가능

char *strncat(chat *dest, const char *source, size_t maxn);
//앞 문자열 dest에 뒤 문자열 source 중에서 n개의 크기만큼을 연결(concaternate)해 저장
//연결된 문자열 반환, 뒤 문자열 수정 불가능
//지정한 maxn이 문자열 길이보다 크면 null 문자까지 연결

errno_t strcat_s(char *dest, size_t sizedest, const char *source);
errno_t strncat_s(char *dest, size_t sizedest, const char *source, size_t maxn);
//두 번째 인자인 sizedest : 정수형, dest 크기 입력
//반환형 errno_t : 정수형, 반환값은 오류번호, 성공하면 0 반환
```

<br>

**5) 문자열 분리 함수**

```c
char *stroke(char *str, const char *delim);
//앞 문자열 str에서 뒤 문자열 delim을 구성하는 구분자를 기준으로 순서대로 토큰을 추출하여 반환하는 함수
//뒤 문자열 delim은 수정 불가능

char *stroke_s(char *str, const char *delim, char **context);
//마지막 인자 context : 함수 호출에 사용되는 위치 정보를 위한 인자
```

<br>
<br>
<br>

---
## **여러 문자열 처리**
### **여러 문자열 처리**
**1) 문자 포인터 배열**
* 여러 개의 문자열을 처리하는 방법(문자 포인트가 하나의 문자열을 참조)
* 각각의 문자열 저장을 위한 최적의 공간을 사용
* 문자열 상수의 수정이 불가능

```c
//배열 크기 : 문자열 개수 or 공백
char *pa[3] = {"java", "c#", "c++"};
printf("%s %s %s",pa[0], pa[1], pa[2]);
```

**2) 2차원 문자 배열**
* 모든 열 수가 동일하게 할당돼, 낭비되는 메모리 공간(`\0`가 저장)이 발생할 수 있음
* 문자열을 수정할 수 있음

```c
//행 크기: 문자열 개수 or 빈 공백
//열 크기: 문자열 중 가장 긴 문자열의 길이 + 1 ('\0')
char ca[][5] = {"java", "c#", "c++"};
printf("%s %s %s", ca[0], ca[1], ca[2]);
```

<br>
<br>

### **명령행 인자**
**1) 명령행인자(conmmand line argument)**
* 명령행인자를 사용하는 방법 : 명령행에서 입력하는 문자열을 프로그램으로 전달하는 방법
* 명령 프롬프트에서 명령어 옵션 실행
	* 프롬프트(prompt) : 도스 창에서 프로그램이 저장된 폴더의 경로 >
	* 명령행(command line) : 명령어 프롬프트가 나타나는 줄, 명령어를 입력할 수 있음 
* 프로그램에서 명령행 인자 : 메인함수의 인자로 기술 `main(int argc, char *argv[])`
	* argc : 명령행에서 입력한 문자열의 수
 	* argv[] : 명령행에서 입력한 문자열을 전달 받는 문자 포인터 배열
* 실행프로그램 이름도 하나의 명령행 인자 


