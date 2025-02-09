---

title:  "[python] 14. 파이썬 클래스"
date:   2024-10-21
 tags:
    - 파이썬기초
thumbnail: "/assets/img/thumbnail/book.jpg"

---
이번에는 파이썬의 클래스에 대해 알아보자



---




## **파이썬 클래스**
### **객체와 클래스**
**1) 클래스**
* 클래스(class)란 똑같은 무언가를 계속 만들어 낼 수 있는 설계 도면
* 클래스는 객체의 구조와 행동을 정의
* 객체의 클래스는 초기화를 통해 제어

**2) 객체(object)**
* 클래스로 만든 피조물
* 객체마다 고유한 성격을 가짐
* 동일한 클래스로 만든 객체들은 서로 전혀 영향을 주지 않음
* 객체는 클래스로 만들고 1개의 클래스는 무수히 많은 객체를 만들 수 있음

> 객체와 인스턴스의 차이

```py
class Cookie
   pass

a = Cookie()
# a : 클래스 Cookie로 만든 객체, Cookie의 인스턴스
# 인스턴스는 관계 클래스와의 관계를 설명할 때 사용
```

<br>
<br>

### **클래스 사용하기**
**1)  클래스 관련 개념**
* `메서드(method)` : 클래스 안에 구현된 함수
   * 파이썬 메서드의 첫 번째 매개변수 이름은 관례적으로 self를 사용 (객체 호출 시 호출한 객체 자신이 전달 되기 때문)
* `객체변수 = 속성` : 객체에 생성되는 객체만의 변수
* 매서드 호출하기
   * 메서드 호출 방법1 : `객체.메서드`, self를 반드시 생략해서 호출
   * 메서드 호출 방법2 : `클래스.메서드`, 잘 사용하지는 않음

```py
class StudentInfo
   def setdata(self, code, score):   # 메서드
      self.code = code
      self.score= score
   def printdata(self):
      print("%d 학생의 점수는 : %d" % (code, score))
```

```py
stu1 = StudentInfo()
stu2 = StudentInfo()

# stu1 객체에 객체변수 code, score가 생성되고 값 저장
stu1.setdata(0001, 78)   

# stu2 객체에 객체변수 생성, code = 0002, score = 79
StudentInfo.setdata(stu2 , 0002, 79)

stu1.printdata()   # 0001 학생의 점수는 : 78
stu2.printdata()   # 0002 학생의 점수는 : 79
```

<br>

**2) 생성자**
* `생성자(constructor)` : 객체가 생성될 떄 자동으로 호출되는 매서드
*   `__init__`을 사용한 메서드는 생성자가 됨
* 언제 사용 : 객체에 초깃값을 설정할 때 생성자를 구현
* 생성자를 사용하면 객체를 생성할 때 필요한 값도 함께 전달해주어야 함
* 다른 메서드와 마찬가지로 첫 번째 매개변수 `self` 에 생성되는 객체가 자동 전달 됨

```py
class StudentInfo
   # 생성자 __init__ 메서드
   def __init__(self, code, score):   
      self.code = code
      self.score= score
   def setdata(self, code, score):   
      self.code = code
      self.score= score
   def printdata(self):
      print("%d 학생의 점수는 : %d" % (code, score))
```

```py
stu3 = StudentInfo(0003, 99)
```

<br>
<br>

### **클래스의 상속과 오버라이딩**
**1) 클래스의 상속**
* 상속(Inheritance) : 어떤 클래스를 만들 때 다른 클래스의 기능을 물려받을 수 있게 만드는 것
    * 상속할 클래스의 모든 기능을 사용할 수 있게 됨
* 상속 방법 : `class 클래스_이름(상속할_클래스_이름)`

```py 
class ScoreSystem(StudentInfo):
    pass
```

<br>

* 상속을 사용하는 이유*
    * 기존 클래스를 변경하지 않고 기능을 추가하거나 기존 기능을 변경하려고 할 때
    * 기존 클래스가 라이브러리 형태로 제공되거나 수정이 허용되지 않는 상황이라면 상속을 사용해야 함


```py
class ScoreSystem(StudentInfo):
    def pow(self):
            result = self.first ** self.second
            return result
```

<br>


**2) 메서드 오버라이딩**
* 메서드 오버라이딩(method overriding) : 부모 클래스(상속한 클래스)에 있는 메서드를 동일한 이름으로 다시 만드는 것
* 메서드를 오버라이딩하면 부모 클래스의 메서드 대신 오버라이딩한 메서드가 호출됨


```py
class ScoreSystem(StudentInfo):
    def scoreprint(self):
            print(self.score)
```

<br>
<br>

### **클래스변수**
**1] 클래스변수**
* 클래스 안에 변수를 선언하여 생성
* 클래스 변수 사용
    * `클래스_이름.클래스변수`
    * 클래스로 만든 객체를 이용
* 클래스변수는 객체변수와 달리 클래스로 만든 모든 객체에 공유

```py
class Family:
    lastname = "김" # 클래스변수
```

```py
print(Family.lastname)  # 김
```


```py
    a = Family()
    b = Family()
    print(a.lastname)    # 김
    print(b.lastname)    # 김

    Family.lastname = "박"
    print(a.lastname)    # 박
    print(b.lastname)    # 박
```


> 클래스변수와 동일한 이름의 객체변수를 생성
객체변수는 클래스변수와 동일한 이름으로 생성할 수 있음
객체변수와 클래스변수는 서로 상관이 없음


```py
    # a 객체에 lastname이라는 객체변수가 새롭게 생성
   a.lastname = "최"
   print(Family.lastname)    # 박
```

