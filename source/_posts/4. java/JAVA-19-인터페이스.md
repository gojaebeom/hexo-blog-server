---
title: JAVA - 19. 인터페이스
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/thumbnail.png?raw=true
date: 2020-05-04 21:20:00
tags: 
- java
- 인터페이스
- interface
- 추상 메소드
category:
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

## 인터페이스란?
```java
interface ExampleIF{
    public void exam();
}
```
위의 예제는 인터페이스 선언의 모습이다. 기본 골격은 클래스와 동일하다. 그러나 class 대신 interface라는 키워드를 사용하고, 내부에 있는 메소드는 몸체 없이 세미콜론으로 마무리 된다. 위와 같이 몸체가 비어있는 메소드를 가리켜 **추상 메소드(Abstract Methods)** 라 한다. <!-- more -->

그리고 인터페이스를 대상으로 인스턴스 생성이 불가능하다. 다른 클래스에 의해 상속이 되어 사용될 뿐이다.
```java
class ExampleClass implements ExampleIF{...}
```
클래스가 인터페이스를 상속하는 행위는 **상속** 이 아닌 **구현(Implementation)** 이라 한다. 문법 관계는 상속과 동일하지만 본질은 구현이기 때문이다. 위의 예제에 클래스에서 인터페이스를 상속할때 extends 라는 키워드 대신 implements가 사용되어진 것을 볼 수 있다.

## 인터페이스의 특징
클래스의 인터페이스 구현을 조금 더 구체적으로 보자면 다음과 같은 특징이 있다.
- _구현할 인터페이스를 명시할 때 키워드 implements를 사용한다._
- _한 클래스는 둘 이상의 인터페이스를 동시에 구현할 수 있다._
- _상속과 구현은 동시에 가능하다._
- _인터페이스의 형(타입)을 대상으로 참조변수의 선언이 가능하다._
- _인터페이스의 추상 메소드와 이를 구현하는 메소드 사이에 오버라이딩 관계가 성립한다._

implements를 사용하는 것은 위의 예제에서 알 수 있고, 다수의 인터페이스를 상속한다는 것은 다음과 같다.
```java
class ExampleClass implements ExampleIF01, ExampleIF02{...}
```
<br>

상속과 구현이 동시에 가능하다는 말은 이전까지 상속에 대하여 포스팅하였는데, 하위 클래스가 상위 클래스를 상속하는 행위와 인터페이스를 구현하는 행위를 동시에 할 수 있다는 뜻이다.
```java
class ExampleClass extends ExampleSuperClass implements ExampleIF01, ExampleIF02{...}
```
<br>

그 이후의 특징들은 말이 조금 어렵게 느껴질 수도 있다. 먼저 인터페이스의 타입을 대상으로 참조변수의 선언이 가능하다는 말은 상속에서도 비슷한 예제를 다루었는데 
```java
class ExampleClass extends SuperExampleClass{...}

public class Test{
    public static void main(String[] args){
        ExampleClass object1 = new  ExampleClass();
        SuperExampleClass object2 = new ExampleClass();
    }
}
```
위와 같이 ExampleClass 의 인스턴스를 생성하고 참조변수에 할당하려고한다. 그렇다면 참조변수의 타입은 ExampleClass의 인스턴스(객체) 이기때문에 당연히 ExampleClass가 될 것 이다. 그리고 ExampleClass가 상속한 SuperExampleClass도 ExampleClass의 부모클래스이기때문에 ExampleClass의 참조변수 타입으로써 인스턴스 할당이 가능 한 것이다. (물론 자식 클래스에서 새로 구현된 메소드는 부모클래스 형인 참조변수에서는 사용할 수 없다)

본론으로 돌아와 인터페이스를 대상으로 참조변수의 선언이 가능하다는것은 다음과 같다.
```java
class ExampleClass implements ExampleIF{...}

public class Test{
    public static void main(String[] args){
        ExampleIF obj = new ExampleClass();
    }
}
```
위의 상속클래스의 참조변수 선언 예제와 비슷하다. 구현한 ExampleIF 인터페이스 역시 ExampleClass 클래스의 인스턴트를 할당할 수 있는 참조변수가 된다는 것 이다.

그렇다면 자연스럽게 '인터페이스의 추상 메소드와 이를 구현하는 메소드 사이에 오버라이딩 관계가 성립한다' 라는 것도 단순하게 생각하면 된다. 인터페이스의 구현되지않은 추상메소드 역시 메소드임으로, 이를 상속하는 인터페이스의 메소드를 재정의(오버라이딩)해주어야 한다. 이는 선택사항이 아닌 강제성이 부여된다.

## 인터페이스의 본질적 의미
인터페이스의 사전적 의미는 연결점 또는 접점으로 둘 사이를 연결하는 매개체를 뜻한다. 실제로 자바의 인터페이스는 그런 역할을 한다. 그럼 이와 관련하여 간단한 예를 하나 들겠다.

- *몬스터의 종류는 다양하다. 몬스터는 이름과 각자의 특성이 있다. 이중 슬라임과 스켈레톤을 몬스터의 한 예로 볼 수 있다.*

이렇듯 몬스터와 슬라임, 스켈레톤 등이 연결되는 한 예를 보았다. 그렇다면 이것을 코드로 구현해보자.

```java
interface Monster{
	
	public void name();//이름
	
	public void characteristic();//특성
}

class Slime implements Monster{

	@Override
	public void name() {
		System.out.println("슬라임");
	}

	@Override
	public void characteristic() {
		System.out.println("몸이 액체로 되어있음");
		
	}
	
}

class Skeleton implements Monster{

	@Override
	public void name() {
		System.out.println("스켈레톤");
	}

	@Override
	public void characteristic() {
		System.out.println("뼈만 앙상한 언데드 몬스터");
	}
}

public class Example {
	
	public static void main(String[] args) {
		Monster slime = new Slime();
		slime.name();
		slime.characteristic();
		
		System.out.println();
		
		Monster skeleton = new Skeleton();
		skeleton.name();
		skeleton.characteristic();
	}
}
```
위의 코드는 몬스터들이 가지고있는 기본적인 속성들을 인터페이스에 추상메소드를 만들어놓고 각 Slime과 Skeleton 클래스들이 이것을 구현한 예제이다. Slime과 Skeleton은 대부분의 RPG 게임에서 많이 다루는 괴물들이기때문에 Monster라는 접점이 있다.

## 인터페이스의 문법 구성
인터페이스에 존재할 수 있는 메소드에는 추상 메소드, 디폴트 메소드, static 메소드가 있다. 그리고 인터페이스 간 상속도 가능하며 인터페이스의 타입 이름을 대상으로 instance of 연산을 할 수도 있다. 즉 많은 특성이 클래스와 유사하다.

위의 예제에서 다음같이 인터페이스를 정의하였다.
```java
interface Monster{
	
	public void name();//추상 메소드
	
	public void characteristic();//추상 메소드
}
```
그리고 위 인터페이스에 정의된 추상 메소드에는 다음의 특징이 있다.

- *인터페이스의 모든 메소드는 public 선언된 것으로 간주합니다.*

즉 인터페이스 내에 위치하는 메소드는 별도의 선언이 없어도 public이 된다. 때문에 위의 인터페이스 정의에서 메소드 앞에 public을 붙일 필요가 없다. 그리고 인터페이스에서도 변수를 선언할 수 있다.

```java
interface Monster{
  int DEFAULT_HP = 100;
  int DEFAULT_PAWER = 10;
}
```
그리고 이렇게 인터페이스 내에 선언되는 변수에는 다음의 특징이 있다. 
- *반드시 선언과 동시에 값으로 초기화를 해야 한다.*
- *모든 변수는 public, static, final 이 선언된 것으로 간주한다.*

결론적으로 인터페이스 내에 선언된 변수는 상수이다. 

## 인터페이스 간 상속 
위에 다루었던 몬스터 인터페이스를 통해 구현된 몬스터들이 있다. 하지만 설계를 하던중 보스몬스터급인 녀석들은 차별을 두려고 한다. 하지만 몬스터 인터페이스에 메소드를 만들게 되면 구현하는 클래스에서는 이것이 강제가 되기때문에 모든 몬스터에게 불필요한 보스몬스터의 기능을 담은 메소드를 강제구현시켜야한다. 그렇다고 보스몬스터가 몬스터와 다른것은 아니다. 공통되는 부분도 존재하기 때문이다. 이런 경우 우리는 인터페이스간의 상속을통해서 문제를 해결할 수 있다. 글로만 이해하기 어려우니 예제를 보자. 
```java
interface Monster{
	
	public void name();//이름
	
	public void characteristic();//특성
}

interface BossMonster extends Monster{
	
	void BossSkill();
	
	void BossItem();
}

class Minotaur implements BossMonster{

	@Override
	public void name() {
		System.out.println("미노타우르스");
	}

	@Override
	public void characteristic() {
		System.out.println("소 머리에 인간의 몸을 한 거대한 몬스터");
	}

	@Override
	public void BossSkill() {
		System.out.println("보스 몬스터 한정 기술");
	}

	@Override
	public void BossItem() {
		System.out.println("보스 몬스터 한정 아이템");
	}
	
}
```

이전의 Monster 인터페이스는 수정하지 않고, 새로운 BossMonster 인터페이스를 만들었다. 그리고 이전의 Monster 인터페이스를 상속하여 Monster의 기본적인 기능들은 가져오고 보스몬스터만의 새로운 기능이 추가가 된 것을 알 수 있다. 이것은 이전에 만들었던 슬라임과 스켈레톤의 코드는 수정할 필요없이 앞으로 추가될 보스몬스터만 BossMonster 인터페이스를 구현할 수 있다는 이점이 있다.

그리고 위의 인터페이스간 상속을 명시할때 extends 키워드를 사용하는데 이에 대한 내용을 정리하자면 다음과 같다.
- *두 클래스 사이의 상속은 extends로 명시한다.*
- *두 인터페이스 사이의 상속도 extneds 로 명시한다.*
- *인터페이스와 클래스 사이의 구현만 implements로 명시한다.*

> 본 문서는 책의 일부 내용을 발췌한 것으로서 온오프라인 상의 무단 배포를 금합니다.
