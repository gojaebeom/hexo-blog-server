---
title: Spring MVC - JDBC과 Mybatis 연결

thumbnail: images/spring/thumbnail.png
date: 2020-07-02 03:39:00

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

이전 글에서 스프링 프로젝트의 가장 기본이 되는 설정을 하였다. 이 후 클라이언트에서 넘어오는 데이터 저장에 대한 처리를 위해 데이터베이스를 프로젝트에 연결해 주어야 하는데, 이번 프로젝트에선 데이터베이스로 `MYSQL`을 사용할 예정이다. 그리고 데이터베이스 저장 작업을 쉽게 하기위한 프레임워크인 `Mybatis`도 함께 사용하도록 하겠다.
<!-- more -->

## 작업 순서
스프링 웹 프로젝트에 db를 연결하는 방법은 다음과 같다.
1. pom.xml에 db관련 디펜던시 설정
  - jdbc를 보다 쉽게 사용할 수 있게 spring에서 제공하는 spring-jdbc 디펜던시 적용
  - 커넥션 풀을 사용할 수 있는 commons-dbcp 디펜던시 적용
  - jdbc에 연결할 mysql 커넥터 적용
  - sql을 java 파일과 분리시키고 보다 편리하게 쿼리 작성을 할 수 있는 mybatis 적용
2. web.xml에 디스패처 서블릿이 실행되기 이전 웹과 관련없는 빈들을 설정할 root-context.xml의 경로 설정
3. root-context.xml에 jdbc, mybatis 설정
4. jdbc.properties 파일을 별도로 분리해 db관련 정보를 저장해준다.(git에 올리거나, 공유시 보안을 위함)


## db관련 디펜던시 
**pom.xml**
<script src="https://gist.github.com/gojaebeom/95c0a05d6146baeeb7241e44590cc1d7.js"></script>


## root-context.xml 경로 설정
**web.xml**
<script src="https://gist.github.com/gojaebeom/b2ad43856dd2969f9166faf49cf3d247.js"></script>

## root-context.xml 설정
**root-context.xml**
<script src="https://gist.github.com/gojaebeom/3aba147670e708d4dfe29f3eed231759.js"></script>

## jdbc.properties 설정
**jdbc.properties**
<script src="https://gist.github.com/gojaebeom/2f16fc09e7235f76702fc77ab6aefa1e.js"></script>


<br>
<hr style="border:0px; border-bottom:2px dotted #D8D8D8">

*개인적인 공부 내용을 정리하는 것을 목적으로 하고 있습니다.*
*설명이 부족하거나 틀린 부분은 지적해 주시기 바랍니다.* 🐥