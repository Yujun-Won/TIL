# HackerRank [Advanced Select]
- CASE WHEN
- CONCAT

1. CASE WHEN
    - 문제
        ```plain text
        TRIANGLES에는 3면의 길이가 기록되어 있다.
        출력은 다음과 같다.
        - Equilateral: 3면이 같은 길이인 삼각형
        - Isosceles: 2면이 같은 길이인 삼각형
        - Scalene: 3면이 모두 다른 길이인 삼각형
        - Not A Triangle: A, B, C가 삼각형을 구성하지 않음
        ```
    - 코드
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
    - 출력
        ```plain text
        Amo 3
        Marine On Saint Croix 21
        ```
    - 배운 점
        1. 삼각형의 어떤 두 변의 길이의 합은 항상 다른 한 변의 길이보다 커야 한다.
        2. `CASE WHEN 조건 ELSE 마무리 END AS 컬럼명`

2. CONCAT
    - 문제
        ```plain text
        1. OCCUPATIONS 테이블에서 이름을 알파벳 순으로 정렬하여 추출한다.
           각 직업의 첫 글자를 괄호 안에 표시하여 출력한다.

        2. OCCUPATIONS 테이블에서 각 직업의 발생 빈도를 계산한다.
           이를 오름차순으로 정렬하여 아래와 같은 형식으로 출력한다.
           "There are a total of [occupation_count] [occupation]s."
        ```
    - 코드
        ```SQL
        SELECT CONCAT(NAME, '(', LEFT(OCCUPATION, 1), ')')
        FROM OCCUPATIONS
        ORDER BY NAME;

        SELECT CONCAT("There are a total of ", COUNT(OCCUPATION), ' ', LOWER(OCCUPATION), "s.")
        FROM OCCUPATIONS
        GROUP BY OCCUPATION
        ORDER BY COUNT(OCCUPATION), OCCUPATION;
        ```
    - 출력
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
    - 배운 점
        1. MySQL의 문자열 자르기 함수 (SUBSTRING, LEFT, RIGHT) [출처: [[MSSQL] 문자열 자르기 (SUBSTRING, LEFT, RIGHT)
](https://gent.tistory.com/436)]
            - `SUBSTRING("문자열", "시작위치", "길이")`: 지정한 위치에서 지정한 문자열 길이만큼 자를 때 사용

                ```SQL
                SELECT SUBSTRING('SQL Server 2019', 1, 3)  AS str1
                    , SUBSTRING('SQL Server 2019', 5, 6)  AS str2
                    , SUBSTRING('SQL Server 2019', 12, 4) AS str3
                ```
                ```plain text
                SQL
                Server
                2019
                ```

            - `LEFT("문자열", "길이")`: 왼쪽에서부터 지정한 문자열의 길이만큼 자를 때 사용

                ```SQL
                SELECT LEFT('SQL Server 2019', 3)  AS str1
                    , LEFT('SQL Server 2019', 10) AS str2
                ```
                ```plain text
                SQL
                SQL Server
                ```

            - `RIGHT("문자열", "길이")` : 오른쪽에서부터 지정한 문자열의 길이만큼 자를 때 사용

                ```SQL
                SELECT RIGHT('SQL Server 2019', 4)  AS str1
                    , RIGHT('SQL Server 2019', 11) AS str2
                ```
                ```plain text
                2019
                Server 2019
                ```
        2. `GROUP BY`에 대해서 다시 한번 공부해보기