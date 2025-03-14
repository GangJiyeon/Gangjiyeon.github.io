---
title:  "[python] 7. 자료형 - 불"
date:   2024-10-14
 tags:
    - 파이썬기초
thumbnail: "/assets/img/thumbnail/book.jpg"

---
이번에는 파이썬의 불 자료형에 대해 알아보자



---
## **불 자료형**
### **불(bool) 자료형이란** 
**1) 불 자료형 : 참(True)과 거짓(False)을 나타내는 자료형
* `True`: 참을 의미
* `False`: 거짓을 의미

<br>
<br>

### **불 자료형 사용 방법**

```py
a = True
b = False

print(type(a))	# <class 'bool'>
print(type(b))	# <class 'bool'>
```

<br>
<br>
<br>

---

## **자료형의 참과 거짓**
* 문자열, 리스트, 튜플, 딕셔너리 : 값이 비어 있으면 거짓이 되고, 비어 있지 않으면 참
* 숫자형 : 값이 0일 때 거짓

|구분|참|거짓|
|:---:|:---:|:---:|
|문자열|`"python"`|`""`|
|리스트|`[1, 2, 3]`|`[]`|
|튜플|`(1, 2, 3)`|`()`|
|딕셔너리|`{'a': 1}`|`{}`|
|숫자형|`1`|`0`|
|-|-|`None`|

