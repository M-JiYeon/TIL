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

### 조건에 맞는 사용자와 총 거래금액 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/164668

```SQL
SELECT U.USER_ID AS USER_ID, U.NICKNAME AS NICKNAME, SUM(PRICE) AS TOTAL_SALES
FROM USED_GOODS_BOARD AS B INNER JOIN USED_GOODS_USER AS U 
ON B.WRITER_ID = U.USER_ID
WHERE B.STATUS = 'DONE'
GROUP BY USER_ID
HAVING SUM(PRICE) >= 700000
ORDER BY TOTAL_SALES;
```

### 저자 별 카테고리 별 매출액 집계하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/144856

```SQL
SELECT B.AUTHOR_ID, AUTHOR_NAME, CATEGORY, SUM(SALES*PRICE) AS TOTAL_SALES
FROM BOOK_SALES AS S JOIN BOOK AS B ON S.BOOK_ID = B.BOOK_ID 
                     JOIN AUTHOR AS A ON B.AUTHOR_ID = A.AUTHOR_ID
WHERE SALES_DATE LIKE ('2022-01%')
GROUP BY B.AUTHOR_ID, AUTHOR_NAME, CATEGORY
ORDER BY AUTHOR_ID ASC, CATEGORY DESC;
```

### 카테고리 별 도서 판매량 집계하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/144855

```SQL
SELECT CATEGORY, SUM(SALES) AS TOTAL_SALES
FROM BOOK AS B JOIN BOOK_SALES AS S 
ON B.BOOK_ID = S.BOOK_ID
WHERE SALES_DATE LIKE ('2022-01%')
GROUP BY CATEGORY
ORDER BY CATEGORY ASC;
```

### 자동차 대여 기록에서 대여중 / 대여 가능 여부 구분하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/157340

```SQL
SELECT CAR_ID, MAX(
            CASE WHEN '2022-10-16' BETWEEN START_DATE AND END_DATE THEN '대여중' 
            ELSE '대여 가능' END) AS AVAILABILITY
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY CAR_ID
ORDER BY CAR_ID DESC;
```

### 진료과별 총 예약 횟수 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/132202

```SQL
SELECT MCDP_CD AS "진료과 코드", COUNT(*) AS "5월예약건수"
FROM APPOINTMENT
WHERE APNT_YMD LIKE '2022-05%'
GROUP BY MCDP_CD
ORDER BY COUNT(*) ASC, MCDP_CD ASC;
```

### 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/151137

```SQL
SELECT CAR_TYPE, COUNT(*) AS CARS
FROM CAR_RENTAL_COMPANY_CAR 
WHERE OPTIONS LIKE '%시트%'
GROUP BY CAR_TYPE
ORDER BY CAR_TYPE ASC;
```

### 대여 횟수가 많은 자동차들의 월별 대여 횟수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/151139

```SQL
SELECT MONTH(START_DATE) AS MONTH, CAR_ID, COUNT(*) AS RECORDS
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE START_DATE BETWEEN '2022-08-01' AND '2022-10-31'
      AND CAR_ID IN (SELECT CAR_ID
                     FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
                     WHERE START_DATE BETWEEN '2022-08-01' AND '2022-10-31'
                     GROUP BY CAR_ID
                     HAVING COUNT(*)>= 5)
GROUP BY MONTH(START_DATE), CAR_ID 
ORDER BY MONTH, CAR_ID DESC;
```

### 성분으로 구분한 아이스크림 총 주문량

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/133026

```SQL
SELECT INGREDIENT_TYPE, SUM(TOTAL_ORDER) AS TOTAL_ORDER
FROM FIRST_HALF JOIN ICECREAM_INFO USING(FLAVOR)
GROUP BY INGREDIENT_TYPE
ORDER BY TOTAL_ORDER ASC;
```

### 식품분류별 가장 비싼 식품의 정보 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131116

```SQL
SELECT CATEGORY, PRICE, PRODUCT_NAME
FROM FOOD_PRODUCT
WHERE CATEGORY IN('과자', '국', '김치', '식용유')
      AND
      PRICE IN (SELECT MAX(PRICE) OVER (PARTITION BY CATEGORY)
                FROM FOOD_PRODUCT) 
ORDER BY PRICE DESC;
```

### 고양이와 개는 몇 마리 있을까

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59040

```SQL
SELECT ANIMAL_TYPE, COUNT(*) AS COUNT
FROM ANIMAL_INS
WHERE ANIMAL_TYPE IN ('CAT', 'DOG')
GROUP BY ANIMAL_TYPE
ORDER BY ANIMAL_TYPE ASC;
```

### 동명 동물 수 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59041

```SQL
SELECT NAME, COUNT(*) AS COUNT
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
GROUP BY NAME
HAVING COUNT(*) >= 2
ORDER BY NAME;
```

### 년, 월, 성별 별 상품 구매 회원 수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131532

```SQL
SELECT YEAR(SALES_DATE) AS YEAR,
       MONTH(SALES_DATE) AS MONTH,
       GENDER,
       COUNT(DISTINCT USER_ID) AS USERS
FROM ONLINE_SALE JOIN USER_INFO USING (USER_ID)
WHERE GENDER IS NOT NULL 
GROUP BY  YEAR, MONTH, GENDER
ORDER BY  YEAR, MONTH, GENDER;
```

### 입양 시각 구하기(1)

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59412

```SQL
SELECT HOUR(DATETIME) AS HOUR, COUNT(*) AS COUNT
FROM ANIMAL_OUTS
WHERE HOUR(DATETIME) BETWEEN '9' AND '19'
GROUP BY HOUR
ORDER BY HOUR;
```

### 입양 시각 구하기(2)

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59413

```SQL
SELECT HOUR, COUNT(ANIMAL_ID) AS COUNT
FROM ( SELECT (ROW_NUMBER() OVER () - 1) AS HOUR
       FROM ANIMAL_OUTS
       LIMIT 24) AS 24HOURS_NUM_TABLE 
     LEFT JOIN ANIMAL_OUTS ON HOUR = HOUR(DATETIME)
GROUP BY HOUR
ORDER BY HOUR ASC;
```

### 가격대 별 상품 개수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131530

```SQL
SELECT TRUNCATE(PRICE, -4) AS PRICE_GROUP, 
       COUNT(*) AS PRODUCTS
FROM PRODUCT 
GROUP BY PRICE_GROUP
ORDER BY PRICE_GROUP ASC;
```

## IS NULL

### 경기도에 위치한 식품창고 목록 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131114

```SQL
SELECT WAREHOUSE_ID, WAREHOUSE_NAME, ADDRESS, IFNULL(FREEZER_YN, 'N') AS FREEZER_YN
FROM FOOD_WAREHOUSE
WHERE ADDRESS LIKE '경기도%'
ORDER BY WAREHOUSE_ID ASC;
```

### 이름이 없는 동물의 아이디

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59039

```SQL
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NULL
ORDER BY ANIMAL_ID ASC;
```

### 이름이 있는 동물의 아이디

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59407

```SQL
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
ORDER BY ANIMAL_ID ASC;
```

### NULL 처리하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59410

```SQL
SELECT ANIMAL_TYPE, IFNULL(NAME, 'No name') AS NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID ASC;
```

### 나이 정보가 없는 회원 수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131528

```SQL
SELECT COUNT(*) AS USERS
FROM USER_INFO
WHERE AGE IS NULL;
```

## JOIN

### 주문량이 많은 아이스크림들 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/133027

```SQL
SELECT F.FLAVOR
FROM FIRST_HALF AS F LEFT JOIN 
    (
    SELECT FLAVOR, SUM(TOTAL_ORDER) AS TOTAL_ORDER
    FROM JULY
    GROUP BY FLAVOR
    ) AS J
ON F.FLAVOR = J.FLAVOR
ORDER BY (F.TOTAL_ORDER + J.TOTAL_ORDER) DESC
LIMIT 3;
```

### 특정 기간동안 대여 가능한 자동차들의 대여비용 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/157339

```SQL
SELECT CAR_ID, C.CAR_TYPE, 
       FLOOR(30*DAILY_FEE*(1-DISCOUNT_RATE/100)) AS FEE 
FROM CAR_RENTAL_COMPANY_CAR AS C 
     JOIN CAR_RENTAL_COMPANY_DISCOUNT_PLAN USING(CAR_TYPE) 
WHERE C.CAR_TYPE IN ('세단', 'SUV') 
      AND CAR_ID NOT IN (SELECT CAR_ID
                         FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY 
                         WHERE END_DATE >= '2022-11-1' 
                               AND START_DATE <= '2022-11-30')
      AND DURATION_TYPE = '30일 이상'
HAVING FEE >= 500000 AND FEE < 2000000 
ORDER BY FEE DESC, CAR_TYPE ASC, CAR_ID DESC;
```

### 5월 식품들의 총매출 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131117

```SQL
SELECT PRODUCT_ID, PRODUCT_NAME, SUM(PRICE*AMOUNT) AS TOTAL_SALES
FROM FOOD_ORDER JOIN FOOD_PRODUCT USING(PRODUCT_ID)
WHERE PRODUCE_DATE LIKE '2022-05%'
GROUP BY PRODUCT_ID
ORDER BY TOTAL_SALES DESC, PRODUCT_ID;
```

### 조건에 맞는 도서와 저자 리스트 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/144854

```SQL
SELECT BOOK_ID, AUTHOR_NAME, DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE
FROM BOOK AS B JOIN AUTHOR AS A 
ON B.AUTHOR_ID = A.AUTHOR_ID
WHERE CATEGORY = '경제'
ORDER BY PUBLISHED_DATE ASC;
```

### 그룹별 조건에 맞는 식당 목록 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131124

```SQL
SELECT MEMBER_NAME, REVIEW_TEXT, 
       DATE_FORMAT(REVIEW_DATE,'%Y-%m-%d') AS REVIEW_DATE
FROM MEMBER_PROFILE JOIN REST_REVIEW USING (MEMBER_ID)
WHERE MEMBER_ID IN (SELECT MEMBER_ID
                    FROM (SELECT *, DENSE_RANK() OVER (ORDER BY COUNT(*) DESC) AS REVIEW_RANK
                          FROM REST_REVIEW 
                          GROUP BY MEMBER_ID) INLINE
                    WHERE REVIEW_RANK = 1
                   )
ORDER BY REVIEW_DATE, REVIEW_TEXT ASC;
```

### 없어진 기록 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59042

```SQL
SELECT ANIMAL_ID, O.NAME
FROM ANIMAL_OUTS O LEFT JOIN ANIMAL_INS USING(ANIMAL_ID) 
WHERE INTAKE_CONDITION IS NULL
ORDER BY ANIMAL_ID, NAME ASC;
```

### 있었는데요 없었습니다

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59043

```SQL
SELECT ANIMAL_ID, I.NAME
FROM ANIMAL_INS AS I JOIN ANIMAL_OUTS AS O USING(ANIMAL_ID)
WHERE I.DATETIME > O.DATETIME
ORDER BY I.DATETIME ASC;
```

### 오랜 기간 보호한 동물(1)

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59044

```SQL
SELECT I.NAME, I.DATETIME
FROM ANIMAL_INS AS I LEFT JOIN ANIMAL_OUTS AS O
ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE SEX_UPON_OUTCOME IS NULL
ORDER BY I.DATETIME ASC
LIMIT 3;
```