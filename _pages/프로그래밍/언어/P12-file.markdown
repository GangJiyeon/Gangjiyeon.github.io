---

title:  "[python] 13. 파이썬 파일 읽고 쓰기"
date:   2024-10-20
 tags:
    - 파이썬기초
thumbnail: "/assets/img/thumbnail/book.jpg"

---
이번에는 파이썬의 파일 읽고 쓰기에 대해 알아보자



---

## **파이썬 파일 입출력**
### **파이썬 파일 열고 닫기**
**1) 파일을 열기위한 파이썬 내장 함수 `open()`**
* `파일객체 = open(파일이름, 파일열기모드)`
   * `파일 이름`과 `파일 열기 모드`를 입력값으로 받고 결괏값으로 `파일 객체`를 리턴
* 프로그램을 실행한 디렉터리에 새로운 파일이 하나 생성

**2) 열려 있는 파일 객체를 닫아 주는  `close()`** 
* `파일객체.close()`
* 생략 가능 : 프로그램을 종료할 때 파이썬 프로그램이 열려 있는 파일의 객체를 자동으로 닫아줌 
* 쓰기모드로 열었던 파일을 닫지 않고 다시 사용하려고 하면 오류가 발생 => 닫아줘야함
* with문으로 파일 자동 닫기 가능

```py
f = open("새파일.txt", 'w')
f.close()

# with 블록(with문에 포함된 문장)을 벗어나면, 열린 파일 객체 f가 자동으로 닫힘
with open("hi.txt", "w") as f:
    f.write("Life is too short, you need python")
```



<br>
<br>
<br>

---

## **파일 열기 모드**
### **파일 열기 모드 종류**
* `r` 읽기 모드: 파일을 읽기만 할 때 사용한다.
* `w` 쓰기 모드: 파일에 내용을 쓸 때 사용한다.
   * 해당 파일이 이미 존재할 경우 원래 있던 내용이 모두 사라짐
   * 해당 파일이 존재하지 않으면 새로운 파일이 생성됨
* `a` 추가 모드: 파일의 마지막에 새로운 내용을 추가할 때 사용한다.

<br>
<br>

### **읽기 모드로 파일 열기**
**1) readline 함수 이용하기**
* `파일객체.readline()` : 파일 한 줄 씩 읽기
*  더 이상 읽을 줄이 없을 경우, `빈 문자열('')` 리턴

```py
# 파일의 첫 번째 줄을 읽어 출력
f = open("C:/project/file.txt", 'r')
line = f.readline()
print(line)
f.close()

# 모든 줄을 읽어 화면에 출력
# 한 줄씩 읽어 출력할 때 줄 끝에  `\n`  문자가 있으므로 빈 줄도 같이 출력된다.
f = open("C:/project/file.txt", 'r')
while True:
    line = f.readline()
    if not line: 
       break
    print(line)
f.close()
```

<br>

**2) readlines 함수 이용하기**
* `파일객체.readlines()` : 파일의 모든 줄을 읽어서 각각의 줄을 요소로 가지는 리스트를 리턴
* 파일을 읽을 때 줄 끝의 줄 바꿈(`\n`) 문자도 같이 출력됨

```py
f = open("C:/project/files.txt", 'r')
lines = f.readlines()
for line in lines:
   line = line.strip()  # 줄 바꿈 문자를 제거
    print(line)
f.close()
```

<br>

**3) read 함수 이용하기**
* `파일객체.read()` : 파일의 내용 전체를 문자열로 리턴

```py
f = open("C:/project/files.txt", 'r')
data = f.read()
print(data)
f.close()
```

<br>

**4) 파일 객체를 for 문과 함께 이용하기**
* 파일 객체를 for 문과 함께 사용하여 파일을 줄 단위로 읽을 수 있음

```py
f = open("C:/project/files.txt", 'r')
for line in f:
    print(line)
f.close()
```




<br>
<br>

### **쓰기 모드로 파일 열기**
**1) 쓰기 모드로 파일 열기**

```py
f = open("new_file.txt", 'w')
# 디렉터리에 파일이 없는 상태에서 ‘new_file.txt’파일을 쓰기 모드인 'w'로 열었기 때문에 
# ‘new_file.txt’라는 이름의 새로운 파일이 현재 디렉터리에 생성
f.close()

# ‘file2.txt’파일을 `C:/project` 디렉터리에 생성
f = open("C:/project/file2.txt", 'w')
f.close()
```

<br>

> 파일 경로
* 슬래시(`/`) : `"C:/project/file2.txt"`
* 역슬래시(`\`) :  
   * 역슬래시를 2개 사용 : `"C:\\project\\file2.txt"`
   * 문자열 앞에 r 문자(raw string)를 덧붙여 사용 : `r"C:\project\file2.txt"`

<br>

**2) 파일을 쓰기 모드로 열고 내용 쓰기**
* `파일객체.write(적을내용)`

```py
f = open("C:/project/file2.txt", 'w')
for i in range(1, 11):
    data = "%d번째 줄입니다.\n" % i
    f.write(data)
f.close()
```



<br>
<br>

### **추가 모드로 파일 열기**
**1) 추가 모드로 파일을 여는 이유**
* 쓰기 모드`w`로 파일을 열 때 이미 존재하는 파일을 열면 그 파일의 내용이 모두 사라짐
* 원래 있던 값을 유지하면서 단지 새로운 값만 추가해야 할 경우에는 파일을 추가 모드   `a`로 열어 사용
* 파일이 원래 가지고 있던 내용 바로 다음부터 내용을 적을 수 있음
```py
f = open("C:/project/mine.txt",'a')
for i in range(11, 20):
    data = "%d번째 줄입니다.\n" % i
    f.write(data)
f.close()

```

