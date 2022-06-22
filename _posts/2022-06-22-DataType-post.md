---
title: "변수, 자료형, 할당"
excerpt: "기본 요소들"

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

date: 2022-06-22
last_modified_at: 2022-06-22
---
# 변수란?  
변수(Variable)는 하나의 값을 저장할 수 있는 메모리 공간의 이름을 의미한다.  
# 자료형이란?  
변수는 크기와 어떤 종류의 데이터가 저장될지 지정해야 하는데  
그것을 자료형(Data Type)이라 한다.  
# 할당이란?  
변수에 값을 저장하는 것을 할당/대입(Assign)이라 한다.  
# 변수의 선언  
변수를 사용하기 위해선 변수를 선언해야 하는데  
```java
int a;
```  
위와 같이 자료형(int)와 변수의 이름(a)를 쓰면된다.  
변수를 선언하게 되면 메모리에 공간이 할당 되고  
위의 경우에는 int자료형으로 4byte만큼의 크기에 정수형태의 값을 저장할 수 있게된다.  
그리고 할당된 공간에 값을 넣으려면  
```java
a = 40;
```
대입연산자(=)를 사용하면 우측의 값을 좌측의 변수에 저장할 수 있다.  
# 자료형의 종류  
자료형은 기본 타입(primitive type)과 참조 타입(reference type)으로 나뉜다  
## 기본 타입
|종류|자료형|예시|
|------|---|---|
|정수|short(2byte), int(4byte), long(8byte)|short a = 7; &nbsp;&nbsp;int b = 7; &nbsp;&nbsp;long c = 7L;|
|실수|float(4byte), double(8byte)|float a = 1.2F; &nbsp;&nbsp;double b = 1.2;|
|문자|char(2byte)|char a = 'c';|
|논리|boolean(1byte)|boolean a = true; &nbsp;&nbsp;boolean b = false;|

long타입은 int의 저장크기를 넘어가는 값을 저장할 때는  
값 뒤에 'l'이나 'L'을 붙인다.  
```java
long a = 10;
long b = 100000000000000L;
```
실수는 기본적으로 double형으로 인식하기 때문에  
float사용시 값 뒤에 'f'또는 'F'를 붙인다.  
```java
float a = 12.3f;
```
## 참조 타입
참조 타입은 새롭게 만들어 사용하는 자료형인데  
이것을 만드는 도구를 class라고 한다.
```java
public class MemberDTO{
    public String name;
    public String address;
    public int age;
}
```
|종류|자료형|예시|
|-|-|-|
|회원|MemberDTO|MemberDTO a = "철수"; &nbsp;&nbsp;MemberDTO b = "서울"; &nbsp;&nbsp;MemberDTO c = 20;


