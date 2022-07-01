---
title: "패키지, 문자열 비교"
excerpt: "패키지란? 문자열 비교 과정"

categories:
    - Java
tags:
    - [Java]

toc: true
toc_sticky: true

comments:
  provider: "utterances"
  utterances:
    theme: "github-light" # "github-dark"
    issue_term: "pathname"
    label: "comment" # Optional - must be existing label.

date: 2022-07-01
last_modified_at: 2022-07-01
---
# 패키지
패키지란 기능이 비슷한 클래스를 모아둔 것이다.  
클래스의 접근권한이 public일 경우에는 외부의 패키지에서 접근이 가능하다.  
접근권한을 명시하지 않으면 기본 값으로 default가 설정된다.  
디폴트는 패키지 내부의 클래스에게는 퍼블릭 권한이 주어지고,  
패키지 외부의 클래스에게는 private 접근권한이 주어진다.  
패키지 외부에서 클래스에 접근하려면 클래스 위치를 알아야한다.  
```java
kr.tpc.print
```
일일이 작성하는 대신에 import를 사용한 후에 클래스 이름만으로 사용할 수 도 있다.  
# String 클래스
## new로 생성
문자열은 java.lang.String을 사용해 객체로 만들어진다.  
new를 사용해 생성하면 서로 다른 별개의 객체가 힙 영역에 만들어지고 각각의 주소를 가리키고 있기 때문에 ==을 사용해 동일한지를 비교하면 같은 문자내용이더라고 주소가 다르기 때문에 다르다고 나오게된다.  
그래서 내용이 같은지를 판별하기 위해선 ```.equals```를 사용하면 문자끼리 비교할 수 있다.
```java
String str1 = new String("APPLE");
String str2 = new String("APPLE");
```
str1과 str2는 별개의 객체를 가리키고 있다.  
## 문자열 상수로 생성
문자열 상수로 생성하게 되면 리터럴 풀에 객체가 생성되고 재활용이 되기떄문에
동일한 내용이면 또 다른 객체를 별개로 생성하지 않고 동일한 객체를 재사용하게 된다.  
가리키는 주소가 같기 때문에 ==을 사용해도 같다고 판별된다.  
```java
String str1 = "APPLE";
String str2 = "APPLE";
```
str1과 str2는 동일한 객체를 가리키고 있다.