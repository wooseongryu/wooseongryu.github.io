---
title: "session"
excerpt: "세션, 유지/제거 조건, 생성, 삭제"

categories:
    - JSP
tags:
    - [JSP]

toc: true
toc_sticky: true

comments:
  provider: "utterances"
  utterances:
    theme: "github-light" # "github-dark"
    issue_term: "pathname"
    label: "comment" # Optional - must be existing label.

date: 2023-08-13
last_modified_at: 2023-08-13
---
{% raw %}
# 세션
클라이언트와 서버는 Stateless방식으로 통신을 한다. 그래서 로그인을 한 사용자가 페이지를 넘어갈 때 마다 인증을 해야하는 문제가 생긴다. 이것을 해결하기 위해 세션을 사용한다. 세션은 서버가 인증이 된 클라이언트에게 발급해주고 클라이언트는 이를 요청 정보에 담아 보내게 된다.  
세션은 사용자의 정보를 서버에 저장하고 매 응답마다 session id만 보내기 때문에 네트워크 부하를 줄일 수 있지만 서버의 자원을 소모한다.

# 세션 객체
HttpSession 타입을 사용하여 관리한다. 요청페이지에서 응답페이지 까지만 정보가 유지되는 request 객체와 달리 session 객체는 로그인 후 세션ID 정보를 기억하여 페이지 이동시에도 로그인 상태가 유지된다.  
서버에 접속시 기본적으로 해당 클라이언트에 해당하는 기억 장소(세션)가 생성되고 자동으로 세션ID값이 부여된다.  

## 세션 유지, 제거 조건
1. 세션 유지 시간(maxInactiveInterval) 값 만큼 세션 정보가 유지된다. 유지 시간 동안 아무런 동작이 없을 경우 유지 시간이 만료될 때 세션 정보가 자동으로 제거된다. 기본 세션 유지 시간은 30분이며 서버와 통신을 수행하면 세션 유지 시간이 다시 초기화 된다.  
2. 세션 유지 시간과 관계없이 invalidate()메서드 호출 시 세션이 초기화 된다.  
3. 해당 브라우저의 모든 창을 닫았을 경우 세션이 초기화 된다.  

```java
// 세션 유지시간(maxInaciveInterval) 값 확인
<%=session.getMaxInactiveInterval() %>

// 세션 유지시간을 10초로 변경
<%session.setMaxInactiveInterval(10); %>

// 새 세션 여부
<%=session.isNew() %>

// 세션 ID
<%=session.getId() %>

// 세션 생성 시각
<%=new Date(session.getCreationTime()) %>

// 세션 강제 초기화(= 세션 객체를 제거)
<%session.invalidate(); %>
//세션 정보 초기화 후에는 초기화 된 페이지에서는 더 이상 세션 객체 접근 불가능
// <%=session.isNew() %> 에러 발생.
// 새로운 세션 생성 전까지 접근 불가하며 다른 페이지로 이동하는 등의
// 작업을 수행하여 서버와 새로운 통신 수행 시 새 세션 객체가 생성된다.
```
# 세션값 생성
session객체의 setAttribute()메서드를 호출하여 속성값을 저장할 수 있다. request, application객체도 속성 데이터 저장 방법이 동일하다.  
```session.setAttribute("속성명", 속성값);``` 을 사용한다. 첫번째 파라미터는 저장할 데이터를 가리키는 이름이며 객체의 변수명과 동일하다고 보면 된다. 두번째 파라미터는 세션 객체에 저장할 데이터이며 타입은 무관하다. 저장된 데이터는 속성명으로 접근이 가능하다. 모든 데이터 타입의 데이터가 Object타입으로 업캐스팅 되어 저장된다.  
```java
<%
//String에서 Object로 업캐스팅 발생
session.setAttribute("sessionValue1", "첫번째 세션값");
//int에서 Object로 업캐스팅 발생
session.setAttribute("sessionValue2", 1);
%>
```

session객체로부터 저장된 데이터를 꺼낼려면 session객체의 getAttribute()메서드를 사용한다. 파라미터는 저장된 데이터를 가리키는 이름(속성명)을 문자열로 전달하며 Object타입을 리턴한다.  
```java
<%
session.getAttribute("sessionValue1");
session.getAttribute("sessionValue2");
%>
```
만약 속성명에 해당하는 값이 존재하지 않을 경우 null값이 리턴된다.

```java
String value1 = (String)session.getAttribute("sessionValue1");
```
여기서 가져온 데이터를 저장하려면 형변환을 해주자.  
확실하게 하려면 instanceof연산자를 통해 변환 가능 여부를 확인하는 것이 좋다.  

# 세션값 삭제
세션 객체에 저장된 특정 속성을 삭제하려면 ```session.removeAttribute("속성명")```메서드를 사용한다.
```java
<%
session.removeAttribute("sessionValue1");
%>
```

만약 세션 내의 모든 데이터를 제거(세션 초기화)하려면 ```session.invalidate()```를 사용한다. 세션 객체 자체를 제거하는 것과 유사하며 특정 속성이 아닌 전체를 제거하므로 파라미터가 불필요하다.

```java
<%
session.invalidate();
%>
```

{% endraw %}