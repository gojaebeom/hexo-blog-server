---
title: 스프링 빈(Bean)

thumbnail: images/spring/thumbnail.png
date: 2020-06-23 23:27:00

tags: 
- spring
- spring bean

category:
- 자바 튜토리얼
- 4. spring

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

이전 글에서 IOC와 DI의 개념을 이해하기 위해 main 메서드에서 테스트를 진행하였다. 이번 글에서 다루어 볼 내용은 제어의 역전을 스프링에게 직접 맡기는 것이다. 스프링의 IOC 컨테이너는 스프링 빈으로 등록된 객체들의 생명주기를 관리한다. 
<!-- more -->

## 스프링 빈이란?
Spring IOC 컨테이너가 관리하는 자바 객체를 빈(Bean) 이라는 용어로 부른다.

## IOC Container
실제로 스프링 컨테이너는 IOC 컨테이너를 가지고 있고, 이곳에서 등록된 Bean들의 의존성을 주입하는등 생명주기를 관리한다. 그렇다면 어떻게 제어역전 컨테이너에게 빈을 등록할까? 

방법은 크게 두가지가 있다.
- spring bean configuration xml 파일에 직접 등록
- Compnent Scanning 어노테이션을 활용한 annotation 등록

그리고 xml형식으로 빈을 등록할 경우 annotation을 섞어서 활용할 수도 있다.

## 마무리 글
등록하는 예제도 다루어 보려고 했지만 너무 피곤하여 내일 다른 포스트로 이어서 쓰도록 하겠다..😓

<br>
<hr style="border:0px; border-bottom:2px dotted #D8D8D8">

*개인적인 공부 내용을 정리하는 것을 목적으로 하고 있습니다.*
*설명이 부족하거나 틀린 부분은 지적해 주시기 바랍니다.* 🐥