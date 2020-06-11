---
title: servlet 상태관리

thumbnail: images/servlet/thumbnail.png
date: 2020-05-24 20:20:00

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

서블릿은 요청이 오면 응답을 주고 메모리에서 사라지기 때문에 서블릿들 간의 연결이 불가능하다. 

만약 기존의 데이터를 저장할 일이 생겼다고 하면 서블릿 스스로 저장할 수 있는 것은 아니다. 이것은 `ServletContext`로 해결할 수 있다.
<!-- more -->

## ServletContext
ServletContext는 웹 어플리케이션이 실행되면서 어플리케이션 전체의 자원이나 정보를 바인딩(Binding)하여 서블릿들이 공유하여 사용할 수 있는 클래스이다.

servletContext클래스는 톰캣 컨테이너 실행 시 각 웹 어플리케이션마다 한개의 객체를 생성한다.

ServletContext의 특징
- javax.servlet.ServletContext 로 정의 됨
- 서블릿과 컨테이너 간의 연동을 위해 사용
- 컨텍스트(웹 어플리케이션)마다 하나의 ServletContext가 생성
- 서블릿끼리 자원을 공유하는 데 사용
- 컨테이너 실행시 생성되고 종료시 소멸

## 자원을 저장하는 방법들
상태유지의 방법으로 application, session, cookie 등의 방법이 있다. 계산기 만드는 예제가 있는데 로직과 결과는 동일하나 각각 다른 객체를 활용한 것을 보자.

### application
- application은 그 값이 전역적으로 사용됨
- 프로세스간 값 공유가 가능

```java
@WebServlet("/app-calc")
public class AppCalcTest extends HttpServlet
{
	protected void service(HttpServletRequest req, HttpServletResponse res)
		throws IOException, ServletException
	{
		ServletContext application =  req.getServletContext();
		PrintWriter out = res.getWriter();
		
		String v_ = req.getParameter("value");
		String op_ = req.getParameter("op");
		
		int v = 0;
		if(!v_.equals("")) v = Integer.valueOf(v_);
		
		if(op_.equals("="))
		{
			int x = (Integer)application.getAttribute("value");
			int y = v;
					
			String operator = (String)application.getAttribute("op");
			if(operator.equals("+"))
				out.println(x + y);
			else if(operator.equals("-"))
				out.println(x - y);
				
			
		}else
		{
			application.setAttribute("value", v);
			application.setAttribute("op", op_);
		}
		
	}
}
```

### session
- session은 해당 사용자 기준으로 값이 사용됨

```java
@WebServlet("/session-calc")
public class SessionCalcTest extends HttpServlet
{
	protected void service(HttpServletRequest req, HttpServletResponse res)
		throws IOException, ServletException
	{
		HttpSession session =  req.getSession();
		PrintWriter out = res.getWriter();
		
		String v_ = req.getParameter("value");
		String op_ = req.getParameter("op");
		
		int v = 0;
		if(!v_.equals("")) v = Integer.valueOf(v_);
		
		if(op_.equals("="))
		{
			int x = (Integer) session.getAttribute("value");
			int y = v;
					
			String operator = (String) session.getAttribute("op");
			if(operator.equals("+"))
				out.println(x + y);
			else if(operator.equals("-"))
				out.println(x - y);
				
		}else
		{
			session.setAttribute("value", v);
			session.setAttribute("op", op_);
		}
	}
}
```

### cookie
```java
@WebServlet("/cookie-calc")
public class CookieCalcTest extends HttpServlet
{
	protected void service(HttpServletRequest req, HttpServletResponse res)
		throws IOException, ServletException
	{
		Cookie[] cookies =  req.getCookies();
		
		PrintWriter out = res.getWriter();
		
		String v_ = req.getParameter("value");
		String op_ = req.getParameter("op");
		
		
		
		if(op_.equals("="))
		{
			int x = 0;
			int y = Integer.valueOf(v_);
			
			for(Cookie cookie : cookies)
			{
				if(cookie.getName().equals("value"))
				{
					x = Integer.valueOf(cookie.getValue());
					break;
				}
			}
			
			
			String op = "";
			for(Cookie cookie : cookies)
			{
				if(cookie.getName().equals("op"))
				{
					op = cookie.getValue();
					break;
				}
			}
			
			if(op.equals("+"))
				out.println(x + y);
			else if(op.equals("-"))
				out.println(x - y);
		}else
		{
			Cookie valueCookie = new Cookie("value", v_);
			Cookie opCookie = new Cookie("op", op_);
			valueCookie.setPath("/");
			opCookie.setPath("/");
			
			res.addCookie(valueCookie);
			res.addCookie(opCookie);
		}
	}
}
```

![image](https://gojaebeom.github.io/images/servlet/example03.png)