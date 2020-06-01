---
title: Spring Boot
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/spring-boot/thumbnail.png?raw=true
date: 2020-05-19 19:00:00
tags: 
- spring
- spring boot
category:
- 웹 개발
- spring-boot
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

## 스프링 프레임워크(Spring Framework)
<!-- more -->
스프링 부트를 다루기 이전에 스프링 프레임워크에 대해 간단히 알아보자.

> **스프링이란?**
> 스프링 프레임워크는 자바 생태계에서 가장 대중적인 응용프로그램 개발 프레임워크입니다. 의존성 주입(DI, Dependency Injection)과 제어의 역전(IOC, Inversion Of Control)은 스프링에서 가장 중요한 특징중 하나입니다. 이들로 인해서 좀더 결합도를 낮추는 방식으로 어플리케이션을 개발할 수 있습니다. 이러한 개발방식으로 개발한 응용프로그램은 단위테스트가 용이하기 때문에 보다 퀄리티 높은 프로그램을 개발할 수 있습니다.

## 스프링 부트(Spring Boot)
스프링은 자바 웹어플리케이션을 개발하는데 거의 필수적인 프레임워크이다. 지금도 원래 개발하던 프로젝트의 유지보수등을 고려해서 스프링 프레임워크를 현장에서 사용중인곳도 많을 것 이다.(주변 지인들이 다니는 회사는 대부분 그러하다)

하지만 이런 스프링도 단점이 존재한다. 최소한의 기능으로 Spring MVC를 사용하여 기본 프로젝트를 셋팅하는데도 많은 시간을 필요로 한다. 스프링 부트는 이와 같은 단점을 보완하기 위해 자동설정(AutoConfiguration)을 이용하였고 어플리케이션 개발에 필요한 모든 내부 디펜던시를 관리한다.

다음은 스프링부트 관련의 내용의 인용문이다.
> **스프링 부트**
> 스프링부트는 자동설정(AutoConfiguration)을 이용하였고 어플리케이션 개발에 필요한 모든 내부 디펜던시를 관리합니다. 개발자가 해야하는건 단지 어플리케이션을 실행할 뿐입니다. 스프링의 jar파일이 클래스 패스에 있는 경우 Spring Boot는 Dispatcher Servlet으로 자동 구성합니다. 마찬가지로 만약 Hibernate의 jar파일이 클래스 패스내에 존재한다면 이를 datasource로 자동설정하게 됩니다. 스프링부트는 미리설정된 스타터 프로젝트를 제공합니다.

## 프로젝트 생성
자신의 로컬에 JDK가 설치되어 있고 이클립스나 IntelliJ 등과 같은 IDE(Integrated Development Environment)이 있다면 각 툴에 맞는 프로젝트 생성 방법을 제공하지만, Spring.io 공식 사이트에서 Spring Boot를 빠르게 생성할 수 있는 이니셜라이즈를 제공한다.

![https://start.spring.io/](https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/spring-boot/initializr.PNG?raw=true)

### Maven or Gradle
기존의 스프링에서는 Maven 기반의 프로젝트를 사용하였다. pom.xml 을 통해 dependency를 관리하였는데 스프링 부트에서는 Maven 뿐만 아니라 Gradle 기반의 프로젝트를 제공해준다.

### Gradle이란?
- Gradle은 Maven을 대체 빌드 도구(build tool) 이다.
- Groovy 기반의 DSL(Domain Specific Language)를 사용한다.
- 스프링 오픈소스 프로젝트, 안드로이드 스튜디오에서 Gradle이 사용되고 있다.

어느 블로거 분의 설명이 인상 깊어 출처를 남기고 공유하였다. 

> **왜 Gradle인가?**
> Java에서는 비교적 일찍부터 "빌드 도구"에 의한 프로젝트 관리가 보급되어 있었다. Aache Ant라는 빌드 도구가 등장한 것은 2000년이다. 그 후에 더욱 강력한 Apache Maven이 등장하고, 이것이 현시점에서도 "Java 빌드 도구의 사실상의 표준"이라고 할 수 있다.
> 
> 이러한 툴에서 "이것이 거의 표준"이라고 정착하면, 그렇게 간단히 바뀌는 것은 아니지만 빌드 도구의 세계에서 그 예외적인 사건이 일어나고 있다. 이 Maven의 아성을 무너지고 있는 강력한 라이벌이 "Gradle "라는 소프트웨어이다.
>
> Gradle은 Groovy라는 언어를 기반으로 만들어진 빌드 도구이다. "Groovy? Java 아냐?"라고 생각했을지도 모른다. 그것은 일부는 맞는 말이다.
>
> Groovy는 Java 가상 머신에서 실행되는 스크립트 언어이다. Java와 마찬가지로 소스 코드를 작성하고 Java 가상 머신에서 동작하지만, Java와 달리 소스 코드를 컴파일을 할 필요는 없다. Groovy는 스크립트 언어이며, 소스 코드를 그대로 실행한다. 또한 Java와 호환되고, Java 클래스 파일을 그대로 Groovy 클래스로 사용할 수 있다. 문법도 Java에 아주 가까워, Java를 보다 사용하기 쉽게 한 것으로 느낄 수 있다. 어떤 사람들은 Groovy는 Java의 방언 중 하나라고 생각하는 사람도 있을 정도이다.
> 
> 이 "간편하게 사용할 수 있는 Java"라고 할 수 있는 Groovy를 사용하여 빌드 처리를 작성하고, 실행하는 것이 Gradle이다.
> 
> 기존에 이미 Maven을 이용하고 있는 사람이라면 느낄 수 있겠지만, Maven은 XML 기반의 빌드 처리를 작성한다. 간단한 내용이라면 상관 없지만, 복잡한 내용을 작성하게 되면 XML 기반 의한 묘사는 상당히 어려워 진다. Java 프로그래머인데, 빌드 관리만을 위해 다른 언어를 사용하지 않으면 안된다는 것은 어쩐지 납득할 수 없는 느낌도 든다.
> 
> Gradle라면, Java와 거의 비슷한 코드를 써서 빌드 처리를 관리 할 수 있다. 이런 면이 Java 프로그래머로 압도적으로 받아들이 기 쉬운지도 모른다.
>
> 출처: https://araikuma.tistory.com/460 [프로그램 개발 지식 공유]

글쓴이도 Spring 프로젝트를 만들때 Maven만 사용해왔지만 Spring-Boot 기반의 프로젝트를 만드는 김에 Gradle을 써서 프로젝트를 진행해보려고 한다.

이번 포스트는 스프링 부트를 시작하기 전에 간단한 정리글을 작성해보았다. 다음 글 부터 스프링 부트를 활용하여 admin프로젝트를 만들어보도록 하겠다. 












