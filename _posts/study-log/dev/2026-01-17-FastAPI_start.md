---
title: "[FastAPI] FastAPI란? / VScode에서 FastAPI 시작하기 - 수정중"
excerpt: "파이썬 가상환경 설정, FastAPI 구조"
categories:
  - dev
tags: [DB]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

<br>
<br>
<br>

# FastAPI란? 
## FastAPI란?

**[ SQLAlchemy ]**
> SQL을 직접 사용하지 않고, `파이썬 객체`로 테이블을 정의하고 조회/삽입/수정/삭제 기능 등을 다루게 해주는 도구를 `SQLAlchemy`라고 한다




<br>
<br>

## FastAPI를 사용하는 이유


**[ DB ]**
• 실제로 데이터가 저장되는 곳으로, SQL을 사용해 DB를 관리한다    
• 흔히 우리가 아는 Mysql, Postgres가 여기에 해당된다    

<br>

**[ Data Access Layer (SQLAlchemy Config) ]**
Data Access Layer는 SQLAlchemy Config를 의미하는데, SQLAlchemy Config는 Engine과 Connection으로 구성되어 있다.    

• **역할 1**: DB 주소 설정하기    
• **역할 2**: 엔진 생성하기    
• **역할 3**: 연결 관리하기

<br>
<br>
<br>


# VScode에서 FastAPI 시작하기

## FastAPI 폴더 구성하기

<br>
<br>

## 파이선 가상환경 설정하기
**1) 백엔드 폴더로 이동하기(필수X)**: `cd backend`<br>
**2) 가상환경 만들기**: `python3.11 -m venv .venv`<br>
**3) 가상환경 활성화하기(맥os/리눅스)**: `source .venv/bin/activate`<br>
**4) vscode 인터프리터 설정**: `which python` 의 값을 `cmd + shift + p` 후 인터프리터로 선택<br>
> 만약 root에서 가상환경을 설정하지 않으면 vscode가 `.venv`를 프로젝트 인터프리터로 인식하지 못해서, 따로 추가해준 후 선택한다

**5) requirements.txt 파일 생성 후 내용 입력**: `pip freeze > requirements.txt`<br>
**4) 의존성 설치**: `pip install -r requirements.txt`

<br>
<br>

## FastAPI 초기 셋팅하기

**1) 폴더 구조 만들기**: 

```py
backend/
	├─ app/
	│   ├─ __init__.py
	│   └─ main.py
	├─ requirements.txt
	└─ ...
```

> `__init__.py`는 파이썬 패키지용 파일

<br>

**2) FastAPI 앱 초기화 `(app/main.py)`**: 

```py
from fastapi import FastAPI

app = FastAPI(
    title="Whalley Commu API",
    version="0.1.0"
)

@app.get("/health")
def health_check():
    return {"status": "ok"}

```

• 이름은 `app` (Uvicorn이 찾는 객체)<br>
• `/health`는 인증 없이 접근 가능<br>
• 나중에 로드밸런서/헬스체크에도 그대로 씀<br>

<br>

**3) 작동 테스트 `(app/main.py)`**: <br>

```
cd backend
source .venv/bin/activate
uvicorn app.main:app --reload
```

`http://127.0.0.1:8000/health` 접속되면 성공!



