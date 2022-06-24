---
title: "클래스 실행절차"
excerpt: "JVM이 클래스를 실행하는 절차"

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
# jvm의 클래스 실행 절차
1. 해당 클래스를 현재 디렉토리에서 찾는다.  

2. 클래스 내부에 static이 있는 메서드를 메서드 영역의 메모리로 로딩한다.  
 - 메서드 영역은 static zone과 non-static zone으로 나뉘는데,  
 static이 있는 메서드는 프로그램 실행시 자동으로 static zone에 로딩된다. 

3. static zone에서 메인 메소드를 찾아 실행한다.  
 - 메인 메서드를 static으로 하지 않으면 프로그램 실행시 메서드 영역에  
 로딩이 되지 않아 프로그램을 실행할 수 가 없으니  
 메인 메서드는 반드시 static으로 한다.  
 - 메인 메서드가 호출되면 메인 메서드의 호출정보가 스택 영역에 저장된다.  
 - 실행이 끝난 메서드는 스택에서 사라진다.  

 4. 스택 영역이 비었으면 프로그램이 종료된 것이다.  
 ```java
 public class Memory {
    public static void main(String[] args) {
        int a = 1;
        int b = 2;
        int c = sum(a, b);
        System.out.println(c);
    }
    public static int sum(int x, int y) {
        return x + y;
    }
 }
 ```
 Memory 클래스를 찾아 static이 있는 메서드(main 과 sum)를 메서드 영역에 로딩한다.  
 main을 실행하면 a, b, c변수가 스택 영역에 들어가고 sum을 실행한다.  
 sum의 x, y변수가 스택 영역에 들어가고 값을 리턴후에 스택 영역에서 사라진다.  
 다시 main으로 돌아와서 리턴 값을 출력후 스택 영역에서 사라지고 프로그램이 종료된다.  
 
# static이 없는 메서드
```java
public class Memory {
   public static void main(String[] args) {
       int a = 1;
       int b = 2;
       Memory z = new Memory();
       int c = z.sum(a, b);
       System.out.println(c);
   }
   public int sum(int x, int y) {
       return x + y;
   }
}
```
 static이 있는 main메서드는 메서드 영역에 자동으로 로딩이 되지만,  
 sum메서드는 로딩이 되지 않는다.  
 sum메서드를 사용하기 위해선 로딩을 시켜줘야 하는데,  
 ```java
 Memory z = new Memory();
 ```
를 통해서 힙 영역에 객체를 생성하면  
스택 영역의 z변수는 객체를 가리키고  
그 객체가 non-static zone에 로딩된 sum메서드를 가리킨다.

순서대로 보자면  
main메서드가 메서드 영역에 로딩되고,  
main을 실행해서 a, b, c, z변수가 스택 영역에 들어간다.  
```Memory z = new Memory();```로 힙 영역에 객체를 생성하고 z변수가 가리키게 한다.  
객체는 non-static zone에 로딩된 sum메서드를 가리키고  
sum을 실행해서 x, y변수가 스택 영역에 들어가고 값을 리턴한다.  
main에서는 리턴받은 값을 c변수에 넣고 출력 후 종료된다.
