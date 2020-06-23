---
title: jsp 프로젝트 만들기 - 시작

thumbnail: images/servlet/thumbnail.png
date: 2020-06-08 20:20:00

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
  - type: category
    position: right
sidebar:
  right:
    sticky: true
---

본격적으로 jsp를 이용한 servlet 프로젝트를 만들어보겠다. jsp와 servlet의 활용 목적이 주된 내용이기 html/css 는 가급적 손대지 않고 비즈니스 로직에 집중하도록 하겠다.
<!-- more -->

## 새 프로젝트 생성
이클립스를 사용하여 `dynamic web project`를 생성해주자. IDE없이 예제를 진행하려고 했으나, 초기 설정부터 설명해야할게 너무 많아 기본적인 설정은 이클립스에게 맡기고 프로젝트만 바로 구현하도록 할것이다.

1. dynimic web project 생성(이름은 상관 없으나 jsp-project 와 같은 명칭을 사용)
2. 기본 폴더 구조를 확인
  1. 자바를 사용할 코드는 `resource/src` 하위에 생성 및 사용
  2. client에 보여줄 문서 html, jsp 등은 `WebContent` 하위에 생성 및 사용
3. 화면을 보일 문서는 홈, 목록, 상세보기 페이지를 가지고 설명
  1. `WebContent` 하위에 index.jsp 파일 생성
  2. `WebContent` 하위에 lists폴더를 만들고 폴더 내부에 board-list.jsp 파일 생성
  3. `WebContent` 하위에 details폴더를 만들고 폴더 내부에 board-detail.jsp 파일 생성

파일들의 소스코드는 다음과 같다.

### index.jsp
```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<nav>
		<a href="/">홈</a>
		<a href="/lists/board-list.jsp">게시글 목록</a>
	</nav>
	<hr/>
	<h1>메인 페이지</h1>
</body>
</html>
```

### board-list.jsp
```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<nav>
		<a href="/">홈</a>
		<a href="/lists/board-list.jsp">게시글 목록</a>
	</nav>
	<hr/>
	<h1>게시글 목록</h1>
	
	<form action="">
		<select name="">
			<option value="">제목</option>
			<option value="">작성자</option>
		</select>
		<input name=""/>
		<button type="submit">검색</button>
	</form>
	<hr/>
	
	<table>
		<tr>
			<th>게시 번호</th>
			<th>제목</th>
			<th>작성자</th>
			<th>작성일</th>
		</tr>
		<tr>
			<td>1</td>
			<td>테스트 제목</td>
			<td>관리자</td>
			<td>yyyy:mm:dd</td>
		</tr>
		<tr>
			<td>2</td>
			<td>테스트 제목</td>
			<td>관리자</td>
			<td>yyyy:mm:dd</td>
		</tr>
	</table>
</body>
</html>
```

### board-detail.jsp
```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<nav>
		<a href="/">홈</a>
		<a href="/lists/board-list.jsp">게시글 목록</a>
	</nav>
	<hr/>
	<h1>제목</h1>
	<p>작성자: / 작성일: / 조회수:  </p>
	<p>첨부 파일: </p>
	<div style="width:500px; height:300px; border:2px dotted gray; padding:10px;">
		내용 입력
	</div>
	<hr/>
	<a href="">다음 글</a>
	<span style="font-weight:bold">/</span>
	<a href="">이전 글</a>
</body>
</html>
```

## 브라우저에서 화면 보기
위의 기본 문서들을 작성했다면 웹에서 잘 작동하는지 실행해보자. 실행하기 이전에 기본 실행경로를 `/`로 변경하자. (변경하지 않으면 `http://localhost:8080/프로젝트명/` 과 같이 주소가 잡힌다 )
1. 만든 프로젝트에 마우스를 올려 우클릭 (또는 alt + enter)
2. 가장 하단의 `properties` 를 클릭
3. 매뉴의 `web project setting` 에서 `context root`를 `/`로 변경하고 저장

이후 톰캣을 이용하여 프로젝트를 웹에 띄운다. 위의 매뉴를 사용하거나 직접 주소 창에 주소를 입력하여 확인해보자.

http://localhost:8080
![index.jsp](https://gojaebeom.github.io//images/servlet/example07.PNG)

http://localhost:8080/lists/board-list.jsp
![board-list.jsp](https://gojaebeom.github.io//images/servlet/example06.PNG)

http://localhost:8080/details/board-detail.jsp
![board-detail.jsp](https://gojaebeom.github.io//images/servlet/example05.PNG)

위의 문서들은 실제 기능은 구현되지 않았다. 다음 글에서 DB를 생성하여 `JDBC`를 사용해 프로젝트와 DB를 연동해보고 DB의 데이터를 client에 보내주는 작업을 해보자. 이어서 jsp의 스파게티 코드와 그로 인해 나온 mvc1, mvc2 패턴을 알아보겠다.

<sup># 해당 글은 개인적인 공부 내용을 정리하는 것을 목적으로 하고있습니다.</sup>
<sup># 설명이 다소 부족하거나 중간 내용이 생략될 수 있습니다.</sup>