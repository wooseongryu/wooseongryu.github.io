---
title: "private 생성자"
excerpt: "private생성자와 static의 관계"

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
# private생성자 메서드
객체를 생성하는 생성자 메서드가 private 접근제어를 가지면 객체를 생성할 수 가 없다.  
그래서 객체를 생성하지 않고 사용이 가능해야 한다.  
## non-static 멤버 (인스턴스 메서드)
```java
public class lang {
    public lang() {

    }
    public void java() {
        System.out.println("java");
    }
    public void python() {
        System.out.println("python");
    }
}
```
객체 생성 후 접근이 가능하다.
```java
lang l = new lang();
l.java();
l.python();
```
## static 멤버 (클래스 메서드)
```java
public class lang {
    private lang() {

    }
    public static void java() {
        System.out.println("java");
    }
    public static void python() {
        System.out.println("python");
    }
}
```
객체 생성 없이 접근이 가능하다.
```java
lang.java();
lang.python();
```
생성자가 private이면 객체 생성이 불가능 하므로  
멤버는 static이 붙어야 사용이 가능하다.