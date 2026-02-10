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

**[ FastAPI ]**
> `FastAPI`는 `Python`으로 만드는 웹 API `프레임워크`이다.    
> 쉽게 말하자면, 프론트엔드나 다른 서비스 데이터를 주고받는 서버를 빠르고 깔끔하게 만들 수 있게 도와주는 도구이다.    




<br>
<br>

**[ FastAPI를 사용하는 이유 ]** 
FastAPI를 사용하는 이유는 크게 4가지로 정리할 수 있다     

• **1)** 이름처럼 정말 빠르다
> 내부적으로 비동기(`async`)처리를 기반으로 동작하기 때문에, 트래픽이 많아져도 성능이 좋다

• **2)** 코드가 직관적이다    
• **3)** 자동 API 문서 생성    
• **3)** 타입 힌트로 안정성을 높힐 수 있다 - 잘못된 요청이 들어오면 자동으로 막아준다

<br>
<br>
<br>


# VScode에서 FastAPI 시작하기

## FastAPI 폴더 구성하기
우선 FastAPI는 일반적으로 백엔드와 프론트엔드를 구분한다    

```py
backend/
	├─ app/
	│   ├─ __init__.py
	│   └─ main.py
	├─ requirements.txt
	└─ ...
```

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

**1) 폴더 구조 만들기**    
보통 프론트앤드와 백앤드가 구분된 프로젝트는 아래와 같은 폴더구조를 갖는다

```py
project-root/
├─ backend/
│  ├─ app/
│  │  ├─ main.py        # FastAPI 엔트리포인트
│  │  ├─ api/           # 라우터들
│  │  ├─ models/        # DB 모델
│  │  ├─ schemas/       # Pydantic 스키마
│  │  └─ services/      # 비즈니스 로직
│  └─ requirements.txt
│
├─ frontend/
│  ├─ src/
│  ├─ public/
│  └─ package.json
│
└─ README.md

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



