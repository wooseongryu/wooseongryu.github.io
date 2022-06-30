---
title: "추상클래스"
excerpt: "추상클래스란?"

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
# 추상클래스
추상클래스는 추상메서드와 구현메서드로 구성되므로 일부 다형성을 보장한다.  
추상메서드는 구현부가 없고 abstract키워드를 추가하며 다형성을 보장한다.    
구형메서드는 서로 기능이 비슷한 클래스에 쓰인다.  
```java
public abstract class Animal {
	public void eat(); //추상메서드
    public void move() { //구현메서드
        System.out.println("무리를 지어 이동한다.");
    }
}
```
```java
public class Cat extends Animal {
	public void eat() {
		System.out.println("고양이가 먹다");
	}
    public void eye() {
        System.out.println("고양이의 눈이 빛나다");
    }
}
```
```java
public class Dog extends Animal {
	public void eat() {
		System.out.println("개가 먹다");
	}
}
```
eat메서드는 하위에서 재정의되어 상위의 eat메서드는 실행될 일이 없으므로  
구현부를 삭제하고 원형만 남긴다.  
원형만 남은 메서드는 불완전하므로 혼자서는 사용이 불가능하다.
```java
Animal a = new Animal(); //불가능
```
부모의 역할로서만 사용이 가능하며 부모가 명령을 내리면 자식은 반드시 작동(다형성을 보장)해야만 한다.  
다형성을 보장하려면 자식은 반드시 추상메서드를 구현(재정의)해야 한다.  

구현메서드는 move메서드와 같이 서로 기능이 비슷한 클래스에 동일한 기능을 넣을 때 사용한다.