---
title: JAVA - 26. 람다식
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/thumbnail.png?raw=true
date: 2020-05-17 21:20:00
tags: 
- java
- 람다식
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

## 람다식이란?
람다식은 <U>식별자 없이 실행가능한 함수</U> 를 말한다. 자바8 버전부터 지원하는 기술로 함수적인 프로그래밍을 위함이다. <!-- more -->

자바는 객체지향언어이다. 그런데 함수지향적인 코드가 가능하게 된 것은 요즘 함수지향적 프로그래밍이 자주 언급되고있기때문에 자바에서도 이를 지원한 것으로 보인다. 

## 함수지향 프로그래밍
함수형 프로그래밍에서 다루는 개념을 잠깐 살펴보자.

### 1급 객체
함수지향에서 함수는 1급 객체라는 표현을 쓴다. 1급 객체의 특징은 다음과 같다.
- 함수를 변수나 데이터 구조안에 담을 수 있다.
- 함수를 파라미터로 전달 할 수 있다.
- 함수를 반환값으로 사용할 수 있다.

위의 특징은 변수가 가지는 특징들이다. 함수지향에서는 함수를 변수처럼 취급할 수 있다는게 큰 특징이다.

### 불변성 
함수형 프로그래밍에서는 데이터가 변할 수 없는데, 이를 불변성 데이터라고 한다. 데이터 변경이 필요한 경우, 원본 데이터 구조를 변경하지 않고 그 데이터의 복사본을 만들어 그 일부를 변경하고, 변경한 복사본을 사용해 작업을 진행한다.

### 순수 함수(Pure function)
순수 함수란 함수형 프로그래밍에서 필수적인 개념으로 다음과 같은 조건을 만족하는 함수를 의미한다.
 -동일한 인자를 주면 동일한 결과를 리턴
 -부수효과가 없어야함 
 -외부의 상태를 변화시키지는다.
 -인자로 들어온 값을 변화시키지않는다.
 -평가시점이 중요하지않다.

이밖의 고차함수, 합성함수등의 개념등이 더 있지만 개인적으로 객체지향의 이점을 이용하기위해 자바를 배우는 입장으로 함수지향은 지금 자세히 공부할 생각은 없다. 

## 람다식 사용해보기
자바에서 함수형 프로그래밍은 인터페이스를 통해 제공된다.

```java
//람다식 사용을 위한 인터페이스
interface Test{
  int add(int x, int y);
}

//테스트해보기
public class LambdaTest{
  public static void main(String[] args){

    //람다식
    Test test = (int x, int y)->x + y;

  }
}

```

위와 같이 람다식을 사용하면 인터페이스를 따로 구현받는 클래스를 정의 할 필요 없이 익명함수로 사용이 가능하다. 중요한 것은 <U>인터페이스 하나당 하나의 함수</U>만 만들 수 있다는 것 이다. 익명함수를 사용하기 때문에 함수를 구분하지 못하는것 이다. 

그래서 람다식을 사용하는 인터페이스를 정의할 때
```java
@FunctionalInterface
interface Test{
	public void add(int x , int y);
}
```

위와 같이 `@FunctionalInterface` 라는 어노테이션을 붙여주면 된다.

## 람다식 예제
```java
@FunctionalInterface
interface Test{
  public int check(int x , int y);
}

public class LambdaTest{
  public static void main(String[] args) {

    Test t = (int x, int y)-> (x > y) ? x : y;
    System.out.println(t.check(90, 40));

  }
}
```
문법적인 생략이 있지만 문법을 자세히 다루지는 않겠다. 함수지향은 추후에 필요해지면 공부할 생각이다.


