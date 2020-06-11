---
title: 한글 인코딩

thumbnail: images/servlet/thumbnail.png
date: 2020-05-23 20:20:00

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

servlet 클래스에서 한글을 출력하면 한글이 깨지는 것을 볼 수 있다. 해당 문제점은 다음과 같이 해결할 수 있다.
```java
public class HelloServlet extends HttpServlet {

	@Override
	protected void service(HttpServletRequest req, HttpServletResponse res) 
			throws ServletException, IOException 
	{	
    //출력 데이터의 인코딩을 UTF-8로 설정
		res.setCharacterEncoding("UTF-8");
		res.setContentType("text/html; charset=UTF-8");
		
		PrintWriter out = res.getWriter();
		
		out.println(data);
	}
}
```
<!-- more -->

하지만 Servlet 클래스는 하나만 있는 것이 아니다. 프로젝트의 규모가 커질 수록 Servlet 클래스를 여러개 생성하게 되는데, 그 때 마다 위와 같이 인코딩설정을 해주는 것은 같은 코드를 반복하여 사용하게 되는 것 이다.

## 필터(Filter)
클라이언트에서 온 요청은 servlet이 받기 이전에 `Filter`라고 하는 클래스에서 먼저 중간 처리를 할 수 있다. 다음 같은 클래스를 생성해보자.

```java
public class CharacterEncodingFilter implements Filter 
{
	@Override
	public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain)
			throws IOException, ServletException 
	{
		
		req.setCharacterEncoding("UTF-8");
		
		res.setCharacterEncoding("UTF-8");
		res.setContentType("text/html; charset=UTF-8");

		chain.doFilter(req, res);
	}
}
```
위 클래스에 대한 설명은 다음과 같다.
- 클래스명은 사용자가 임의로 지정
- Filter 인터페이스를 구현 받음
- doFilter 메소드를 오버라이딩하여 해당 로직을 작성

물론 위의 필터 역시 web.xml에 filter 속성으로 등록해주어야 한다.

## Filter Mapping
필터 클래스를 톰캣에서 읽기 위해 매핑해줄 수 있는데 servlet과 마찬가지로 web.xml에 기술하는 방법과 어노테이션을 이용한 방법이 있다.

### web.xml에서 등록
```xml
<filter>
  <filter-name>characterEncodingFilter</filter-name>
  <filter-class>com.example.web.filter.CharacterEncodingFilter</filter-class>
</filter>
<filter-mapping>
  <filter-name>characterEncodingFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>
```

### annotaction(@) 등록
```java
@WebFilter("/*")
public class CharacterEncodingFilter implements Filter 
{
  ...
}
```
<sup>url을 위와 같이 /*를 사용하면 모든 주소 요청에 대한 처리를 하겠다는 것</sup>