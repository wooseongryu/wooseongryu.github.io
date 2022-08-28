---
title: "집계함수와 산술함수"
excerpt: "집계함수, 산술함수"

categories:
    - SQL
tags:
    - [SQL]

toc: true
toc_sticky: true

comments:
  provider: "utterances"
  utterances:
    theme: "github-light" # "github-dark"
    issue_term: "pathname"
    label: "comment" # Optional - must be existing label.

date: 2022-08-28
last_modified_at: 2022-08-28
---
# 집계함수
집계함수(Aggregate Funtion)는 어떤 컬럼의 값들을 대상으로 원하는 특정값을 구해주는 함수이다.  
여러 row값들을 동시에 고려해서 실행된다.  
## COUNT
해당 컬럼의 값을 가진 총 row의 수를 구한다.  
```sql
COUNT(컬럼)
```
```sql
SELECT COUNT(height) FROM school.member;
```
height컬럼의 NULL이 아닌 row들의 수를 구해준다.  

NULL의 유무와 상관없이 모든 row를 구하고 싶다면 *를 사용하면 된다.  
```sql
COUNT(*)
```
## MAX, MIN
```sql
MAX(컬럼)
MIN(컬럼)
```
```sql
SELECT MAX(height) FROM school.member;
SELECT MIN(height) FROM school.member;
```
해당 컬럼의 최댓값과 최솟값을 구해준다.  

## AVG, SUM, STD
```sql
AVG(컬럼)
SUM(컬럼)
STD(컬럼)
```
```sql
SELECT AVG(height) FROM school.member;
SELECT SUM(height) FROM school.member;
SELECT STD(height) FROM school.member;
```
해당 컬럼의 평균(NULL은 제외하고 계산된다), 합계, 표준편차를 구해준다.  

# 산술함수
산술함수(Mathematical Funtion)는 특정 컬럼의 각 row의 값마다 실행된다.  
## ABS
```sql
ABS(컬럼)
```
```sql
SELECT ABS(height) FROM school.member;
```
해당 컬럼의 절댓값을 구해준다.
## SQRT
```sql
SQRT(컬럼)
```
```sql
SELECT SQRT(height) FROM school.member;
```
해당 컬럼의 제곱근을 구해준다.  
## CEIL, FLOOR, ROUND
```sql
CEIL(컬럼)
FLOOR(컬럼)
ROUND(컬럼)
```
```sql
SELECT CEIL(height) FROM school.member;
SELECT FLOOR(height) FROM school.member;
SELECT ROUND(height) FROM school.member;
```
해당 컬럼의 올림값, 내림값, 반올림값을 구해준다.  