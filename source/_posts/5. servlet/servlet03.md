---
title: Servlet 다루기

thumbnail: images/servlet/thumbnail.png
date: 2020-05-22 20:20:00

tags: 
- servlet
- jsp

category:
- 자바 튜토리얼
- 2. servlet & jsp

#카탈로그 생성 및 위치
toc: true
widgets:
  - type: toc
    position: right
  - type: bgm
    position: right
sidebar:
  right:
    sticky: true
---

<sup>해당 글은 개인적인 공부 내용을 정리하는 것을 목적으로 하고있습니다. 설명이 다소 부족하거나 중간 내용이 생략될 수 있습니다.</sup>

- 기존의 html 문서만으로는 동적인 내용을 전달할 수 없다. --> `WAS : web application server` 에서 동작하는 프로그래밍 언어를 사용하면 가능하다.
- 그렇기에 해당 Java에서 제공하는 servlet 클래스를 활용하여 동적인 웹 페이지를 사용자에게 보여줄 수 있다.
<!-- more -->

## 서블릿 만들기
이클립스에서 제공하는 `Dynamic web project` 를 생성하면 쉽게 servlet 프로그램을 구현할 수 있다.
- src 하위에 자바 클래스 파일을 생성한다.(이름은 상관 없다)
- 만든 클래스에게 HttpServlet 클래스를 상속받게 한다.
- 구현된 메소드들 중 `service`, `doGet`, `doPost` 등이 있는데 먼저 `service` 메소드를 오버라이드해보자.

```java
import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class HelloServlet extends HttpServlet {

	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) 
			throws ServletException, IOException 
	{
		PrintWriter out = response.getWriter();
		
		out.println("hello servlet");
	}
}
```
- HttpServlet 클래스를 상속 받아 servlet 기능을 사용할 수 있음
- service 메소드는 입력도구 `HttpServletRequest`와 출력도구 `HttpServletResponse`을 매개변수로 받아 활용 가능
- 위의 코드는 출력도구 `response`를 사용하여 사용자에게 `hello servlet` 문구를 응답하는 내용

## 서블릿 mapping
위의 클래스 파일은 바로 사용할 수 없다. 톰캣에게 web.xml의 내용을 통해 servlet 클래스라는 것을 명시해 주어야 한다. 명시하는 방법은 2가지가 있다.

### web.xml 에서 설정해주기
- 해당 프로젝트의 WebContent\WEB-INF 경로에 web.xml 파일 생성
- 다음 내용 적용

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
  version="4.0"
  metadata-complete="true">

  <display-name>Welcome to Tomcat</display-name>
  <description>
     Welcome to Tomcat
  </description>
  
  <!-- servlet mapping! -->
  <servlet>
  	<servlet-name>hello</servlet-name>
  	<servlet-class>HelloServlet</servlet-class>
  </servlet>
  <servlet-mapping>
  	 <servlet-name>hello</servlet-name>
  	 <url-pattern>/hello</url-pattern>
  </servlet-mapping>

</web-app>
```

하단의 `<!-- servlet mapping! -->` 부분만 이해해보자.
- 먼저 servlet 클래스를 명시해주는데 src 폴더의 하위 경로를 기준으로 해당 Servlet 클래스명 입력
    - 사실 src 폴더의 경로는 아니다. 프로젝트의 최상위 디렉토리에 가보면 `build`라는 폴더가 있는데 해당 폴더의 .class 파일을 찾는 것 같다.
- 그리고 servlet이 이름이 hello 인 servlet가 주소(url) 요청이 '프로젝트 주소/hello' 로 오면 해당 서블릿 클래스를 실행하라는 내용이다. 

### annotaction(@) 사용
- 서블릿 3.0 버전 이상에서 사용가능하다.
- web.xml의 servlet과 servlet-mapping 태그가 필요 없다. 
- 대신 web.xml의 root element인 metadata-complete의 값을 false로 바꿔주어야 함

```xml
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
  version="4.0"
  metadata-complete="false"> <!-- 이부분 -->
```
- 그리고 해당 서블릿 클래스 파일에 어노테이션을 작성

```java
@WebServlet("/hello") // <-- 다음과 같이 명시
public class HelloServlet extends HttpServlet {

	@Override
	protected void service(HttpServletRequest req, HttpServletResponse res) 
			throws ServletException, IOException 
	{
		PrintWriter out = res.getWriter();
		
		out.println("hello servlet");
	}
}
```
위와 같이 작성하면 web.xml에서 설정한 것과 같이 작동한다.

위 설정들이 완료 되었다면 이클립스에서 톰캣에 해당프로젝트를 올려 실행하면 잘 작동할 것이다.