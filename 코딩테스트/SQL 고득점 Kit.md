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

### 업그레이드 된 아이템 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/273711

```SQL
SELECT I.ITEM_ID, ITEM_NAME, RARITY
FROM ITEM_INFO AS I JOIN ITEM_TREE AS T
ON I.ITEM_ID = T.ITEM_ID
WHERE T.PARENT_ITEM_ID IN (
    SELECT ITEM_ID FROM ITEM_INFO WHERE RARITY='RARE'
    )
ORDER BY ITEM_ID DESC;
```

### Python 개발자 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/276013

```SQL
SELECT ID, EMAIL, FIRST_NAME, LAST_NAME
FROM DEVELOPER_INFOS
WHERE 'Python' IN (SKILL_1, SKILL_2, SKILL_3)
ORDER BY ID ASC;
```

### 조건에 맞는 개발자 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/276034

```SQL
SELECT ID, EMAIL, FIRST_NAME, LAST_NAME
FROM DEVELOPERS
WHERE SKILL_CODE&(select sum(CODE) from SKILLCODES where NAME in('Python','C#'))
ORDER BY ID ASC;
```

### 잔챙이 잡은 수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/293258

```SQL
SELECT COUNT(*) AS FISH_COUNT
FROM FISH_INFO
WHERE LENGTH IS NULL;
```

### 가장 큰 물고기 10마리 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/298517

```SQL
SELECT ID, LENGTH
FROM FISH_INFO
ORDER BY LENGTH DESC, ID ASC
LIMIT 10;
```

### 특정 물고기를 잡은 총 수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/298518

```SQL
SELECT COUNT(*) AS FISH_COUNT
FROM FISH_INFO JOIN FISH_NAME_INFO USING(FISH_TYPE)
WHERE FISH_NAME IN ('BASS', 'SNAPPER');
```

### 대장균들의 자식의 수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/299305

```SQL
SELECT A.ID, COUNT(B.ID) AS CHILD_COUNT
FROM ECOLI_DATA A LEFT JOIN ECOLI_DATA B
ON A.ID = B.PARENT_ID
GROUP BY A.ID
ORDER BY A.ID;
```

### 대장균의 크기에 따라 분류하기 1

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/299307

```SQL
SELECT ID, 
    CASE 
        WHEN SIZE_OF_COLONY <= 100 THEN 'LOW'
        WHEN SIZE_OF_COLONY BETWEEN 101 AND 1000 THEN 'MEDIUM'
        ELSE 'HIGH'
    END AS 'SIZE'        
FROM ECOLI_DATA
ORDER BY ID ASC;
```

### 특정 형질을 가지는 대장균 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/301646

```SQL
SELECT COUNT(*) AS COUNT
FROM ECOLI_DATA
WHERE GENOTYPE & 5 AND NOT GENOTYPE & 2;
```

### 부모의 형질을 모두 가지는 대장균 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/301647

```SQL
SELECT P.ID, P.GENOTYPE, C.GENOTYPE AS PARENT_GENOTYPE
FROM ECOLI_DATA AS P JOIN ECOLI_DATA AS C
ON P.PARENT_ID = C.ID
WHERE P.GENOTYPE & C.GENOTYPE = C.GENOTYPE
ORDER BY P.ID;
```

### 대장균의 크기에 따라 분류하기 2

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/301649

```SQL
SELECT ID, 
    CASE 
        WHEN NTILE(4) OVER (ORDER BY SIZE_OF_COLONY) = 1 THEN 'LOW'
        WHEN NTILE(4) OVER (ORDER BY SIZE_OF_COLONY) = 2 THEN 'MEDIUM'
        WHEN NTILE(4) OVER (ORDER BY SIZE_OF_COLONY) = 3 THEN 'HIGH'
        ELSE 'CRITICAL'
    END AS 'COLONY_NAME'        
FROM ECOLI_DATA
ORDER BY ID ASC;
```

### 특정 세대의 대장균 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/301649

```SQL
WITH RECURSIVE ECOLI_TREE AS (
    -- Non-Recursive
    SELECT ID, PARENT_ID, 1 GENERATION
    FROM ECOLI_DATA
    WHERE PARENT_ID IS NULL
    UNION ALL

    -- Recursive
    SELECT D.ID, D.PARENT_ID, T.GENERATION + 1
    FROM ECOLI_DATA D INNER JOIN ECOLI_TREE T 
    ON D.PARENT_ID = T.ID
)

SELECT ID
FROM ECOLI_TREE
WHERE GENERATION = 3
ORDER BY ID ASC;
```

### 멸종위기의 대장균 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/301651

```SQL
WITH RECURSIVE ECOLI_TREE AS (
    -- Non-Recursive
    SELECT ID, PARENT_ID, 1 GENERATION
    FROM ECOLI_DATA
    WHERE PARENT_ID IS NULL
    UNION ALL

    -- Recursive
    SELECT D.ID, D.PARENT_ID, T.GENERATION + 1
    FROM ECOLI_DATA D INNER JOIN ECOLI_TREE T 
    ON D.PARENT_ID = T.ID
), 
ECOLI_CHILDREN AS (
    SELECT T.ID, T.GENERATION
    FROM ECOLI_TREE AS T LEFT JOIN ECOLI_DATA AS D 
    ON T.ID = D.PARENT_ID
    WHERE D.ID IS NULL
)

SELECT COUNT(*) AS COUNT, GENERATION
FROM ECOLI_CHILDREN
GROUP BY GENERATION
ORDER BY GENERATION ASC;
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

### 조건에 맞는 아이템들의 가격의 총합 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/273709

```SQL
SELECT SUM(PRICE) AS TOTAL_PRICE
FROM ITEM_INFO
WHERE RARITY = 'LEGEND';
```

### 물고기 종류 별 대어 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/293261

```SQL
SELECT ID, FISH_NAME, LENGTH
FROM FISH_INFO AS I JOIN FISH_NAME_INFO AS N 
ON I.FISH_TYPE = N.FISH_TYPE
WHERE (FISH_NAME, LENGTH) IN (
    SELECT FISH_NAME , MAX(LENGTH) AS LENGTH
    FROM FISH_INFO I JOIN FISH_NAME_INFO N
    ON I.FISH_TYPE = N.FISH_TYPE
    GROUP BY I.FISH_TYPE, FISH_NAME
);
```

### 잡은 물고기 중 가장 큰 물고기의 길이 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/298515

```SQL
SELECT CONCAT(MAX(LENGTH), 'cm') AS MAX_LENGTH
FROM FISH_INFO;
```

### 연도별 대장균 크기의 편차 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/299310

```SQL
WITH MAX_TABLE AS (
    SELECT YEAR(DIFFERENTIATION_DATE) AS YEAR, MAX(SIZE_OF_COLONY) AS MAX_SIZE
    FROM ECOLI_DATA
    GROUP BY YEAR
)
SELECT YEAR(DIFFERENTIATION_DATE) AS YEAR, (M.MAX_SIZE - E.SIZE_OF_COLONY) AS YEAR_DEV, E.ID
FROM ECOLI_DATA AS E INNER JOIN MAX_TABLE AS M 
ON YEAR(DIFFERENTIATION_DATE) = M.YEAR
ORDER BY YEAR, YEAR_DEV;
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

### 언어별 개발자 분류하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/276036

```SQL
WITH GROUP_DEVELOPERS AS (
    SELECT 
        ID, 
        EMAIL, 
        GROUP_CONCAT(DISTINCT NAME, CATEGORY) AS GROUPED
    FROM 
        SKILLCODES
    JOIN 
        DEVELOPERS
        ON DEVELOPERS.SKILL_CODE & SKILLCODES.CODE
    GROUP BY 1,2
)
SELECT 
    CASE
        WHEN GROUPED LIKE '%Front%' AND GROUPED LIKE '%Python%' THEN 'A'
        WHEN GROUPED LIKE '%C#%' THEN 'B' 
        WHEN GROUPED LIKE '%Front%' THEN 'C'
    END AS GRADE,
    ID, 
    EMAIL
FROM
    GROUP_DEVELOPERS
HAVING GRADE IS NOT NULL
ORDER BY GRADE, ID;
```

### 조건에 맞는 사원 정보 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/284527

```SQL
SELECT SUM(G.SCORE) AS SCORE, E.EMP_NO, E.EMP_NAME, E.POSITION, E.EMAIL
FROM HR_EMPLOYEES E JOIN HR_GRADE G
ON E.EMP_NO = G.EMP_NO
GROUP BY G.EMP_NO
ORDER BY SCORE DESC
LIMIT 1;
```

### 연간 평가점수에 해당하는 평가 등급 및 성과금 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/284528

```SQL
WITH CTE AS (
    SELECT EMP_NO, AVG(SCORE) AS SCORE
    FROM HR_GRADE
    GROUP BY EMP_NO
)
SELECT CTE.EMP_NO,EMP_NAME,(
    CASE
        WHEN SCORE>=96 THEN 'S'
        WHEN SCORE>=90 THEN 'A'
        WHEN SCORE>=80 THEN 'B'
        ELSE 'C'
    END
)AS GRADE,(
    CASE 
        WHEN SCORE>=96 THEN SAL*0.2
        WHEN SCORE>=90 THEN SAL*0.15
        WHEN SCORE>=80 THEN SAL*0.1
        ELSE SAL*0
    END
)AS BONUS
FROM CTE JOIN HR_EMPLOYEES E ON CTE.EMP_NO = E.EMP_NO
ORDER BY CTE.EMP_NO;
```

### 부서별 평균 연봉 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/284529

```SQL
SELECT D.DEPT_ID, D.DEPT_NAME_EN, ROUND(AVG(SAL),0) AVG_SAL
FROM HR_DEPARTMENT D JOIN HR_EMPLOYEES E
ON D.DEPT_ID = E.DEPT_ID
GROUP BY D.DEPT_ID
ORDER BY AVG_SAL DESC;
```

### 노선별 평균 역 사이 거리 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/284531

```SQL
SELECT ROUTE, 
    CONCAT(ROUND(SUM(D_BETWEEN_DIST), 1), 'km') AS TOTAL_DISTANCE,
    CONCAT(ROUND(AVG(D_BETWEEN_DIST), 2), 'km') AS AVERAGE_DISTANCE
FROM SUBWAY_DISTANCE
GROUP BY ROUTE
ORDER BY ROUND(SUM(D_BETWEEN_DIST), 1) DESC;
```

### 물고기 종류 별 잡은 수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/293257

```SQL
SELECT COUNT(*) AS FISH_COUNT, FISH_NAME
FROM FISH_INFO JOIN FISH_NAME_INFO USING(FISH_TYPE)
GROUP BY FISH_NAME
ORDER BY FISH_COUNT DESC;
```

### 월별 잡은 물고기 수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/293260

```SQL
SELECT COUNT(*) AS FISH_COUNT, MONTH(TIME) AS MONTH
FROM FISH_INFO
GROUP BY MONTH
ORDER BY MONTH ASC;
```

### 특정 조건을 만족하는 물고기별 수와 최대 길이 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/298519

```SQL
SELECT COUNT(*) AS FISH_COUNT, MAX(LENGTH) AS MAX_LENGTH, FISH_TYPE
FROM FISH_INFO
GROUP BY FISH_TYPE
HAVING AVG(IFNULL(LENGTH, 10)) > 33
ORDER BY FISH_TYPE;
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

### ROOT 아이템 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/273710

```SQL
SELECT I.ITEM_ID, I.ITEM_NAME
FROM ITEM_INFO AS I JOIN ITEM_TREE AS T
ON I.ITEM_ID = T.ITEM_ID
WHERE PARENT_ITEM_ID IS NULL;
```

### 업그레이드 할 수 없는 아이템 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/273712

```SQL
SELECT I.ITEM_ID, ITEM_NAME, RARITY
FROM ITEM_INFO AS I LEFT JOIN ITEM_TREE AS T
ON I.ITEM_ID = T.PARENT_ITEM_ID
WHERE PARENT_ITEM_ID IS NULL
ORDER BY ITEM_ID DESC;
```

### 잡은 물고기의 평균 길이 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/293259

```SQL
SELECT ROUND(AVG(IFNULL(LENGTH, 10)), 2) AVERAGE_LENGTH
FROM FISH_INFO;
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

### 보호소에서 중성화한 동물

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59045

```SQL
SELECT I.ANIMAL_ID, I.ANIMAL_TYPE, I.NAME
FROM ANIMAL_INS AS I JOIN ANIMAL_OUTS AS O 
ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE I.SEX_UPON_INTAKE != O.SEX_UPON_OUTCOME
ORDER BY I.ANIMAL_ID;
```

### 상품 별 오프라인 매출 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131533

```SQL
SELECT P.PRODUCT_CODE, SUM(SALES_AMOUNT*PRICE) AS SALES
FROM PRODUCT AS P JOIN OFFLINE_SALE AS O
ON P.PRODUCT_ID = O.PRODUCT_ID
GROUP BY PRODUCT_CODE
ORDER BY SALES DESC, PRODUCT_CODE ASC;
```

### 상품을 구매한 회원 비율 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131534

```SQL
SELECT YEAR(SALES_DATE) AS YEAR, MONTH(SALES_DATE) AS MONTH, 
       COUNT(DISTINCT USER_ID) AS PUCHASED_USERS, 
       ROUND(
           COUNT(DISTINCT USER_ID) / 
           (SELECT COUNT(USER_ID)
            FROM USER_INFO 
            WHERE YEAR(JOINED) = 2021), 1
       ) AS PUCHASED_RATIO
FROM USER_INFO JOIN ONLINE_SALE USING(USER_ID)
WHERE YEAR(JOINED)=2021
GROUP BY YEAR, MONTH
ORDER BY YEAR, MONTH ASC;
```

### FrontEnd 개발자 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/276035

```SQL
SELECT DISTINCT ID, EMAIL, FIRST_NAME, LAST_NAME
FROM SKILLCODES JOIN DEVELOPERS
ON CODE & SKILL_CODE
WHERE CATEGORY = 'Front End'
ORDER BY ID ASC;
```

## String, Date

### 자동차 대여 기록에서 장기/단기 대여 구분하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/151138

```SQL
SELECT HISTORY_ID, CAR_ID, 
       DATE_FORMAT(START_DATE, '%Y-%m-%d') AS START_DATE,   
       DATE_FORMAT(END_DATE,'%Y-%m-%d') AS END_DATE,
       IF( (TIMESTAMPDIFF(DAY, START_DATE, END_DATE) + 1)>=30, 
           '장기 대여','단기 대여') AS RENT_TYPE
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE START_DATE LIKE '2022-09%'
ORDER BY HISTORY_ID DESC;
```

### 조회수가 가장 많은 중고거래 게시판의 첨부파일 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/164671

```SQL
SELECT CONCAT('/home/grep/src/', BOARD_ID, '/',FILE_ID, FILE_NAME, FILE_EXT) AS FILE_PATH
FROM USED_GOODS_BOARD JOIN USED_GOODS_FILE USING(BOARD_ID) 
WHERE VIEWS = (SELECT MAX(VIEWS) FROM USED_GOODS_BOARD)
ORDER BY FILE_ID DESC;
```

### 자동차 대여 기록 별 대여 금액 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/151141

```SQL
WITH RENTAL_DATE_AND_DURATION_TYPE AS (
    SELECT *, CASE 
                 WHEN DATEDIFF(END_DATE, START_DATE) + 1 < 7 THEN NULL
                 WHEN DATEDIFF(END_DATE, START_DATE) + 1 < 30 THEN '7일 이상'
                 WHEN DATEDIFF(END_DATE, START_DATE) + 1 < 90 THEN '30일 이상'
                 ELSE '90일 이상' 
               END AS R_DURATION_TYPE
            , DATEDIFF(END_DATE, START_DATE) + 1 AS R_DATE
    FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY 
         JOIN CAR_RENTAL_COMPANY_CAR USING(CAR_ID)
)
SELECT HISTORY_ID, 
       TRUNCATE(R_DATE * DAILY_FEE * (1 - COALESCE(DISCOUNT_RATE, 0)/100), 0) "FEE"
FROM RENTAL_DATE_AND_DURATION_TYPE AS R 
     LEFT JOIN CAR_RENTAL_COMPANY_DISCOUNT_PLAN AS P 
     ON R.CAR_TYPE = P.CAR_TYPE AND R.R_DURATION_TYPE = DURATION_TYPE
WHERE R.CAR_TYPE = '트럭'
ORDER BY FEE DESC, HISTORY_ID DESC;
```

### 조건에 부합하는 중고거래 상태 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/164672

```SQL
SELECT BOARD_ID, WRITER_ID, TITLE, PRICE, 
    CASE WHEN STATUS = "SALE" then "판매중"
    WHEN STATUS = "RESERVED" then "예약중"
    WHEN STATUS = "DONE" then "거래완료"
    END AS STATUS
FROM USED_GOODS_BOARD
WHERE CREATED_DATE = "2022-10-05"
ORDER BY BOARD_ID desc;
```

### 조건별로 분류하여 주문상태 출력하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131113

```SQL
SELECT ORDER_ID, PRODUCT_ID, DATE_FORMAT(OUT_DATE, '%Y-%m-%d'),
    CASE WHEN DATE_FORMAT(OUT_DATE,'%m-%d') <= '05-01' THEN '출고완료'
    WHEN DATE_FORMAT(OUT_DATE,'%m-%d') > '05-01' THEN '출고대기'
    ELSE '출고미정'
    END AS '출고여부'
FROM FOOD_ORDER
ORDER BY ORDER_ID ASC;
```

### 대여 기록이 존재하는 자동차 리스트 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/157341

```SQL
SELECT DISTINCT(C.CAR_ID) AS CAR_ID
FROM CAR_RENTAL_COMPANY_CAR AS C INNER JOIN CAR_RENTAL_COMPANY_RENTAL_HISTORY AS H
ON C.CAR_ID = H.CAR_ID
AND MONTH(START_DATE) = 10 AND CAR_TYPE = '세단'
ORDER BY CAR_ID DESC;
```

### 조건에 맞는 사용자 정보 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/164670

```SQL
SELECT USER_ID, NICKNAME, 
       CONCAT_WS(' ', CITY, STREET_ADDRESS1, STREET_ADDRESS2) AS 전체주소, 
       CONCAT_WS('-', SUBSTRING(TLNO, 1,3), SUBSTRING(TLNO, 4,4), SUBSTRING(TLNO, 8,4)) AS 전화번호
FROM USED_GOODS_USER 
WHERE USER_ID IN ( 
    SELECT WRITER_ID FROM USED_GOODS_BOARD 
    GROUP BY WRITER_ID HAVING COUNT(*) >= 3)
ORDER BY USER_ID DESC;
```

### 특정 옵션이 포함된 자동차 리스트 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/157343

```SQL
SELECT *
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS LIKE '%네비게이션%'
ORDER BY CAR_ID DESC;
```

### 자동차 평균 대여 기간 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/157342

```SQL
SELECT CAR_ID, ROUND(AVG(DATEDIFF(END_DATE,START_DATE)+1),1) AVERAGE_DURATION
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY CAR_ID
HAVING AVERAGE_DURATION >= 7
ORDER BY AVERAGE_DURATION DESC, CAR_ID DESC;
```

### 취소되지 않은 진료 예약 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/132204

```SQL
SELECT APNT_NO, PT_NAME, PT_NO, A.MCDP_CD, DR_NAME, APNT_YMD
FROM PATIENT JOIN APPOINTMENT A USING(PT_NO)
     JOIN DOCTOR ON MDDR_ID = DR_ID
WHERE APNT_YMD LIKE '2022-04-13%' 
      AND APNT_CNCL_YN = 'N'
      AND A.MCDP_CD = 'CS'
ORDER BY APNT_YMD ASC;
```

### 이름에 el이 들어가는 동물 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59047

```SQL
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE ANIMAL_TYPE = 'Dog' AND UPPER(NAME) LIKE '%EL%'
ORDER BY NAME;
```

### 중성화 여부 파악하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59409

```SQL
SELECT ANIMAL_ID, NAME,
    CASE WHEN SEX_UPON_INTAKE LIKE '%Neutered%' OR SEX_UPON_INTAKE LIKE '%Spayed%'
    THEN 'O'
    ELSE 'X'
    END AS 중성화
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

### 오랜 기간 보호한 동물(2)

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59411

```SQL
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS I JOIN ANIMAL_OUTS O USING(ANIMAL_ID, ANIMAL_TYPE, NAME)
ORDER BY TIMESTAMPDIFF(DAY, I.DATETIME, O.DATETIME ) DESC
LIMIT 2;
```

### DATETIME에서 DATE로 형 변환

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/59414

```SQL
SELECT ANIMAL_ID, NAME, DATE_FORMAT(DATETIME, '%Y-%m-%d')
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

### 카테고리 별 상품 개수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/131529

```SQL
SELECT LEFT(PRODUCT_CODE, 2) AS CATEGORY_CODE, COUNT(*) AS PRODUCT_COUNT
FROM PRODUCT
GROUP BY CATEGORY_CODE
ORDER BY CATEGORY_CODE;
```

### 연도 별 평균 미세먼지 농도 조회하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/284530

```SQL
SELECT YEAR(YM) AS YEAR, ROUND(AVG(PM_VAL1), 2) AS PM10, ROUND(AVG(PM_VAL2), 2) AS 'PM2.5'
FROM AIR_POLLUTION
WHERE LOCATION2 LIKE '수원'
GROUP BY YEAR
ORDER BY YEAR ASC;
```

### 한 해에 잡은 물고기 수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/298516

```SQL
SELECT COUNT(*) AS FISH_COUNT
FROM FISH_INFO
WHERE YEAR(TIME) = 2021;
```

### 분기별 분화된 대장균의 개체 수 구하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/299308

```SQL
SELECT CASE WHEN MONTH(DIFFERENTIATION_DATE) BETWEEN 1 AND 3 THEN '1Q'
            WHEN MONTH(DIFFERENTIATION_DATE) BETWEEN 4 AND 6 THEN '2Q'
            WHEN MONTH(DIFFERENTIATION_DATE) BETWEEN 7 AND 9 THEN '3Q'
            WHEN MONTH(DIFFERENTIATION_DATE) BETWEEN 10 AND 12 THEN '4Q'
        END AS QUARTER,
        COUNT(*) AS ECOLI_COUNT
FROM ECOLI_DATA
GROUP BY QUARTER
ORDER BY QUARTER ASC;
```