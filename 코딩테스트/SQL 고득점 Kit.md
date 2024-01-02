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

### 조건에 맞는 도서 리스트 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/144853

```SQL
SELECT BOOK_ID, DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE
FROM BOOK
WHERE PUBLISHED_DATE LIKE '2021%' AND CATEGORY = '인문'
ORDER BY PUBLISHED_DATE ASC;
```

### 12세 이하인 여자 환자 목록 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/132201

```SQL
SELECT PT_NAME, PT_NO, GEND_CD, AGE, IFNULL(TLNO, 'NONE') AS TLNO
FROM PATIENT
WHERE AGE <= 12 and GEND_CD = 'w'
ORDER BY AGE DESC, PT_NAME ASC;
```