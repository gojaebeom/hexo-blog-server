---
title: jsp 프로젝트 만들기 - DB 연결

thumbnail: images/servlet/thumbnail.png
date: 2020-06-09 20:20:00

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

`JDBC`를 이용하여 자바 웹 프로젝트에 `mysql`을 연동하여 프로그램을 이어 나가겠다. JDBC는 자바에서 데이터베이스에 접속할 수 있도록 하는 자바 API이다. JDBC는 데이터베이스에서 자료를 쿼리하거나 업데이트하는 방법을 제공한다.
<!-- more -->

## mysql table 생성
이번 프로젝트는 mysql을 이용할 예정이다. 먼저 mysql table을 다음과 같이 생성해 주자.

```sql
CREATE TABLE board (
  `id` INT NOT NULL AUTO_INCREMENT,
  `title` VARCHAR(45) NOT NULL,
  `writer_id` VARCHAR(45) NOT NULL,
  `content` TEXT NOT NULL,
  `hit` INT NULL,
  `created_at` DATETIME NOT NULL,
  `files` VARCHAR(100) NULL,
  PRIMARY KEY (`id`));
```

## JDBC 사용하기
만들어 놓은 자바 웹 프로젝트에 JDBC 를 사용하여 Mysql 데이터베이스를 연동할 것다. jdbc는 jdk를 설치하면 기본적으로 java.sql 하위에 내장되어 있지만, 사용자에 따라 오라클 또는 mysql 과 같은 다른 DB를 사용할 수 있기 때문에 연결할 틀만 제공해준다. 따라서 사용자는 사용할 DB의 드라이버를 다운 받아 사용해야 한다.

## mysql connector 설치
라이브러리를 사용하기 위해선 해당 jar파일을 프로젝트에 추가해주어야 한다. 이전 자바 프로젝트와는 달리 servlet 프로젝트는 `WEB-INF/lib` 하위 경로에 파일을 추가해 주어야한다. 

우리가 웹 프로젝트를 완성하면 실제 사용할 서버에 배포를 해주어야 하는데 해당 라이브러리를 같이 가져가서 사용하게 할 목적이다.

- https://mvnrepository.com/artifact/mysql/mysql-connector-java/8.0.18 해당 주소에 접속한다.
- file에 jar파일을 다운받는다.
- 프로젝트의 `/WEB-INF/lib` 하위에 해당 jar 파일을 넣어준다. (만약 .zip파일로 압축 되어 있다면 내부의 mysql-connector-java-8.0.20.jar 과 같은 파일만 빼서 넣어주어야 함)

## 프로젝트에 DB 연동
이전에 만들어논 3개의 페이지 index, board-list, board-detail 문서중 board-detail.jsp 를 예제로 db를 연동하여 데이터를 웹에 출력해보자.

board-detail.jsp 문서의 제일 상단에 스크랩트립 `<% %>`을 사용하여 다음 내용을 넣어보자.
```java

//getConnection에 필요한 파라미터 각 mysql의 url, 사용자 아이디, 비밀번호를 받는다.
String url = "jdbc:mysql://localhost:3306?characterEncoding=UTF-8&serverTimezone=UTC";
String id = "root";
String pw = "woqja5164!";

//라이브러리로 받은 mysql connector의 Driver 클래스를 JVM에게 알려준다. 메모리에 올라감
Class.forName("com.mysql.cj.jdbc.Driver");

//java.sql.DriverManager 를 사용하여 mysql에 대한 정보를 주고 Connection 이 참조
Connection con = DriverManager.getConnection(url,id,pw);
```
자바 파일에 작성했다면 `Class.forName`은 `ClassNotFoundException`예외를,  `DriverManager.getConnection`는 `SQLException` 예외를 처리 해주어야 하지만 스크랩트릿 내부에서의 코드는 예외 처리가 필요 없다. 위 코드를 입력 후 http://localhost:8080/details/board-detail.jsp 에 접속시 화면이 잘 뜬다면 성공적으로 연결한 것이다.

## DB의 데이터를 웹에 보여주기
board-detail.jsp를 다음과 같이 수정한다.
```jsp
<%@page import="java.util.Date"%>
	그 밖의 import... 
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
String url = "jdbc:mysql://localhost:3306?characterEncoding=UTF-8&serverTimezone=UTC";
String id = "root";
String pw = "woqja5164!";

String sql = "SELECT * FROM example01.board where id = 1";
	
Class.forName("com.mysql.cj.jdbc.Driver");
Connection con = DriverManager.getConnection(url,id,pw);
Statement state = con.createStatement();
ResultSet result = state.executeQuery(sql);

result.next();
%>
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
	<h1>제목 : <%= result.getString("title") %> </h1>
	<p>작성자:<%= result.getString("writer_id") %> / 작성일: <%= result.getDate("created_at") %>/ 조회수: <%= result.getInt("hit") %>  </p>
	<p>첨부 파일:<%= result.getString("files") %> </p>
	<div style="width:500px; height:300px; border:2px dotted gray; padding:10px;">
		<%= result.getString("content") %>
	</div>
	<hr/>
	<a href="">다음 글</a>
	<span style="font-weight:bold">/</span>
	<a href="">이전 글</a>
</body>
</html>
<%
con.close();
state.close();
result.close();
%>
```
http://localhost:8080/details/board-detail.jsp
위 문서를 브라우저에서 실행하면 다음과 같은 화면을 볼 수 있다.
![board-detail.jsp](https://gojaebeom.github.io//images/servlet/example08.PNG)

위의 코드를 보면 java 코드를 담기 위한 스크립트릿과 html이 뒤엉켜있는 것을 볼 수 있다. 위와 같은 코드를 스파게티 코드라고 한다. 혼자 프로젝트를 만들때는 괜찮겠지만, 기업에서의 협업, 또는 프로젝트의 규모가 커질 수 록 관리하기 힘든 점이 있다. 그래서 MVC1이라는 패턴이 나왔는데 다음 글에 이어서 다루도록 하겠다.


<sup># 해당 글은 개인적인 공부 내용을 정리하는 것을 목적으로 하고있습니다.</sup>
<sup># 설명이 다소 부족하거나 중간 내용이 생략될 수 있습니다.</sup>