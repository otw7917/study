```sql
-- 부모의 형질을 모두 가지는 대장균 찾기
-- https://school.programmers.co.kr/learn/courses/30/lessons/301647
WITH GENO_DATA AS (
    SELECT ID, GENOTYPE
    FROM ECOLI_DATA
)
SELECT E.ID, E.GENOTYPE, G.GENOTYPE AS PARENT_GENOTYPE
FROM ECOLI_DATA E
JOIN GENO_DATA G
ON E.PARENT_ID = G.ID
WHERE G.GENOTYPE & E.GENOTYPE = G.GENOTYPE
ORDER BY ID
```

```sql
-- 가격이 제일 비싼 식품의 정보 출력하기
-- https://school.programmers.co.kr/learn/courses/30/lessons/131115

-- 솔루션 1 -> 가장 간단함 ✅
SELECT *
FROM FOOD_PRODUCT
ORDER BY PRICE DESC
LIMIT 1

-- 솔루션 2 -> 서브쿼리 복잡해질수록 가독성이 떨어진다고 생각  ✅
SELECT *
FROM FOOD_PRODUCT
WHERE PRICE = (SELECT MAX(PRICE) FROM FOOD_PRODUCT)


-- 솔루션 3 -> 확장성? 뛰어남 근데 가장 비싼거 찾는데 굳이? ✅
WITH MAXPRICE AS (
    SELECT MAX(PRICE) AS PRICE
    FROM FOOD_PRODUCT
)
SELECT PRODUCT_ID, PRODUCT_NAME, PRODUCT_CD, CATEGORY, PRICE
FROM FOOD_PRODUCT F
JOIN MAXPRICE M
--- ON F.PRICE = M.PRICE -> PRICE 가 두 테이블에 모두 존재해서 에러메세지로 ambiguous 🔨
USING(PRICE)
```

```sql
-- 월별 잡은 물고기 수 구하기 (year X)
-- https://school.programmers.co.kr/learn/courses/30/lessons/293260
SELECT COUNT(ID) AS FISH_COUNT, MONTH(TIME) AS MONTH
FROM FISH_INFO
GROUP BY MONTH(TIME)
ORDER BY MONTH
```

**ROUND(number, place:0 -> 소수점 첫째 자리에서 반올림)**, **AVG()** 아오! 🔥
**쿼리 실행 순서에 대해서**

- from -> group -> having -> select 실행 순 => select절 별칭을 having에서 사용할 경우 에러일줄 ❓ 알았으나 사용 가능
- https://stackoverflow.com/questions/49888360/using-alias-in-the-where-and-having-statements
- 다른 rdbms의 경우 having에서 별칭 사용이 안됌.
- 결론 sql옵티마이저가 변환해주는 과정이 있음 -> 다른 rdbms의 경우 안될수 있으니 확인.

```sql
-- 자동차 평균 대여 기간 구하기
-- https://school.programmers.co.kr/learn/courses/30/lessons/157342

-- 솔루션 1 ✅
SELECT CAR_ID, ROUND(SUM(DATEDIFF(END_DATE, START_DATE)+1) / COUNT(CAR_ID),1) AS AVERAGE_DURATION
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY CAR_ID
HAVING AVERAGE_DURATION >= 7
ORDER BY AVERAGE_DURATION DESC, CAR_ID DESC

-- 솔루션 2 ✅ AVG
SELECT CAR_ID, ROUND(AVG(DATEDIFF(END_DATE, START_DATE)+1),1) AS AVERAGE_DURATION
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY CAR_ID
HAVING AVERAGE_DURATION >= 7
ORDER BY AVERAGE_DURATION DESC, CAR_ID DESC
```
