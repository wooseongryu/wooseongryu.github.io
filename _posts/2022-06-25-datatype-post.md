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
생성자는 리턴값이 없고  
기본 생성자는 클래스가 가지고 있는 멤버들을 메모리에  
객체로 생성하는 역할을 하며, 생략이 가능하다.
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
