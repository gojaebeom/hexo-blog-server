---
title: Jsp -> Servlet 변환

thumbnail: images/servlet/thumbnail.png
date: 2020-05-25 20:20:00

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

웹 어플리케이션에 배포된 jsp 페이지는 최초 클라이언트 요청이 들어올 때 servlet으로 변환된다.
<!-- more -->

변환되는 내용은 다음과 같다.
- `Scriptlet <% %>` 에 작성된 소스는 변환된 Servlet의 `service()` 메서드 안에 들어간다.
- **표현식**은 변환된 servlet의 `service()` 메서드 안에서 `out.print()` 으로 변환된다.
- **선언문**에 작성된 소스는 변환된 servlet의 맴버 영역에 생성 (변수 선언시 맴버변수, 메서드 선언시 맴버매서드)
- 일반 HTML 태그들은 변환된 servlet의 `service()` 메서드 안에 `out.write()` 메서드로 변환된다.
- page 디렉티브의 속성값들은 servlet으로 변환시 참고할 정보로 활용된다.

위의 문장으로는 이해하기 힘들 수도 있다. 다음 예제를 보자.

### jsp -> servlet 변환 예제
```jsp
<!-- index.jsp -->
<!-- 일반 html 코드 : out.write() 내부에 작성  -->
<%@ page language="java" contentType="text/html; charset=UTF-8"
pageEncoding="UTF-8"%>
<!DOCTYPE html>
<%! //선언문 : class 전역에 생성
  String name = "gojaebeom";
  int age = 26;
%>
<html>
  <head>
    <meta charset="UTF-8">
    <title>example page</title>
  </head>
  <body>
    <!-- 표현식: out.println() 내부에서 사용 -->
    <p>제 이름은 <%= name %> 이고 나이는 <%= age  %> 입니다.
  </body>
</html>
```

위와 같은 jsp 파일을 만들었다고 가정하면 index.jsp 파일은 jsp 컨테이너에 의해 index_jsp.java 파일로 변환된다. 변환되는 부분이 많아 중간 중간 생략하여 보이겠다.

```java
//index_jsp.java
public final class index_jsp extends org.apache.jasper.runtime.HttpJspBase
    implements org.apache.jasper.runtime.JspSourceDependent,
                 org.apache.jasper.runtime.JspSourceImports {

  //선언문의 내용은 class의 전역에서 사용
  String name = "gojaebeom";
  int age = 26;

  public void _jspService(final javax.servlet.http.HttpServletRequest request, final javax.servlet.http.HttpServletResponse response)
      throws java.io.IOException, javax.servlet.ServletException {

    //jsp의 내장 객체들
    final javax.servlet.jsp.PageContext pageContext;
    javax.servlet.http.HttpSession session = null;
    final javax.servlet.ServletContext application;
    final javax.servlet.ServletConfig config;
    javax.servlet.jsp.JspWriter out = null;
    final java.lang.Object page = this;
    javax.servlet.jsp.JspWriter _jspx_out = null;
    javax.servlet.jsp.PageContext _jspx_page_context = null;

    //page 디렉티브의 속성값
    response.setContentType("text/html; charset=UTF-8");

    //html 태그들은 out.write로 사용
    out.write("\r\n");
    out.write("<!DOCTYPE html>\r\n");
    out.write("\r\n");
    out.write("<html>\r\n");
    out.write("<head>\r\n");
    out.write("<meta charset=\"UTF-8\">\r\n");
    out.write("<title>example page</title>\r\n");
    out.write("</head>\r\n");
    out.write("<body>\r\n");
    out.write("\t<p>제 이름은 ");

    //표현식은 out.print로 사용
    out.print( name );
    out.write(" 이고 나이는 ");

    //표현식은 out.print로 사용
    out.print( age  );
    out.write(" 입니다.\r\n");
    out.write("</body>\r\n");
    out.write("</html>");
  }
}
```

원래 더 많은 소스코드들이 포함되어 있지만 설명을 위해 부분부분 제거하였다. 위 `index_jsp.java` 예제를 보면 `index_jsp` 클래스가 `org.apache.jasper.runtime.HttpJspBase` 를 상속하고 있는데 `HttpJspBase`는 `HttpServlet`을 상속하고 있는 클래스이므로 서블릿이라고 할 수 있다.

`Tip`
이클립스 기준으로 jsp 파일을 만들면 사용되는 것은 개발 프로젝트 폴더 내부의 jsp 파일이 아니다. 
이클립스 내부의 톰캣은 톰캣의 사본을 만들어 프로젝트들을 관리하게 되는데, 기본 작업폴더에 `metadata\.plugins\org.eclipse.wst.server.core` 폴더에 `tmp0` 또는 `tmp1~` 의 폴더 내부의 `work` 폴더가 있다. `work`가 바로 servlet 파일로 변환된 jsp 들을 관리 하는 폴더이다. 우리가 개발을 하며 봐온 jsp 파일은 바로 `work` 하위 디렉토리에 있는 servlet 파일이다.

## servlet 변환 과정
![image](https://gojaebeom.github.io/images/servlet/example04.png)

<sup># 해당 글은 개인적인 공부 내용을 정리하는 것을 목적으로 하고있습니다.</sup>
<sup># 설명이 다소 부족하거나 중간 내용이 생략될 수 있습니다.</sup>
