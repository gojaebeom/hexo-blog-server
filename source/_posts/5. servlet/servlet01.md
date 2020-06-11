---
title: 자바 웹 프로그래밍

thumbnail: images/servlet/thumbnail.png
date: 2020-05-20 20:20:00

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

이전 [자바 카테고리](https://gojaebeom.github.io/categories/%EC%9E%90%EB%B0%94-%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC/1-java/) 에서는 자바 언어를 배우고 자바 프로그램을 만드는 과정을 진행하였다. 

하지만 자바의 주 사용 목적은 웹 프로그램을 만드는 것이고 앞으로 자바 웹 프로그램을 만드는 것을 목표로 할 것이다. <!-- more -->

그렇다면 자바 프로그램과 자바 웹 프로그램은 다른점이 무엇일까? 먼저 자바 프로그램은 콘솔, 윈도우를 통해 사용자가 입, 출력을 하여 프로그램과 상호작용을 하는 것을 말한다. 

지금까지 다루었던 예제들은 IDE에서 지원하는 터미널이나 콘솔창등을 통해 Scanner로 입력을 받거나 출력받아 볼 수 있었을 것 이다. 

웹 프로그램은 말 그대로 웹을 통하여 사용자와 상호작용을 하는 프로그램이다.  콘솔을 통해 입력을 받고 결과를 출력 받는 곳이 웹의 브라우저로 바뀐것 뿐이다. 

위 내용을 간소화하면 다음과 같이 말 할수 있다.
- 사용자가 상호작용(조작)하는 곳은 브라우저(클라이언트) 이다.
- 클라이언트에서 온 요청을 처리하는 곳은 서버이다.

## 웹 서버(web server)
웹 서버는 클라이언트의 요청을 받으면 정적인 html파일을 보내준다. 

![img](images/servlet/example01.png)


## 서블릿(Servlet)
서블릿은 <U>서버 쪽에서 실행되고 클라이언트의 요청에 따라 동적으로 서비스를 제공하는 자바 클래스</U> 를 말한다.











