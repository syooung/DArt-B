# SQL_ADVANCED 7주차 정규 과제 

📌SQL_ADVANCED 정규과제는 매주 정해진 분량의 『*혼자 공부하는 SQL*』 을 읽고 학습하는 것입니다. 이번주는 아래의 **SQL_ADVANCED_7th_TIL**에 나열된 분량을 읽고 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 제시된 강의를 참고하여 보완하는 것이 좋습니다.

<!-- 강의 링크는 아래와 같습니다.
https://www.youtube.com/watch?v=KZmW6VaY5BU&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=16
https://www.youtube.com/watch?v=vWTDuoSG-YQ&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=17
https://www.youtube.com/watch?v=aiMSluMNzI8&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=18
-->

**교재 실습 예제 파일은 08_SQL_ADVANCED_Template 레포지토리의 src 폴더에 업로드되어 있습니다. market_db 파일도 해당 폴더에 함께 포함되어 있으니 참고하시기 바랍니다.**

**👀(수행 인증샷은 필수입니다.)** 

## SQL_ADVANCED_7th_TIL

### 8장 SQL과 파이썬 연결 
#### 01. 파이썬 개발 환경 준비
#### 02. 파이썬과 MySQL의 연동
#### 03. GUI 응용 프로그램 


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.24~99    | ✅         |
| 2주차 | p.102~155   | ✅         |
| 3주차 | p.158~213  | ✅         |
| 4주차 | p.216~271 | ✅         |
| 5주차 | p.274~327 | ✅         |
| 6주차 | p.330~369 | ✅         |
| 7주차 | p.372~407 | ✅         |


<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 학습 내용 정리

## 1. 파이썬 개발 환경 준비

<!-- 이번 챕터에서 제시된 실습을 흐름에 맞게 진행한 후, 실습 과정이 보일 수 있도록 인증 사진을 2장 이상 제출해 주세요. -->

![alt text](<images/SQL 7주차 1.png>)
![alt text](<images/SQL 7주차 2.png>)
<!-- 이 부분을 지우고 인증사진을 제출해주세요.-->


## 2. 파이썬과 MySQL의 연동

<!-- 이번 챕터에서 제시된 실습을 흐름에 맞게 진행한 후, 실습 과정이 보일 수 있도록 인증 사진을 2장 이상 제출해 주세요. -->

<!-- 이 부분을 지우고 인증사진을 제출해주세요.-->
![alt text](<images/SQL 7주차 3.png>)
![alt text](<images/SQL 7주차 4.png>)


## 3. GUI 응용 프로그램 

<!-- GUI 응용 프로그램에 관해 배우게 된 점을 적어주세요. -->


**1) GUI와 tkinter**
- GUI(Graphical User Interface)는 텍스트 대신 창·버튼 같은 그래픽 환경으로 프로그램을 사용하게 해주는 방식이다.
- 파이썬 표준 라이브러리인 `tkinter`를 쓰면 별도 설치 없이 윈도 프로그램을 만들 수 있고, SQL을 모르는 사용자도 클릭만으로 DB에 데이터를 입력·조회할 수 있다.

**2) 기본 구조**
- `root = Tk()`로 루트 윈도를 만들고, `root.mainloop()`로 클릭·키 입력 같은 이벤트를 계속 처리한다.
- `title()`은 창 제목, `geometry("400x200")`은 창 크기를 지정한다. 크기를 바꾸는 함수는 title()이 아니라 geometry()다.

**3) 주요 위젯**
| 위젯 | 역할 | 비고 |
|---|---|---|
| Label | 문자 표시 | text, font, fg(글자색), bg(배경색) |
| Button | 클릭 시 동작 실행 | `command=함수명`으로 실행할 함수 지정 |
| Frame | 화면 구역 나누기 | 화면에는 보이지 않음 |
| Entry | 입력 상자 | `get()`으로 입력값 가져오기 |
| Listbox | 목록 표시 | `insert(END, 값)`으로 뒤에 추가 |

- 모든 위젯은 `pack()`을 호출해야 화면에 나타난다.
- pack 옵션: `side`(LEFT/RIGHT/TOP/BOTTOM, UP은 없음), `fill`(X/Y/BOTH), `expand`, `padx/pady`(여백)

**4) SQL 연동 GUI 프로그램**
- [입력] 버튼: Entry 4개의 값을 `get()`으로 받아 INSERT 문을 만들고 `execute()` → `commit()` → `close()` 후 messagebox로 성공을 알린다.
- [조회] 버튼: SELECT 결과를 `fetchone()`으로 한 행씩 읽어 리스트에 담고, 리스트 박스를 비운 뒤 `zip()`으로 4개 열을 동시에 돌며 다시 채운다.
- 결국 앞에서 배운 "연결 → 커서 → 실행 → 커밋 → 종료" 흐름을 버튼 함수 안에 넣은 구조다.

**5) 느낀 점**
- 8-2의 콘솔 프로그램과 SQL 로직은 같고, 입력 방식만 `input()`에서 Entry 위젯으로 바뀐 것이라 구조가 쉽게 이해됐다.
- 교재는 입력값을 문자열로 이어 붙여 SQL을 만드는데, 이 방식은 SQL 인젝션에 취약하다. 실무에서는 `cur.execute("INSERT INTO userTable VALUES(%s,%s,%s,%s)", (data1, data2, data3, data4))`처럼 파라미터 바인딩을 쓰는 것이 안전하다는 점도 알게 됐다.
- 일반 사용자가 SQL 없이 DB를 다룰 수 있게 해주는 것이 응용 프로그램의 역할이라는 점을 체감했다.

---

이번 주는 마지막 주로 별도의 실습 과제는 진행하지 않습니다.

한 학기 동안 다소 부족한 커리큘럼이었음에도 불구하고 성실하게, 그리고 열심히 과제를 수행해주셔서 진심으로 감사드립니다.

이번 과정을 통해 배운 내용이 앞으로 여러분이 SQL을 다루는 데에 조금이나마 도움이 되기를 바랍니다.

여러분의 앞날을 진심으로 응원합니다. 😊


### 🎉 수고하셨습니다.






