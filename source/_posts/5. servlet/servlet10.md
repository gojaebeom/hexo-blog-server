---
title: jsp 프로젝트 만들기 - mvc1, mvc2

thumbnail: images/servlet/thumbnail.png
date: 2020-05-27 20:30:00

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

이전에 만든 `board-detail.jsp`은 DB와 잘 연결되어 화면에 데이터를 잘 출력하는 것을 볼 수 있다. 하지만 jsp 파일 내의 코드를 보면 자바코드와 html코드가 뒤엉켜 있는 것을 볼 수 있다. 이것을 스파게티 코드라 한다.
<!-- more -->

## MVC1
스파게티 코드는 코드량이 많아질 수록 점점 복잡해 지는 단점이 있다. 이와 같은 문제점을 해결하기 위해 MVC1 모델이 나오게 된다. 다음 그림을 보자.
![board-detail.jsp](https://gojaebeom.github.io//images/servlet/example09.png)

위 처럼 제어에 의한 코드들은 상단에 모아놓고 밑에는 html 코드만 두는 것이다. 물론 데이터의 전달을 위한 model을 사용하는 java코드는 아직까진 해결하지 못한것 같다. (이후의 el과 jstl에 의해 어느정도 해결이 된다.)

```jsp
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

String title = result.getString("title");
String writerId = result.getString("writer_id");
String content = result.getString("content");
String files = result.getString("files");
int hit = result.getInt("hit");
Date createdAt = result.getDate("created_at");

con.close();
state.close();
result.close();
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
	<h1>제목 : <%= title %></h1>
	<p>작성자:<%= writerId %> / 작성일: <%= createdAt %> / 조회수: <%= hit %>  </p>
	<p>첨부 파일:<%= files %> </p>
	<div style="width:500px; height:300px; border:2px dotted gray; padding:10px;">
		<%= content %>
	</div>
	<hr/>
	<a href="">다음 글</a>
	<span style="font-weight:bold">/</span>
	<a href="">이전 글</a>
</body>
</html>

```

별 차이 없어 보일 수 있는데, 이전의 코드는 html 최하단에 DB의 연결을 끊기 위한 코드를 작성했었다. 그 코드들을 모두 상단으로 가져갔는데, 여기서 포인트는 
```java
con.close();
state.close();
result.close();
```
가 먼저 실행되어 db의 연결이 끊겼지만 result에서 빼온 값을 변수에 저장하여 별개로 데이터를 넘겨 줄 수 있는 점이다. (물론 다수의 데이터를 가져온다고 하면 조금 더 복잡해 지지만) 위와 같은 방법으로 java 코드를 한군데 모아 놓으니 더 깔끔해 진거 같다.

## MVC2
하지만 MVC1 모델도 개발자들이 불편함을 느꼈는지 이후의 MVC2 방식이 나오게 된다. MVC2 방식은 기존의 자바 소스코드를 아예 별도의 파일로 분리하여 요청을 servlet에서 받아 데이터를 가공하고 jsp에게 요청과 데이터를 위임하는 방식을 사용한다. 다음 예제를 살펴보자.

### com.example.demo.controller.BoardDetail
```java
@WebServlet("/board-detail")
public class BoardDetail extends HttpServlet {
	
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse res) 
			throws ServletException, IOException {
		
		String bId_ = req.getParameter("id");
		
		int bId = (bId_ != null && !bId_.equals("")) ? Integer.valueOf(bId_) : 1 ;
		
		
		String url = "jdbc:mysql://localhost:3306?characterEncoding=UTF-8&serverTimezone=UTC";
		String id = "root";
		String pw = "woqja5164!";

		String sql = "SELECT * FROM example01.board where id = "+ bId;
		
		Connection con = null;
		Statement state = null;
		ResultSet result = null;
		
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			con = DriverManager.getConnection(url,id,pw);
			state = con.createStatement();
			result = state.executeQuery(sql);

			result.next();

			Board board = new Board();
			board.setTitle(result.getString("title"));
			board.setWriterId(result.getString("writer_id"));
			board.setContent(result.getString("content"));
			board.setFiles(result.getString("files"));
			board.setHit(result.getInt("hit"));
			board.setCreatedAt(result.getDate("created_at"));
					
			req.setAttribute("board", board);
			
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			try {
				con.close();
				state.close();
				result.close();
			} catch (SQLException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
		
		req.getRequestDispatcher("/details/board-detail.jsp").forward(req, res);
	}
}
```
- 요청이 http://localhost:8080/board-detail 로 들어올 경우 해당 서블릿 실행
- 쿼리스트링으로 id 값을 받아오면 쿼리의 인자로 들어감 
- 만약 id 값을 받아오지 않으면 기본 값 1로써 쿼리를 실행 -> 즉 board 테이블의 1번째 행을 조회
- 변수로 담았던 title, writer_id 등의 값을 Board.java 파일로 따로 만들어 DB에서 추출한 값을 담음
- request의 setAttribute 를 통해 값을 request 저장소에 담아둔다. 
- 이후의 req.getRequestDispatcher("/details/board-detail.jsp").forward(req, res) 를 통해 board-detail.jsp에게 요청을 양도하고 불러옴'

### com.example.demo.entity.Board
```java
public class Board {
	private int id;
	private String title;
	private String writerId;
	private String content;
	private Date createdAt;
	private int hit;
	private String files;

	//생성자 정의 생략

	//getter&&setter 정의 생략
}
```
- board 테이블에 대한 데이터를 담기 위한 클래스 정의

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
	<h1>제목 : ${board.title }</h1>
	<p>작성자:${board.writerId } / 작성일: ${board.createdAt } / 조회수:${board.hit }  </p>
	<p>첨부 파일:${board.files } </p>
	<div style="width:500px; height:300px; border:2px dotted gray; padding:10px;">
		${board.content }
	</div>
	<hr/>
	<a href="">다음 글</a>
	<span style="font-weight:bold">/</span>
	<a href="">이전 글</a>
</body>
</html>
```
- forword를 통해 BoardDetail.java에게 req, res를 위임 받아 setAttribute에 저장한 board 값을 사용할 수 있음
- el태그를 이용하여 보다 깔끔하게 model을 입력할 수 있음

## view 은닉
- http://localhost:8080/board-detail 주소를 입력하게 되면 board 테이블의 id가 1인 데이터들이 출력되는 것을 볼 수 있다.
- 이것은 사실 id 값을 받지 않으면 기본값을 1로 받기 때문에 출력이 되는 것이다. 실제로 저 주소 대신 http://localhost:8080/board-detail?id=1 과같은 주소를 사용하여 사용자들은 목록에서 해당하는 게시물을 찾아 들어갈 수 있게 될 것이다.

그렇다면 다음과 같은 주소를 입력해보자. 
http://localhost:8080/details/board-detail.jsp?id=1

화면에 데이터가 출력되지 않거나 NullPointException 오류창이 뜰 것이다. MVC2 패턴을 사용하면서 사용자는 `details/board-detail.jsp`를 직접 요청하는게 아닌 `/board-list`를 입력하여 서블릿을 먼저 실행시켜 데이터를 가공하고 가공된 데이터를 board-detail.jsp 파일에서 위임하여 실행 시키는 구조이다. 즉 위와 같이 jsp 문서를 사용자가 직접 요청하게 되면 데이터가 없는 문서를 보여주게되고, 로직에 따라 오류가 날 수 있는 가능성이 크다는 것이다. 이것은 잘못된 접근이며 그렇기에 사용자가 jsp파일을 직접 접근할 수 없게 만들어 주어야 한다.

## WEB-INF
WebContent 폴더 하위에 WEB-INF라는 폴더가 보일 것이다. 이름 그대로 `WEB INFORMACTION`의 약자이며 보안에 관련된 파일들은 이 폴더의 내부에 둔다. 그렇다면 우리가 만든 index, detail, list 파일들을 이 폴더 내부로 옮겨주자. 

- WEB-INF 폴더에 views 라는 폴더를 하나 만든다.
- 그 안에 index.jsp, (board-list.jsp를 포함한)lists폴더 , (board-detail.jsp를 포함한) details 폴더를 옮겨주자.
- BoardDetail.java의 하단의 getRequestDispacher()의 경로를 `/WEB-INF/views/details/board-detail.jsp`로 바꿔주자.

이제 파일 경로로 jsp를 호출하려고 해도 페이지를 찾을 수 없다는 404오류가 뜰 것이다. 이로써 사용자는 상세페이지를 조회하기 위해 무조건 servlet을 요청하게 되고 servlet은 해당하는 id 값을 받아 jsp 파일을 호출해 client에 응답을 해주게 된다.

![board-detail.jsp](https://gojaebeom.github.io//images/servlet/example10.png)


<sup># 해당 글은 개인적인 공부 내용을 정리하는 것을 목적으로 하고있습니다.</sup>
<sup># 설명이 다소 부족하거나 중간 내용이 생략될 수 있습니다.</sup>