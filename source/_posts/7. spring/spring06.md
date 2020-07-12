---
title: Spring MVC - 프로젝트 생성, 설정

thumbnail: images/spring/thumbnail.png
date: 2020-06-27 03:39:00

tags: 
- spring
- spring mvc


category:
- 자바 튜토리얼
- 4. spring

#카탈로그 생성 및 위치
5toc: true
widgets:
  - type: toc
    position: right
  - type: category
    position: right
sidebar:
  right:
    sticky: true
---

자바 웹 프로그램을 만들때 자주 사용되는 빌드 툴은 maven이라고 할 수 있다. (물론 gradle도 많이 사용된다고는 한다)
<!-- more -->

글쓴이는 스프링 웹 프로젝트를 만들때 메이븐을 이용하여 spring mvc 프로젝트를 진행해 보려고 한다. 순서는 다음과 같다.

1. maven 프로젝트 생성
2. spring mvc 를 사용하기 위한 dependency 설정
3. web.xml을 통해 dispatcher servlet 설정
4. 그 외 웹과 관련없는 bean들을 설정할 root-context 설정
5. 기본적인 틀만 만들어놓고 톰캣에 배포해보기(물론 이클립스의 도움으로 이클립스 톰캣으로 실행)

이번 글에선 단순히 spring mvc 프로젝트를 만들기 위한 프로젝트의 셋팅만 다루어 보겠다.

## mvc를 위한 pom 설정
먼저 생성된 maven 프로젝트의 pom.xml의 최소한의 설정은 다음과 같이 하면 된다.

**pom.xml**
<script src="https://gist.github.com/gojaebeom/f67a1022893a56233f33450f9c851a28.js"></script>

Spring-context는 스프링 프레임워크를 사용하기 위한 핵심이다. 내부적으로 스프링 core, bean, aop, context, logging 등을 포함하고 있다.

spring-mvc는 말 그대로 spring mvc 프로젝트를 할 수 있게 도와주는 디펜던시다. 

설정이후 이클립스 툴을 쓰고있다면 프로젝트에 에러가 날것이다. 원인은 여러가지가 있는데, 패키징 타입을 war로 하였기때문에 webapp 폴더 하위에 WEB-INF가 존재하고 web.xml을 가지고 있는 형태가 완성되야 war 패키징 타입을 만족하기 때문이다. webapp 폴더 하위에 아무것도 안만들어져 있다면 WEB-INF/web.xml 을 만들어주자.

## web.xml 설정
웹 프로젝트를 실행하기 위해 본 프로젝트를 톰캣을 이용하여 실행할 텐데, 톰캣은 프로젝트에 WEB-INF 폴더 하위에 존재하는 web.xml 파일을 읽어 프로그램을 실행하게 된다.

**web.xml**
<script src="https://gist.github.com/gojaebeom/da5b773e4fb8f884cded4c8a349115ed.js"></script>
물론 위의 코드는 최소한의 설정이다. 톰캣에게 디스페처 서블릿 클래스의 위치를 알려주고 톰캣은 그것을 실행시키는데, 이전의 서블릿 프로젝트는 하나의 서블릿에 한 페이지를 만들었다. 그 결과 서블릿의 수가 상당히 많아지게 되었는데, 스프링 mvc에서는 dispatcher servlet이 오는 모든 요청을 받아 각 컨트롤러의 맞는 url로 분기시키는 작업을 한다.

## 컨트롤러 , 뷰 설정

**servlet-context.xml**
<script src="https://gist.github.com/gojaebeom/704eef7c78dfab38ac9ef41894b4d961.js"></script>
view와 관련된 파일을 어디 폴더에 둘지, 컴포너트를 스캔할 패키지는 어떤건지 작성해준다.

**HomeController**
<script src="https://gist.github.com/gojaebeom/2f142dc819d5948c9bff8123e136805a.js"></script>

servlet-context.xml 에서 명시해준 패키지에 해당 클래스를 만들어준다. Controller 어노테이션은 Component 어노테이션을 포함하고 있기때문에 해당 어노테이션을 가지는 클래스를 컨트롤러 클래스로 인식하게 된다. 그리고 각 메서드에 매핑된 url로 요청이 오면 return 값인 이름의 jsp 파일로 응답해준다.

**home.jsp**
<script src="https://gist.github.com/gojaebeom/3213325d3be849fcf90349ca80048d8a.js"></script>

프로그램이 잘 작동하는지 보여주기 위해 간단히 작성한다. 


## 마무리 글
최근 게시판 프로젝트 만드는데 열중하다보니, 만든 프로젝트를 다시 설명하면서 다루는게 보통일이 아닌것 같다,,

<br>
<hr style="border:0px; border-bottom:2px dotted #D8D8D8">

*개인적인 공부 내용을 정리하는 것을 목적으로 하고 있습니다.*
*설명이 부족하거나 틀린 부분은 지적해 주시기 바랍니다.* 🐥