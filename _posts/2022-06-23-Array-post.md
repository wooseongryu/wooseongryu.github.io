---
title: "변수와 배열"
excerpt: "변수와 배열의 관계"

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

date: 2022-06-23
last_modified_at: 2022-06-23
---
# 배열이란?
동일한 타입의 데이터를 여러 개 저장하기 위한 연속적인 메모리 구조.  
배열은 여러개의 변수를 만들기 용이하고 데이터 이동이 쉽다.  
또한 반복문을 사용하여 메모리 접근이 용이하지만  
class와는 달리 서로 다른 타입의 데이터를 저장할 수 가 없다.
# 변수와 배열
## 변수를 개별적으로 만드는 방법
```java
int a, b, c;
int a = 10;
int b = 20;
int c = 30;
```
변수를 일일이 선언해 줘야 한다.
## 변수를 연속적으로 만드는 방법
```java
int[] a;
a = new int[3];
a[0] = 10;
a[1] = 20;
a[2] = 30;
```
변수 a를 사용하면 배열내의 모든 값을 이동할 수 있고  
반복문을 사용하여 메모리의 접근이 용이해진다.
# 다차원 배열
```java
int[][] a;
a = new int[2][3];
a[0][0] = 1;
a[0][1] = 2;
a[0][2] = 3;
a[1][0] = 1;
a[1][1] = 2;
a[1][2] = 3;
```
위의 경우에는 2행 3열이다.  
```a.length```는 행의 길이(2)이고  
```a[i].length```는 열의 길이(3)이다.
## 가변길이 배열
```java
int[][] a;
a = new int[3][];
a[0] = new int[1];
a[1] = new int[3];
a[2] = new int[2];
```
행의 길이는 고정시켜 놓고  
각 행마다 열의 길이를 유동적으로 쓸 수가 있다.