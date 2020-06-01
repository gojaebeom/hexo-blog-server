---
title: JAVA - 11. this 키워드
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/thumbnail.png?raw=true
author: JaeBeom Go
date: 2020-04-28 20:20:00
tags:
  - 자바
  - this
categories:
  - 자바 튜토리얼
  - 1. java
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

## this의 의미
자바에서 제공하는 this 키워드는 인스턴스 자기 자신를 가리키는 키워드이다. 이 this 키워드를 통해 클래스 메서드 및 생성자에서 자기 자신의 데이터를 업데이트하거나 조작할 수 있다.<!-- more -->

## this의 사용 예제

### this를 이용한 생성자 호출
this를 이용하여 생성자를 호출하는 방법을 알아보자.

```java
public class ExampleTest {
	public static void main(String[] args) {
		new Person(0);
	}
}

public class Example{
	Example(){
		System.out.println("생성자 1");
	}
	Example(int num1, int num2){
		System.out.println("생성자 2");
	}
	Example(int num){
		this(3, 4);
		System.out.println("생성자 3");
	}
}
```
위의 예제를 보면 this 키워드를 이용하여 다른 생성자를 호출하고있다. 정수를 하나 받는 인스턴트를 새로 호출하자, 생성자2, 생성자3 이 콘솔에 출력된다. 

생성자 3이 사용이 되었는데 생성자 3에서는 this(3, 4) 라는 키워드가 먼저 작성되어있다.
여기서 this는 오버로딩된 다른 생성자를 의미한다. 거기에 정수를 두개 받는 생성자를 찾기때문에 생성자 2가 먼저 호출이 되고 그다음 출력문을 만나 생성자 3이 콘솔에 찍히게 된다.

### this - 인스턴수 변수 접근
앞서 키워드 this를 이용한 생성자의 호출에 대해 설명했는데, this는 다른 의미로도 사용이 된다. 이와 관련하여 다음 예제를 보자.
```java
public class Example{
	private String name;
	
	void setName(String name) {
		this.name = name;
	}
	String getName(){
		return this.name;
	}
}
```
위와 같이 매개변수의 이름이 인스턴스 변수의 이름과 동일하게 선언된 경우, 선언된 지역 내에서의 해당 이름은 매개변수를 의미하게 된다.
하지만 키워드 this를 이용하면 이 영역 안에서도 인스턴스 변수에 접근할 수 있다. 

즉 this.name에서 this가 의미하는 것은 '이 문장이 속한 인스턴스' 이다. 따라서 this.name은 인스턴스 변수 name을 의미하는 것이 된다.