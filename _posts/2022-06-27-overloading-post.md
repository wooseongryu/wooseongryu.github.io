---
title: "메소드 오버로딩"
excerpt: "메소드 오버로딩이란?"

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
# 메서드 오버로딩
같은 이름의 메서드를 매개변수의 타입과 개수가 다르게해서 여러개 만드는 것.
```java
public class OverLoad {
	public void hap(int a, int b) {
		System.out.println(a + b);
	}
	public void hap(float a, int b) {
		System.out.println(a + b);
	}
	public void hap(int a, int b, int c) {
		System.out.println(a + b + c);
	}
}
```
메서드의 이름은 같지만 에러가 나지 않는다.  

```java
OverLoad o = new OverLoad();
o.hap(1, 2);
```
오버로딩은 정적 바인딩으로 컴파일 시점에서 호출될 메서드가 이미 결정되어 있다.  
위의 코드를 컴파일 하게되면 컴파일러는 메서드 이름을  
```hap_int_int```로 만들고 바로 호출하게 되므로, 속도와는 관계가 없다.