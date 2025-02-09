---

title:  "[python] 12. 파이썬 입출력"
date:   2024-10-19
 tags:
    - 파이썬기초
thumbnail: "/assets/img/thumbnail/book.jpg"

---
이번에는 파이썬의 입출력(print, input)에 대해 알아보자



---

## **파이썬 사용자 입출력**
### **사용자 입력 input**
* `input("보여줄 문구")
* 프롬프트에 보여줄 문구를 띄워주고, 사용자의 입력을 받음
* 입력되는 모든 것은 문자열로 취급함

```py
number = input("숫자 입력 =>")
print(number) 	# 3
```

<br>
<br>

### **출력 print**
* 사용자에게 보여줄 내용을 `print()`를 통해 보여줄 수 있음
* print 옵션 : `sep` `end` `file`

```py
# print option - sep ===========================================
# default value == ' '
print('a', 'b', 'c') 				# result : a b c
print('a', 'b', 'c', sep='') 		# result : abc
print('a', 'b', 'c', sep=' and ') 	# result : a and b and c
print('a', 'b', 'c', sep=' ') 		# result : a b c
```
 

 ```py
# print option - end ===========================================
# defalt value == \n
print('welcome')
print("t", end='')
print("o", end=" ")
print('the new world')
# result : welcome
# to the new world
```

```py
# print option - flie ===========================================
import  sys
print('learn python', file=sys.stdout)
```



* 큰따옴표로 둘러싸인 문자열은 + 연산과 동일

```py
print("life" "is" "too short")  # lifeistoo short
print("life"+"is"+"too short")  # lifeistoo short
```

* 문자열 띄어쓰기는 쉼표로 한다

```py
print("life", "is", "too short")	# life is too short
```
