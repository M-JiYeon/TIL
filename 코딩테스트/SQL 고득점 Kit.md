# SQL 고득점 Kit

## SELECT

### 평균 일일 대여 요금 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/151136

```SQL
SELECT ROUND(AVG(DAILY_FEE), 0) AS AVERAGE_FEE
FROM CAR_RENTAL_COMPANY_CAR
WHERE CAR_TYPE = 'SUV';
```