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

### 3월에 태어난 여성 회원 목록 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131120

```SQL
SELECT MEMBER_ID, MEMBER_NAME, GENDER, DATE_FORMAT(DATE_OF_BIRTH, '%Y-%m-%d') AS DATE_OF_BIRTH
FROM MEMBER_PROFILE
WHERE GENDER = 'W' AND DATE_OF_BIRTH LIKE '%-03-%' AND TLNO IS NOT NULL
ORDER BY MEMBER_ID ASC;
```

### 인기있는 아이스크림

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/133024

```SQL
SELECT FLAVOR
FROM FIRST_HALF
ORDER BY TOTAL_ORDER DESC, SHIPMENT_ID ASC;
```

### 흉부외과 또는 일반외과 의사 목록 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/132203

```SQL
SELECT DR_NAME, DR_ID, MCDP_CD, DATE_FORMAT(HIRE_YMD, '%Y-%m-%d') AS HIRE_YMD
FROM DOCTOR
WHERE MCDP_CD IN ('CS', 'GS')
ORDER BY HIRE_YMD DESC, DR_NAME ASC;
```

### 조건에 부합하는 중고거래 댓글 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/164673

```SQL
SELECT B.TITLE, R.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, DATE_FORMAT(R.CREATED_DATE, '%Y-%m-%d') AS CREATED_DATE
FROM USED_GOODS_BOARD AS B INNER JOIN USED_GOODS_REPLY AS R
ON B.BOARD_ID = R.BOARD_ID
WHERE B.CREATED_DATE LIKE '2022-10%'
ORDER BY R.CREATED_DATE ASC, B.TITLE ASC;
```

### 과일로 만든 아이스크림 고르기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/133025

```SQL
SELECT F.FLAVOR
FROM FIRST_HALF AS F JOIN ICECREAM_INFO AS I 
ON F.FLAVOR = I.FLAVOR
WHERE F.TOTAL_ORDER > 3000 AND I.INGREDIENT_TYPE = 'fruit_based'
ORDER BY F.TOTAL_ORDER DESC;
```

### 서울에 위치한 식당 목록 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131118

```SQL
SELECT I.REST_ID, I.REST_NAME, I.FOOD_TYPE, I.FAVORITES, I.ADDRESS, ROUND(AVG(R.REVIEW_SCORE), 2) AS SCORE
FROM REST_INFO AS I INNER JOIN REST_REVIEW AS R
ON I.REST_ID = R.REST_ID
WHERE I.ADDRESS LIKE '서울%'
GROUP BY I.REST_ID
ORDER BY SCORE DESC, I.FAVORITES DESC;
```

### 강원도에 위치한 생산공장 목록 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131112

```SQL
SELECT FACTORY_ID, FACTORY_NAME, ADDRESS
FROM FOOD_FACTORY
WHERE ADDRESS LIKE '강원도%'
ORDER BY FACTORY_ID ASC;
```

### 재구매가 일어난 상품과 회원 리스트 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131536

```SQL
SELECT USER_ID, PRODUCT_ID
FROM ONLINE_SALE
GROUP BY USER_ID, PRODUCT_ID
HAVING COUNT(PRODUCT_ID) >= 2
ORDER BY USER_ID ASC, PRODUCT_ID DESC;
```

### 오프라인/온라인 판매 데이터 통합하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131537

```SQL
SELECT DATE_FORMAT(SALES_DATE, "%Y-%m-%d") AS SALES_DATE, PRODUCT_ID, USER_ID, SALES_AMOUNT
FROM ONLINE_SALE
WHERE SALES_DATE LIKE '2022-03%'
UNION ALL
SELECT DATE_FORMAT(SALES_DATE, "%Y-%m-%d") AS SALES_DATE, PRODUCT_ID, NULL USER_ID, SALES_AMOUNT
FROM OFFLINE_SALE
WHERE SALES_DATE LIKE '2022-03%'
ORDER BY SALES_DATE ASC, PRODUCT_ID ASC, USER_ID ASC;
```

### 모든 레코드 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59034

```SQL
SELECT * 
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

### 역순 정렬하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59035

```SQL
SELECT NAME, DATETIME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC;
```

### 아픈 동물 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59036

```SQL
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION = 'SICK'
ORDER BY ANIMAL_ID ASC;
```

### 어린 동물 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59037

```SQL
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION != 'Aged'
ORDER BY ANIMAL_ID ASC;
```

### 동물의 아이디와 이름

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59403

```SQL
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID ASC;
```

### 여러 기준으로 정렬하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59404

```SQL
SELECT ANIMAL_ID, NAME, DATETIME
FROM ANIMAL_INS
ORDER BY NAME ASC, DATETIME DESC;
```

### 상위 n개 레코드

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59405

```SQL
SELECT NAME
FROM ANIMAL_INS
ORDER BY DATETIME ASC
LIMIT 1;
```

### 조건에 맞는 회원수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131535

```SQL
SELECT COUNT(*) AS USERS
FROM USER_INFO
WHERE (JOINED LIKE '2021%') AND (AGE BETWEEN 20 AND 29);
```

## SUM, MAX, MIN

### 가격이 제일 비싼 식품의 정보 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131115

```SQL
SELECT *
FROM FOOD_PRODUCT
WHERE PRICE = (SELECT MAX(PRICE) FROM FOOD_PRODUCT);
```

### 가장 비싼 상품 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131697

```SQL
SELECT MAX(PRICE) AS MAX_PRICE
FROM PRODUCT;
```

### 최댓값 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59415

```SQL
SELECT MAX(DATETIME) AS 시간
FROM ANIMAL_INS;
```

### 최솟값 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59038

```SQL
SELECT MIN(DATETIME) AS 시간
FROM ANIMAL_INS;
```

### 동물 수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59406

```SQL
SELECT COUNT(*) AS count
FROM ANIMAL_INS;
```

### 중복 제거하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59408

```SQL
SELECT COUNT(DISTINCT(NAME)) AS count
FROM ANIMAL_INS;
```

## GROUP BY

### 즐겨찾기가 가장 많은 식당 정보 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131123

```SQL
SELECT FOOD_TYPE, REST_ID, REST_NAME, FAVORITES
FROM REST_INFO
WHERE 
    (FOOD_TYPE, FAVORITES)
    IN (
        SELECT FOOD_TYPE, MAX(FAVORITES)
        FROM REST_INFO
        GROUP BY FOOD_TYPE
    )
ORDER BY FOOD_TYPE DESC;
```