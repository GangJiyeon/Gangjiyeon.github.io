---
title:  "[python] 10. 파이썬 제어문(if, while, for)"
date:   2024-10-17
 tags:
    - 파이썬기초
thumbnail: "/assets/img/thumbnail/book.jpg"

---
이번에는 파이썬의 제어문(if, while, for문)에 대해 알아보자



---

## **제어문**
### **제어문이란**
**1) 파이썬 제어문**
* if문
* for문
* while문

<br>
<br>
<br>
  

---
  

## **if문**
### **if문 구조**
**1) if문 기본구조**
* elif문 : if문 이후에 갯수 상관없이 사용가능
* else문 : 가장 마지막에 한 번만 사용가능(elif문 없어도 사용 가능)

  
```py
# if문의 조건문이 True이면 다음 문장(if 블록) 수행
# if문의 조건문이 False이면 elif 조건문 판단
# elif문의 조건문이 True이면 elif 블록 수행
# elif문의 조건문이 False이면 else 블록 수행

if 조건문:  # 콜론 필수
	수행할문장1  # if 블록의 문장은 모두 들여쓰기 해야함
	수행할문장2  # 안하면 오류 발생
	pass  # 아무것도 안하고 싶으면 pass를 사용한다
elif 조건문: # 콜론 필수
	수행할문장1 # elif 블록의 문장은 모두 들여쓰기 해야함
	수행할문장2 # 안하면 오류 발생
else:  # 콜론 필수
	수행할문장A  # else 블록의 문장은 모두 들여쓰기 해야함
	수행할문장B  # 안하면 오류 발생
```

  
> 들여쓰기(tab) = 띄어쓰기(space) 4번


<br>  

**2) 조건문**
* 조건문이란 : 참과 거짓을 판단하는 문장
* 조건문의 표현 방식
	* 비교연산자
	* and, or, not
	* in, not in

|비교연산자|설명|
|:---:|:---:|
|`x < y`|x가 y보다 작음|
|`x > y`|x가 y보다 큼|
|`x == y`|x와 y가 같음|
|`x != y`|x와 y가 같지 않음|
|`x >= y`|x가 y보다 크거나 같음|
|`x <= y`|x가 y보다 작거나 같음|

<br>

|연산자|설명|
|:---:|:---:|
|`x or y`|x와 y 둘 중 하나만 참이어도 참|
|`x and y`|x와 y 모두 참이어야 참|
|`not x`|x가 거짓이면 참|


<br>

|in|not in|
|:---:|:---:|
|`x in 리스트`|`x not in 리스트`|
|`x in 튜플`|`x not in 튜플`|
|`x in 문자열`|`x not in 문자열`|

<br>

  

```py
grade = 98
if grade >= 90:
	print("A+학점")  # "A+학점"
elif grade >= 80:
	print("A학점")
else:
	print("p")

if grade >= 80 and grade < 90:
print("A학점")

1 in [1, 2, 3]  	# True
1 not in [1, 2, 3]  # False
```


<br>
<br>

 
### **if문 한 줄로 작성하기**
```py
pocket = ['paper', 'money', 'cellphone']
if 'money' in pocket : pass
else: print("카드!!!!")
```

<br>
<br>

### **조건부 표현식**
**1) 조건부 표현식(conditional expression)이란**
* 정의 : `변수 = 참일때 if 조건문 else 거짓일때`
* `message = "success" if score >= 60 else "failure"`

<br>
<br>
<br>


---

  

## **while문**
### **while문 구조**
**1) while문 기본구조**

```py
while 조건문:
	수행할문장1
	수행할문장2
	수행할문장3
```
  
<br>

**2) break와 continue**
* `break` : while문을 빠져나감
* `continue` : 다음 문장을 실행하지 않고 while문의 처음으로 돌아감


```py
# 1부터 10까지 숫자 중 홀수만 출력하기
a = 0
while a < 10:
	a += 1
	if a % 2 == 0:
		continue
	print(a)
```

<br>
<br>
<br>

  

---

  

## **for문**
### **for문 구조**
**1) for문 기본구조**

```py
for 변수 in 리스트(튜플/문자열):
	수행할문장1
	수행할문장2
```

<br>

**2) for문 예시**
* 리스트

```py
list1 = ['one', 'two', 'three]
for i in list1:
	print(i)

# one
# two
# three
```

<br>

* 튜플

```py
tuple1 = [(1,0), (2,0), (3,0)]
for (i, k) in tuple1:
	print(i + k)

# 1
# 2
# 3
```

<br>
<br>




### **for문과 continue**
* continue를 만나면 for문의 처음으로 돌아감

```py
marks = [90, 25, 67, 45, 80] 
number = 0  
for mark in marks: 
	number = number +1 
	if mark < 60: 
		continue  
	print("%d번 학생 축하합니다. 합격입니다. " % number)
```

<br>
<br>

### **range 함수**
**1) range 함수란**
* `range(정수1, 정수2)` : 정수1부터 정수2 미만의 숫자를 포함하는 range 객체를 생성
* `range(정수)` : 시작 숫자 생략 시 0부터 시작

<br>

**2) for문에서 range 함수 사용하기**

```py
total = 0
for i in range(1, 11):
	total += i

print(total)	# 55
```


<br>
<br>

### **리스트 컴프리헨션 사용하기**
**1) 리스트 컴프리헨션(list comprehension)이란**
* 리스트 안에 for문을 포함하는 것

```py
# 리스트의 각 항목에 3을 곱해 리스트에 담기
a = [1, 2, 3, 4]
result = [num * 3 for num in a]
print(result)	# [3, 6, 9, 12]

# 리스트에서 짝수에만 3을 곱해 리스트에 담기
result = [num * 3  for num in a if num % 2 == 0] 
print(result) 	# [6, 12]
```
