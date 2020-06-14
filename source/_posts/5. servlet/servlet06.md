---
title: Jsp 프로그래밍

thumbnail: images/servlet/thumbnail.png
date: 2020-05-24 22:20:00

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

**JSP** 란 `Java Server Pages` 의 약자이며 HTML 코드에 JAVA 코드를 넣어 동적웹페이지를 생성하는 웹어플리케이션 도구이다. 
<!-- more -->

jsp에서는 기본적인 html 코드에 자바 문법을 추가하여 문서 내용을 동적으로 관리할 수 있는데, `<% %>` <-- 처럼 생긴 코드블럭 내부에 자바 문법을 작성하면 된다. 

### 코드 블럭
다음 예제를 보고 코드블럭에 대한 설명을 보자.

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<%
	String name = "gojaebeom";
	int age = 26;
%>
<html>
<head>
<meta charset="UTF-8">
<title>example page</title>
</head>
<body>
	<p>제 이름은 <%= name %> 이고 나이는 <%= age  %> 입니다.
</body>
</html>
```

### 스크립트릿(Scriptlet)
`<% %>` 블럭 사이에 오는 코드이며 가장 기본이되는 코드블럭이다. 기본적인 자바 프로그래밍은 이곳에서 처리 할 수 있고, 다음에 다루는 블럭들의 조건에 맞으면 상황에 따라 바꿔 사용하면 된다.

### 지시자(Directives)
`<%@ %>` 블럭 사이에 오는 코드를 말한다. 주로 `page` 지시자를 사용한다.

`contentType`, `pageEncoding`등을 설정한다.
- contentType은 jsp 파일을 html 문서로 변환할 때 적용되는 인코딩이다.
- pageEncoding은 jsp 파일에 적용되는 인코딩이다.

page 지시자 대신 `import` 지시자도 사용될 수 있는데, 자바에서 사용하는 import와 같은 사용법 이다.

### 선언문(Declarations)
`<%! %>` 블럭 사이에 오는 코드이다. 보통 서블릿 클래스의 선언부(전역, 맴버)에 입력되는 내용이다.

`tip`
<sup>jsp는 jsp 컨테이너에 의해 최종적으론 servlet파일로 변환된다. 다음 글에서 이해 대해 다룰 예정이다.</sup>

### 표현식(Expression)
`<%= %>`태그 사이에 오는 코드이다. 출력할 내용은 이곳에 입력해야된다. 

## EL(Expression Language)
EL의 개념은 표현 언어를 이해하고 속성 값들을 편리하게 출력하기 위해 제공된 언어이다.

### 사용목적
<%= %> , out.println()과 같은 자바코드를 더 이상 사용하지 않고 좀더 간편하게 출력을 지원하기 위한 도구.

### 문법
- Attribute형식에서는 `${num}` 과 같이 사용.
- Parameter형식에서는 `${param.num}` 과 같이 사용.

<sup># 해당 글은 개인적인 공부 내용을 정리하는 것을 목적으로 하고있습니다.</sup>
<sup># 설명이 다소 부족하거나 중간 내용이 생략될 수 있습니다.</sup>
