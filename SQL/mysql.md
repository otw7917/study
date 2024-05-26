- **SELECT** : 보여주고자 하는 데이터 **IFNULL(column, replaced_value)** as
- **FROM** : 어디 테이블
- **WHERE** : 조건 AND, OR
- **ORDER** BY : 순서[ ..[..조건 우선순위 하이], [조건 우선순위 로우] ] - **ASC**:default, **DESC**

```sql
-- 12세 이하인 여자 환자 목록 출력하기
SELECT PT_NAME,PT_NO,GEND_CD, AGE, IFNULL(TLNO, 'NONE') as TLNO
FROM PATIENT
WHERE AGE<=12 AND GEND_CD="W"
ORDER BY AGE DESC, PT_NAME
```

**DATE**

- DATE_FORMAT(VALUE, FORMAT)
- YEAR, MONTH, DAY, DAYNAME..

```sql
-- 3월에 태어난 여성 회원 목록 출력
SELECT MEMBER_ID, MEMBER_NAME, GENDER, DATE_FORMAT(DATE_OF_BIRTH, "%Y-%m-%d") as DATE_OF_BIRTH
FROM MEMBER_PROFILE
WHERE  MONTH(DATE_OF_BIRTH) = 3 AND TLNO IS NOT NULL AND GENDER="W"
ORDER BY MEMBER_ID
```

---

**GROUP BY** 데이터 그룹화 - column 기준
**HAVING** 데이터 그룹화 조건

```sql
-- 재구매가 일어난 상품과 회원 리스트 구하기
-- https://school.programmers.co.kr/learn/courses/30/lessons/131536
SELECT USER_ID, PRODUCT_ID, SALES_AMOUNT, SUM(SALES_AMOUNT)
FROM ONLINE_SALE
# WHERE USER_ID = 15
GROUP BY USER_ID, PRODUCT_ID
HAVING COUNT(USER_ID) > 1
ORDER BY USER_ID ASC, PRODUCT_ID DESC
-- HAVING 재구매의 경우 행이 2개이상이 될것
```

---

**WHERE IN** 여러값을 비교해야할 경우!
**DATE_FORMAT(COLUMN NAME, FORMAT)** //(PostgreSQL) TO_CHAR

```sql
-- https://school.programmers.co.kr/learn/courses/30/lessons/132203
SELECT DR_NAME, DR_ID,  MCDP_CD ,DATE_FORMAT(HIRE_YMD, '%Y-%m-%d') as HIRE_YMD
FROM DOCTOR
-- WHERE MCDP_CD = 'CS' OR MCDP_CD = 'GS'
WHERE MCDP_CD IN ('CS', 'GS')
ORDER BY HIRE_YMD DESC, DR_NAME ASC
```
