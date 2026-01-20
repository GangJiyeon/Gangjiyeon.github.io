---
title: "[FastAPI] SQLAlchemy"
excerpt: ""
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

# SQLAlchemy이란?
## SQLAlchemy이란?

**[ SQLAlchemy ]**
> SQL을 직접 사용하지 않고, `파이썬 객체`로 테이블을 정의하고 조회/삽입/수정/삭제 기능 등을 다루게 해주는 도구를 `SQLAlchemy`라고 한다

예를 들자면, 아래처럼 sql을 python 코드로 사용할 수 있다

```sql
SELECT * FROM regions;
```

```py
db.query(Region).all()
```


<br>
<br>

## SQLAlchemy의 구조

SQLAlchemy는 여러 형태로 사용할 수 있는데, 실무(?)에서는 보통 아래 그림과 같은 구조로 사용된다고 한다

![SQLAlchemy 다이어그램](https://christophergs.com/assets/images/ultimate-fastapi-tut-pt-7/diagram-overall.jpeg)

> 이미지 출처: https://christophergs.com/tutorials/ultimate-fastapi-tutorial-pt-7-sqlalchemy-database-setup/

해당 구조와 각 부분별 역할을 알아보도록 하자


**[ DB ]**
• 실제로 데이터가 저장되는 곳으로, SQL을 사용해 DB를 관리한다    
• 흔히 우리가 아는 Mysql, Postgres가 여기에 해당된다    

<br>

**[ Data Access Layer (SQLAlchemy Config) ]**
Data Access Layer는 SQLAlchemy Config를 의미하는데, SQLAlchemy Config는 Engine과 Connection으로 구성되어 있다.    

• **역할 1**: DB 주소 설정하기    
• **역할 2**: 엔진 생성하기    
• **역할 3**: 연결 관리하기

```py
engine = create_engine(...)
SessionLocal = sessionmaker(bind=engine)
```


> `요약!`     
> SQLAlchemy Config = Engine + Connection
> 파이썬과 DB를 연결하는 역할을 한다!

<br>

**[ ORM Layer ]**    
> ORM Layer는 ORM Models와 ORM Layer으로 구성된다

**(1) ORM Models**    
• 테이블을 정의한다    
• `models/*`: models/Region, models/Test, models/TestAnswer

**(2) ORM Session**    
• session을 생성하고, API에서 주입해 사용한다    
• API가 DB를 사용할 수 있게 해준다    

```py
db/session.py

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()
```

<br>

**[ Alembic Migration ]**    
• ORM 모델을 보고 migration 스크립트를 생성해 DB 구조를 변경한다    
• `alembic/*`


<br>

**[ Endpoint Logic ]**    
**(1) Pydantic Schemas**    
• 클라이언트와 약속한 API 요청/응답 형식으로, DB 모델이 아닌 JSON 구조를 가진다     
• `schemas/*`    

**(2) Path Operations**    
• `GET /regions`    

```py
@router.get("/regions")
def get_regions(db: Session = Depends(get_db)):
    return db.query(Region).all()
```

