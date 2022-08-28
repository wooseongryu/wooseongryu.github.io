---
title: "컬럼끼리 계산"
excerpt: "Alias, CONCAT, CASE, IF, DISTINCT, SUBSTRING"

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
# 컬럼끼리 계산하기
컬럼끼리 기본적인 산술연산을 할 수 있다. (+, - , *, /, %)
```sql
SELECT age + height FROM school.member;
```
age와 height를 더한 값이 나온다.  

# Alias
컬럼의 이름을 alias로 대체할 수 있다.  
```sql
컬럼 AS 바꿀이름
```
```sql
SELECT age + height AS b FROM school.member;
```
age + height의 이름이 b로 대체되어 나오게 된다.  

AS를 생략하고 한칸을 띄우기만 해도 alias가 적용된다.  
```sql
컬럼 바꿀이름
```
```sql
SELECT (age + height) b FROM school.member;
```
동일한 결과가 나오지만 항상 AS를 붙여 가독성을 높여주는 편이 좋다.  

alias에 스페이스를 포함시키려면 따옴표를 붙여야 한다.  
따옴표를 생략하면 스페이스를 기준으로 구문해석을 하는 SQL의 특성상 에러가 발생하게된다.  
예시) AS 'a b c'  

# CONCAT
CONCAT으로 여러 컬럼의 값을 하나의 값으로 나타낼 수 있다.  
```sql
CONCAT(컬럼, 컬럼)
```
```sql
SELECT CONCAT(height, '---', age) AS aaa FROM school.member;
```
height와 문자열 '---', age가 하나의 값으로 출력된다.  
예시) 167.2---27  
그리고 CONCAT은 보통 alias를 같이 해준다.  

# CASE
CASE는 특정 값을 원하는 방식으로 변환하여 표현하게 해준다.   
## 단순 CASE()함수
```sql
CASE 컬럼
    WHEN 값1 THEN 값2
    WHEN 값1 THEN 값2
    ELSE 값2
END
```
해당 컬럼과 값1이 같으면 값2를 리턴한다.
```sql
SELECT
(CASE age
	WHEN 29 THEN 'A'
    WHEN 30 THEN 'B'
    WHEN 31 THEN 'C'
    ELSE 'D'
END) AS ageabc
FROM school.member;
```
age가 29면 A, 30이면 B, 31이면 C가 나오고 그밖에는 D가 나오게 된다.  
CASE문 바로 뒤에 컬럼 이름을 쓰고 그 컬럼의 값과 비교할 값이 같은지(=) 비교하는 함수를 단순CASE함수라고 한다.  
## 검색 CASE()함수
```sql
CASE
    WHEN 조건 THEN 값
    WHEN 조건 THEN 값
    ELSE 값
END
```
WHEN에서 True인 조건을 만나면 THEN의 값을 리턴한다.   
```sql
SELECT
(CASE
	WHEN age >= 25 THEN 'A'
    ELSE 'B'
END) AS ageab
FROM school.member;
```
age가 25이상이면 A, 아니면 B를 리턴한다.  

단순CASE()에서는 등호연산 밖에 할 수 없었지만 검색CASE()에서는 다양한 형태의 조건을 걸 수 있다.  
그리고 alias도 같이 해주면 좋다.  
# IF
IF는 첫번째 인자로 조건식이 오고, 그 조건식이 True라면 두번째 인자, False라면 세번째 인자를 리턴한다.  
```sql
IF(조건식, True, False)
```
```sql
SELECT IF(height >= 170, height, 'a') FROM school.member;
```
조건식이 True라면 height가 리턴되고, False라면 'a'가 리턴된다. 

# DISTINCT
DISTINCT()를 사용하면 고유값만 받을 수 가 있다.  
```sql
DISTINCT(컬럼)
```
```sql
SELECT DISTINCT(age) FROM school.member;
```

# SUBSTRING
SUBSTRING()으로 문자열의 일부를 추출할 수 있다.  
```sql
SUBSTRING(컬럼, a, b)
```
해당 컬럼의 a번째 부터 b개의 문자를 추출한다.
```sql
SELECT SUBSTRING(address, 1, 2) FROM school.member;
```
address컬럼의 1번째 문자부터 2개의 문자를 추출한다.  

# DISTINCT 활용
```sql
SELECT DISTICNT(SUBSTRING(address, 1, 2)) FROM school.member;
```
컬럼의 특정 내용을 고유값으로 받을 수 있다.  
```sql
SELECT COUNT(DISTICNT(SUBSTRING(address, 1, 2))) FROM school.member;
```
컬럼에 존재하는 고유값의 개수를 구할 수 있다.

# LENGTH
LENGTH()는 문자열의 길이를 구해준다.
```sql
LENGTH(컬럼)
```
```sql
SELECT LENGTH(address) FROM school.member;
```
address의 길이를 보여준다.

# UPPER, LOWER
문자열을 모두 대문자, 소문자로 바꿔 보여준다.
```sql
UPPER(컬럼)
LOWER(컬럼)
```
```sql
SELECT UPPER(email) FROM copang_main.member;
SELECT LOWER(email) FROM copang_main.member;
```

# LPAD, RPAD
LPAD(Left Padding)는 문자열의 왼쪽을 특정 문자열로 채워준다.  
RPAD(Right Padding)는 문자열의 오른쪽을 특정 문자열로 채워준다.  
```sql
LPAD(컬럼, 자릿수, 문자)
RPAD(컬럼, 자릿수, 문자)
```
```sql
SELECT LPAD(age, 10, '0') FROM copang_main.member;
SELECT RPAD(age, 10, '0') FROM copang_main.member;
```
age컬럼의 값을 왼쪽에 문자'0'을 붙여서 총 10자리로 만든다.  
어떤 숫자의 자릿수를 맞출때 사용하는 함수다.  
예시) 0000000021, 0000000009

# TRIM, LTRIM, RTRIM
LTRIM()은 왼쪽 공백삭제, RTRIM()은 오른쪽 공백삭제, TRIM()은 양쪽 공백삭제.  
```sql
LTRIM(컬럼)
RTRIM(컬럼)
TRIM(컬럼)
```
```sql
SELECT LTRIM(age) FROM school.trim_test;
SELECT RTRIM(age) FROM school.trim_test;
SELECT TRIM(age) FROM school.trim_test;
```
age의 값이 " &nbsp;&nbsp;19"같이 공백이 있으면 LTRIM으로 왼쪽의 공백을 삭제할 수 있다.