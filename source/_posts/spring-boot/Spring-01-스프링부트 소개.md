---
title: Spring-boot 시작하기
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











