---
title: "PostgreSQL(포스트그레스) 완전 정복"
excerpt: "포그트그레스가 무엇인지, 언제쓰이는지, 왜 쓰이는지 자세히 알아보자..."
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

# PostgreSQL이란?
## PostgreSQL이란?

**[ PostgreSQL(Postgres)이란 ]**
> 데이터를 `표(테이블)` 형태로 저장하고, SQL 로 조회/수정하는 `관계형 데이터베이스(RDBMS)`의 일종

Mysql과 비교하자면, 포스트그레스는    
• 기능이 많고 표준에 충실한 데이터베이스<br>    
• 정합성을 강하게 지키는 데이터베이스<br>    
• 복잡한 조회나 분석 쿼리를 잘 다루는 데이터베이스<br>

<br>
<br>

## PostgreSQL를 사용하는 이유
**(1) 트랜잭션, 정합성에 강하다**<br>
> 트랜잭션

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 10000
WHERE id = 1;

UPDATE accounts
SET balance = balance + 10000
WHERE id = 2;

COMMIT;
```

• 중간에 오류가 생기면 `ROLLBACK`으로 전체를 되돌릴 수 있음




> 정합성    

• `Atomicity(원자성)`: 전체 성공 or 전체 실패<br>
• `Consistency(일관성)`: 제약조건을 어기면 저장 불가<br>
• `Isolation(격리성)`: 동시에 실행돼도 꼬이지 않게<br>
• `Durability(지속성)`: 저장된 데이터는 장애가 나도 유지

<br>

**(2) 성능을 설계로 끌어올리기 좋다**<br>
> 단순히 데이터를 저장하는 것이 아니라, 빠른 SQL 실행을 위한 계획을 세우는 `쿼리 플래너`가 중요함
• 다양한 `인덱스` 옵션<br>
• 복잡합 `JOIN/집계/서브쿼리`를 잘 처리
• 병목 분석을 위한 `EXPLAIN`이 강력: DB가 느린 이유를 추척하고 개선하기 쉬움

```sql
'''인덱스'''
CREATE INDEX idx_users_email ON users(email);

'''JSONB'''
CREATE TABLE events (
  id BIGSERIAL PRIMARY KEY,
  payload JSONB NOT NULL
);

SELECT *
FROM events
WHERE payload->>'type' = 'purchase';
```

<br>

**(3)관계형임에도 확장성이 좋다**<br>
> Postgres는 `관계형`이지만 실제 서비스에서 필요한 기능이 많이 내장
• `JSON/JSONB`: 반정형 데이터를 꽤 광력하게 저장, 검색 가능<br>
• `Full Text Search`: 간단한 검색 기능 구현 가능<br>
• `Window Function`: 랭킹, 누적합, 이동평균 같은 분석 쿼리<br>
• `Materialized View`: 결과를 미리 계산해 저장해서 성능 확보<br>
• `Extensions`: PostGIS(지도/공간), 다양한 확장 모듈

<br>

**(4) 정합성을 DB 레벨에서 강하게 강제할 수 있다(feat. 제약조건)**<br>
> 포스트그레스는 DB에서 제약조건 등 규칙을 강하게 걸 수 있어서, DB가 데이터 품질을 지킬 수 있다


<br>
<br>

## PostgreSQL의 단점
**(1) 운영/튜닝 난이도가 올라갈 수 있다**<br>
> 운영 지식이 성능을 좌우한다

• 인덱스 설계<br>
• EXPLAIN으로 실행 계획 분석<br>
• 커넥션 풀 관리<br>
• autovacuum 모니터링/튜닝<br>

**(2) VACUUM(청소)이 중요하다**<br>
> Postgres는 동시성 처리를 위해 사용하는 MVCC 구조는 과거 버전 데이터(찌꺼기)가 남을 수 있어 VACUUM이 매우 중요하다

• 업데이트/삭제가 많고 테이블이 커지면: 디스크가 예상보다 빠르게 늘 수 있고, 성능이 흔들릴 수 있으며 autovacuum 튜닝이 필요해질 수 있다<br>


**(3) 초대규모 수평 샤딩이 기본 내장 기능은 아니다**<br>
> Postgres도 확장이 가능하지만, 대규모 분산/샤딩은 보통 별도 설계나 확장(Citus)이 필요


**(4) 워크로드에 따라 MySQL이 더 유리한 경우도 있다**<br>
> Postgres가 항상 더 빠른 것이 아니라, 복잡한 문제에 강한 DB에 가깝다

|구분|PostgreSQL|MySQL|
|---|---|---|
|정확성/표준/기능 폭|더 강함|비교적 약함|
|단순 CRUD, 쉬운 운영|비교적 어려움|더 편함|
|복잡한 쿼리/분석/확장 기능|더 유리|비교적 불리|
|JSON/검색/윈도우 함수|DB하나로 더 많이 해결 가능|-|


<br>
<br>

## 언제 PostgreSQL을 쓰면 좋을까?
• 유저/주문/결제처럼 정합성이 중요한 서비스<br>
• JOIN/집계/검색이 섞인 복잡한 조회가 많은 서비스<br>
• 데이터가 커질 가능성이 있고 쿼리 튜닝까지 하며 운영하고 싶은 경우<br>
• JSON 같은 유연함도 필요하지만 관계형 구조도 유지하고 싶은 경우


<br>
<br>
<br>

# 요약
> PostgreSQL은 “관계형 DB의 기본기(정합성/트랜잭션)”가 탄탄하면서도
JSONB, 검색, 분석 기능까지 폭이 넓어서 메인 서비스 DB로 정말 많이 쓰이는 선택지다.

다만 MVCC 기반이라 VACUUM/autovacuum 같은 운영 포인트가 있고,
규모가 커질수록 “잘 쓰려면” 튜닝/운영 지식이 중요해진다.