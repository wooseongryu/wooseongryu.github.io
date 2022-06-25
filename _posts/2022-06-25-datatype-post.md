---
title: "기본 타입과 참조 타입"
excerpt: "기본 타입과 참조 타입의 관계"

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

date: 2022-06-25
last_modified_at: 2022-06-25
---
# 기본 타입
기본 타입은 컴파일러에서 기본적으로 제공해주는 자료형이다.  
# 참조 타입
참조 타입은 사용자가 직접 만들어서 사용하는 자료형이다.  

```java
public class BookDTO {
    public String title;
    public int price;
    //기본 생성자
    public BookDTO() {
        super();
    }
}
```
BookDTO생성자 메서드가 title, price변수를 가진  
객체를 생성하는 역할을 한다. 
## 생성자 메서드
생성자 메서드는 객체를 생성할 때 사용된다.
```java
public BookDTO() {
    super();
}
```
객체 생성 후 초기화를 하는 역할을 한다.  
리턴 타입이 없고 생성자가 없을때는 기본 생성자가 자동으로 만들어지며, 생략이 가능하다.
## 참조 타입 선언
```java
BookDTO b;
b = new BookDTO();
// '.'을 사용해 멤버에 접근
b.title = "자바";
b.price = 17000;
```
BookDTO라는 자료형을 선언하고 싶으면  
생성자 메서드(new)를 사용해야한다.  
스택 영역에 BookDTO객체를 가리키는 b와 this변수가 생성된다.  
this는 객체 자신을 가리키고 객체 내부에서 멤버에 접근할 때 사용된다.  
## 중복정의(오버로딩)
오버로딩은 매개 변수를 달리하는 생성자를  
여러 개 선언하는 것을 말한다.
```java
BookDTO b = new BookDTO();
BookDTO b1 = new BookDTO("파이썬", 18000);
```
```java
public class BookDTO {
    public String title;
    public int price;

    public BookDTO() {
        super();
    }

    public BookDTO(String title, int price) {
        this.title = title;
        this.price = price;
    }
}
```
생성자를 오버로딩하면 기본생성자는 자동으로 만들어지지 않는다.  


