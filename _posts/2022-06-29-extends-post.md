---
title: "상속"
excerpt: "오버라이드, 형변환"

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
# 상속
## 수평적 설계
코드가 중복되고 관리하기가 어렵다.
## 수직적 설계
수평적 설계의 단점을 보완하고 확장이 용이하다.
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
		System.out.println("고양이가 먹다"); //오버라이드(재정의)
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
		System.out.println("개가 먹다"); //오버라이드
	}
	public Dog() {
		super();
	}
}
```
하위 클래스(Cat, Dog)는 상위 클래스(Animal)를 상속받는다.  
super()메소드가 부모의 생성자를 호출하고 그 후에 자신의 생성자를 호출하게 된다.  
상속 받는다는 것은 부모 클래스의 영역까지 접근영역을 늘리는 것이고 extends를 사용한다.  
모든 클래스의 가장 상위에는 최종적으로 Object클래스가 있다.  
Object클래스는 생략이 가능하다.

# 오버라이드(재정의)
상속관계에서 하위 클래스가 상위 클래스의 동작을 수정하는 것을 오버라이드라 한다.  
메모리에 부모와 자식 메서드가 공존하지만 부모 메서드는 무시되고, 결국에는 자식 메서드가 실행된다.  
오버라이드를 통해 하위 클래스로 접근 할 수 있으며, 동적 바인딩이므로 프로그램의 속도가 떨어지는 단점이있다.  

```java
Animal a = new Dog();
a.eat();
```
Dog자식 타입은 Animal부모 타입으로 자동 형 변환(업캐스팅)이 된다.  
Animal클래스를 실행하면 자식 클래스에 오버라이드된 메소드가 있는 지 확인하고 있다면 그것을 실행한다.  
그래서 호출될 메서드가 실행시점에서 결정되기 떄문에 속도가 느리게 된다.
```java
Animal a = new Cat();
a.eat();
a.night(); // X
((Cat)a).night(); // O
```
Animal클래스에는 night메소드가 존재하지 않는다.  
그래서 다운캐스팅(강제 형 변환)을 해줘야 접근할 수 있다.  
# 상속관계에서 객체생성 방법
## 직접이용
```java
Dog d = new Dog();
```
상속의 이점을 활용하지 못한다.
## 간접이용
```java
Animal d = new Dog();
```
.class파일만 있는 경우같이 하위 클래스의 동작 방식을 모를 때 사용한다.
