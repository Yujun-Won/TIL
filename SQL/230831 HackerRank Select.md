# HackerRank Select
- [ORDER BY](#1-order-by)
- [SUBSTRING (1)](#2-substring-1)
- [SUBSTRING (2)](#3-substring-2)
- [CASE WHEN](#4-case-when)
- [CONCAT](#5-concat)

## 1. ORDER BY

### 1. 문제
```plain text
STATION에서 CITY 이름이 가장 짧거나 가장 긴 두 CITY의 이름과 이름의 길이를 추출하라.
만약 가장 짧거나 가장 긴 도시가 한 개 이상이라면, 알파벳 순서로 1개 출력하라.
```

### 2. 코드
```SQL
SELECT CITY, LENGTH(CITY) AS LEN
FROM STATION
ORDER BY LEN ASC, CITY ASC
LIMIT 1;

SELECT CITY, LENGTH(CITY) AS LEN
FROM STATION
ORDER BY LEN DESC, CITY ASC
LIMIT 1;
```
### 3. 출력
```plain text
Amo 3
Marine On Saint Croix 21
```
### 4. 배운 점
1. 위와 같이 가장 짧거나 가장 긴 것을 고르는 서로 상반된 조건은 쿼리문 하나 당 하나만 가능하다.
2. 쿼리를 여러 번 날려서 하나씩 추출하고, 문제는 그것을 원할 수 있다.

## 2. SUBSTRING (1)
### 1. 문제
```plain text
STATION에서 CITY 이름의 맨 앞과 맨뒤에 모음(A, E, I, O, U)을 가지고 있는 데이터를 추출하라.
중복은 허용되지 않는다.
```
### 2. 코드
```SQL
SELECT DISTINCT CITY
FROM STATION
WHERE SUBSTRING(CITY, 1, 1) IN ('A', 'E', 'I', 'O', 'U')
AND SUBSTRING(CITY, -1, 1) IN ('A', 'E', 'I', 'O', 'U');
```
### 3. 출력
```plain text
Acme
Aguanga
Alba
Aliso Viejo
Alpine
Amazonia
Amo
Andersonville {-truncated-}
```
### 4. 배운 점
1. `SUBSTRING(CITY, 1, 1) IN ('A', 'E', 'I', 'O', 'U')`: `CITY`의 첫번째 글자가 모음인지 확인
2. `SUBSTRING(CITY, -1, 1) IN ('A', 'E', 'I', 'O', 'U')`: `CITY`의 마지막 글자가 모음인지 확인
3. `SUBSTRING(COLUMN, NUM1, NUM2)`: 대상컬럼 `COLUMN`에서 `NUM1`은 시작 위치를 나타내고 `NUM2`는 추출할 문자의 길이를 의미

    예를 들어, SUBSTRING('HELLO', 1, 2)의 경우:

    NUM1 = 1: 문자열 'HELLO'에서 1번째 위치에서 시작 / NUM2 = 2: 시작 위치로부터 2개의 문자를 추출

    따라서 이 함수는 'HE'를 반환한다.

## 3. SUBSTRING (2)
### 1. 문제
```plain text
STUDENTS에서 MARKS가 75보다 큰 임의의 학생의 NAME을 추출하라.
NAME의 마지막 3글자를 기준으로 정렬하고, 만약 중복이 있다면 ID를 기준으로 오름차순 정렬하라.
```
### 2. 코드
```SQL
SELECT NAME
FROM STUDENTS
WHERE MARKS > 75
ORDER BY SUBSTRING(NAME, -3, 3) ASC, ID ASC;
```
### 3. 출력
```plain text
Stuart
Kristeen
Christene
Amina
Aamina {-truncated-}
```
### 4. 배운 점
1. `SUBSTRING(NAME, -3, 3) ASC`: NAME의 마지막 3개의 글자를 기준으로 오름차순 정렬한다.
2. `ID ASC`: ID 기준의 오름차순은 두번째 우선순위이다.

## 4. CASE WHEN
### 1. 문제
```plain text
TRIANGLES에는 3면의 길이가 기록되어 있다.
출력은 다음과 같다.
- Equilateral: 3면이 같은 길이인 삼각형
- Isosceles: 2면이 같은 길이인 삼각형
- Scalene: 3면이 모두 다른 길이인 삼각형
- Not A Triangle: A, B, C가 삼각형을 구성하지 않음
```
### 2. 코드
```SQL
SELECT
    CASE
        WHEN A + B <= C OR A + C <= B OR B + C <= A THEN 'Not A Triangle'
        WHEN A = B AND B = C THEN 'Equilateral'
        WHEN A = B OR B = C OR A = C THEN 'Isosceles'
        ELSE 'Scalene'
    END AS TriangleType
FROM TRIANGLES;
```
### 3. 출력
```plain text
Amo 3
Marine On Saint Croix 21
```
### 4. 배운 점
1. 삼각형의 어떤 두 변의 길이의 합은 항상 다른 한 변의 길이보다 커야 한다.
2. `CASE WHEN 조건 ELSE 마무리 END AS 컬럼명`

## 5. CONCAT
### 1. 문제
```plain text
1. OCCUPATIONS 테이블에서 이름을 알파벳 순으로 정렬하여 추출한다.
    각 직업의 첫 글자를 괄호 안에 표시하여 출력한다.

2. OCCUPATIONS 테이블에서 각 직업의 발생 빈도를 계산한다.
    이를 오름차순으로 정렬하여 아래와 같은 형식으로 출력한다.
    "There are a total of [occupation_count] [occupation]s."
```
### 2. 코드
```SQL
SELECT CONCAT(NAME, '(', LEFT(OCCUPATION, 1), ')')
FROM OCCUPATIONS
ORDER BY NAME;

SELECT CONCAT("There are a total of ", COUNT(OCCUPATION), ' ', LOWER(OCCUPATION), "s.")
FROM OCCUPATIONS
GROUP BY OCCUPATION
ORDER BY COUNT(OCCUPATION), OCCUPATION;
```
### 3. 출력
```plain text
Aamina(D)
Ashley(P)
Belvet(P)
Britney(P)
Christeen(S)
Eve(A)
Jane(S)
Jennifer(A)
Jenny(S)
Julia(D)
Ketty(A)
Kristeen(S)
Maria(P)
Meera(P)
Naomi(P)
Priya(D)
Priyanka(P)
Samantha(A)
There are a total of 3 doctors.
There are a total of 4 actors.
There are a total of 4 singers.
There are a total of 7 professors.
```
### 4. 배운 점
1. MySQL의 문자열 자르기 함수 (SUBSTRING, LEFT, RIGHT) [출처: [[MSSQL] 문자열 자르기 (SUBSTRING, LEFT, RIGHT)
](https://gent.tistory.com/436)]
    - `SUBSTRING("문자열", "시작위치", "길이")`: 지정한 위치에서 지정한 문자열 길이만큼 자를 때 사용
        ```SQL
        SELECT SUBSTRING('SQL Server 2019', 1, 3) AS str1,
               SUBSTRING('SQL Server 2019', 5, 6) AS str2,
               SUBSTRING('SQL Server 2019', 12, 4) AS str3
        ```
        ```plain text
        SQL
        Server
        2019
        ```

    - `LEFT("문자열", "길이")`: 왼쪽에서부터 지정한 문자열의 길이만큼 자를 때 사용

        ```SQL
        SELECT LEFT('SQL Server 2019', 3) AS str1,
               LEFT('SQL Server 2019', 10) AS str2
        ```
        ```plain text
        SQL
        SQL Server
        ```

    - `RIGHT("문자열", "길이")` : 오른쪽에서부터 지정한 문자열의 길이만큼 자를 때 사용

        ```SQL
        SELECT RIGHT('SQL Server 2019', 4) AS str1,
               RIGHT('SQL Server 2019', 11) AS str2
        ```
        ```plain text
        2019
        Server 2019
        ```
2. `GROUP BY`에 대해서 다시 한번 공부해보기