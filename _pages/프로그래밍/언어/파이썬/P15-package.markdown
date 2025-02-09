---
title: "[python] 16. 파이썬 패키지"
tags:
    - 파이썬기초
date:  2024-10-23
thumbnail: "/assets/img/thumbnail/book.jpg"
---
이번에는 파이썬의 패키지에 대해 알아보자



---


## **파이썬 패키지**
### **파이썬 패키지 개념**
**1) 패키지란?**
* `packages` : 관련 있는 모듈의 집합
* 파이썬 모듈을 디렉터리 구조(계층적)으로 관리할 수 있게 해줌
* 예시

```py
app/            # 패키지 app, 루트 디렉터리
   __init__.py      # 파이썬 모듈
   asset/         # 서브 디렉터리
      __init__.py
      picture.py
      sound.py
      render.py
      echo.py
      wav.py
   option/
      __init__.py
      run.py
      test.py
```


<br>

**2) 패키지 안의 함수 실행하기**
* `import 패키지명.서브디렉터리.모듈` => 사용 시    `패키지명.서브디렉터리.모듈.함수()`
* `from 패키지명.서브디렉터리 import 모듈` => 사용 시 `모듈.함수()`
* `from 패키지명.서브디렉터리.모듈 imfort 함수` => 사용 시 `함수()`

> 도트 연산자를 사용해 import할 때 가장 마지막은 모듈이나 패키지여야 함

<br>
<br>

### **파이썬 `__init__.py`**
**1) `__init__.py`의 용도**
* 해당 디렉터리가 패키지의 일부임을 알려줌
   * python 3.3 이전 버전 : 해당 디렉터리가 패키지의 일부임을 알려줌
   * python 3.3 버전부터 : 파일이 없어도 패키지로 인식하나 하위 버전 호환을 위해 생성하기도 함
* 패키지와 관련된 설정이나 초기화 코드 포함

<br>

**2) 패키지 설정, 초기화 하기**
* 패키지 변수 및 함수 정의하기
* 패키지 내 모듈 미리 import하기
* 패키지 초기화 
   * 패키지 하위 모듈의 함수를 import 할때에도 실행
   * 한 번 실행된 후에는 다시 import를 수행하더라도 실행되지 않음(처음 한 번만 실행)
   
```py
# __init__.py

# 모듈 import
from .asset.render import render

# 패키지 변수 정의
VERSION 2.0      

# 패키지 함수 정의
def print_version_opt():   
   print(f"The version of this app is {VERSION}.")

# 패키지 초기화
# 패키지를 처음 불러올 때 실행되어야 하는 코드를 작성한다.
# ex) 데이터베이스 연결, 설정파일 로드
```

<br>
<br>

### **`__all__`**
**1) `__all__` 변수
* `from 패키지.서브디렉터리 import *`: 특정 디렉터리의 모듈을 `*`를 사용하여 `import`할 때 
   * 해당 디렉터리의 `__init__.py`파일에 `__all__` 변수를 설정하고  import할 수 있는 모듈을 정의해야 함
* `from a.b.c.모듈 import *` : `__all__`이 없어도 전부 import 됨

```py
# __init__.py
__all__ = ['모듈이름']
```

<br>
<br>

### **relative 패키지**
**1) 접근자를 사용해 relative하게 import**
* 전체 경로를 사용하지 않아도 import가 가능하다
   * `..` 부모디렉터리 
   * `.` 현재 디렉터리

```py
from ..패키지.서브디렉터리 import 모듈
```
