---
title: "배열과 클래스"
excerpt: "배열과 클래스의 관계"

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

date: 2022-06-27
last_modified_at: 2022-06-27
---
# 배열
동일한 데이터 타입들의 구조
```java
//동일한 int형 10개 짜리 배열
int[] ary = new int[10];
```
# 클래스
서로 다른 데이터 타입들의 구조
```java
//자료형 혼합 가능
BookDTO b = new BookDTO("자바", 17000);
```
## 객체 배열
```java
BookDTO[] b = new BookDTO[3];
b[0] = new BookDTO("자바", 17000);
b[1] = new BookDTO("파이썬", 18000);
b[2] = new BookDTO("C", 19000);
```
# 클래스, 객체, 인스턴스 관계
```java
public class BookDTO {
    public String title;
    public String price;
}
```
설계도를 클래스라 한다.  
새로운 자료형 BookDTO를 만들어 낸다.
```java
BookDTO b;
```
클래스 자료형으로 선언된 변수를 객체라 한다.
```java
b = new BookDTO();
```
변수가 클래스를 바탕으로 생성된 객체를 가리키면 인스턴스라 한다.  
즉, 객체가 실제로 메모리에 만들어질때(설계도를 바탕으로 실체를 구현할떄)를 말한다.