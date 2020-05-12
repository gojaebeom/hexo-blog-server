---
title: JAVA - 22. String, Wrapper 클래스
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
date: 2020-05-11 21:20:00
tags: 
- java
- 자바 객체지향
- String
- Wrapper 클래스
category:
- 웹 개발
- java

#카탈로그 생성 및 위치
toc: true
widgets:
  - type: toc
    position: right
  - type: category
    position: right
  - type: tagcloud
    position: right
#위치고정 여부
sidebar:
  right:
    sticky: true
---

## String 클래스 사용하기
자바에서 문자열을 사용하기 위해 기본적으로 String 클래스라는 것을 재공한다. 선언 방법은 다음과 같다.

## String 사용하기
```java
public static void main(String[] args){
  String str1 = new String("hello"); // 인스턴스로 생성
  String str2 = "world"; // 상수 풀에 있는 문자열을 가리킴
}
```
위의 두가지 선언방법을 보았는데, 두가지 방법의 차이점은 다음과 같이 확인할 수 있다.
```java
public static void main(String[] args){
  String str1 = new String("hello"); // 인스턴스로 생성
  String str2 = new String("hello"); // 인스턴스로 생성

  String str3 = "world"; // 상수 풀에 있는 문자열을 가리킴
  String str4 = "world"; // 상수 풀에 있는 문자열을 가리킴

  System.out.println(str1 == str2); //false
  System.out.println(str3 == str4); //true
}
```
위의 `str1`,`str2`은 서로 다른 인스턴스를 참조하기때문에 `false`라는 값이 출력되고 `str3`,`str4`는 상수 풀에 있는 같은 값을 가리키기 때문에 `true`가 출력되었다. 상수풀은 [상수와 형변환](https://gojaebeom.github.io/2020/04/22/java/JAVA-03-%EC%83%81%EC%88%98%EC%99%80%20%ED%98%95%EB%B3%80%ED%99%98/) 편에서 한번 다룬적이 있다.

위의 코드는 다음과 같은 이미지로 비유될 수 있다.