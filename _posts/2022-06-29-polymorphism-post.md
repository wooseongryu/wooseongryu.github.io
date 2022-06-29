---
title: "다형성"
excerpt: "다형성이란?"

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

date: 2022-06-29
last_modified_at: 2022-06-29
---
# 다형성
상속관계에서 상위클래스가 동일한 메시지로 하위클래스들을 서로 다르게 동작시키는 것.  
```java
public class Animal extends Object {
	public void eat() {
		System.out.println("먹다");
	}
	public Animal() {
		super();
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
	public Cat() {
		super();
	}
}
```
```java
public class Dog extends Animal {
	public void eat() {
		System.out.println("개가 먹다");
	}
	public Dog() {
		super();
	}
}
```
상위 클래스(Animal)가 하위 클래스(Cat, Dog)의 구동방식을 알 지 못해도 상위 클래스를 통해 하위클래스를 구동 시킬 수 있다.  
Animal클래스에서 eat메소드를 작동시키면 하위 클래스들의 eat메소드가 각자 작동이된다.  
## 다형성 인수
```java
public static void main(String[] args) {
		Dog d = new Dog();
		display(d);
		Cat c = new Cat();
		display(c);	
	} 
	private static void display(Animal r) {
		r.eat();
		r.night(); // X
		if (r instanceof Cat) {
			((Cat)r).night();
		}
	}
```
다형성인수(Animal r)로 모든 하위 클래스를 받을 수 있다.  
## 다형성 배열
```java
public static void main(String[] args) {
		Animal[] ani = new Animal[2];
		ani[0] = new Dog();
		ani[1] = new Cat();
		
		for (int i = 0; i < ani.length; i++) {
			ani[i].eat();
			if (ani[i] instanceof Cat) {
				((Cat)ani[i]).night();
			}
		}
	}
```
서로 다른 하위 클래스를 담을 수 있다.

