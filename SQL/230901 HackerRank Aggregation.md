# HackerRank Aggregation
- [ROUND](#1-round)
- [REPLACE](#2-replace)
- [WHERE](#3-where)

## 1. ROUND

### 1. 문제
```plain text
CITY 테이블에서 모든 도시의 평균 인구를 구하라.
이때 정수에 근접하게 반올림하라.
```

### 2. 코드
```SQL
SELECT ROUND(AVG(POPULATION))
FROM CITY;
```
### 3. 출력
```plain text
454250
```
### 4. 배운 점
1. COUNT, AVG 등의 집계함수에 ROUND를 입혀서 반올림할 수 있다는 것을 알 수 있었다.
2. 집계함수에 대해 정리했다.
    - SUM: 데이터의 합
    - COUNT: 데이터의 개수
    - MAX: 데이터의 최대값
    - MIN: 데이터의 최소값
    - AVG: 데이터의 평균값

## 2. REPLACE

### 1. 문제
```plain text
Samantha는 EMPLOYEES 테이블에서 모든 근로자의 월 평균 SALARY를 계산하고 있었다.
그러나 계산을 완료한 이후, 키보드의 0키가 고장나 있음을 깨달았다.
Samantha는 실제 평균 SALARY와 miscalculated SALARY(0이 제거된 SALARY) 간의 차이를 구하고자 한다.

ACTUAL SALARY - MISCALCULATED SALARY를 구하고, 정수로 올림하여 추출하라.
```

### 2. 코드
```SQL
SELECT CEIL(AVG(SALARY) - AVG(REPLACE(SALARY, 0, '')))
FROM EMPLOYEES;
```
### 3. 출력
```plain text
2253
```
### 4. 배운 점
1. 올림, 내림, 반올림, 소수점 아래 버림 등의 함수를 배웠다.
    - `CEIL(숫자)`: 올림
    - `TRUNCATE(숫자, 자릿수)`: 내림
        ```SQL
        SELECT TRUNCATE(SUM(LAT_N), 4) AS SUM_LAT
        FROM STATION
        WHERE LAT_N > 38.7880 AND LAT_N < 137.2345
        ```
        ```plain text
        36354.8135
        ```
    - `ROUND(숫자, 자릿수)`: 반올림
        ```SQL
        SELECT ROUND(SUM(LAT_N), 2), ROUND(SUM(LONG_W), 2)
        FROM STATION;
        ```
        ```plain text
        42850.04 47381.48
        ```
    - `FLOOR(숫자)`: 내림(소수점 아래 버림)
2. 수학 관련 함수를 배웠다.
    - `ABS(숫자)`: 절댓값
    - `POW(X, Y)`: X의 Y제곱
    - `MOD(X, Y)`: X를 Y로 나눈 나머지
3. 문자열 변경함수에 대해 배웠다.
    - `REPLACE(대상, 바꾸고 싶은 것, 무엇으로 바꿀지)`

## 3. WHERE

### 1. 문제
```plain text
STATION 테이블에서 LAT_N이 137.2345보다 작은, 가장 큰 LONG_W를 추출하라.
답은 소수점 이하 4자리로 반올림하라.
```

### 2. 코드
```SQL
SELECT ROUND(LONG_W, 4)
FROM STATION
WHERE LAT_N < 137.2345
ORDER BY LAT_N DESC LIMIT 1;
```
### 3. 출력
```plain text
117.2465
```
### 4. 배운 점
1. SQL에서 `SUM`, `MAX` 등의 집계 함수는 `WHERE`절에 직접 사용할 수 없다.
    - `SELECT`, `HAVING`, `ORDER BY`절에서 사용 가능하다.
    - `WHERE` 절은 특정 레코드를 필터링할 때 사용하다.
    - `GROUP BY` 절은 필터링된 결과를 특정 칼럼에 따라 그룹화한다.
    -  `HAVING` 절은 `GROUP BY`를 수행한 뒤에 그룹별로 조건을 적용할 때 사용한다.
    ```plain text
    (예시)
    이름별로 총 급여를 계산하고, 총 급여가 5000 이상인 경우만 선택하는 SQL 쿼리
    ```
    ```SQL
    SELECT name, SUM(salary) as total_salary
    FROM employees
    GROUP BY name
    HAVING total_salary >= 5000;
    ```