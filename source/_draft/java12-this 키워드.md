---
title: JAVA - 12. this 키워드
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
date: 2020-04-26 16:38:00
tags: 
- java
- this
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

## this의 의미
자바에서 제공하는 this 키워드는 인스턴스 자기 자신를 가리키는 키워드이다. 이 this 키워드를 통해 클래스 메서드 및 생성자에서 자기 자신의 데이터를 업데이트하거나 조작할 수 있다.<!-- more -->

## this를 이용한 생성자 호출
this를 이용하여 생성자를 호출하는 방법을 알아보자.

```java
public class this를_이용한_생성자호출 {
	
	public static void main(String[] args) {
		new Person(0);
	}

}

class Person{
	
	Person(){
		System.out.println("생성자 1");
	}
	
	Person(int num1, int num2){
		System.out.println("생성자 2");
	}
	
	Person(int num){
		this(3, 4);
		System.out.println("생성자 3");
	}
}
```
위의 예제를 보면 this 키워드를 이용하여 다른 생성자를 호출하고있다. 정수를 하나 받는 인스턴트를 새로 호출하자, 생성자2, 생성자3 이 콘솔에 출력된다. 

생성자 3이 사용이 되었는데 생성자 3에서는 this(3, 4) 라는 키워드가 먼저 작성되어있다.
여기서 this는 오버로딩된 다른 생성자를 의미한다. 거기에 정수를 두개 받는 생성자를 찾기때문에 생성자 2가 먼저 호출이 되고 그다음 출력문을 만나 생성자 3이 콘솔에 찍히게 된다.

## this - 인스턴수 변수 접근
앞서 키워드 this를 이용한 생성자의 호출에 대해 설명했는데, this는 다른 의미로도 사용이 된다. 이와 관련하여 다음 예제를 보자.
```java
public class this_인스턴스변수_접근 {

}

class Animal{
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

> 본 문서는 책의 일부 내용을 발췌한 것으로서 온오프라인 상의 무단 배포를 금합니다.