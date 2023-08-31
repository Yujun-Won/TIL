# HackerRank [Basic Select]
- ORDER BY
- SUBSTRING (1)
- SUBSTRING (2)

1. ORDER BY
    - 문제
        ```plain text
        STATION에서 CITY 이름이 가장 짧거나 가장 긴 두 CITY의 이름과 이름의 길이를 추출하라.
        만약 가장 짧거나 가장 긴 도시가 한 개 이상이라면, 알파벳 순서로 1개 출력하라.
        ```
    - 코드
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
    - 출력
        ```plain text
        Amo 3
        Marine On Saint Croix 21
        ```
    - 배운 점
        1. 위와 같이 가장 짧거나 가장 긴 것을 고르는 서로 상반된 조건은 쿼리문 하나 당 하나만 가능하다.
        2. 쿼리를 여러 번 날려서 하나씩 추출하고, 문제는 그것을 원할 수 있다.

2. SUBSTRING (1)
    - 문제
        ```plain text
        STATION에서 CITY 이름의 맨 앞과 맨뒤에 모음(A, E, I, O, U)을 가지고 있는 데이터를 추출하라.
        중복은 허용되지 않는다.
        ```
    - 코드
        ```SQL
        SELECT DISTINCT CITY
        FROM STATION
        WHERE SUBSTRING(CITY, 1, 1) IN ('A', 'E', 'I', 'O', 'U')
        AND SUBSTRING(CITY, -1, 1) IN ('A', 'E', 'I', 'O', 'U');
        ```
    - 출력
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
    - 배운 점
        1. `SUBSTRING(CITY, 1, 1) IN ('A', 'E', 'I', 'O', 'U')`: `CITY`의 첫번째 글자가 모음인지 확인
        2. `SUBSTRING(CITY, -1, 1) IN ('A', 'E', 'I', 'O', 'U')`: `CITY`의 마지막 글자가 모음인지 확인
        3. `SUBSTRING(COLUMN, NUM1, NUM2)`: 대상컬럼 `COLUMN`에서 `NUM1`은 시작 위치를 나타내고 `NUM2`는 추출할 문자의 길이를 의미

            예를 들어, SUBSTRING('HELLO', 1, 2)의 경우:

            NUM1 = 1: 문자열 'HELLO'에서 1번째 위치에서 시작 / NUM2 = 2: 시작 위치로부터 2개의 문자를 추출

            따라서 이 함수는 'HE'를 반환한다.

3. SUBSTRING (2)
    - 문제
        ```plain text
        Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

        STUDENTS에서 MARKS가 75보다 큰 임의의 학생의 NAME을 추출하라.
        NAME의 마지막 3글자를 기준으로 정렬하고, 만약 중복이 있다면 ID를 기준으로 오름차순 정렬하라.
        ```
    - 코드
        ```SQL
        SELECT NAME
        FROM STUDENTS
        WHERE MARKS > 75
        ORDER BY SUBSTRING(NAME, -3, 3) ASC, ID ASC;
        ```
    - 출력
        ```plain text
        Stuart
        Kristeen
        Christene
        Amina
        Aamina {-truncated-}
        ```
    - 배운 점
        1. `SUBSTRING(NAME, -3, 3) ASC`: `NAME`의 마지막 3개의 글자를 기준으로 오름차순 정렬한다.
        2. `ID ASC`: `ID` 기준의 오름차순은 두번째 우선순위이다.
