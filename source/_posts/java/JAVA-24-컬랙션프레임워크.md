---
title: JAVA - 24. 컬랙션 프레임워크
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
date: 2020-05-13 21:20:00
tags: 
- java
- 컬랙션 프레임워크
category:
- 웹 개발
- java

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

## 컬랙션 프레임워크(Colletion FrameWork)
우리가 프로그램을 만들다보면 기본적인 자료구조들이 많이 쓰이게 된다.<!-- more --> 컬랙션 프레임워크들은 이러한 자료구조들을 미리 구현해놓은 라이브러리를 말한다. JDK를 다운받으면 같이 제공되는 라이브러리로 java.util 패키지에 구현되어있다. 
- Collection 인터페이스와 Map 인터페이스로 구성되어있음

## Collection 인터페이스
`Collection`은 하나의 객체 관리를 위해 선언된 인터페이스로 필요한 기본 메서드가 선언되어 있다. (즉 하나의 객체를 대상으로 하는 자료구조이다)

![image](https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/%EC%BD%9C%EB%9E%99%EC%85%98/%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C1.PNG?raw=true)
위의 이미지와 같이 하위에 `List`와 `Set` 인터페이스가 있다. 

### List 인터페이스의 특징
- 순서가 있는 자료 관리
- 중복 허용
- 이 인터페이스를 구현한 클래스는 `ArrayList`, `Vectior`, `LinkedList`, `Stack`, `Queue` 등이 있음

### Set 인터페이스의 특징
- 순서가 정해져 있지 않음
- 중복을 허용하지 않음
- 이 인터페이스를 구현한 클래스는 `HashSet`, `TreeSet` 등이 있음

## Map 인터페이스
`Map`은 `Collection`과 다르게 쌍으로 이루어진 객체를 관리하는데 필요한 여러 메서드가 선언되어 있다. 여기서 객체는 `Key-value` 쌍으로 되어 있고 `key`는 중복될 수 없다.

![image](https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/%EC%BD%9C%EB%9E%99%EC%85%98/%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C2.PNG?raw=true)

위의 이미지와 같이 하위에 `HashTable`,`HashMap`,`TreeMap` 등의 인터페이스가 있다. 

위의 인터페이스들의 각 설명은 다른 포스트에 작성하도록 하겠다.
