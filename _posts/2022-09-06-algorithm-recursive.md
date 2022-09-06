---
title: "재귀"
excerpt: "재귀, 팩토리얼, 피보나치"

categories:
    - 알고리즘
tags:
    - [알고리즘]

toc: true
toc_sticky: true

comments:
  provider: "utterances"
  utterances:
    theme: "github-light" # "github-dark"
    issue_term: "pathname"
    label: "comment" # Optional - must be existing label.

date: 2022-09-06
last_modified_at: 2022-09-06
---
# 재귀
재귀 함수는 자기 자신을 호출하는 함수다.  
재귀적으로 문제를 풀려면 같은 형태의 더 작은 문제를 푼다. 그리고 그 답을 이용해서 기존 문제를 푼다.  
base case와 recursive case를 생각해야 한다.  
# 팩토리얼
3! = 3 * 2 * 1  
2! = 2 * 1  
1! = 1  
예외 - 0! = 1  

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)
```

3!을 구하려면 2!를 구해야 하고 2!를 구하려면 1!을 구하고 1!을 구하려면 0!을 구해야한다. 0! 즉 n = 0인 경우 n! = 1, n > 0 인 경우 n! = (n - 1)! * n 이다.  

n = 0인 경우는 base case  
n > 0인 경우는 recursive case  

# 재귀함수와 반복문
재귀 함수 호출이 너무 많으면 call stack이 너무 많이 쌓여 프로그램이 중단될 수 있다.  
파이썬은 1000개 까지의 call stack을 허용한다.  
반복문보다 재귀를 썼을 때 코드가 더 깔끔하지만 재귀적으로 너무 많은 함수 호출을 한다면 반복문을 쓰는게 좋다.  

# 피보나치 수열
```python
def fib(n):
    if n < 3:
        return 1
    return fib(n - 1) + fib(n - 2)
```
피보나치1 = 1  
피보나치2 = 1  
피보나치3 = 2  
피보나치4 = 3  
피보나치5 = 5  

base case는 n = 1 or 2 음수는 제외해야 하니 n < 3  
피보나치5는 피보나치3과 4의 합이고 피보나치4는 피보나치3과 2의 합이다.  
recursive case는 fib(n - 1) + fib(n - 2)  


