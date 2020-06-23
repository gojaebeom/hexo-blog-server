---
title: servlet 복습, 생명주기

thumbnail: images/servlet/thumbnail.png
date: 2020-06-10 22:20:00

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
서블릿 프로그램을 공부하면서 배운 내용들을 정리하려고 한다.<!-- more -->

## 서블릿(Servlet) 의 등장 배경
1. 자바 프로그램은 OS 또는 콘솔을 통해 사용자와 상호작용을 함
2. 웹의 엄청난 발전으로 인해 점차 자바 프로그램은 -> 자바 웹 프로그램으로 바뀌기 시작
3. 사용자는 브라우저를 통해 조작을 하여 원하는 기능들을 사용
4. 사용자가 조작한 것, 예를 들어 www.example.com 이라는 도메인 주소를 요청하면 브라우저(클라이언트)는 도메인주소에 해당하는 ip주소의 서버에게 요청을 보냄 
5. 웹 서버는 요청에 대한 html 문서를 응답해줌
6. 하지만 html문서는 정적인 문서이기때문에 서버에 존재하는 html문서만으로는 데이터의 변화를 줄 수 없음
7. 그래서 웹 서버는 동적인 데이터가 필요하다면 웹 어플리케이션 서버(줄여서 WAS)에게 요청을 위임하여 웹 어플리케이션을 실행시켜 필요한 기능을 수행하게하고 그 결과를 웹 서버가 다시 받아 응답해주는 방법을 사용한다.
8. WAS에서 사용된 웹 어플리케이션이 바로 `서블릿(Servlet)` 이다.

![image](https://gojaebeom.github.io//images/servlet/example02.png)

## 서블릿(Servlet)
서블릿은 다음과 같이 말할 수 있다.
- 자바 웹 서버 프로그램

좀 더 풀어서 말하면 다음과 같이 말할 수 있다. 
- 서버쪽에서 실행되고 클라이언트의 요청에 따라 동적으로 서비스를 제공하는 자바 클래스

## 서블릿 컨테이너(Servlet Container)
사실 위의 일련의 과정중 생량된 것이 바로 서블릿의 컨테이너이다. WAS를 위에서 언급하였는데 브라우저에서 요청이오면 웹서버는 WAS의 내부에 서블릿 컨테이너에게 요청을 위임하는 것이다. <U>서블릿 컨테이너는 서블릿들의 생성, 실행, 파괴를 담당한다.</U> 

### 서블릿 생명 주기(Servlet Life Cycle)
- init() : servlet이 생성되는 단계 (최초 한번만 실행)
- service() : servlet이 실행되는 단계
    - 상황에 따라 doGet(), doPost() 메소드를 호출
- destroy() : servlet이 소멸되는 단계

![image](https://t1.daumcdn.net/cfile/tistory/995D5E435C56BC4914)

위의 서블릿 컨테이너에 의한 서블릿의 생명주기 상세보기이다.
1. HTTP 요청을 서블릿 컨테이너가 받음
2. 서블릿 컨테이너는 `HttpServletRequest`, `HttpServletResponse` 두 객체를 생성
3. 배포 서술자(Web.xml)을 참고하여 요청한 URL이 어느 서블릿에 대한 요청인지 찾음
4. 해당 서블릿 클래스가 컨테이너에서 실행된 적이 없거나 현재 메모리에 생성된 인스턴스가 없다면 새로 인스턴스를 생성하고 `init()` 메소드를 실행하여 최기화하고 스레드를 하나 생성
5. 이미 인스턴스가 존재한다면 새로 생성하지 않고 기존의 인스턴스에 스레드만 하나 생성  
6. 컨테이너는 `service()` 메소드를 호출하여 POST, GET 여부에 따라 `doGet()` 또는 `doPost()` 메서드가 호출됨
7. `doGet()`, `doPost()`등의 메서드는 동적인 페이지를 생성 후 `HttpServletResponse`을 호출
8. 응답을 주고 `HttpServletRequest`, `HttpServletResponse` 객체 소멸