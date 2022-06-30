---
title: "인터페이스"
excerpt: "인터페이스란?"

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

date: 2022-06-30
last_modified_at: 2022-06-30
---
# 인터페이스
```java
public interface RC {
    public abstract void chUp();
    public void chDown();

    public static final int MAXCH = 100;
    int MINCH = 1;
}

```
인터페이스는 기능이 서로 다른 클래스끼리 묶고 다형성을 완전히 보장한다.  
abstract키워드는 생략이 가능하다.  
구현 메서드를 가질 수 없고 불완전한 메서드만 올 수 있다.  
인터페이스는 상수를 둘 수 있으며 "public static final"은 생략 가능하다.  
인터페이스는 객체 생성이 불가능 하기 때문에 static을 사용하고 final로 상수 값으로 지정한다.  
하위 클래스의 작동 방식을 몰라도 인터페이스를 통해 완전히 동작시킬 수 있다.
```java
public class TV implements RC {
	public void chUp() {
		System.out.println("티비 채널 올라감.");
	}
	public void chDown() {
		System.out.println("티비 채널 내려감.");
	}
}
```
```java
public class Radio implements RC {
	public void chUp() {
		System.out.println("라디오 채널이 올라감.");
	}
	public void chDown() {
		System.out.println("라디오 채널이 내려감.");
	}
}
```
하위 클래스는 상위 클래스의 추상 메서드를 반드시 작동해야한다.