# SQL_ADVANCED 4주차 정규 과제 

📌SQL_ADVANCED 정규과제는 매주 정해진 분량의 『*혼자 공부하는 SQL*』 을 읽고 학습하는 것입니다. 이번주는 아래의 **SQL_ADVANCED_4th_TIL**에 나열된 분량을 읽고 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 제시된 강의를 참고하여 보완하는 것이 좋습니다.

<!-- 강의 링크는 아래와 같습니다.
https://www.youtube.com/watch?v=DMNpkj_bZIs&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=13
https://www.youtube.com/watch?v=BUHj-behLyc&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=14
https://www.youtube.com/watch?v=JrXWxku7ZIM&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=15
-->

**교재 실습 예제 파일은 08_SQL_ADVANCED_Template 레포지토리의 src 폴더에 업로드되어 있습니다. market_db 파일도 해당 폴더에 함께 포함되어 있으니 참고하시기 바랍니다.**

**👀(수행 인증샷은 필수입니다.)** 

## SQL_ADVANCED_4th_TIL

### 5장 테이블과 뷰
#### 01. 테이블 만들기
#### 02. 제약조건으로 테이블을 견고하게
#### 03. SQL 가상의 테이블: 뷰 


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.24~99    | ✅         |
| 2주차 | p.102~155   | ✅         |
| 3주차 | p.158~213  | ✅         |
| 4주차 | p.216~271 | ✅         |
| 5주차 | p.274~327 | 🍽️         |
| 6주차 | p.330~369 | 🍽️         |
| 7주차 | p.372~407 | 🍽️         |


<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 학습 내용 정리

## 1. 테이블 만들기 

<!-- 테이블 만들기에 관해 배우게 된 점을 적어주세요. -->


### 기본 개념
- **테이블**: 행(row = 레코드)과 열(column = 필드)로 이뤄진 2차원 표 (엑셀 시트와 유사)
- 테이블을 만들기 전에 **이름, 열 이름, 데이터 형식, 기본 키** 등을 먼저 설계한다.


### SQL로 테이블 만들기

```sql
CREATE DATABASE naver_db;
USE naver_db;
```
```sql
CREATE TABLE member (
  mem_id     CHAR(8) NOT NULL PRIMARY KEY,
  mem_name   VARCHAR(10) NOT NULL,
  mem_number TINYINT NOT NULL,
  addr       CHAR(2) NOT NULL,
  phone1     CHAR(3) NULL,
  phone2     CHAR(8) NULL,
  height     TINYINT UNSIGNED NULL,
  debut_date DATE NULL
);
```
```sql
CREATE TABLE buy (
  num        INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
  mem_id     CHAR(8) NOT NULL,
  prod_name  CHAR(6) NOT NULL,
  group_name CHAR(4) NULL,
  price      INT UNSIGNED NOT NULL,
  amount     SMALLINT UNSIGNED NOT NULL,
  FOREIGN KEY(mem_id) REFERENCES member(mem_id)  -- 맨 마지막에 지정
);
```

### 데이터 입력과 외래 키 오류

```sql
INSERT INTO member VALUES('TWC', '트와이스', 9, '서울', '02', '11111111', 167, '2015-10-19');
INSERT INTO buy VALUES(NULL, 'BLK', '지갑', NULL, 30, 2);
```
- `num`은 자동 증가라 `NULL`로 입력한다.
- `member`에 없는 아이디(예: `APN`)로 `buy`에 넣으면 **Error 1452** (외래 키 제약 위반)가 난다.
- 즉, **회원가입(member)이 먼저, 구매(buy)는 그다음**이다.




## 2. 제약조건으로 테이블을 견고하게 

<!-- 제약조건에 관해 배우게 된 점을 적어주세요. -->
### 제약조건
**데이터의 무결성(결함 없음)을 지키기 위해 입력값을 제한하는 조건**이다.  
=> 제약조건이 많을수록 잘못된 데이터가 들어올 가능성이 줄어 테이블이 튼튼해진다.

### 기본 키 제약조건
- **기본 키**: 행을 구분하는 식별자로, 중복과 NULL이 불가능하고 테이블당 1개만 지정할 수 있다. 
- 열 이름 뒤에 PRIMARY KEY 를 붙여주면 기본 키로 설정됨
- 기본 키를 지정하면 클러스터형 인덱스가 자동 생성된다.

### 외래 키 제약조건
: 두 테이블 사이의 관계를 연결해주고, 그 결과 데이터의 무결성을 보장해주는 역할
- **기준 테이블** : 기본 키가 있는 회원 테이블
- **참조 테이블** : 외래 키가 있는 구매 테이블
- 외래 키를 생성하는 방법은 CREATE TABLE 끝에 FOREIN KEY 키워드를 설정
```SQL
# 외래 키의 형식 

FOREIGN KEY(열_이름) REFERENCES 기준 테이블(열_이름)
```
  - 열 이름이 두 테이블에서 달라도 상관없다.
  - 기준 테이블의 값을 바꾸거나 삭제하려 하면 오류가 나는데, `ON UPDATE CASCADE` / `ON DELETE CASCADE`를 쓰면 참조 테이블에도 **자동 반영**된다.
  - 테이블을 삭제할 때는 **외래 키 테이블을 먼저**, 기준 테이블을 나중에 삭제한다.

### 기타 제약조건
- **고유 키(UNIQUE) 제약조건**
  - 중복은 안 되지만 **NULL은 허용**된다. PK와 달리 한 테이블에 여러 개 지정할 수 있다. (예: email)
- **체크(CHECK) 제약조건**
  - 입력값이 조건에 맞는지 검사한다. (예: `CHECK (height >= 100)`, `CHECK (phone1 IN ('02','031',...))`)
- **기본값(DEFAULT) 정의**
  - 값을 입력하지 않았을 때 자동으로 들어갈 값을 지정한다. (예: `height ... DEFAULT 160`)
- **널 값 허용(NOT NULL / NULL)**
  - 빈 값의 허용 여부를 정한다. NULL은 공백(`' '`)이나 0과 다르다.



> **확인문제: 다음 보기 중에서 각 문항이 설명하는 것을 고르세요.**

보기는 아래와 같습니다.
```
CHECK / DEFAULT / PRIMAY KEY / UNIQUE / NOT NULL / FOREIGN KEY
```


여기에 답과 그 이유를 적어주세요!

**1. 입력되는 데이터가 조건에 맞는지 검사하는 기능:**   
**✅ 정답:** CHECK  
**✅ 이유:** 입력값이 조건(예: height >= 100)에 맞는지 검사하고, 위반하면 오류(Error 3819)를 발생시키기 때문.

**2. 값을 입력하지 않으면 자동으로 들어갈 값:**
**✅ 정답:** DEFAULT   
**✅ 이유:** 값을 생략했을 때 미리 지정해 둔 값(예: 키 160, 국번 02)이 자동으로 입력되기 때문.

**3. 빈 값을 입력하는 것을 허용하지 않음:**  
**✅ 정답:** NOT NULL  
**✅ 이유:** 해당 열에 반드시 값을 넣어야 하므로 NULL이 들어갈 수 없게 하기 때문.


## 3. 가상의 테이블: 뷰 

<!-- 뷰에 관해 배우게 된 점을 적어주세요. -->

**뷰(View)는 데이터베이스 개체 중 하나로, '가상의 테이블'임**   
- 실제 데이터를 갖고 있지 않고, 실체는 `SELECT` 문이다.  
- 뷰에 접근하는 순간 SELECT가 실행되어 결과가 출력된다. (바탕화면 바로가기 아이콘과 비슷)
- **단순 뷰** : 하나의 테이블과 관련
- **복합 뷰** : 2개 이상의 테이블과 관련 (복합 뷰로는 테이블의 데이터를 수정할 수 없음)

**기본 문법**
```sql
CREATE VIEW v_member AS
    SELECT mem_id, mem_name, addr FROM member;

SELECT * FROM v_member WHERE addr IN ('서울', '경기');  -- 테이블처럼 조회
```
- 뷰 이름 앞에 `v_`를 붙이는 것이 일반적이다.
- 생성 `CREATE VIEW` / 수정 `ALTER VIEW` / 삭제 `DROP VIEW`
- `CREATE OR REPLACE VIEW`는 기존 뷰가 있으면 덮어쓰고, 없으면 새로 만든다.
- 뷰 정보 확인은 `DESCRIBE`(뷰의 소스 코드는 `SHOW CREATE VIEW`)를 쓴다. 뷰는 PK 정보가 표시되지 않는다.

**뷰를 사용하는 이유**
1. **보안**: 민감한 열(연락처, 키 등)은 빼고 필요한 열만 보이게 해서, 사용자에게 테이블 대신 뷰에만 접근 권한을 줄 수 있다.
2. **복잡한 SQL 단순화**: 긴 JOIN 쿼리를 뷰로 만들어 두면 `SELECT * FROM v_memberbuy WHERE ...`처럼 간단히 쓸 수 있다.

**별칭**
- 뷰의 열 이름을 테이블과 다르게 지정할 수 있다. (`AS` 사용, 띄어쓰기·한글도 가능하지만 한글은 비권장)
- 공백이 있는 열 이름은 조회할 때 **백틱(`` ` ``)**으로 묶어야 한다.

**뷰를 통한 데이터 수정/삭제/입력**

```SQL
 UPDATE v_member SET addr = '부산' WHERE mem_id = 'BLK';
 ```
- **`WITH CHECK OPTION`**: 뷰에 설정된 범위를 벗어난 값의 입력을 막는다. 
-  **`CHECK TABLE`** : 뷰가 조회되지 않을 때, 뷰의 상태를 확인해 볼 수 있다.

> **확인문제: 다음은 뷰의 특징입니다. 거리가 먼 것을 하나 고르세요.**

보기는 아래와 같습니다.
```
1️⃣ 뷰에는 테이블의 모든 열을 포함시켜야 합니다.
2️⃣ 뷰는 복잡한 SQL을 단순하게 만드는 효과가 있습니다.
3️⃣ 뷰는 보안에 도움이 됩니다.
4️⃣ 일부 사용자가 테이블에는 접근하지 못하게 하고, 뷰에만 접근하도록 설정할 수 있습니다.
```

```
정답: 1️⃣ 뷰에는 테이블의 모든 열을 포함시켜야 합니다.

이유: 뷰는 SELECT 문으로 만들기 때문에 필요한 열만 골라서 포함시킬 수 있습니다.
실제로 v_member는 member 테이블의 mem_id, mem_name, addr 3개 열만 포함합니다.
오히려 연락처 같은 민감한 열을 빼서 보안에 활용하는 것이 뷰의 장점이기 때문입니다.

```


---

# 2️⃣ 실습과제

## 1. 데이터베이스 구축

아래 코드를 MySQL Workbench에 붙여넣은 후,  
**전체 드래그 → 실행 (Ctrl + Shift + Enter)** 하여 데이터베이스를 생성하세요.

```sql
CREATE DATABASE IF NOT EXISTS week4_db;
USE week4_db;
```

## 2. 실습문제

### 💡 1. 다음 조건을 만족하는 `users` 테이블을 생성하시오.
```
- user_id는 INT이며 **기본키(Primary Key)**로 설정합니다.
- name은 VARCHAR(20)이며 NULL을 허용하지 않습니다.
- email은 VARCHAR(50)이며 중복을 허용하지 않습니다.
- signup_date는 DATE 타입으로 설정합니다.
- grade는 INT이며 기본값(Default)을 1로 설정합니다.
```

![alt text](<images/SQL 4주차 1.png>)
### 💡 2. 다음 조건을 만족하는 `orders` 테이블을 생성하시오.
```
- order_id는 INT이며 기본키(Primary Key)로 설정합니다.
- user_id는 INT이며 NULL을 허용하지 않습니다.
- amount는 INT이며 0보다 커야 합니다.
- order_date는 DATE 타입으로 설정합니다.
```

![alt text](<images/SQL 4주차 2.png>)

### 💡 3. 다음 조건을 만족하여 데이터를 삽입하시오.
```
- users 테이블에 3명 이상의 데이터를 직접 INSERT 하시오. (단, user 중 본인이 포함돼야 함)
- orders 테이블에 3건 이상의 데이터를 직접 INSERT 하시오.
```
![alt text](<images/SQL 4주차 3.png>)
![alt text](<images/SQL 4주차 4.png>)
### 💡 4. users와 orders 테이블을 활용하여 다음 컬럼을 보여주는 뷰 user_order_view를 생성하시오.
```
- user_id
- name
- amount
```

### 💡 5. 생성한 user_order_view를 조회하시오.

![alt text](<images/SQL 4주차 5.png>)

## 3. 제출 방법

1. 각 문제의 실행 결과가 보이도록 화면을 캡처합니다.
2. 테이블 생성 결과, 데이터 삽입 결과, 뷰 생성 및 조회 결과가 모두 보이도록 제출합니다.

<!-- 이 부분을 지우고 인증사진을 제출해주세요.-->

### 🎉 수고하셨습니다.






