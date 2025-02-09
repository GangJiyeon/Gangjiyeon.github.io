---
title: "[C언어] 파일처리"
tags:
    - C언어기초
date: "2024-12-16"
thumbnail: "/assets/img/thumbnail/book.jpg"
---
이번에는 C언어의 파일처리에 대해 알아보자


## **파일 기초**
### **텍스트 파일과 이진 파일**
**1) 파일이란**
* 파일 : 보조기억장치의 정보저장단위로, 자료의 집합

<br>

**2) 파일의 필요성**
* 파일의 저장 : 보조기억장치인 디스크에 저장
	* 직접 삭제하지 않으면 프로그램이 종료되더라도 계속 저장 가능
	* 프로그램에서 사용하던 정보를 종료 후에도 계속 사용하고 싶을 때 파일에 저장

> 주기억장치의 메모리 공간 : 변수와 같이 프로그램 내부에서 할당되어 사용

<br>

**3) 텍스트 파일과 이진 파일**
* **텍스트 파일(text file)**
	* 메모장(notepad) 등 `편집기로 작성된 파일`
	* 문자기반의 파일 : 내용이 `문자코드 값(ex_ascii code)`로 저장
	* 메모리에 저장된 실수, 정수 값도 문자형식으로 변환되어 저장
	* 편집기를 통해 그 내용을 보고 수정할 수 있음
* **이진 파일(binary file)**
	* 실행파일, 그림파일, 음악파일, 동영상파일 등과 같이 목적에 알맞은 자료가 `이진 형태(binary format)로 저장된 파일`
	* 프로그램 내부 형식으로 저장되는 파일, 텍스트 편집기로는 내용을 볼 수 없음
	* 메모리 자료 내용에서 변환을 거치지 않고 그대로 파일에 기록
	* 입출력 속도가 텍스트 파일에 비해 빠름

<br>

**4) 입출력 스트림**
* 스트림(stream) : 자료의 이동경로
	* 자료는 스트림이 연결되어야 이동할 수 있음 
* 입출력 스트림(io stream) : 입출력시 이동 경로
	* 입력 스트림(input stream) : 다른 곳에서 프로그램으로 들어오는 경로
		자료원천지(data source) : 자료가 떠나는 시작부분
	* 출력 스트림(output string) : 프로그램에서 다른 곳으로 나가는 경로
		자료목적지(data destination) : 자료의 도착 장소
* 표준입력 스트림 : 키보드에서 프로그램으로 자료가 이동하는 경로, scanf()
* 표준출력 스트림 : 프로그램에서 모니터의 콘솔로 자료가 이동하는 경로, printf()

<br>

**5) 파일 스트림 이해**
* 파일 스트림(file stream) :  보조기억장치의 파일과 프로그램을 연결하는 전송경로
	* 입력을 위한 파일입력 스트림(file input stream) 
	* 출력을 위한 파일출력 스트림(file output stream)
* 프로그램에서 보조기억장치에 파일로 정보를 저장하거나 파일에서 정보를 참조하기위해 파일 스트림을 연결해야함
* 파일 스트림을 만들기 위해서 : 특정한 `파일이름`, `파일모드(스트림의 특성)` 필요

<br>
<br>

### **파일 스트림 열고 닫기**
**1) 함수 fopen(), fopen_s()으로 파일 스트림 열기**
* 프로그램에서 특정 파일이나 파일스트림을 열기 위해 : fopen() 또는 fopen_s() 이용
* 헤더파일 `stdio.h`에 정의
* FILE : 파일을 처리하기 위한 구조체 유형
* 파일열기 종류 모드
	* `r` : 읽기모드, 읽기가 가능한 모드로 쓰기는 불가능
	* `w` : 쓰기모드, 파일 어디에는 쓰기가 가능한 모드, 읽기는 불가능
 	* `a` : 추가모드, 파일 중간에 쓸 수 없고 파일 마지막에 추가적으로 쓰는 것만 가능한 모드, 읽기 불가능

```c
/* fopen */
FILE * fopen(const char *_Filename, const char *_Mode);
//_Filename의 파일 스트림을 모드 _Mode로 연결하는 함수
//인자 : 파일이름, 파일열기 모드
//스트림연결에 성공하면 파일포인터 반환, 실패하면 NULL 반환

/* fopen_s */
errno_t fopen_s(FILE **_FILE, const char *_Filename, const char *_Mode);
//스트림 연결에 성공하면 첫 번째 인자인 _File에 파일포인터 저장, 정수 0 반환
//실패하면 양수 반환
//-FILE **_FILE : 파일포인터 주소값
//-const char *_Filename : 처리하려는 파일 이름
//-const char *_Mode : 파일열기 종류인 모드
```

```c
/* fopen() 사용하기 */

FILE *f;					//파일포인터
char *fname = "basic.txt";	//파일이름

if((f = fopen(fname, "w")) == NULL)
{
	printf("파일이 열리지 않습니다."\n);
	exit(1);
};
```

```c
/* fopen_s() 사용하기 */

if(fopen_s(&f, "basic.txt", "w") != 0)
{
	printf("파일이 열리지 않습니다."\n);
	exit(1);
};
```

<br>
<br>

**2) 함수 fclose()로 파일 스트림 닫기**
* fclose() 
	* `fopen()`으로 연결한 파일 스트림을 닫는 기능
	* 파일을 연결한 후 파일처리가 끝나면 파일포인터 f를 인자로 함수 fclose()를 호출하여 파일 닫기
	* 내부적으로 파일스트림 연결에 할당된 자원을 반납
	* 파일과 메모리 사이에 있던 버퍼의 내용을 모두 지움

```c
int fclose(FILE *_File);
//파일스트림 f를 닫는 함수
//파일성공하면 0, 실패하면 EOR 반환
```

<br>
<br>
<br>

---
## **텍스트 파일 입출력**
### **파일에 서식화된 문자열 입출력**
**1) fprint()와 fscanf()**
* 텍스트 파일에 서식화된 자료(문자열)을 출력 혹은 입력 하는 함수
* 헤더파일 `stdio.h` 포함

```c
int fprintf(FILE *_File, const char *_Format, ...);
int fscanf(FILE *_File, const char *_Format, ...);
int fscanf_s(FILE *_File, const char *_Format, ...);

//_File : 서식화된 입출력 스트림의 목적지 파일, 입출력에 이용될 파일
//_Format : 입출력 제어문자열
//... : 여러 개의 출력될 변수 또는 상수
```

```c
//이름과 성적을 입력해 파일에 쓰고, 다시 표준 출력에 보이기

#define _CTR_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

int main()
{
	char fname[] = "grade.txt";
	FILE *f;
	char name[30];
	int point1, point2, cnt = 0;

	//1. 파일 열기 - 쓰기 권한
	if(fopen_s(&f, fname, "w") != 0)	//인자 : 파일포인터 주소, 파일이름, 모드
	{
		printf("파일이 열리지 않음");
		exit(1);
	}

	//2. 이름과 성적 입력받기
	printf("이름, 중간성적, 기말성적을 입력하세요\n");
	scanf("%s %d %d", name, &point1, &point2);

	//3. 파일에 쓰기
	fprintf(f, "%d %s %d %d\n", ++cnt, name, point1, point2);

	//4. 파일 닫기
	fclose(f);

	//5. 파일 열기 - 읽기 권한
	if(fopen_s(&f, fname, "r") != 0)
	{
		printf("파일이 열리지 않음");
		exit(1);
	}

	//6. 파일 gread.txt에서 읽기
	fscanf(f, "%d %s %d %d\n", &cnt, name, 30, &point1, &point2);

	//7. 표준출력에 쓰기
	fprintf(stdout, "%s %s %s %s\n", 번호, 이름, 중간, 기말);
	fprintf(stdout, "%d %s %d %d", cnt, name, point1, point2);

	//8. 파일 종료 후 스트림 닫기
	fclose(f);

	return 0;
}	
```

<br>
<br>

**2) 표준파일의 종류**
* `fprintf()`와 `fscanf()`, `fscanf_s()`의 첫 번째 인자에 `stdin`또는 `stdout`을 이용하면 표준입력과 표준출력으로 이용 가능

|표준파일|키워드|장치(device)|
|---|---|---|
|표준입력|`stdin`|키보드|
|표준출력|`stdout`|모니터 화면|
|표준에러|`stderr`|모니터 화면|

<br>
<br>

### **파일 문자열 입출력**
**1) fgets()와 fputs()**
* `fgets()` : 파일로부터 한 행의 문자열을 입력받는 함수
* `fputs()` : 파일로 한 행의 문자열을 출력하는 함수
* 헤더파일 `stdio.h` 포함

```c
/* fgets() */
char *fgets(char *_Buf, int _MaxCount, FILE *_File);

/*
1) _File로부터 한 행의 문자열을 _MaxCount 수의 _Buf 문자열에 입력 수행
- char *_Buf : 문자열이 저장될 포인터
- int _MaxCount : 입력할 문자의 최대 수
- FILE *_File : 입력 문자열이 저장될 파일

2) 파일로부터 문자열을 개행문자(\n)까지 읽어 
   마지막 개행문자를 '\0'문자로 바꾸어 입력버퍼 문자열에 저장
*/

/* fputs() */
int fputs(char *_Buf, FILE *_File);

/*
1) _Buf 문자열을 _File에 출력 수행
- char *_Buf : 출력된 문자열이 저장된 문포인터
- FILE *_File : 문자열이 출력되는 파일

2) 문자열을 한 행에 출력
*/
```

<br>
<br>

**2) feof()와 ferror()**
* `feof()` : 파일 스트림의 EOR(end of file) 표시를 검사하는 함수
	* 읽기 작업이 파일의 이전 부분을 읽으면 : 0 반환 
	* 일기 작업이 파일의 이전 부분을 읽지 않으면 : 0이 아닌 값 반환
* `ferror()` : 파일 처리에서 오류가 발생했는지 검사하는 함수
	* 이전 파일 처리에서 오류가 발생한 경우 :  0 반환
	* 이전 파일 처리에서 오류가 발생하지 않은 경우 : 0이 아닌 값 반환
	* 파일 지시자가 파일의 끝에 있는 경우 : 0 반환

> 파일 스트림의 EOF
> 이전 읽기 작업에서 EOF 표시에 도달하면 0이 아닌 값으로 지정

<br>

```c
/* feof */
int feof(FILE *_File);

/* 예시 */
while(!feof(stdin))
{
	fgets(names, 80, stdin);
}


/* ferror */
int ferror(FILE *_File);
```

```c
//여러 줄에 걸쳐 이름, 성적을 입력해 지정된 이름의 파일에 그 내용을 모두 저장
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

int main()
{
	char fname[] = "grade.txt";
	char names[80];
	int cnt = 0;
	FILE *f;
	
	if(fopen_s(&f, fname, "w") != 0)
	{
		printf("파일이 안 열린다!\n");
		exit(1);
	};

	printf("이름과 성적(중간, 기말)을 입력하세요.\n");

	//표준입력으로 받은 한 행을 변수 names에 저장
	//한 행이 79열보다 크면 배열 names[]의 크기를 더 크게 조정
	fgets(names, 80, stdin);

	//콘솔에 이름 중간 기말 입력 후 enter 치고
	//계속 여러 줄에 여러 학생의 성적을 입력하다가
	//종료하고 싶을 때 새로운 줄 처음에 ctrl + z 누르고 enter 치면 종료
	while(!feof(stdin))
	{
		fprint(f, "%d ', ++cnt);	//맨 앞에 번호를 삽입
		fputs(names, f);			//이후에 입력 받은 이름과 성적 2개 저장
		fgets(names, 80, stdin);	//다시 표준입력
	}
	
	fclose(f);
	
	return 0;
}
```

<br>
<br>

### **파일 문자 입출력**
**1) 함수 fgetc()와 fputs()**
* `fgetc()`와 `getc()` : 파일로부터 문자 하나를 입력 받는 함수
* `fputc()`와 `putc()` : 문자하나를 파일로 출력하는 함수

> -문자 하나의 입출력 대상인 파일 포인터를 인자로 이용
> -헤더파일 `stdio.h` 사용

```c
int fgetc(FILE *_File);
int getc(FILE *_File);
//_File에서 문자 하나를 입력받는 함수

int fputc(int _Ch, FILE *_FIle);
int putc(int _Ch, FILE *_File);
//_Ch를 파일 _File에 출력하는 함수
```

```c
#define _CTR_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>

int main()
{
	char fname[] = "char.txt";	//입력한 내용이 저장될 파일이름
	FILE *f;					//파일 포인터

	if(fopen_s(&f, fname, "w")!=0)	//쓰기 모드로 파일 열기
	//if((fopen_s(&f, fame, "w")) == NULL)
	{	
		printf("파일이 안 열린당...\n");
		exit(1);
	};
	puts("영어 문자를 계속 입력하다가 종료하려만 x를 입력 >>");

	/* 표준입력으로 받은 영어 문자를 파일 char.txt에 출력하는 부분 */
	int ch;	//입력된 문자 저장
	while((ch = _getche()) != 'x')
		fputc(ch, f);	
	fclose(f);
	puts("");

	if(fopen_s(&s, fname, "r") != 0)	//읽기모드로 파일 열기
	{
		printf("파일이 열리지 않습니다.\n");
		exit(1);
	};

	//* 파일 char.txt에서 다시 문자를 입력받아 콘솔에 표준출력하는 부분 */
	while((ch = fgetc(f)) != EOF)	//파일 "char.txt"에서 다시문자 읽기
		_putch(ch);					//파일로부터 입력 받은 문자를 표준출력
	fclose(f);
	puts("");

	return 0;
	
}
```

<br>
<br>
<br>

---
## **이진 파일 입출력**
### **텍스트와 이진 파일 입력과 출력**
**1) 함수 `fprintf()`와 `fscanf_s()`**
* 자료의입출력을 텍스트 모드로 처리
* fprintf()로 변수를 출력하면 파일에는 아스키코드 값이 저장

<br>

**2) 함수 fwrite()와 fread()**
> 이진파일(binary file)
> - C언어의 자료형을 모두 유지하면서 바이트단위로 저장되는 파일

* `fwrite()`와 `fread()` : 이진모드로 블록 단위 입출력을 처리
	* `fwrite()` : 바이트 단위로 원하는 블록을 파아ㅣㄹ에 출력하기 위한 함수
	* `fread()` : `fwrite()`로 출력할 자료는 `fread()`로 입력해야 자료유형을 유지할 수 있음 

```c
/* fwrite() */
size_t fwrite(const void *_Buffer, size_t _ElementSize,
				size_t _ElementCount, FILE *_Stream);
//_Buffer가 가리키는 메모리에서
//_ElementSize만큼 _ElementCount를 _Stream에 저장하는 함수


/* fread */
size_t fread(void *_Buffer, size_t _ElementSize,
				size_t _ElementCount, FILE *_Stream);
//파일 _Stream에서 _ElementSize의 _ElementCount개만큼 _Stream에 읽어오는 함수
//반환값 : 성공적으로 입출력을 수행한 항목의 수
```

* 이진파일 열기 함수 fopen()의 모드 기본 종류
	* `rb` : 이진 파일의 읽기모드로 파일 열기
	* `wb` : 이진 파일의 쓰기모드로 파일 열기
	* `ab` : 이진 파일의 추가모드로 파일 열기

<br>
<br>

### **구조체 파일 입출력**
**1) 학생 성적 구조체 파일 쓰기와 읽기 예제**

```c
/* 학생 성적 구조체 파일 쓰기와 읽기 */
//1. 학생성적정보를 구조체로 표현
//2. 표준입력으로 여러 명의 자료를 입력 받은 구조체 자료형을 "score.bin"에 저장
//3. 생성된 이진파일 score.bin의 내용을 읽어 표준출력

#define _CTR_SECURE_NO_WARNINGS
#include <stdio.h>
#include <strings.h>
#include <stdlib.h>

//1. 학생성적정보를 구조체로 표현
typedef struct personscore
{
	int number, mind, final, quiz;	//번호, 중간성적, 기말성적, 퀴즈성적
	char mane[40];					//이름
} pscore;	//구조체 자료형 pscore정의

void printhead()
{
	printf("%s\n", "   ---------------------------------------------");
	printf("%8s%15s%10s%8s%8s\n", "번호", "이름", "중간", "기말", "퀴즈");
	printf("%s\n", "   ---------------------------------------------");	
}

int main()
{
	//2. 표준입력으로 여러 명의 자료를 입력 받은 구조체 자료형을 "score.bin"에 저장
	char fname[] = "score.bin"
	FILE *f;
	
	if(fopen_s(&f, fname, "wb") != 0)	//이진, 읽기모드로 파일열기
	{
		printf("파일이 열리지 않습니다.");
		exit(1);
	}
	
	char line[80];	//표준입력으로 행을 저장하기 위한 변수
	int cnt = 0;	//입력 학생 번호(자동 생성) qustn
	pscore score;	//구조체 변수 선언
	printf("이름과 성적(중간, 기발, 퀴즈)을 입력하세요\n");

	fgets(line, 80, stdin);
	while(!feof(stdin))
	{
		scanf_s(line, "%s %d %d %d", score.name, 40, &score.mid,
					&score.final, &score.quiz);
		score.number = ++cnt;
		fwrite(&score, sizeof(pscore), 1, f);
		fgets(line, 80, stdin);
	}

	fclose(f);

	//3. 생성된 이진파일 score.bin의 내용을 읽어 표준출력
	if((f=fopen(fname, "rb")) == NULL)
	{	
		printf("파일이 열리지 않습니다.\n");
		exit(1);
	}
	printhead();
	
	fread(&score, sizeof(pscore), 1, f);
	while(!feof(f))
	{
		printf(stdout, "%6d%18s%8d%8d%8d\n",
				score.number, score.name, score.mid, score.final, score.quiz);
		fread(&score, sizeof(pscore), 1, f);
	}
	printf("%s\n", "   ---------------------------------------------");	
	fclose(f);

	return 0;
```


<br>
<br>
<br>



---
## **파일 접근 처리**
### **순차 접근과 임의 접근**
**1) 파일 위치(file position)**
* 파일 위치 : 파일 내부를 바이트 단위로 파일 내부 위치를 나타내는 값
* 파일위치 = 파일 지시자(file indicator) = 파일표시자
* 파일의 마지막 : 파일의 마지막을 알리는 EOF(End of FIle)

<br>

**2) 파일스트림 연결 시 파일 위치**
* 파일을 처음 열면 : 모드에 관계 없이 파일 위치는 0
* 모드가 파일추가(a) 
	* 파일을 처음 열면 : 파일 위치 0
	* 자료를 파일에 쓰면 : 자동으로 파일 위치가 마지막으로 이동되어 추가
	* 파일 위치를 임의로 이동 : 파일의 마지막으로 이동하여 추가해야 함 

<br>


**3) 파일의 순차접근과 임의접근**
* 순차접근(sequential access) : 파일 위치를 처음부터 하나씩 증가시키면서 파일을 참조하는 방식
* 임의접근(random-access) 
	* 파일의 어디라도 바로 참조하는 방식
	* `fseek()`, `ftell()`, `rewind()` 등을 활용해 임의접근 

|함수|기능|
|---|---|
|`int fseek(FILE *, long offset, int pos)`|파일 위치를 세 기준점(pos)으로 부터 offset만큼 이동|
|`long ftell(FILE *)`|파일의 현재 파일 위치를 반환|
|`void rewind(FILE *)`|파일의 현재 위치를 0위치(파일의 시작점)로 이동|

<br>
<br>

### **파일의 임의 접근 함수**
**1) 함수 fseek()**
```c
/* fseek() 
- 파일 위치를 자유 자래로 이동하는 함수 
- 함수 원형이 헤더파일 stdio.에 정의 */

/* 함수원형 
1) 파일 _File의 기준점 _Origin에서 _Offset만큼 파일 포인터 이동
- FILE *_File : 파일 포인터
- long _Offset : 기준점으로부터 떨어진 값(offset)
- int _Origin : 오프셋을 계산하는 기준점, 정수형 기호 상수
2) 성공하면 0반환, 실패하면 0이 아닌 정수 반환 */
int fseek(FILE *_File, long _Offset, int _Origin);
```

> 파일의 오프셋 기준의종류를 나타내는 상수

|기호|값|의미|
|---|---|---|
|SEEK_SET|0|파일의 시작위치|
|SEEK_CUR|1|파일의 현재위치|
|SEET_END|2|파일의 끝 위치|

<br>

**2) 파일 열기 다양한 모드**
* 파일 열기 함수 `fopen_s()`의 모드 종류
	* 파일모드에서 + : 수정모드, 원래의 모드에서 읽기 또는 쓰기가 추가되는 모드
	* 파일모드 전환 : `fseek()`, `rewind()`와 같은 함수 호출이 반드시 필요 

|모드|파일열기모드|모드전환|파일이 있는 경우|파일이 없는 경우|
|---|---|---|---|---|
|`r`|읽기(read)|쓰기(write) 불가능|파일의 처음에서 읽기 시작|에러|
|`w`|쓰기(write)|읽기(read) 불가능|이전 내용을 지우고 처음부터 쓰기 시작|새로 생성|
|`a`|추가(append)|읽기(read) 불가능|파일의 마지막에서 파일의쓰기를 시작<br>파일의 중간에 쓰는 것은 불가능|새로 생성|
|`r+`|읽기(read)|쓰기(write)|파일의 처음에서 읽기 시작|에러|
|`w+`|쓰기(write)|읽기(read)|이전 내용을 지우고 처음부터 쓰기 시작|새로 생성|
|`a+`|추가(append)|읽기(read)|파일의 마지막에서 파일의쓰기를 시작<br>파일의 중간에 쓰는 것은 불가능|새로 생성|

* 이진파일 열기 함수 fopen()의 모드 종류
	* `rb` : 이진 파일의 읽기(read) 모드로 파일 열기
	* `wb` : 이진 파일의 쓰기(write) 모드로 파일 열기
	* `ab` : 이진 파일의 추가(append) 모드로 파일 열기
	* `rb+`, `r+b` : 이진 파일의 읽기(read)와 쓰기(write) 모드로 파일 열기
	* `wb`, `w+b` : 이진 파일의 읽기(read)와 쓰기(write) 모드로 파일 열기
	* `ab`, `a+b` : 이진 파일의 추가(append) 모드로 파일 열기

<br>
<br>

### **입출력 및 파일 삭제, 이름 바꾸기 함수**
**1) 텍스트 파일 입출력 함수**
* 헤더파일 stdio.h 삽입

|자료|종류|표준입출력|파일입출력|
|---|---|---|---|
|문자|입력|`int getchar(void)`|`int getc(FILE *)`<br>`int fgetc(FILE *)`|
||출력|`int putchar(int)`|`int putc(int, FILE *)`<br>`int fputc(int, FILE *)`|
|문자열|입력|`char *gets(char *)`|`char *fgets(char *, int, FILE *)`|
||출력|`int puts(const char *)`|`int fputs(const char *, FILE *,)`|
|서식자료|입력|`int scanf(const char *, ...)`<br>`int scanf_s(const char *,...)`|`int fscanf(FILE *, const char *, ...)`<br>`int fscanf_s(FILE *, const char *, ...)`|
||출력|`int printf(const char *, ...)`|`int fprintf(FILE *, const char*,...)`|

<br>

**2) 이진 파일 입출력 함수**
* 블록 입력 : `size_t fread(void *, size_t, size_t, FILE *)`
* 블록 출력 : `size_t fwrtie(const void *, size_t, size_t, FILE *)`
* 정수 입력 : `int _getw(FILE *)`
* 정수 출력 : `int _putw(int, FILE *)`

<br>

**3) 파일 처리함수 `remove()`, `rename()`**
* remove() : 지정된 특정한 파일 삭제
* rename() : 지정된 파일 또는 폴더의 이름을 새로운 이름으로 바꾸는 기능 수행

```c
int remove(char const* _FileName);
//성공적으로 삭제되면 0, 삭제되지 않으면 -1 반환

int rename(char const *_OldFileName, char const * _NewFileName);
//성공적으로 수정되면 0, 수정되지 않으면 0이 아닌 정수 반환
```
