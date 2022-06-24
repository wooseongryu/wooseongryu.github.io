---
title: "변수와 메서드"
excerpt: "변수와 메서드의 관계"

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

date: 2022-06-24
last_modified_at: 2022-06-24
---
# 변수와 메서드
## 변수
변수는 한개의 데이터만 저장 가능하고,  
저장만 한다.
```java
int a = 10;
```
## 메서드
메서드는 동작을 한 후에 한개의 데이터만 만들어 내고, 리턴값을 저장한다.  
```java
//선언문
public int sum(int a, int b) {
    return a + b;
}
```
메서드는 동작 후 리턴값을 메서드의 이름(sum)에 저장한다.
```java
//호출문
int a = sum(1, 2); //결과 -> a = 3;
```
# 메서드의 매개변수 전달기법
## 값 전달 기법
```java
public static void main(String[] args) {
    int a = 10;
    int b = 20;
    //호출문
    int c = sum(a, b);    
}
//선언문
public static int sum(a, b) {
    return a + b;
}
```
a, b값을 직접 메소드로 넘겨주게 된다.
## 번지 전달 기법
```java
public static void main(Stirng[] args){
    int[] ary = {1, 2, 3};
    //호출문
    int c = sum(ary);
}
//선언문
public static int sum(int[] ary) {
    int total = 0;
    for (int i = 0; i < ary.lenth; i++) {
        total += ary[i];
    }
    return ary;
}
```
배열은 참조 타입이므로  
ary변수는 배열의 주소를 가지기 때문에   
메소드로 주소를 넘겨주는 것이다.