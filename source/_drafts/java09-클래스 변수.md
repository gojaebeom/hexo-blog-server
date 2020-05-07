---
title: JAVA - 09. 클래스 변수
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
date: 2020-04-26 15:43:00
tags: 
- java
- 클래스 변수
- 맴버 변수
- 필드 변수
- static 변수
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

## 클래스 변수(static 변수)
인스턴스 변수는 인스턴스가 생성되었을 때, 생성된 인스턴스 안에 존재하는 변수이다. 그러나 클래스 변수는 인스턴스의 생성과 상관없이 존재하는 변수이다. <!-- more -->

클래스 내에 선언된 변수 앞에 static 키워드를 붙이면 이는 인스턴스 변수가 아닌 클래스 변수가 된다. 이러한 클래스 변수의 특성을 파악하기 위해서 다음 예제를 관찰하자.

```java
class InstCnt{
	static int instNum = 0;// 클래스변수 (static 변수)
	
	InstCnt(){//생성자
		instNum++; //static으로 선언된 변수의 값 증가
		System.out.println("인스턴스 생성:"+instNum);
	}
}

public class Static변수_선언 {
	
	public static void main(String[] args) {
		InstCnt cnt1 = new InstCnt();
		InstCnt cnt2 = new InstCnt();
		InstCnt cnt3 = new InstCnt();
	}
}
```
클래스 InstCount의 생성자에서 static으로 선언된 변수 instNum의 값을 하나 증가시킨  다음에 그 결과를 출력하고 있다. 그런데 출력 결과를 보면 그 값이 인스턴스 생성 시마다 1씩 증가함을 알 수 있다. 그리고 이를 통해 다음 사실을 알 수 있다.
	
- static으로 선언된 변수는 변수가 선언된 클래스의 모든 인스턴스가 공유하는 변수이다. 

클래스 변수는 인스턴스 내에 존재하는 변수가 아니라 '어떠한 인스턴스에도 속하지 않는 상태로 메모리 공간에 딱 하나만 존재하는 변수' 이다. 다만 이 변수가 선언된 클래스의 인스턴스들은 이 변수에 바로 접근할 수 있는 권한이 있을 뿐 이다.

> 본 문서는 책의 일부 내용을 발췌한 것으로서 온오프라인 상의 무단 배포를 금합니다.

## 클래스 변수 접근 방법
클래스 변수도 '접근 수준 지시자' 의 규칙을 그대로 적용받기 때문에 public으로 선언되면 어디서든 접근이 가능하다. 물론 접근 방법에 있어서는 차이를 보이는데 이와 관련된 내용은 이어서 설명하겠다.

클래스 변수에 접근하는 방법은 접근 영역을 기준으로 다음과 같이 크게 두 가지로 나뉜다.
- 클래스 내부 접근 : 변수의 이름을 통해 직접 접근
- 클래스 외부 접근 : 클래스 또는 인스턴스의 이름을 통해 접근

다음예제를 보면서 클래스 변수의 접근 방법을 알아보자.
```java
class AccessWay{
	static int num = 0;
	
	AccessWay(){
		incrCnt();
	}
	
	void incrCnt() {
		num++; //클래스 내부에서 이름을 통한 접근
	}
}

public class example01{
	public static void main(String[] args) {
		AccessWay way = new AccessWay();
		way.num++; //외부에서 인스턴스의 이름을 통한 접근
		AccessWay.num++; //외부에서 클래스의 이름을 통한 접근
		System.out.println("num = " + AccessWay.num);// 총 3이 찍힌다.
		
		AccessWay way2 = new AccessWay();//way2라는 새로운 AccessWay의 인스턴스를 생성하였다.
		System.out.println(way2.num);//그리고 way2의 클래스변수 num을 조회 하였는데 값은 4가 찍힌다.
		
	}
	
}
```
인스턴스의 이름을 통한 접근 방법을 보면서, 클래스 변수를 인스턴스 내부에 위치한 것으로 오해하면 안된다. 그리고 클래스 변수 num은 default로 선언되었다. 따라서 클래스 내부는 물론 클래스 외부이더라도 동일 패키지로 묶여 있으면 접근이 가능하다.

## 클래스 변수의 초기화
클래스 변수는 인스턴스의 생성과 상관이 없다고 하였다. 그렇다면 클래스 변수는 언제 메모리 공간에 할당되고 초기화될까? 이와 관련하여 다음 예제를 보자.
	
```java
class InstCnt{
	static int instNum = 100;
	
	InstCnt(){
		instNum++;
		System.out.println("인스턴스 생성: "+instNum);
	}
}

public class 클래스변수_초기화 {

	public static void main(String[] args) {
		InstCnt.instNum -=15; //인스턴스 생성 없이 instNum에 접근
		System.out.println(InstCnt02.instNum);
	}
}
```
위의 예제를 통해서 언급하고 싶은 내용은 다음과 같다.
 
- 클래스 변수는 인스턴스 생성 이전에 메모리 공간에 존재한다.
 
결론을 말하면, 클래스 변수는 해당 클래스 정보가 가상머신에 의해 읽히는 순간 메모리 공간에 할당되고 초기화 된다. 그리고 한 가지 확실한 것은 이러한 할당과 초기화는 위의 예제에서 보이듯이 인스턴스의 생성과 문관하게 이뤄진다는 점이다. 따라서 다음과 같이 생성자를 통한 클래스 변수의 초기화를 진행하지 않도록 주의해야 한다.

```java
class InstCnt{
 		static int instNum =100; //클래스 변수의 정상적인 초기화 방법
 
 		InstCnt(){
 			instNum = 0;// 클래스 변수의 초기화가 아니다!
    }  
}
```
위의 클래스 변수 instNum 은 100으로 초기화 된다. 클래스 정보가 가상머신에 의해 읽히는 순간 100으로 초기화된다. 그런데 생성자에서 변수 instNum을 0으로 다시 초기화 한다. 따라서 인스턴스가 생성될 때마다 instNum은 매번 그 값이 0으로 바뀌게 된다.

### 클래스로딩
앞서 설명에서 클래스 정보를 가상머신이 읽는다 는 표현을 썼는데, 이렇듯 가상머신이 특정 클래스 정보를 읽는 행위를 가리켜 클래스 로딩 이라 한다. 그리고 특정 클래스의 인스턴스 생성을 위해서는 해당 클래스가 반드시 가상머신에 의해 로딩되어야 한다. 즉 인스턴스 생성보다 클래스 로딩이 먼저이다.

> 본 문서는 책의 일부 내용을 발췌한 것으로서 온오프라인 상의 무단 배포를 금합니다.