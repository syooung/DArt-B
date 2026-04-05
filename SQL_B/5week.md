# SQL_BASIC 5주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_5th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**5주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **3 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 4문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀(수행 인증샷은 필수입니다.)** 



## SQL_BASIC_5th

### 섹션 5. 데이터 탐색 - 변환

### 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

### 4-5. 시간 데이터 연습문제 1~2번

### 4-5. 시간 데이터 연습문제 3~5번

### 4-6. 조건문 (CASE WHEN, IF)

### 4-7. 조건문 연습 문제

### 4-8. 정리

### 4-9. BigQuery 공식 문서 확인하는 법

(강의에서 연습문제가 많아서 따로 프로그래머스 문제 과제는 없습니다.)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>



<!-- 여기까진 그대로 둬 주세요-->

---

# 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

~~~
✅ 학습 목표 :
* 날짜 및 시간 데이터에 대해서 더 자세히 설명할 수 있다. 
* CURRENT_TIME, EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME 을 설명할 수 있다. 
~~~

**`CURRENT_DATETIME`**: 현재 DATETIME 출력
**`EXTRACT`** : DATETIME에서 특정 부분만 추출하고 싶은 경우  
- 요일을 추출하고 싶은 경우  
     * `DAYOFWEEK`: 한 주의 첫날이 일요일인 [1,7] 범위의 값을 반환 

**`DATETIME_TRUNC`** : 원하는 값만 남기고, 자르기   
**`PARSE_DATETIME`** : 문자열로 저장된 DATETIME을 DATETIME 타입으로 바꾸고 싶은 경우  
**`FORMAT-DATETIME`** : DATETIME 타입 데이터를 특정 형태의 **문자열** 데이터로 변환하고 싶은 경우 

--------

**`LAST_DAY`** : 마지막 날을 알고 싶은 경우(자동으로 월의 마지막 값을 계산해서 특정 연산을 할 경우)

**`DATETIME_DIFF`** : 두 DATETIME의 차이를 알고 싶은 경우

------

```
[ 정리 ]
날짜 및 시간 데이터 타입
- DATE
- DATETIME : DATE + TIME. 타임존 정보 X
- TIMESTAMP : 특정 시점에 도장찍은 값. 타임존 정보 O
- UTC : 국제적인 표준 시간. 한국은 UTC+9
- Millisecond : 1/1000초
- Microsecond : 1/1000ms

<시간 데이터 타입 변환하기>
TIMESTAMP_MILLIS
TIMESTAMP_MICROS
DATETIME
- 문자열 => DATETIME : PARSE-DATETIME
- DATETIME => 문자열 : FORMAT_DATETIME
```


# 4-6. 조건문(CASE WHEN, IF)

~~~
✅ 학습 목표 :
* 조건문 함수의 기능을 이해하고, 설명할 수 있다. 
~~~

### 조건문
- 만약 특정 조건이 충족되면, 어떤 행동을 하자  
- 특정 조건이 참일 때, A 아니면 B
- 조건에 따라 다른 값을 표시하고 싶을 때 사용

### 조건문 함수가 사용되는 이유
: 데이터 분석을 하다보면, **특정 카테고리를 하나로 합치는 전처리**가 필요할 수 있음
- 데이터를저장하는 쪽과 데이터를 분석하는 쪽이 나뉨
- 분석할 때 필요한 부분에서 조건 설정해서 변경하는 것이 더 유용

**`CASE WHEN`** : 여러 조건이 있을 경우 유용, 조건의 순서에 주의
```SQL
SELECT
 CASE
  WHEN 조건1 THEN 조건1이 참일 경우 결과
  WHEN 조건2 THEN 조건2가 참일 경우 결과
  ELSE 그 외 조건일 경우 결과
END AS 새로운_컬럼_이름
```

ex) CASE WHEN 순서

**`IF`** : 단일 조건일 경우 유용
```SQL
SELECT 
   IF (조건문, True일때의 값, False일때의 값) AS 새로운_컬럼_이름
```

 # 4-5. 시간 데이터 연습문제 & 4-7. 조건문 연습 문제

~~~
✅ 학습 목표 :
* 4-5, 4-7 각각에서 두 문제 이상 (최소 4문제) 푼 내용 정리하기
~~~

### [4-5] Q1. 트레이너가 포켓몬을 포획한 날짜(catch_date)를 기준으로, 2023년 1월에 포획한 포켓몬의 수를 계산해주세요.

```sql
# 쿼리 계산 방법: COUNT
# 데이터의 기간: 2023년 1월
# 사용할 테이블: trainer_pokemon
# Join KEY: X
# 데이터 특징: 직접 봐야함
--- catch_date: DATE 타입

SELECT
 *
FROM (
SELECT
 id,
 catch_date,
 DATE(DATETIME(catch_datetime, "Asia/Seoul")) AS catch_datetime_kr_date
FROM basic.trainer_pokemon
)
WHERE
 catch_date!=catch_datetime_kr_date

SELECT
 COUNT(DISTINCT id) AS cnt
FROM basic.trainer_pokemon
WHERE
 EXTRACT(YEAR FROM DATETIME(catch_datetime, "Asia/Seoul"))=2023
 AND EXTRACT(MONTH FROM DATETIME(catch_datetime, "Asia/Seoul"))=1
```

### [4-5] Q2. 배틀이 일어난 시간(battle_datetime)을 기준으로, 오전 6시에서 오후 6시 사이에 일어난 배틀의 수를 계산해주세요.

```SQL
SELECT
 id,
 battle_datetime,
 DATETIME(battle_timestamp, "Asia/Seoul") AS battle_timestamp_kr,
 COUNTIF(battle_datetime=DATETIME(battle_timestamp, "Asia/Seoul")) AS batle_Datetime_same_battle_timestamp_kr
 COUNTIF(battle_datetime != DATETIME(battle_timestamp, "Asia/Seoul")) AS battle_datetime_not_same_battle_timestamp_kr
FROM basic.battle

SELECT
 COUNT(DISTINCT id) AS battle_cnt
FROM basic.battle
WEHRE
 EXTRACT(HOUR FROM battle_datetime)>=6
 AND EXTRACT(HOUR FROM battle_datetime)<18
```
### [4-7] Q1.  포켓몬의 Speed가 70이상이면 빠름, 그렇지 않으면 느림으로 표시하는 새로운 컬럼 Spee_Category를 만들어 주세요.

```SQL
SELECT
  *, 
  CASE
    WHEN speed >= 70 THEN '빠름'
    ELSE '느림'
  END AS Speed_Category
FROM Basic.pokemon

--- 조건이 1개뿐이므로 `IF` 사용

SELECT
  *, 
  IF(speed >= 70, "빠름", "느림") AS Speed_Category
FROM Basic.pokemon
```
### [4-7] Q2.포켓몬의 type1에 따라 Water, Fire, Eletric 타입은 각각 물, 불, 전기로, 그 외 기타 타입은 기타로 분류하는 새로운 컬럼 'type_Korean'을 만들어 주세요.

```SQL
SELECT 
  kor_name, 
  type1,
  CASE 
    WHEN type1 = 'Water' THEN "물"
    WHEN type1 = 'Fire' THEN "불"
    WHEN type1 = 'Eletric' THEN "전기"
    ELSE "기타"
  END AS type_Korean
FROM Basic.pokemon
```



# 학습인증
![alt text](<SQL 5주차 학습인증.jpeg>)










<br>
<br>

---

# 확인문제

## 문제 1

> **🧚Q. 광윤이는 카페 주문 로그 데이터(order_log)를 분석하여, '오전(0시-11시)'과 '오후(12시-23시)'의 주문 건수를 집계하려고 합니다. 광윤이가 작성한 다음 SQL 쿼리 중 문법적으로 틀렸거나 의도한 결과가 나오지 않는 것을 모두 골라보세요. (복수 선택 가능)**

~~~sql
1. SELECT 
   IF(EXTRACT(HOUR FROM order_time) < 12, '오전', '오후') AS time_type,
   COUNT(*)
   FROM order_log
   GROUP BY time_type;

2. SELECT 
   DATETIME_TRUNC(order_time, HOUR) AS truncated_hour,
   COUNT(*)
   FROM order_log
   WHERE order_time BETWEEN '2021-01-01' AND '2021-12-31'
   GROUP BY order_time;

3. SELECT 
   FORMAT_DATETIME(order_time, '%H') AS order_hour,
   COUNT(*)
   FROM order_log
   GROUP BY 1;

4. SELECT 
    CASE 
      WHEN EXTRACT(HOUR FROM order_time) BETWEEN 0 AND 11 THEN '오전'
      ELSE '오후'
    AS time_group,
    COUNT(*)
   FROM order_log
   GROUP BY time_group;
~~~

<!-- 틀린쿼리에 대한 오류의 원인도 같이 작성해주세요. 문제에서 제공된 order_time 컬럼은 DATETIME type의 데이터를 가지고 있다고 가정합니다. -->

~~~
[2] GROUP BY order_time이라고 작성해서 원본 주문 시간(분, 초까지 포함된 시간)을 기준으로 그룹화함. 이렇게 되면 같은 시간에 들어온 주문만 묶이기 때문에 원하는 집계 결과를 얻을 수 없음.

[3] FORMAT_DATETIME 함수의 인자 순서가 틀렸기 때문에, FORMAT_DATETIME('%H', order_time)로 작성해야함.

[4] CASE 문을 열었으면 반드시 END로 닫아주어야 함.
~~~



## 문제 2

> **🧚Q. 예운이는 포켓몬 타입에 따라 설명을 부여하는 쿼리를 작성했습니다. type 1 컬럼의 값에 따라 조건을 분기했으며, 다음 SQL 쿼리를 실행했습니다.**

~~~sql
SELECT name,
       CASE 
         WHEN type1 = 'Fire' THEN 'Hot'
         WHEN type1 = 'Water' THEN 'Cool'
         ELSE 'Normal'
       END AS type_description
FROM pokemon;
~~~

> **다음 중 type_description의 결과가 'Normal'로 출력될 포켓몬은?**

| **name**   | **type1** |
| ---------- | --------- |
| Pikachu    | Electric  |
| Charmander | Fire      |
| Squirtle   | Water     |
| Bulbasaur  | Grass     |

<!-- 근거와 함께 답을 작성해주세요 -->

~~~
Pikachum, Bulbasaur이다.
type1이 Fire과 WATER이 아닌 그 외라면 NORMAL 로 출력되기 때문이다.
~~~


<br>

### 🎉 수고하셨습니다.