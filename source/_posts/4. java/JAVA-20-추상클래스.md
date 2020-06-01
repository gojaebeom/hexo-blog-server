---
title: JAVA - 20. 추상 클래스
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/thumbnail.png?raw=true
author: JaeBeom Go
date: 2020-05-05 21:20:00
tags:
  - 자바
  - 추상 클래스
  - abstract class
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

## 추상 클래스(Abstract Class)
하나 이상의 추상 메소드를 갖는 클래스를 가리켜 추상 클래스라 한다.<!-- more -->

## 추상 클래스의 특징
- 선언시 abstract 예약어를 사용한다.
- 추상 메서드를 포함하는 클래스이다.
- 추상 메서드는 하위 클래스가 구현해야하는 메서드이다.
- 추상클래스는 인스턴트화 할 수 없다.

## 추상클래스의 선언
```java
public abstract class Animal{...}
```
위와 같이 `class` 키워드 앞에 `abstract` 키워드를 붙이면 이는 추상 클래스로 사용이 가능하다. 

## 추상 메소드
그리고 추상 클래스는 추상 메소드를 다음과 같이 정의할 수 있다.
```java
public abstract class Animal{
  public abstract void move();//추상 메소드
}
```
인터페이스와 같이 메소드의 구현부를 생략하고 `세미클론;`으로 정의한다. 인터페이스는 `abstract` 키워드를 생략할 수 있지만, 추상클래스의 추상메서드는 abstract 키워드를 꼭 붙여주어야 한다. 

## 추상 클래스의 구현 메소드
추상 클래스는 구현부가 있는 일반 메소드도 정의할 수 있다.
```java
public abstract class Animal{
  public abstract void move();//추상 메소드

  public void info() {
    System.out.println("동물 입니다.");
  }
}
```
이게 인터페이스와 추상 클래스의 차이점인가 생각할 수 있지만, 자바8 부터 인터페이스에서도 default 메소드로 구현부가 있는 메소드를 정의할 수 있게 되었다. 아직 알아가는 단계에서 본인은 추상 클래스와 인터페이스의 차이가 점점 모호해지고 있음을 느끼고 이런 저런 블로그를 찾아보았다. 의견이 조금식 다른 부분은 인터페이스가 추상클래스의 보완하는 용도이다~ 라는 글도 있지만, 서로의 목적은 명확하게 다르다는 글도 있다.

물론 이전에 [인터페이스](http://localhost:4000/2020/05/04/java/JAVA-19-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4/#%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EB%9E%80)에대한 글을 포스팅할때에도 인터페이스는 상속이 아닌 구현이라고 하였다. 이 점만 보아도 `인터페이스`와 `추상 클래스`의 사용목적은 다르다는 것을 알 수 있다. 

## 인터페이스와 추상 클래스
먼저 인터페이스와 추상 클래스의 특징을 서로 비교해보자.

**공통점**
- 추상 메소드를 사용한다.(선언만하고 구현부가 없다)
  - 추상 클래스는 `abstract` 키워드를 사용하지만, 인터페이스는 생략할 수 있다는 점이 다르다.
- 일반 메소드의 선언이 가능하다.
  - 추상 클래스는 추상 메소드가 아닌 일반 메소드 선언이 가능하다. 인터페이스는 자바8 버전 이후에 default 키워드를 통해 메소드 내부를 구현할 수 있게 되었다.
- 자기 자신을 인스턴트(객체)화 할 수 없다.

**차이점**
- 추상 클래스와 다르게 인터페이스에서 일반 변수는 사용할 수 없다.
  - 인터페이스에서 사용되는 변수는 상수이다.
- 추상클래스는 extends로 상속될 수 있고, 인터페이스는 implements 로 구현 되어질 수 있다.
- 자바에서 상속은 다중상속이 안된다. 이에 반해 인터페이스를 구현하는 것은 다중 구현이 가능하게 된다.

## 템플릿 메소드(Template Method) 패턴
위의 특징 외에도 추상 클래스가 자주 사용되는 이유중 하나가 `템플릿 메소드`의 구현이다. 템플릿 메소드는 알고리즘의 프로그램 뼈대를 정의하는 행위 디자인 패턴이다.

```java
abstract class LolChampions{
	public abstract void champName();
	
	public abstract void qSkill();
	
	public abstract void wSkill();
	
	public abstract void eSkill();
	
	public abstract void rSkill();
	
	public final void champInfo() {
		System.out.println("챔피언 정보");
		champName();
		qSkill();
		wSkill();
		eSkill();
		rSkill();
	}
}
```
위의 추상클래스 `LolChampions`는 리그오브레전드라는 게임의 캐릭터를 추상화하는 클래스이다. 각 챔피언들의 특징인 이름과 q~r까지의 스킬을 가지고있는것으로 함축하여 만들었다. 끝으로 챔피언에대한 정보를 보여주는 `champinfo`라는 메소드를 정의하였다. 

위의 추상 메소드들은 구현이 강제가 된다. 그렇기에 우리는 위의 추상 클래스를 상속받아 추상 메소드들을 재정의하여 각 챔프에게 맞는 스킬의 정보를 입력해주면 된다. 하지만 `champInfo`는 글쓴이가 설계 당시에 만들어놓은 메뉴얼과도 같다. 챔피언의 정보를 보여주되 이름부터 스킬도 q,w,e,r 순으로 순서있게 조회가 되길 원한다. 그러한 이유로 메소드에  `final` 키워드를 붙여 하위클래스에서 재정의하는것을 막아 놓았다. 이것이 템플릿 메소드 패턴이다. 

인터페이스에선 디폴트 메소드를 통해 몸체를 구현하는 것은 가능하나, `final` 키워드를 붙여 템플릿메소드를 구현할 수 없다.(정확한 이유는 모른다. 시도해보았으나 구현되지 않았다)

정리하자면 추상 클래스는 비슷한 기능들을 가진 하위클래스들이 존재한다면 정의할 수 있는 부분을 제외한 나머지 부분은 추상 메소드로 남겨두고 하위클래스들이 상속을 받아 재정의하게 하는 것을 목적으로 하는 것 같다.

(인터페이스와 추상클래스의 다른점은 찾아볼 수 있었으나, 예제들을 보면 정확히 무엇을 어느시점에 어느 기준으로 나누어야하는지 정말 모호하다.)