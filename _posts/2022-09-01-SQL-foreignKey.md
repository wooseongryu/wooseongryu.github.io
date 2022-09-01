---
title: "Foreign Key"
excerpt: "On Delete, On Update, schema"

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

date: 2022-09-01
last_modified_at: 2022-09-01
---
# foreign key 설정
foreign key는 참조무결성(Referential Integrity)을 지키기위해 설정한다.  
```sql
ALTER TABLE `course_rating`.`review` 
ADD CONSTRAINT `fk_review_table`
  FOREIGN KEY (`course_id`)
  REFERENCES `course_rating`.`course` (`id`)
  ON DELETE RESTRICT
  ON UPDATE RESTRICT;
```
course_id컬럼을 외래키로 설정하고 course테이블의 id컬럼을 참조한다.  

# SHOW CREATE TABLE
```sql
SHOW CREATE TABLE 테이블이름;
```
특정 테이블을 바로 생성한다고 할 때 작성해야할 CREATE TABLE문이 뭔지를 보여준다.  

# 부모테이블의 로우가 삭제될 때(On Delete)
부모테이블의 로우가 삭제될 때 그 로우를 참조하던 자식테이블의 로우는 어떤 정책을 취하냐에 따라 처리가 달라진다.  
## RESTRICT(NO ACTION) 정책
RESTRICT가 설정되어 있으면 자신을 참조하고 있는 자식테이블의 로우가 하나라도 있는 부모테이블의 로우는 삭제할 수 없다.  
NO ACTION도 동일한 기능을 한다.  
## CASCADE 정책
부모테이블의 로우를 삭제할 때 그것을 참조하고 있던 자식테이블의 로우도 함께 삭제된다.  
## SET NULL 정책
부모테이블의 로우가 삭제됐을 때 그것을 참조하던 자식테이블의 foreign key컬럼의 값을 모두 NULL로 바꾼다.  

# 부모테이블의 로우가 갱신될 때(On Update)
부모 테이블의 로우가 갱신될 때 취하는 정책은 삭제될 때와 동일하다.  
## RESTRICT(NO ACTION) 정책
RESTRICT가 설정되어 있으면 자신을 참조하고 있는 자식테이블의 로우가 하나라도 있는 부모테이블의 로우는 갱신할 수 없다. 
## CASCADE 정책
부모테이블의 로우를 갱신할 때 그것을 참조하고 있던 자식테이블의 로우도 함께 갱신된다.
## SET NULL 정책
부모테이블의 로우가 갱신됐을 때 그것을 참조하던 자식테이블의 foreign key컬럼의 값을 모두 NULL로 바꾼다. 

# 논리적 Foreign Key, 물리적 Foreign Key
실제로 해당 컬럼을 외래키로 설정해서 두 테이블 간의 참조 무결성을 지키게 된것을 물리적 외래키라 하고 개념상, 논리적으로 성립하는 외래키를 논리적 외래키라 한다.  
논리적 외래키를 사용하는 이유는 첫 째로 성능 문제인데 물리적 외래키는 추가로 검증하는 단계를 거치기 때문에 속도가 저하되는 단점이 있다. 두번 째로 레거시 데이터의 참조 무결성이 이미 깨진 상태일 때가 있다. 레거시 데이터는 기존의 데이터, 코드 등을 말하는데 이럴 때 물리적 외래키를 설정하려면 참조 무결성을 어기는 로우들을 삭제할 수 밖에 없게된다. 그래서 참조 무결성이 깨지더라도 데이터를 지키기위해 물리적 외래키를 사용하지 않는 경우도 있다. 다만 참조 무결성을 완벽하게 지켜야하는 서비스에서는 반드시 물리적 외래키를 설정해야한다.  

# Foreign Key 삭제
```sql
ALTER TABLE 테이블 이름
    DROP FOREIGN KEY 외래키이름;
```
# 스키마(SCHEMA)
데이터베이스에 관한 모든 설계사항을 스키마라고 한다.  
데이터베이스를 새롭게 구축해야 할 때는 먼저 스키마를 짜야한다.  
스키마를 짜는 것을 데이터베이스 모델링, 데이터베이스 디자인 이라고 한다.  
스키마는 두가지 종류가 있다.  
## 개념적 스키마
위의 내용이 개념적 스키마에 해당하는 내용이다. 보통 스키마라 하면 개념적 스키마를 의미한다.  
## 물리적 스키마
물리적 스키마는 데이터를 실제로 컴퓨터의 저장장치에 어떤 방식으로 저장할지를 결정하는 스키마다.  
DBMS를 만드는 개발자들이 다루는 개념이다.  

그리고 DBMS들이 제각각 조금씩 다른의미로 스키마라는 단어를 사용하는데 MySQL에서는 스키마를 그냥 데이터베이스와 같은 의미로 혼용하고 있다.  
