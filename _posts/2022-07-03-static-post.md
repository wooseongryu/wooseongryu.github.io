---
title: "static과 final"
excerpt: "staic과 final의 관계"

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

date: 2022-07-03
last_modified_at: 2022-07-03
---
# static
스테틱은 클래스가 실행될때 메서드 영역에 자동으로 로딩이 된다. 그래서 사용할 때 마다 메모리에 따로 로딩을 할 필요가 없다.  
스테틱과 인스턴스 중 어떤 것으로 선언할 것인지 판단 기준은 객체마다 가지는 데이터라면 인스턴스, 그렇지 않다면 스테틱으로 선언한다.  
```java
public class sum {
    static double pi = 3.14;
    int num;
}
```
파이(3.14)에 임의의 정수를 더한다고 하면 파이는 고정된 값, 공용적인 데이터이기 때문에 스테틱으로 선언한다.  
정수는 선언을 할때 마다 바뀔 필요가 있으니 인스턴스로 선언한다.  
스테틱은 클래스 실행시에 메모리에 자동으로 로딩되기 때문에 객체생성 과정없이 바로 사용이 가능하다.  
```java
sum.pi;
```
스테틱은 객체 생성없이도 사용가능해야 하므로 생성자에서 초기화를 할 수 없고 스테틱 블록으로 초기화한다.  
```java
static {
    초기화 내용
}
```
# final
파이널은 초기값이 설정되면 이후에 바뀌지 않는다.  
필드 선언 시에 초기화 하거나 생성자에서 초기화 할 수 있다.  
# static final
불변의 값을 상수라 한다. 파이널은 한번 초기화하면 바뀌지 않는 값이기 때문에 파이널을 상수라 할 것 같지만 그렇지 않다.  
파이널은 변하지 않는 값은 맞지만 객체마다 생성되고 여러가지의 값을 가질 수 있기 떄문이다.  
상수는 불변이며 한가지의 값을 가져야한다.  
그렇기 때문에 객체마다 저장할 필요가 없는 공용성을 띠는 스테틱을 함께 써야한다.
