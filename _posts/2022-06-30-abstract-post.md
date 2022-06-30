---
title: "추상클래스와 인터페이스의 관계"
excerpt: "추상클래스, 인터페이스, 다형성?"

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
# 추상클래스와 인터페이스
추상클래스와 인터페이스는 다형성을 보장받아야 할때 쓰이며 객체를 생성 할 수 없다.    
단독으로 쓰일 수 없고 부모의 역할로 사용하며 추상 메서드를 가진다. 
추상 메서드는 하위 클래스에서 반드시 오버라이드가 되어야 한다.  
## 추상클래스
추상클래스는 기능이 비슷한 클래스의 공통 부분을 묶을 때 사용한다.  
구현메서드와 추상메서드를 함께 가질 수 있다.
## 인터페이스
인터페이스는 기능이 다른 클래스의 공통 부분을 묶을 떄 사용한다.  
추상메서드로만 이루어져 있고 구현메서드를 가질 수 없다.  
final static 멤버변수를 가질 수 있다.