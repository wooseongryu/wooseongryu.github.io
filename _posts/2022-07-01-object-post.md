---
title: "Object"
excerpt: "Object클래스에 대해 알아보자"

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
# Object클래스
```java
import java.lang.*; // 생략가능
public class A extends Object { //extends키워드 생략가능
	public A() { // 기본생성자 생략가능
		super();
	}
	public void display() {
		System.out.println("나는 A이다.");
	}
	@Override
	public String toString() {
		return "재정의 메서드입니다.";
	}
}
```
Object클래스는 모든 클래스의 최상위 클래스이다.  
Object클래스의 toString메소드는 원래 주소값을 출력하지만  
재정의를 해서 기능을 바꿀 수 있다.
```java
Object o = new A();
((A)o).display();
```
업캐스팅이 가능하며 반대로 다운캐스팅도 가능하다.
## 다형성 인수
```java
public static void main(String[] args) {
	A a = new A();
	display(a);
		
	B b = new B();
	display(b);
}
private static void display(Object o) { //다형성인수
	if (o instanceof A) { //o가 A로 부터 나온 인스턴스라면
		((A)o).go();
	} else {
		((B)o).go();			
	}
}
```
display메소드에 A a, B b로 받는 대신 Object o로 한번에 받을 수 있다.
## 다형성 배열
```java
Object[] o = new Object[2]; //다형성배열
o[0] = new A();
o[1] = new B();

for (int i = 0; i < o.length; i++) {
	if (o[i] instanceof A) {
		((A)o[i]).go();
	} else {
		((B)o[i]).go();				
	}
}
```
Object를 부모로 사용해 배열로 담을 수 있다.