---
title: 톰캣 사용하기

thumbnail: images/servlet/thumbnail.png
date: 2020-06-02 20:20:00

tags: 
- servlet
- jsp
- tomcat

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

지난 글에 이어 본격적으로 servlet을 이용한 자바 웹 프로그래밍을 할 것이다. 프로그램 예제를 다루기 이전에 필요한 준비물이 있는데, servlet은 웹 어플리케이션 서버에서 동작한다.(줄여서 `WAS`라고 하겠다) 그렇기에 로컬 pc에 was를 설치해주어야 한다.<!-- more -->

`WAS`는 여러 플랫폼이 있지만 그 중에 `Tomcat`이라는 프로그램을 사용하도록 하겠다. 

## 톰캣(Tomcat)이란?
> 위키백과
> 아파치 톰캣은 아파치 소프트웨어 재단에서 개발한 서블릿 컨테이너만 있는 웹 애플리케이션 서버이다. 톰캣은 웹 서버와 연동하여 실행할 수 있는 자바 환경을 제공하여 자바서버 페이지와 자바 서블릿이 실행할 수 있는 환경을 제공하고 있다.

## 톰캣의 특징
- Apache 제단에서 만들어졌다.
- 웹 어플리케이션 서버이다.
- HTTP 서버를 자체 내장하기도 한다.
- xml파일을 편집하여 설정할 수 있다.

## 톰캣 다운로드
1. [공식 홈페이지](http://tomcat.apache.org/) 에 접속
2. 좌측 매뉴의 `Download 카테고리`에서 해당 버전을 선택
3. 사용자 pc에 맞는 버전 - `32-bit Windows zip (pgp, sha512)` 또는 `64-bit Windows zip (pgp, sha512)`를 다운 받기


## 톰캣 사용하기
1. 다운 받은 압축파일을 푼다.
2. 생성된 폴더 내부의 bin 폴더 내부의 startup.bat 파일을 클릭
3. 브라우저에 접속하여 url에 localhost:8080 을 입력
4. 톰캣 메인화면이 보이면 성공

이 밖의 톰캣을 사용하는 방법들은 톰캣 카테고리를 만들어 따로 다루어 볼 예정이다. 지금은 servlet 프로젝트를 만드는 것에 초점을 두기위해 이클립스에서 톰캣을 연동하여 프로그램을 만들어보도록 하겠다.