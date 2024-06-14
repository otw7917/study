### lv1

```sql
-- 특정 형질을 가지는 대장균 찾기
-- <!-- https://school.programmers.co.kr/learn/courses/30/lessons/301646 -->
SELECT COUNT(*) as COUNT
FROM ECOLI_DATA
WHERE (GENOTYPE & 2) != 2 AND ((GENOTYPE & 1) = 1 OR (GENOTYPE & 4) = 4)
```

```sql
-- 가장 큰 물고기 10마리 구하기
-- <!-- https://school.programmers.co.kr/learn/courses/30/lessons/298517 -->
SELECT ID, LENGTH
FROM FISH_INFO
WHERE LENGTH > 10
ORDER BY LENGTH DESC, ID
LIMIT 10
```

**ROUND(value, 자릿수)**, **IFNULL(column, replace)** ≈ **COALESCE()**

```sql
-- 잡은 물고기의 평균 길이 구하기
SELECT ROUND(AVG(IFNULL(LENGTH, 10)),2) AS AVERAGE_LENGTH
FROM FISH_INFO
```

```sql
-- 특정 형질을 가지는 대장균 찾기
-- <!-- https://school.programmers.co.kr/learn/courses/30/lessons/301646 -->
SELECT COUNT(*) as COUNT
FROM ECOLI_DATA
WHERE (GENOTYPE & 2) != 2 AND ((GENOTYPE & 1) = 1 OR (GENOTYPE & 4) = 4)
```

**DATEDIFF** 특정 기간이 필요할때 유용!
**CASE** **WHEN ~ THEN ~ ELSE ~ END**

**쿼리 실행순서** 🔥 **_FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY_** 🔥

```sql
-- 자동차 대여 기록에서 장기/단기 대여 구분하기
-- https://school.programmers.co.kr/learn/courses/30/lessons/151138
SELECT HISTORY_ID, CAR_ID,
  DATE_FORMAT(START_DATE, "%Y-%m-%d") AS START_DATE,
  DATE_FORMAT(END_DATE, "%Y-%m-%d") AS END_DATE,
    CASE
        WHEN DATEDIFF(END_DATE, START_DATE) >= 29 THEN "장기 대여"
        ELSE "단기 대여"
    END AS RENT_TYPE
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE YEAR(START_DATE) = 2022 AND MONTH(START_DATE) = 9
ORDER BY HISTORY_ID DESC
```

```sql
-- 한 해에 잡은 물고기 수 구하기
-- # https://school.programmers.co.kr/learn/courses/30/lessons/298516
SELECT COUNT(ID) AS FISH_COUNT
FROM FISH_INFO
WHERE YEAR(TIME) = 2021
```
