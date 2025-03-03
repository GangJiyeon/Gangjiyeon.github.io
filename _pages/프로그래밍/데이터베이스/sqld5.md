---
title: "[SQLD] 2과목 - 3. 관리구문"
tags:
    - SQLD
date: "2025-03-03"
thumbnail: "/assets/img/thumbnail/pic1.jpg"
---


# DML(Data Manipulation Language) 
---
## **💡 DML(Data Manipulation Language)**
> 데이터 INSERT(삽입), UPDATE(수정), DELETE(삭제), MERGE(병합)을 담당하는 언어

👉 반드시 commit이나 rollback을 통한 트랜젝션 제어가 필요함

<br>
<br>


## **💡 INSERT**
> 테이블에 행을 삽입할 때 사용

• ORACLE: 모든 삭제와 삽입의 단위는 행이므로, 한 번에 한 행만 입력가능
• SQL Server: 한 번에 여러개의 행 입력 가능 > 서브쿼리 사용하기

<br>

**[ INSERT 규칙 ]**

(1) 컬럼별 데이터 타입과 크기에 맞게 삽입
(2) 하나의 컬럼에는 한 값만 삽입 가능
• 문자 컬럼에 숫자값 입력 가능, 숫자 컬럼에 숫자형태의 문자열 입력 가능 => 권장X
(3) 작성하지 않은 컬럼은 NULL 입력
(4) NOT NULL 칼럼에 NULL 입력 시 오류 발생

<br>

**[ 컬럼에 값 입력하기 ]**
• 일부 컬럼만 입력: INTO 절에 컬럼명을 명시

```sql
INSERT INTO 테이블명 
(컬럼1, 컬럼2, ...) VALUES (값1, 값2, ...);
```

• 전체 컬럼 입력: 테이블 명 뒤 컬럼명 생략 가능

```sql
-- 테이블 이름 뒤 컬럼이름 생략
INSERT INTO 테이블명 
VALUES (값1, 값2, ...);
```

<br>

**[ INSERT Action ]**
> `Automatic`, `Set Null`, `Set Default`, `Dependent`, `No Action`

• Automatic: Master(참조) 테이블에 PK가 없는 경우 Master PK를 생성한 후 Child 입력
• Set Null: Master 테이블에 PK가 없는 경우 Child 외부키를 Null 값으로 처리
• Set Default: Master 테이블에 PK가 없는 경우 Child의 지정된 Default 값으로 입력
• Dependent: Master 테이블에 PK가 존재할 때만 Child 입력 허용
• No Action: 참조무결성을 위반하는 입력 액션을 취하지 않음

<br>
<br>

## **💡 UPDATE**
> 데이터를 수정할 때 사용

<br>

**[ UPDATE 규칙 ]**
• 컬럼 단위로 작업 수행
• WHERE 절을 생략하면 모든 행 수정

<br>

**[ 컬럼 값 수정하기 ]**
• 단일컬럼 수정하기

```sql
UPDATE 테이블명
SET 수정할컬럼명 = 값
WHERE 조건;
```

• 다중컬럼 수정하기 

```sql
UPDATE 테이블명
SET 수정할컬럼명1 = 값1, 수정할컬럼명2 = 값2, ...
WHERE 조건;
```


```sql
UPDATE 테이블명
SET (수정할컬럼명1, 수정할컬럼명2, ...) = (값1, 값2, ...)
WHERE 조건;
```

=> 수정 값으로는 상수도 사용 가능하고, 서브쿼리를 통해 설정할 수도 있음

<br>
<br>

## **💡 DELETE**
> 데이터를 삭제할 때 사용, 행단위 실행

<br>

**[ 행 삭제하기 ]**

```sql
DELETE 
[FROM] 테이블명
[WHERE 조건];
```

<br>

**[ DELETE / MODIFY 옵션 ]**
> `Cascade`, `Set Null`, `Set Default`, `Restrict`

• Cascade: Master 삭제 시 Child 같이 삭제
• Set Null: Master 삭제 시 Child 해당 필드 Null
• Set Default: Master 삭제 시 Child 해당 필드 Default 값으로 설정
• Restrict: Child 테이블에 PK 값이 없는 경우만 Master 삭제 허용


<br>
<br>

## **💡 MERGE**
> 참조 테이블을 기준으로 다른 테이블을 수정하는 것으로 데이터 병합 시 사용

<br>

**[ MERGE 규칙 ]**
• INSERT, UPDATE, DELETE 작업을 동시에 수행
• ON (연결조건): 괄호 필수
• UPDATE/DELETE (조건): 괄호 생략 가능
• UPDATE 문에서는 테이블 명X
• INSERT문에서는 INTO X

```sql
MERGE INTO 테이블명
USING 참조테이블명
ON (테이블명.컬럼명 = 참조테이블명.컬럼명)
WHEN MATCHED THEN
	UPDATE (SET 테이블명.컬럼명 = 참조테이블명.컬럼명)
	DELETE (조건)
WHEN NOT MATCHED THEN
	INSERT VALUES(참조테이블명.컬럼1, ...);
```


<br>
<br>
<br>


# TCL(Transaction Control Language) 
---

## **💡 트랜잭션**
> 트랜잭션: 데이터베이스의 논리적 연산 단위(하나의 연속적인 업무 단위)

👉 분할 할 수 없음, 모두 COMMIT하거나 ROLLBACK 처리 해야함

<br>

**[ 트랜잭션의 ACID 특징 ]**
• 원자성(atomicity): 트랜잭션 정의된 연산들 모두 성공적으로 실행되거나 전혀 실행되지 않은 상태로 남아있어야 함
• 일관성(consistency): 트랜잭션 실행 전 데이터베이스 내용이 잘못되어 있지 않다면 실행 이후에도 잘못이 있으면 안 됨
• 고립성(isolation): 트랜잭션 실행 중 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어서는 안 됨
• 지속성(durability): 트랜잭션이 성공적으로 수행되면 갱신한 데이터베이스 내용이 영구적으로 저장

<br>
<br>

## **💡 TCL(Transation Control Language)**
> 트랜잭션 제어어: DML에 의해 조작된 결과를 작업단위 별로 제어하는 명령어

(1) COMMIT과 ROLLBACK 포함
(2) DML 수행 후 트랜잭션을 정상 종료하지 않으면 LOCK 발생
• LOCK(잠금): 트랜잭션이 수행하는 통한 특정 데이터에 대해서 다른 트랜잭션이 동시에 접근하지 못하도록 제한
• 잠금이 걸린 데이터는 잠금을 실행한 트랜잭션만이 접근, 해제 가능(관리자 권한 계정 제외)

<br>
<br>

## **💡 COMMIT과 ROLLBACK**
> COMMIT: 입력, 수정, 삭제한 데이터에 이상이 없을 경우 데이터를 저장하는 명령어
> ROLEBACK: 테이블 내 입력한 데이터나 수정한 데이터, 삭제한 데이터에 대해 변경을 취소하는 명령어

<br>

**[ COMMIT 규칙 ]**
• 한번 COMMIT을 수행하면 COMMIT 이전에 수행된 DML은 되돌릴 수 없음
• ORACLE: DDL 시 AUTO COMMIT(23c 이전)
• SQL Server: AUTO COMMIT 비활성화 설정 가능 

<br>

**[ ROLLBACK 규칙 ]**
• 데이터베이스에 저장되지 않고 최종 COMMIT 지점, 변경 전, SAVEPOINT 지점 중 하나로 원복
• 최종 COMMIT 시점 이전까지 ROLLBACK 가능
> SAVEPOINT: 트랜잭션 내에서 롤백을 부분적을 수행하기 위해 사용되는 지점
COMMIT 이전을 제외한 사용자가 원하는 위치와 이름으로 설정가능

<br>

**[ 사용하기 ]**

```sql
INSERT INTO 테이블 VALUES(1, 2);

-- COMIIT 사용하기
COMMIT;					

-- SAVEPOINT 지정하기
SAVEPOINT TO SAVEPOINT명;		
INSERT INTO 테이블명 VALUES(3, 4);

-- ROLEBACK 사용하기
ROLLBACK TO SAVEPOINT명;		
```




<br>
<br>
<br>

# DDL(Data Definition Language) 
---

## **💡 DDL(Data Definition Language)**
> 데이터 정의어로 객체 생성, 변경, 삭제 등 데이터 구조를 정의하는 언어

• 종류: `CREATE(객체생성)`, `ALTER(객체변경)`, `DROP(객체삭제)`, `TRUNCATE(구조는 유지하고 데이터삭제)`
• ORACLE은 AUTO COMMIT(자동 저장돼 복구X) O, SQL Server X


<br>
<br>

## **💡 제약조건**

> 데이터 무결성을 위해 각 컬럼에 생성하는 데이터의 제약 장치

<br>

**[ 제약조건의 종류 ]**
**(1) PRIMARY KEY(기본키)**
• 각 행을 구별할 수 있는 유일한 식별자
• 중복(UNIQUE), NULL을 허용하지 않음: 컬럼에 PRIMARY KEY를 생성하면 NOT NULL 속성이 자동으로 부여 됨
• PK 생성 시 자동으로 UNIQUE INDEX를 생성할 수 있음
• CTAS로 테이블 복사 시 PK, NOT NULL 속성은 복사되지 않음
• 하나의 테이블에 여러 기본키를 생성할 수 없지만, 여러 컬럼을 결합하여 생성할 수는 있음
**(2) NOT NULL**
• 다른 제약조건과 달리 컬럼의 특징을 나타내므로 CTAS로 복제가 가능함
• 컬럼 생성 시에 NOT NULL을 선언하지 않으면 Nullable 컬럼으로 생성
• 이미 있는 컬럼에 NOT NULL 선언을 하고 싶으면 MODIFY로 해결해야 함
**(3) FOREIGN KEY**

```sql
CREATE TABLE 테이블명(
	컬럼1 데이터타입 [DEFAULT 값] PREPERENCES 참조테이블명(참조키),
	컬럼2 데이터타입 [DEFAULT 값] PREPERENCES 참조테이블명(참조키),
	...
)
```

• 참조 테이블의 참조 컬럼에 있는 데이터를 확인하면서 본 테이블 데이터를 관리하기 위해 생성
• 반드시 참조 테이블의 참조 컬럼이 PK나 UNIQUE KEY를 가져야 함
• 옵션
	‣ ON DELETE CASCADE: 부모 데이터 삭제 시 자식 데이터도 같이 삭제
	‣ ON DELETE SET NULL: 부모 데이터 삭제 시에 자식 데이터의 참조값이 NULL로 변경
**(4) CHECK**
• 직접적으로 데이터의 값 범위(도메인)을 제한하는 제약조건

<br>

**[ 제약조건 정의하기 ]**

• 테이블을 생성할 때 제약조건 정의하기

```sql
CREATE TABLE 테이블명(
	컬럼1 데이터타입 [DEFAULT 기본값] [[CONSTRAINT 제약조건명] 제약조건 종류],
	컬럼2 데이터타입 [DEFAULT 기본값] [[CONSTRAINT 제약조건명] 제약조건 종류],
	...
)
```

•  컬럼을 추가할 때 제약조건 정의하기

```sql
ALTER TABLE 테이블명
ADD 컬럼명 데이터타입 [DEFAULT 기본값] [[CONSTRAINT 제약조건명] 제약조건 종류];
```

•  컬럼을 변경할 때 제약조건 정의하기

```sql
ALTER TABLE 테이블명
ADD [[CONSTRAINT 제약조건명] 제약조건 종류];
```

<br>

**[ 제약조건 삭제하기 ]**

```sql
ALTER TABLE 테이블명
DROP CONSTRAINT 제약조건명;
```

<br>
<br>





## **💡 CREATE**
> 테이블이나 인덱스와 같은 객체를 생성하는 명령어

<br>

**[ 테이블 생성하기 ]**
(1) 필수 정의: 테이블명, 컬럼명, 컬럼순서, 컬럼크기, 컬럼의 데이터타입
(2) 생략 가능: 각 컬럼의 제약조건, 기본값, 소유자(생략 시 명령어 수행 계정이 소유자가 됨), 숫자컬럼의 사이즈
(3) 명시 불가능: 날짜 컬럼

```sql
CREATE TABLE [소유자.]테이블명
(
	컬럼1 테이터타입 [DEFAULT 기본값1] [제약조건],
	컬럼2 테이터타입 [DEFAULT 기본값2] [제약조건],
	...
);
```

<br>

**[ 테이블 복제 ]**
(1) 복제되는 것: 복제테이블의 컬럼명, 컬럼의 데이터 타입, NULL 속성
•  SELECT문에서 컬럼별칭 사용 시 컬럼별칭 이름으로 생성
•  CREATE문에서 컬럼명 변경 가능
(2) 복제되지 않음: 테이블의 제약조건, INDEX

```sql
CREATE TABLE 테이블명
AS
SELECT * FROM 복제테이블명;
```

<br>
<br>

## **💡 ALTER**
> 테이블 구조를 변경하는 명령어

(1)변경가능: 컬럼명, 컬럼 데이터타입, 컬럼 사이즈, default 값, 컬럼 삭제, 컬럼 추가, 제약조건 변경
(2)변경불가능: 컬럼순서는 변경할 수 없고, 재생성으로 해결해야함

<br>

**[ 컬럼추가 ]**
(1) 필수규칙: 무조건 맨 마지막에 위치, 데이터 타입 명시 필수
(2) ORACLE 에서는 괄호를 사용해 여러 컬럼을 동시에 추가할 수 있음
(3) NOT NULL 속정 지정: DEFAULT 값을 선언하거나 데이터가 없는 경우 가능


```SQL
ALTER TABLE 테이블명 
ADD 컬럼명 데이터타입 [DEFAULT] [제약조건];
```

<br>

**[ 컬럼속성 변경 ]**

• 컬럼 사이즈, 데이터 타입, DEFAULT값, 컬럼명 변경 가능
• 여러 컬럼을 동시에 변경할 수 있음


**(1) 컬럼 사이즈 변경**
• 증가는 항상 가능, 축소는 데이터가 존재할 때 데이터의 길이까지만 축소 가능
• 동시 변경 가능

```sql
ALTER TABLE 테이블명
MODIFY 컬럼명(크기), 컬럼명(크기),...;
```

**(2) 데이터타입 변경**
• 데이터가 없는 경우 자유롭게 변경 가능
• CHAR, VARCHAR의 경우에는 데이터가 있어도 서로 변경 가능

```sql
ALTER TABLE 테이블명
MODIFY (컬럼명 DEFAULT 값);
```

**(3) DEFAULT 값 변경**
• INSERT 시 DEFAULT값이 선언된 컬럼에 NULL을 직접 입력하면 NULL이 저장
• 이미 데이터가 존재하는 테이블에 DEFAULT값을 선언할 경우 기존 데이터는 수정되지 않음
• DEFAULT값을 해제할 경우 DEFAULT값을 NULL로 선언하면 됨

```sql
ALTER TABLE 테이블명
MODIFY (컬럼명 DEFAULT 값);
```

**(4) 컬럼명 변경**

```sql
ALTER TABLE 테이블명
RENAME COLUMN 기존컬럼명 TO 바꿀 컬럼명
```

<br>

**[ 컬럼 삭제 ]**

• 데이터의 존재 여부와 상관없이 항상 가능함
• RECYCLEBIN에 남지 않기때문에 복구가 불가능함
• 동시에 삭제가 불가능함

```sql
ALTER TABLE 테이블명
DROP COLUMN 컬럼명;
```

<br>
<br>

## **💡 DROP**
> DROP: 테이블 또는 INDEX와 같은 객체를 삭제하는 명령어

• DROP 이후에는 조회가 불가능함
• PURGE로 테이블을 삭제하면 RECYCLEBIN에서 조회할 수 없음

```sql
DROP TABLE 테이블명 [PURGE];
```

<br>
<br>

## **💡 TRUNCATE**
> TRUNCATE: 객체 구조는 남기고 데이터만 삭제하는 명령어

• AUTO COMMIT되므로 RECYCLEBIN에 남지 않고 복구가 불가능함

```sql
TRUNCATE TABLE 테이블명 [PURGE];
```

<br>
<br>

## **💡 DELETE vs DROP vs TRUNCATE**

|명령어|설명|ROLEBACK 여부|
|:---:|:---:|:---:|
|`DELETE`|데이터 일부/전체 삭제|가능|
|`TRUNCATE`|데이터 전체 삭제|불가능|
|`DROP`|데이터 구조 삭제|불가능|


<br>
<br>
<br>



# DCL(Data Control Language)
---

## **💡 DCL(Data Control Language)**
> 데이터 제어어

• 객체에 대한 권한을 부여(GRANT)하거나 회수(REVOKE)하는 기능
• 테이블 소유자는 타계정에 테이블 조회 및 권한을 부여하거나 회수할 수 있음

<br>
<br>

## **💡 권한**
> 특정 사용자나 역할이 데이터베이스 객체(테이블, 뷰, 스키마 등)에 대해 수행할 수 있는 작업을 정의하는 규칙 

**(1) 오브젝터 권한**
• 테이블에 대한 권한을 제어함: SELECT, INSERT, UPDATE, DELETE, MERGE
• 테이블 소유자는 타계정 소유 테이블에 대해 조회, 수정 권한을 부여하거나 회수 가능
**(2) 시스템 권한**
• 시스템 작업에 대한 권한을 제어함: 테이블 생성, 인덱스 삭제
• 관리자 권한만 권한을 부여하거나 회수 가능

<br>
<br>

## **💡 GRANT**
>권한을 부여하는 명령어

• 반드시 소유자나 관리자 계정으로 접속해 권한 부여
• 동시에 여러 유저에 대한 권한 부여 가능, 여러 객체에 대한 권한 부여 불가능

```sql
GRANT 권한 ON 테이블명 TO 유저;
```

<br>
<br>

## **💡 REVOKE**
> 권한을 회수하는 명령어

권한 회수 시
• 동시에 여러 유저로부터 여러 권한 회수 가능
• 이미 회수한 권한을 재회수 하는 것은 불가능 > 오류 발생

```sql
REVOKE 권한 ON 테이블명 FROM 유저;
```

<br>
<br>

## **💡 ROLE**
> ROLE: 권한의 묶음, CREATE로 생성할 수 있는 객체
• SYSTEM 계정에서 ROLE 생성 가능
• ROLE에서 회수된 권한은 즉시 반영되므로 다시 ROLE을 부여할 필요가 없음

<br>

**[ ROLE 사용하기 ]**
• ROLE 생성

```sql
CREATE ROLE 롤이름;
```

• ROLE 부여

```sql
GRANT 롤이름 TO 유저;
```

• ROLE에서 권한 제외

```sql
REVOKE SELECT ON 유저 FROM 롤이름;
```

<br>
<br>

## **💡 권한부여 옵션**
> 권한부여 옵션: 중간 관리자를 둘 때 사용하는 옵션

**(1) WITH GRANT OPTION**
• 받은 오브젝트 권한을 다른 사용자에게 부여할 수 있음
• 중간관리자가 부여한 권한은 중간관리자만 회수할 수 있음
• 중간관리자에게 부여된 권한이 회수될 경우 제 3자에게 부여된 권한도 같이 회수됨
**(2) WITH ADMIN OPTION**
• WITH GRANT OPTION을 통해 부여 받은 시스템 권한이나 ROLL 권한을 다른 사용자에게 부여
• 중간관리자가 부여한 권한도 총괄관리자가 직접 회수 가능
•  중간관리자에게 부여된 권한이 회수 될 경우 제 3자에게 부여된 권한은 회수되지 않고 남아있음


<br>
<br>

## 💡 객체

**[ View(뷰) ]**
> 테이블처럼 물리적으로 디스크에 저장되지는 않지만 메타 데이터가 생성되어 조회 및 수정할 수 있는 객체

• 자주 사용하는 쿼리를 View로 설정하면 별칭처럼 간단하게 사용할 수 있음

```sql
-- 뷰 생성
CREATE [OR REPLACE] VIEW 뷰이름
AS 조회쿼리;

-- 뷰 삭제
DROP VIEW 뷰명;
```

<br>

**[ SEQUENCE(시퀀스) ]**
> SEQUENCE: 자동으로 연속적인 숫자를 부여해주는 객체

```sql
CREATE SEQUENCE 시퀀스명
INCREMENT BY	-- 증가값(DEFAULT 1)
START WITH 		-- 시작값(DEFAULT 1)
MAXVALUE 		-- 마지막값(증가시퀀스), 재사용 시 시작값(감소시퀀스)
MINVALUE		-- 시작값(감소시퀀스), 재사용 시 마지막값(증가시퀀스)
CYCLE | NOCYCLE	-- 시퀀스 번호 재사용
CACHE N			-- 캐시값(DEFALT 20)
;
```

<br>

**[ SYNONYM(시노님) ]**
> SYNONYM: 테이블의 별칭을 생성하는 객체

(1) 본인 소유 테이블이 아니더라도 테이블의 별칭을 붙여 간단하게 조회할 수 있음
(2) 사용하기
• OR REPLACE: 기존에 같은 이름으로 시노님이 생성되어 있는 경우에 대체
• PUBLIC: 시노님을 생성한 유저만 사용 가능한 PRIVATE SYNONYM의 반대로 누구나 사용 가능
• PUBLIC으로 생성한 시노님은 반드시 PUBLIC으로 삭제해야 함

```sql
CREATE [OR REPLACE] [PUBLIC] 
SYNONYM 별칭 FOR 테이블명;
```
