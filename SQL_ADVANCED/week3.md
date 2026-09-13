# SQL_ADVANCED 3주차 정규 과제 

📌SQL_ADVANCED 정규과제는 매주 정해진 분량의 『*혼자 공부하는 SQL*』 을 읽고 학습하는 것입니다. 이번주는 아래의 **SQL_ADVANCED_3rd_TIL**에 나열된 분량을 읽고 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 제시된 강의를 참고하여 보완하는 것이 좋습니다.

<!-- 강의 링크는 아래와 같습니다.
https://www.youtube.com/watch?v=1YmWy-7-OhQ&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=10
https://www.youtube.com/watch?v=tuQFkzjqEGw&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=11
https://www.youtube.com/watch?v=IOCsreDYqFE&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=12
-->

**교재 실습 예제 파일은 08_SQL_ADVANCED_Template 레포지토리의 src 폴더에 업로드되어 있습니다. market_db 파일도 해당 폴더에 함께 포함되어 있으니 참고하시기 바랍니다.**

**👀(수행 인증샷은 필수입니다.)** 

## SQL_ADVANCED_3rd_TIL

### 4장 SQL 고급 문법
#### 01. MySQL의 데이터 형식
#### 02. 두 테이블을 묶는 조인
#### 03. SQL 프로그래밍 


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.24~99    | ✅         |
| 2주차 | p.102~155   | ✅         |
| 3주차 | p.158~213  | ✅         |
| 4주차 | p.216~271 | 🍽️         |
| 5주차 | p.274~327 | 🍽️         |
| 6주차 | p.330~369 | 🍽️         |
| 7주차 | p.372~407 | 🍽️         |


<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 학습 내용 정리

## 1. MySQL의 데이터 형식

### ▶️ 정수형
&rarr; 소수점이 없는 숫자. 즉 인원 수,가격, 수량

| 데이터 형식   | 바이트 수 |            숫자 범위 |
| -------- | ----: | ---------------: |
| TINYINT  |     1 |       -128 ~ 127 |
| SMALLINT |     2 | -32,768 ~ 32,767 |
| INT      |     4 |    약 -21억 ~ +21억 |
| BIGINT   |     8 |  약 -900경 ~ +900경 |

`Out of range` : 입력값의 범위를 벗어남

---
### ▶️ 문자형
&rarr; 글자를 저장하기 위해 사용하며, 입력할 최대 글자의 개수를 지정해야함.

| 데이터 형식      |   바이트 수 | 내용                                   |
| ----------- | ------: | ------------------------------------ |
| CHAR(개수)    |   1~255 | **고정길이 문자형** → 정해진 길이만큼 공간을 할당       |
| VARCHAR(개수) | 1~16383 | **가변길이 문자형** → 실제 입력한 문자 길이만큼 공간을 사용 |
--- 
### ▶️ 실수형
&rarr; 소수점이 있는 숫자
| 데이터 형식 | 바이트 수 | 설명               |
| ------ | ----: | ---------------- |
| FLOAT  |     4 | 소수점 아래 7자리까지 표현  |
| DOUBLE |     8 | 소수점 아래 15자리까지 표현 |

---

### ▶️ 날짜형
&rarr; 날짜 및 시간
| 데이터 형식   | 바이트 수 | 설명                                        |
| -------- | ----: | ----------------------------------------- |
| DATE     |     3 | 날짜만 저장. `YYYY-MM-DD` 형식으로 사용              |
| TIME     |     3 | 시간만 저장. `HH:MM:SS` 형식으로 사용                |
| DATETIME |     8 | 날짜 및 시간 저장. `YYYY-MM-DD HH:MM:SS` 형식으로 사용 |

---
### ▶️ 데이터 형 변환

**`형 변환`** : 문자형을 정수로 바꾸거나, 반대로 정수형을 문자형으로 바꾸는 것  
- **`1) 명시적인 변환`** : 직접 함수를 사용해서 변환  
- **`2) 암시적인 변환`** : 별도의 지시 없이 자연스럽게 변환

```SQL
CAST ( 값 AS 데이터_형식 [ (길이) ] )
CONVERT ( 값, 데이터_형식 [ (길이) ] ) 
```

![alt text](<SQL 3주차 1.png>)
<!-- MySQL의 데이터 형식에 관해 배우게 된 점을 적어주세요. -->
<!-- 과제 설명 예시처럼 직접 실습 후 사진 한 장 이상을 첨부해주세요. -->  



> **확인문제: 다음 보기에서 데이터 형식의 변환에 사용되는 함수를 2개 고르세요.**

보기는 아래와 같습니다.
```
CONVERT() / DATA() / CAST() / MOVE() / TYPE() / SUM() / AVG() / CURRENT_DATE()
```

```
CONVERT(), CAST()
```


## 2. 두 테이블을 묶는 조인

### 🔗 내부 조인
&rarr; 일반적으로 조인이라고 부르는 것  


**일대다(one to many) 관계**  
: 한쪽 테이블에는 하나의 값만 존재해야 하지만, 연결된 다른 테이블에는 여러 개의 값이 존재할 수 있는 관계

```sql
SELECT <열 목록>
FROM <첫 번째 테이블>
     INNER JOIN <두 번째 테이블>
     ON <조인될 조건>
[WHERE 검색 조건]
```
![alt text](<SQL 3주차 2.png>)

**내부 조인의 간결한 표현**   
&rarr; 필요한 아이디/이름/구매 물품/주소/연락처만 추출

![alt text](<SQL 3주차 3.png>)

**내부 조인의 활용**
&rarr; ***전체 회원의*** 아이디/이름/구매 물품/주소 출력

![alt text](<SQL 3주차 4.png>)

**=> 내부 조인은 두 테이블에 모두 있는 내용만 조인되는 방식임. 만약, 양쪽 중에 한곳이라도 내용이 있을 때 조인하려면 외부 조인을 사용해야 함**




### 🔗 외부 조인
&rarr; 두 테이블 모두 데이터가 있어야만 결과가 나오는 내부 조인과 달리 한쪽에만 데이터가 있어도 결과가 나옴
```SQL
SELECT <열 목록>
FROM <첫 번째 테이블(LEFT 테이블)>
    <LEFT | RIGHT | FULL> OUTER JOIN <두 번째 테이블(RIGHT 테이블)>
    ON <조인될 조건>
[WHERE 검색 조건] ;
```
![alt text](<SQL 3주차 5.png>)

![alt text](<SQL 3주차 6.png>)
<!-- 두 테이블을 묶는 조인에 관해 배우게 된 점을 적어주세요. -->
<!-- 과제 설명 예시처럼 직접 실습 후 인증 사진 4장 이상을 첨부해주세요. -->

> **확인문제: 다음 SQL은 회원으로 가입만 하고, 한 번도 구매한 적이 없는 회원의 목록을 조회하는 쿼리입니다. 빈칸에 들어갈 가장 적절한 구문을 고르세요..**

```sql
SELECT DISTINCT M.mem_id, B.prod_name, M.mem_name, M.addr
  FROM member M
    LEFT OUTER JOIN buy B
    ON M.mem_id = B.mem_id
  __________
  ORDER BY M.mem_id;
```
보기는 아래와 같습니다.
```
1. JOIN B.prod_name IS NULL
2. LIMIT B.prod_name IS NULL
3. HAVING B.prod_name IS NULL
4. WHERE B.prod_name IS NULL
```
```
✅ 정답 : 4번
✅ 이유 : '회원 테이블' 기준으로 '구매 테이블'을 외부 조인하면,  
제품을 구매한 적이 없는 회원의 경우 '구매 테이블' 항목이 모두 NULL 값으로 채워지게 됨.  
따라서 회원으로 가입만 하고 구매한 적 없는 회원 목록을 조회하기 위해서는,  
'구매 테이블' 이 NULL 값인 조건을 만족하는 행만 걸러내야 하기 때문에 WHERE절을 사용해야함.
```

## 3. SQL 프로그래밍 

<!-- IF문, CASE문, WHILE문에 관해 배우게 된 점을 적어주세요. -->

### IF 문
: 조건문으로 가장 많이 사용됨.

```SQL
IF <조건식> THEN
    SQL문장들
END IF;
```
- 두 문장 이상이 처리되어야 할 때는 `BEGIN~END` 로 묶어줘야 함

### CASE 문
: 여러가지 조건 중에서 선택해야 하는 경우

```SQL
CASE
    WHEN 조건1 THEN
        SQL문장들1
    WHEN 조건2 THEN
        SQL문장들2
    WHEN 조건3 THEN
        SQL문장들3
    ELSE
        SQL문장들4
END CASE;
```

### WHILE 문
: 반복

```SQL
WHILE <조건식> DO
    SQL 문장들
END WHILE;
```


> **확인문제: 다음은 CASE 문의 형식입니다. 빈칸에 들어갈 가장 적절한 명령어를 보기에서 고르세요..**

```sql
CASE
    (1) 조건 THEN
        SQL문장들1
    ELSE
        SQL문장들4
END (2);
```

보기는 아래와 같습니다.
```
WHEN / THEN / CURRENT / DATE / TIME / IF / END IF / CASE
```

```
여기에 답을 적어주세요!
(1) WHEN
(2) CASE
```


---

# 2️⃣ 실습과제

## 1. 데이터베이스 구축

아래 코드를 MySQL Workbench에 붙여넣은 후,  
**전체 드래그 → 실행 (Ctrl + shift + Enter)** 하여 데이터베이스를 구축하세요.

```sql
-- 1. 데이터베이스 생성
CREATE DATABASE IF NOT EXISTS week3_db;

-- 2. 사용할 데이터베이스 선택
USE week3_db;

-- 3. 기존 테이블 삭제 (초기화용)
DROP TABLE IF EXISTS orders;
DROP TABLE IF EXISTS customers;

-- 4. 테이블 생성 (조인 실습용)
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(20),
    signup_date_str VARCHAR(8) 
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,           
    order_date_str VARCHAR(8), 
    amount_str VARCHAR(10)     
);

-- 5. 데이터 삽입
INSERT INTO customers VALUES
(1, '신영', '20241528'),
(2, '경모', '20220261'),
(3, '세원', '20203401'),
(4, '진우', '20221024'),
(5, '성환', '20225100'),
(6, '혜준', '20244946'),
(7, '채은', '20250412'),
(8, '다나', '20212774'); -- 주문 없는 고객(외부 조인용)

INSERT INTO orders VALUES
(101, 1, '20240220', '12000'),
(102, 1, '20240303', '30000'),
(103, 2, '20240111', '15000'),
(104, 3, '20221201', '9000'),
(105, 5, '20231111', '20000'),
(106, 7, '20220707', '5000'),
(107, 99, '20240210', '7000'); -- 고객 테이블에 없는 customer_id (외부 조인용)
```

## 2. 실습 문제

다음 SQL 문을 작성하고 실행 결과를 확인 후 인증 사진을 아래에 업로드하세요.

1. **데이터 형식 변환**
   - orders 테이블의 `order_date_str`을 DATE 형식으로 변환하여 조회하시오.
   (힌트: STR_TO_DATE 사용)
  ![alt text](<SQL 3주차 7.png>)

2. **데이터 형식 변환**
   - orders 테이블의 `amount_str`을 숫자형으로 변환하여 조회하시오.
![alt text](<SQL 3주차 8.png>)

3. **내부 조인 (INNER JOIN)**
   - customers와 orders를 customer_id 기준으로 내부 조인하여
     고객 이름(name)과 주문 번호(order_id)를 함께 조회하시오.
![alt text](<SQL 3주차 9.png>)

4. **외부 조인 (LEFT JOIN)**
   - customers를 기준으로 LEFT JOIN을 수행하여,
     주문이 없는 고객도 함께 조회하시오.
![alt text](<SQL 3주차 10.png>)

5. **스토어드 프로시저 (IF문 사용)**
   - 입력받은 금액이 10000 이상이면 '고객 주문',
     그렇지 않으면 '일반 주문'을 출력하는
     프로시저를 생성하시오.
   - 생성 후 CALL로 실행 결과를 확인하시오.
   ![alt text](<SQL 3주차 11.png>)
   ![alt text](<SQL 3주차 12.png>)
<!-- 이 부분을 지우고 인증사진을 제출해주세요.-->


### 🎉 수고하셨습니다.






