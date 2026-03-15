# SQL_BASIC 2주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_2nd_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**2주차 과제**는 1주차 과제처럼 SQL의 필요성이나 느낀점 위주가 아닌, **실제 강의 내용을 바탕으로 개념을 정리하고 학습한 내용을 집중적으로 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요. 

**👀(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_2nd

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-3. 데이터 탐색 (SELECT, FROM, WHERE)

### 2-4. SELECT 연습문제

### 2-5. 집계 (Group By + Having + Sum/Count)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | 🍽️         |
| 4주차 | 섹션 **3-4** ~ **4-4** | 🍽️         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리 

## 2-3. 데이터 탐색 (SELECT, FROM, WHERE)

~~~
✅ 학습 목표 :
* SQL 쿼리 구조를 이해할 수 있다. 
* SELECT, FROM, WHERE의 핵심 문법을 설명할 수 있다. 
~~~

### SQL 쿼리 구조 : SELECT, FROM, WHERE

**`SELECT`**: 테이블의 **어떤 컬럼**을 선택(출력)할 것인가?
- `AS` 뒤에는 별칭, 컬럼 이름 변경
- `*` : 모든 컬럼을 출력하겠다 but, 비용 多
- `*EXCEPT` : 제외할 컬럼

**`FROM`** Dataset.Table : **어떤 테이블**에서 데이터를 확인할 것인가?  
**`WHERE`** : **만약 원하는 조건**이 있다면 어떤 조건인가?
> Col1=1: 조건문

```sql
SELECT
 * EXCEPT(eng_name)
  -- id AS pokemon_id ,
  # id AS "pokemon_id" # 컬럼 이름에 따옴표를 넣는 경우 : 자주하는 실수 => 따옴표 없이 기록
  -- kor_name,
  -- type1,
  -- total
FROM basic.pokemon
WHERE
 type1 = "Fire"
# 데이터를 활용하고 싶은 목적이 있어야, 어떤 컬럼을 선택할지 알 수 있게 됨
# 마지막에 ;(세미콜론)을 붙이면 쿼리 끝

# 가독성 있는 쿼리
# 쿼리를 잘 읽을 수 있으려면 잘 작성해야 함-> 협업 때 중요
```
<br>

| 명령어 | 설명 |
| :---: | :--- |
| **FROM** | 데이터를 확인할 Table 명시<br>이름이 너무 길다면 AS "별칭"으로 별칭 지정 가능<br>`FROM Table1 AS t1` |
| **WHERE** | FROM에 명시된 Table에 저장된 데이터를 필터링(조건 설정)<br>Table에 있는 컬럼을 조건 설정 |
| **SELECT** | Table에 저장되어 있는 컬럼 선택<br>여러 컬럼 명시 가능<br>`col1 AS "별칭"`으로 컬럼의 이름도 별칭 지정 가능 |
 

**실행 순서** `FROM` > `WHERE` > `SELECT`  
**문법 순서** `SELECT` > `FROM`> `WHERE`

## 2-4. 연습문제
### 문제 1. 
```
Q. trainer 테이블에 있는 모든 데이터를 보여주는 SQL 쿼리를 작성해주세요.
```

1) Trainer 테이블에 어떤 데이터가 있는지 확인해보기  
2) Trainer 테이블을 어디에 명시해야 할까? => FROM
3) 필터링 조건이 있을까? => 모든 데이터 => 필터링을 할 필요가 없겠다
4) 모든 데이터=> 모든 컬럼일 수도 있겠다(추측)
```sql
SELECT 
 *
FROM basic.trainer
```

### 문제 2.

```
Q. trainer 테이블에 있는 트레이너의 name을 출력하는 쿼리를 작성해주세요 
```
```sql
SELECT 
 name
FROM basic.trainer
```

### 문제 3.
```
Q. trainer 테이블에 있는 트레이너의 name, age를 출력하는 쿼리를 작성해주세요.
```
```sql
SELECT 
 name,
 age
FROM basic.trainer
```

### 문제 4.
```
Q. trainer의 테이블에서 id가 3인 트레이너의 name, age, hometown을 출력하는 쿼리를 작성해주세요.
```
```sql
SELECT 
 name,
 age,
 hometown
FROM basic.trainer
WHERE
 id = 3
```

### 문제 5.
```
Q. pokemon 테이블에서 "피카츄"의 공격력과 체력을 확인할 수 있는 쿼리를 작성해주세요.
```
```sql
SELECT 
 attack,
 hp
FROM basic.pokemon
WHERE
 kor_name = "피카츄"
 ```
<br>

## 2-5. 집계 (Group By / HAVING / SUM,COUNT)

~~~
✅ 학습 목표 :
* 데이터를 집계하고 그룹화하는 방법을 설명할 수 있다.
* GROUP BY, HAVING, ORDER BY, 집계함수(SUM/COUNT 등)을 활용하는 방법을 설명할 수 있다.
* having과 where의 차이에 대해서 설명할 수 있다.
~~~

### 집계와 그룹화 : 계산하다
: 모아서(=그룹화)해서 계산하다

**계산**  
- 더하기, 빼기
- 최대값, 최소값
- 평균
- 갯수 세기

### `GROUP BY` : 같은 값끼리 모아서 그룹화한다
- 색상을 기준으로 집계  

| 도형 ID | 색상 |
|:---|:---:|
| 1 | RED | 
| 2 | RED | 
| 3 | BLUE | 
| 4 | BLUE | 
| 5 | GREEN | 
| 6 | PINK | 

- 타입을 기준으로 그룹화해서 평균 공격력, 타입별 포켓몬 수 집계  

| 타입 | 평균공격력 | 포켓몬 수 |
|:---|:---:|:---|
| 전기 | 61 | 15 |
| 물 | 69 | 46 |
| 풀 | 65 | 21 |
| 불 | 81 | 20 |

```sql
SELECT 
    집계할_컬럼
    집계함수(COUNT,MAX,MIN 등)
FROM Table
GROUP BY 
    집계할_컬럼1
```
**집계할 컬럼을 SELECT에 명시하고 그 컬럼을 꼭 GROUP BY에 작성**

### `DISTINCT`: 고유값을 알고 싶은 경우
별개의 여러 값 중에 ** Unique한 것만 보고 싶은 경우 사용  
**DISTINCT 는 중복을 제거하는 것**
| user_id  | event            | event_date |
| ----- | ---------------------- | --------- |
| 1 | view_main_page | 2024-04-02  |
| 1 | view_main_page | 2024-04-02  |
| 2 | view_main_page | 2024-04-02  |
| 3 | view_main_page | 2024-04-02 |

- 메인 페이지의 view수  : COUNT(user_id)
- 메인페이지 view한 유저의 수 : COUNT(**DISTINCT** user_id) 

```SQL
# 1. pokemon 테이블에 있는 포켓몬 수를 구하는 쿼리를 작성해주세요.

SELECT 
 COUNT(id) AS cnt
FROM basic.pokemon

# 2. 포켓몬의 수가 세대별로 얼마나 있는지 알 수 있는 쿼리를 작성해주세요.

SELECT
 generation,
 COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY
 generatio

```
### 그룹화(집계) 활용
데이터 분석하다가 그룹화하는 경우
> - 일자별 집계 (원본 데이터는 특정 시간에 어떤 유저가 한 행동이 기록, 일자별로 집계)  
> - 연령대별 집계 (특정 연령대에서 더 많이 구매?)    
> - 특정 제품 타입별 집계 (특정 제품 타입을 많이 구매?)  
> - 앱 화면별 집계 (어떤 화면에 유저가 많이 접근?)

### 조건을 설정하고 싶은 경우 : WHERE, HAVING
### `WHERE`
: **Table에 바로** 조건을 설정하고 싶은 경우 사용  
: Raw Data 인 **테이블 데이터**에서 조건 설정

```sql
SELECT 
 컬럼1, 컬럼2
 COUNT(컬럼1) AS col1_count
FROM <table>
WHERE
 컬럼1 >= 3
```

### `HAVING`
: **GROUP BY한 후** 조건을 설정하고 싶은 경우 사용
```SQL
SELECT 
 컬럼1, 컬럼2
 COUNT(컬럼1) AS col1_count
FROM <table>
GROUP BY 컬럼1, 컬럼2
HAVING
 col1_count > 3
```

### 서브 쿼리
- SELECT 문 안에 존재하는 SELECT 쿼리
- FROM 절에 또 다른 SELECT문을 넣을 수 있음
- 괄호로 묶어서 사용

서브 쿼리를 작성하고, 서브 쿼리 바깥에서 WHERE 조건 설정하는 것  
= 서브 쿼리에서 HAVING 으로 하는 것

### `ORDER BY` : 정렬하기
```SQL
SELECT
 컬럼
FROM table
ORDER BY <컬럼><순서>
```
***순서 : DESC(내림차순), OSC(오름차순 - 보통 Default)***

ORDER BY 는 쿼리의 맨 마지막(아래)에 두고, 쿼리의 맨 마지막에만 작성하면 됨(중간에 필요없음)

### `LIMIT` : 출력 개수 제한하기
쿼리문의 결과 Row 수를 제한하고 싶은 경우 LIMIT 사용  
***쿼리문의 제일 마지막에 작성***

```SQL
SELECT
 col
FROM Table
LIMIT 10
```
```sql
# 3. 포켓몬의 수를 타입별로 집계하고, 포켓몬의 수가 10 이상인 타입만 남기는 쿼리를 작성해주세요. 포켓몬의 수가 많은 순으로 정렬해주세요.

SELECT
 type1,
 COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY
 type1
HAVING cnt >= 10
ORDER BY cnt DESC
```

# 2️⃣ 학습 인증란

![alt text](image.png)



<br><br>



---

# 3️⃣ 확인문제

## 문제 1

> **🧚Q. 포켓몬 마스터 진아는 포켓몬 데이터 조회하는 SQL문에 재미를 느껴서 혼자서 데이터를 조회하는 쿼리문을 짰습니다. 하지만 세 가지의 오류로 다음 코드가 실행이 안된다고 하는데, 각 오류의 위치와 이유를 설명하고, 올바른 쿼리문으로 수정해보세요.**

~~~sql
# 진아의 SQL Query문 
SELECT name. type
FROM pokemon;
WHERE type = Electric;
~~~



~~~
1. SELECT 절에서 여러 개의 컬럼을 한 번에 불러올 때는 마침표(.)가 아니라 쉼표(,) 로 구분을 해야함
2. 세미콜론(;)은 쿼리를 끝내는 역할이기 때문에 중간에 넣게 되면 뒤에 있는 WHERE 절을 읽지 못함
3.  특정 데이터를 조건에 넣을 때는 반드시 작은 따옴표로 감싸주어야 함. (단, 숫자 데이터는 따옴표 없이 그냥 써도 됨)
~~~



## 문제 2

> **🧚Q. 앞서 SQL Query의 오류를 해결한 진아는 기분 좋게 이번에는 포켓몬 데이터에서 타입별 평균 공격력이 60 이상인 타입만 조회하려는 쿼리를 작성하려고 했습니다. 하지만 이번에도 실수를 하여 쿼리문이 실행되지 않거나 잘못된 결과가 나오고 있는데, 쿼리에서 잘못된 부분이 무엇인지 설명하고, 올바르게 수정한 쿼리를 작성해보세요.**

~~~sql
SELECT type, AVG(attack) AS avg_attack
FROM pokemon
WHERE AVG(attack) >= 60
GROUP BY type;
~~~



~~~
WHERE 절은 데이터를 그룹으로 묶기 전(GROUP BY 이전)에 개별 데이터들을 필터링할 때 사용합니다. 따라서 포켓몬 타입별로 그룹을 묶은 후 계산된 '평균(AVG)' 값을 기준으로 조건을 걸려면, WHERE 을 HAVING으로 바꾸고, 순서도 GROUP BY 뒤로 배치해야 합니다. 
~~~



### 🎉 수고하셨습니다.