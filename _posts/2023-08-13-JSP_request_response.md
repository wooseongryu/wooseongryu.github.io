---
title: "request, response"
excerpt: "request, response, redirect, forward"

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
# request 객체
```html
<form action="test.jsp" method="get">
    <table border="1">
        <tr>
            <th>이름</th>
            <td><input type="text" name="name" required="required"></td>
        </tr>
        <tr>
            <th>취미</th>
            <td>
                <input type="checkbox" name="hobby" value="여행">여행
                <input type="checkbox" name="hobby" value="독서">독서
                <input type="checkbox" name="hobby" value="게임">게임
                <input type="checkbox" name="check_all">전체선택
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <input type="submit" value="전송">
            </td>
        </tr>
    </table>
</form>
```
- action 속성  
submit 동작 시 action속성에 지정된 페이지로 이동 요청을 수행한다. 이 때 폼 태그 내의 파라미터를 모두 request객체에 저장하여 함께 전송하게 된다.
- method 속성  
  - GET 방식  
  method="get"으로 작성한다. GET이 기본값이므로 생략할 수 있다. 전달되는 파라미터를 URL뒤에 붙여서 전송한다. 한글처리를 위해서는 문서의 문자 인코딩 방식을 UTF-8로 변경해야 한다. 이클립스의 설정에서 JSP파일 인코딩 설정을 변경하면 된다.
  - POST 방식  
  method="post"로 작성한다. 한글 처리를 위해서는 request객체의 setCharactorEncoding()메서드를 호출하여 "UTF-8"문자열을 파라미터를 전달하면 된다.


```java
<!-- test.jsp -->
<%
	request.setCharacterEncoding("UTF-8");	

	String strName = request.getParameter("name");
	out.print("이름 : " + strName + "<br>");

    String[] strHobbies = request.getParameterValues("hobby");
%>

<%=strName %>
```
전달받은 정보는 모두 request객체에 저장되어 있으므로 요청과 관련된 모든 정보는 request객체가 관리한다. 요청받은 request객체에 저장된 폼 파라미터 데이터를 가져오려면 ```request.getParameter("파라미터명");``` 를 사용하면 되며 String타입을 리턴한다. 복수 항목 파라미터를 가져오려면 ```request.getParameterValues("파라미터명");``` 를 사용하고 String[] 타입을 리턴한다. 반복문을 사용해 값을 가져오면 된다.
여기서 파라미터명은 폼 요소의 name속성값이다. 만약 전달받은 파라미터가 존재하지 않을 경우, 즉 파라미터명이 폼 요소의 name속성에 존재하지 않을 경우 null값이 리턴되고, 파라미터는 있으나 데이터가 없는 경우에는 널스트링이 리턴된다.

POST방식으로 폼 파라미터가 전송된 경우 한글이 깨질 수 있다. 그래서 반드시 데이터를 가져와 처리하는 위치에서 인코딩 방식을 변경해야 한다. request 객체의 setCharacterEncoding()메서드를 호출하여 "UTF-8"을 파라미터로 전달하면 된다. 이 때 반드시 파라미터 값을 가져오는 코드```request.getParameter();``` 보다 먼저 수행되어야 한다.

# 페이지 이동
```java
// JS코드를 사용한 페이지 이동 처리
<%if(id.equals("admin") && passwd.equals("1234")) {%>
    <script type="text/javascript">
        location.href = "#";
    </script>
<%} %>

// 자바 코드를 사용한 페이지 이동 처리
<%
if(id.equals("admin") && passwd.equals("1234")) {
    response.sendRedirect("#");
}
%>
```
내장 객체인 response객체의 sendRedirect()메서드를 사용하여 페이지를 이동할 수 있다. 이동 처리 자체를 서버에서 수행하는 것이 아니라 리다이렉트 신호를 response객체에 담아 클라이언트에게 전송하면 클라이언트가 해당 신호를 보고 다시 새 페이지로 이동 요청(리다이렉트)을 수행한다.
주의할 점은 자바 코드가 먼저 실행되므로 ```response.sendRedirect();``` 보다 이전에 HTML태그 및 JS코드를 작성해도 실행되지 못한다.

{% endraw %}

```java
<%
pageContext.forward("#");
%>
```
내장 객체인 pageContext객체의 forward메서드를 사용하여 동일한 페이지로 포워딩하는 방법도 있다.

## redirect와 forward
리다이렉트는 페이지 전환 주체가 클라이언트고 포워드는 서버다. 클라이언트가 주체가 되어 페이지를 전환하는 방식은 URL을 변경하는 방법밖에 없다. 서버가 전환 주체가 되면 URL을 변경하지 않고 내부적으로 다른 응답을 보내줄 수 있다.  
URL이 변경되는 방식을 리다이렉트 방식이라 하고 그렇지 않은 방식을 디스패치 방식이라 한다. 두 가지 방식 모두 지정한 페이지로 포워딩 시 제어권도 함께 넘어간다.  
디스패치 방식은 서버측에서 페이지 이동을 처리하므로 그 과정이 클라이언트에 노출되지 않으며 현재 실행중인 페이지와 호출될 페이지는 request, response객체를 공유한다.  
리다이렉트 방식은 호출한 페이지에서 request, response객체가 새롭게 생성된다.  
