---
title: "action tag"
excerpt: "forward, include"

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
# forward
```java
<%
int age = 25;
%>
<jsp:forward page="forwardPro2.jsp">
    <jsp:param name="paramValue1" value="forward 액션태그의 param 액션태그 데이터"/>
    <jsp:param name="paramValue2" value="<%=age %>"/>
</jsp:forward>
```
forward 액션태그로 포워딩 시 데이터를 추가하여 포워딩 수행이 가능하다. jsp:forward 액션태그 사이에 jsp:param 액션태그를 사용하여 데이터 추가가 가능하다. name 속성에 파라미터명, value 속성에 파라미터값을 지정한다. 자바 변수 데이터를 포함시켜야 할 경우 value 속성의 "" 사이에 표현식으로 포함시켜야 한다.  

POST 방식으로 전달받은 파라미터에 한글 데이터가 있을 경우 깨지는 현상이 발생하므로 요청 파라미터에 대한 한글 인코딩 방식 변경 처리가 필요하다. ```	request.setCharacterEncoding("UTF-8");``` 이 코드를 작성해야 하는데 이 때 jsp:forward 액션태그를 통한 dispatch방식 포워딩 시 주의해야할 사항이있다. request 객체를 전달받은 시점에 이미 한글 처리가 완료되어 있어야 포워딩 된 페이지에서 한글이 깨지지 않는다는 것이다. 그래서 위의 코드에서 forwardPro2.jsp로 포워딩을 하기 전에 아래와 같이 한글처리를 해야만 한다.
```java
<%
request.setCharacterEncoding("UTF-8");
int age = 25;
%>
<jsp:forward page="forwardPro2.jsp">
    <jsp:param name="paramValue1" value="forward 액션태그의 param 액션태그 데이터"/>
    <jsp:param name="paramValue2" value="<%=age %>"/>
</jsp:forward>
```

만약 이렇게 하지 않고 포워딩된 페이지에서 ```request.setCharacterEncoding("UTF-8");``` 를 작성하여 한글 처리를 하려고 하면 한글이 다 깨질것이다.
```java
// forwardPro2.jsp

// 아래의 한글 처리는 무의미한 코드
// 반드시 이전 페이지에서 처리해야 한다.
// request.setCharacterEncoding("UTF-8");

String paramValue1 = request.getParameter("paramValue1");
String paramValue2 = request.getParameter("paramValue2");
```
액션태그로 전달받은 데이터를 가져오는 것은 기존과 동일하게 작성하면 된다.

# include
```java
<body>
	<h1>includeForm.jsp</h1>
	<hr>

	<jsp:include page="includePro.jsp">
		<jsp:param name="paramValue" value="parameter value"/>
	</jsp:include>

	<hr>
	<h1>includeForm.jsp</h1>
</body>
```
jsp:include를 사용해 다른 페이지를 현재 페이지에 포함시킬 수 있다. 이 때 param액션태그로 파라미터를 포함하여 전달할 수 있으며 포함되는 페이지에서 해당 파라미터에 접근이 가능하다.  
```java
<body>
	<h1>includePro.jsp</h1>
	<h3>include 액션태그에 의해 포함되는 페이지입니다.</h3>
	<%
	String paramValue = request.getParameter("paramValue");
	%>
	<h3>전달받은 파라미터값 : <%=paramValue %></h3>
</body>
```
includeForm.jsp 페이지가 현재 페이지를 포함할 때 param 액션태그로 전달한 파라미터를 현재 페이지에서 가져다 사용이 가능하다.  

{% endraw %}
