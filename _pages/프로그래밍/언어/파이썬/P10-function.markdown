---
title:  "[python] 11. 파이썬 함수"
date:   2024-10-18
 tags:
    - 파이썬기초
thumbnail: "/assets/img/thumbnail/book.jpg"

---
이번에는 파이썬의 함수 대해 알아보자



---

## **함수란**
### **함수란**
* 입력값을 가지고 어떤 일을 수행한 후 그 결과물을 내어 놓는 것
* 반복되는 부분이 있을 경우, ‘반복적으로 사용되는 가치 있는 부분’을 한 뭉치로 묶어 ‘어떤 입력값을 주었을 때 어떤 결괏값을 리턴해 준다’라는 식의 함수로 작성하는 것

<br>
<br>

### **함수의 역할**
* 작성한 프로그램을 기능 단위의 함수로 분리해 놓으면 프로그램 흐름을 일목요연하게 볼 수 있기 때문
* 입력한 값이 여러 함수를 거치면서 원하는 결괏값을 내는 것을 볼 수 있다. 이렇게 되면 프로그램 흐름도 잘 파악할 수 있고 오류가 어디에서 나는지도 쉽게 알아차릴 수 있다.

<br>
<br>
<br>

## **파이썬 함수**
### **파이썬 함수 구조**
**1) 파이썬 함수 선언하기**

* `def` : 함수를 만들 때 사용하는 예약어, 필수 입력값
* `함수이름` : 사용자가 임의로 정함, 필수 잆력값
* `매개변수` : 함수에 전달할 값을 받는 변수
* `return` : 함수의 결과값(리턴값)을 리턴하는 명령어

```py
def 함수이름(매개변수1, 매개변수2, ...):
   수행할문장1
   수행할문장2
   return a, ...
   ...
```

<br>

**2) 파이썬 함수 사용하기**

```py
def add(a, b)      # a, b는 매개변수
   return a + b   # a + b는 반환값

print(add(3, 4))   # 3, 4 는 인수

# 매개변수, 리턴값, 인수는 없을 수도 있음

def hi()
   print("hi")

a = hi()
print(a)   # None   
```

* 매개변수
   * 함수에 입력으로 전달된 값을 받는 변수
   * = 입력값, 함수의 인수, 파라미터
* 인수
   * 함수를 호출할 때 전달하는 입력 값 
* 반환값
   * 함수가 돌려주는 값
   * = 결과값, 출력값, 돌려주는 값, 리턴값 


<br>
<br>
<br>

---

## **함수와 매개변수**
### **매개변수를 지정하여 호출하기**
```py
# 기존 함수
def sub(a, b):
   return a - b

# 매개변수를 지정하여 사용하기
result = sub(a=7, b=3)  # a에 7, b에 3을 전달
print(result)   # 4

result = sub(b=5, a=3)  # b에 5, a에 3을 전달 => 순서에 상관없이 사용가능함
print(result)   # 4
```

<br>
<br>

### **입력값이 몇 개가 될지 모를 때**
**1) 여러 개의 입력값을 받는 함수**
* `*매개변수명` 사용 : 매개변수 이름 앞에  `*`을 붙이면 입력값을 전부 모아 튜플로 만들어 줌
* 다른 매개변수도 동시에 사용가능 함

```py
def 함수이름(*매개변수):
    수행할문장

def add_all(*args):
   result = 0
   for i in args:
      result += i
   return result

result1 = add_all(1, 2, 3)
print(result1)   # 6

result2 = add_all(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
print(result2)   # 55
```

```py
def add_mul(choice, *args): 
   if choice == "add":   
      result = 0 
      for i in args: 
         result += i 
   elif choice == "mul": 
      result = 1 
      for i in args: 
      result *= i 
   return result 

result = add_mul('add', 1,2,3,4,5)
print(result)   # 15
result = add_mul('mul', 1,2,3,4,5)
print(result)   #120
```

<br>
<br>

### **키워드 매개변수 kwargs**

**1) 키워드 매개변수를 사용**
* 매개변수 앞에 별 2개(`**`)를 붙이기
* 매개변수 kwargs는 딕셔너리가 되고 모든  `Key=Value`  형태의 입력값이 그 딕셔너리에 저장
* kwargs는 ‘keyword arguments’의 약자, args와 마찬가지로 관례적으로 사용

```python
def print_kwargs(**kwargs):
   print(kwargs)

print_kwargs(a=1)            # {'a': 1}
print_kwargs(name='foo', age=3)   #{'age': 3, 'name': 'foo'}
```

<br>
<br>

### **매개변수 초기값 설정**
**1) 매개변수의 초기값 설정하기**
* 초깃값이 없는 매개변수는 초깃값이 있는 매개변수 뒤에 사용할 수 없음
* 초기화하고 싶은 매개변수는 항상 뒤쪽에 놓아야 함

```py
def set_character(name, age, man=True): 
    print("이름 : %s" % name) 
    print("나이 : %d" % age) 
    if man: 
        print("성별 : 남자")
    else: 
        print("성별 : 여자")

# 사용하기 - 값을 지정하지 않으면 초기값으로 셋팅됨
set_character("김요정", 1200)         # name = "김요정", age = 1200, man = True   
set_character("이요정", 10000, True)      # name = "이요정", age = 10000, man = True   
set_character("박요정", 2700, False)      # name = "이요정", age = 10000, man = False
```





<br>
<br>
<br>

---

## 함수의 리턴값

### **함수의 리턴값**
**1) 함수의 리턴값** 
* 함수의 리턴값은 `튜플` 형태로 반환됨
* 리턴값이 없는 함수에서 `return`으로 함수를 빠져나갈 수 있음

```py
def add_and_mul(a,b): 
   return a+b, a*b
   
result = add_and_mul(3,4)   # (7, 12)

# 하나의 튜플 값을 2개의 값으로 분리하여 받기
result1, result2 = add_and_mul(3, 4)

# 리턴 활용
def print_name(name): 
   if name== "메롱": 
      return 
   print("학생의 이름은 %s 입니다." % name)
```



<br>
<br>
<br>

---


## **함수 안에서 선언한 변수**
### **함수 안에서 선언한 변수의 범위**
**1) 매개변수와 함수 안에서 선언한 변수**
* 함수 안에서만 사용하는 변수일 뿐, 함수 밖의 변수와는 전혀 상관이 없음

```py
a = 1
def app(a):
    a += 1

app(a)      # 2
print(a)   # 1
```

<br>
<br>

### **함수 안에서 함수 밖의 변수를 변경하는 방법**

**1) return 사용하기**
* 값을 전달하는 것일 뿐 함수 내부의 변수와 밖의 변수는 이름이 같아도 다른 변수

```py
def app(a): 
    a += 1 
    return a

a = app(a) 
print(a)

```

<br>

**2) global 명령어 사용하기**
* `global` 
   * 함수가 함수 밖의 외부 변수에 종속됨
   * 함수 밖의 변수를 직접 사용하겠다는 의미

```py
a = 1 
def app(): 
    global a 
    a += 1

app() 
print(a)   # 2
```

<br>
<br>
<br>

---

## **lambda 예약어**
### **lambda**
**1) lambda란**
* 함수를 생성할 때 사용하는 예약어, `def`와 동일한 역할
* 읽는 법 :    `람다`
* 사용 
   * def를 사용해야 할 정도로 복잡하지 않은 경우
   * def를 사용할 수 없는 곳
   * 함수를 한 줄로 간결하게 만들 때
* 만드는 법 : `함수이름 = lambda 매개변수1, 매개변수2, ... : 표현식`
*  return 명령어가 없어도 표현식의 결괏값을 리턴

```py
add = lambda a, b: a+b
result = add(3, 4)
print(result)   # 7
```

