---
title: JAVA - 16. 상속
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/java-thumbnail.jpg?raw=true
author: JaeBeom Go
date: 2020-05-01 21:20:00
tags:
  - 자바
  - 상속
categories:
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

## 상속의 기본문법 이해
상속의 적절한 활용 방법은 한두 문자응로 가볍게 설명할 수 있는 내용이 아니다. 그리고 이에 대한 설명을 듣기에 앞서 상속에 대한 문법적인 이해가 선행되어야 한다. <!-- more -->

## 상속이란?
상속의 이유와 목적을 물어보면 
- 상속은 코드의 재활용를 위한 문법입니다.

그러나 이는 정확한 표현은 아니다.

- 연관된 일련의 클래스들에 대해 공통적인 규약을 정의할 수 있다.

위의 답변은 매우 모범적인 답변이다.

### 상속의 가장 기본적인 특성
상속을 단순하게 설명하면 , 기존에 정의된 클래스에 메소드와 변수를 추가하여 새로운 클래스를 정의하는 것이 상속이다. 예를 들어서 다음의 클래스가 정의되어 있다고 가정해보자.

```java	
class Animal{
	String name;
	
	Animal(String name){
		this.name = name;
	}
	
	public void name() {
		System.out.println("이 동물의 이름은 "+name+"입니다.");
	}
}
```

이때 위의 클래스를 상속하여 다음과 같이 새로운 클래스를 정의 할 수 있다.
```java
class Cat extends Animal{
	String cry;
	
	Cat(String name , String cry){
		super(name);//부모의 String타입의 매개변수를 받는 생성자 호출(super는 이후에 배우게 된다.)
		this.cry = cry;
	}
	
	public void info() {
		name();//Animal 클래스를 상속했기 때문에 호출 가능
		System.out.println("울음소리는 "+cry);
	}
}
```

위 예제를 보면 새로운 super 키워드가 등장한 것을 알 수 있다. 이건 나중에 더 자세히 다루어보겠다.

## 클래스 변수와 클래스 메소드의 상속이 가능한가?
static 선언이 붙는 클래스 변수와 클래스 메소드도 상속의 대상에 포함이 되겠는가?

static 선언이 갖는 의미를 떠올리고 논리적으로 접근을 하면 이 질문에 스스로 답을 할 수 있다.

앞서 공부한 클래스 변수와 클래스 메소드의 특징을 정리하면 다음과 같다. 
- 인스턴스의 생성과 상관없이 접근이 가능하다.
- 클래스 내부와 외부에서 접근이 가능하다.
- 클래스 변수와 클래스 메소드가 위치한 클래스 내에서는 직접 접근이 가능하다.

즉 클래스 변수와 클래스 메소드는 인스턴스에 속하지 않는, 딱 하나만 존재하는 변수와 메소드이다. **따라서 상속의 대상이 아니다.**

그렇다면 다음 내용에 대해서는 생각을 해볼 필요가 있다. 
- 상위 클래스에 위치한 클래스 변수와 메소드에 하위 클래스에서 어떻게 접근하는가?

결론을 말하자면 변수의 이름만으로 접근이 가능하다. 단 접근 수준 지시자가 접근을 허용해야 접근이 가능하다. 다음 예제를 통해 알아보자. 

```java
public class Example{
    public static void main(String[] args) {

		SuperClass sc1 = new SuperClass(); // 값 1 증가
		SuperClass sc2 = new SuperClass(); // 값 1 증가
		
		SubClass sub1 = new SubClass();//인스턴스 생성 과정에서 부모생성자가 호출 되므로 count 값 1 증가
		sub1.showCount();
	}
}

class SuperClass{
	protected static int count = 0; //protected는 하위 클래스 접근을 허용
	
	public SuperClass() {
		count++;
	}
}

class SubClass extends SuperClass{
	public void showCount() {
		System.out.println(count);
    }
}
```
위의 예제에서 변수 count의 접근 수준 지시자를 private으로 선언하면 이로 인해 컴파일 오류가 발생하는 것도 확인하기 바란다.

## IS - A 
두 클래스를 상속의 관계로 맺는 것이 도움이 되는 상황이 있고 도움이 되지 않는 상황이 있다. 그렇다면 언제 두 클래스를 상속의 관계로 맺어야 할까? 

기본적으로 IS-A 관계라는 것이 성립해야 상속의 후보로 고려할 수 있다.

상속이 갖는 문법적 특성을 통해서 상위 클래스와 하위 클래스를 다음과 같이 이야기할 수 있다.
- 하위 클래스는 상위 클래스의 모든 특성을 지닌다. 
- 거기에 더하여 하위 클래스는 자신만의 추가적인 특성을 더하게 된다.

이러한 상속의 특성을 현실 세계에서도 찾아볼 수 있다. 대표적인 예가 다음과 같다.
- 모바일폰 vs 스마트폰

모바일폰이 상위 클래스라면 스마트폰은 하위 클래스이다. 즉 이 둘을 객체지향의 관점에서 보면 다음과 같이 이야기할 수 있다. 
- 모바일폰을 스마트폰이 상속한다.

스마트폰은 모바일폰이 갖는 특성을 모두 갖는다. 게다가 스마트폰은 앱의 설치 및 실행 등 컴퓨터의 특성을 추가적으로 갖고 있다. 따라서 클래스를 설계한다면 다음과 같은 설계가 논리적으로 타당하다.
- class 스마트폰 extends 모바일폰 {...}

그런데 우리는 스마트폰도 모바일폰의 한 종류라 말한다. 즉 컴퓨터의 기능이 추가된 모바일폰이 스마트 폰인 것이다. 따라서 다음과 같이 이야기할 수 있다. 
- 스마트폰도 모바일폰이다.
- 스마트폰은 일종의 모바일폰이다.

그리고 위의 문장들이 나타나는 관계를 가리켜 IS-A 관계라 하고, 이것이 상속의 관계를 맺기 위한 두 클래스의 기본 조건이 된다. 참고로 is a는 ~은 ~ 이다. 로해석 된다. 예를 들면 다음과 같다.
- Life is a journey - 인생은 여행이다. 

지금까지 설명한 내용을 정리하면 다음과 같다.
### IS-A 관계 총 정리
- IS - A 관계는 ~은 ~이다. 로 표현되는 관계이다. 
- 상속이 갖는 문법적 특성은 IS - A 관계의 표현에 적합하다.
- 따라서 상속 관계를 형성하기 위한 두 클래스는 IS -A 관계에 있어야 한다.

### IS-A 관계 예제
관련된 예제를 github에 올려두었다.
- [IS - A 예제](https://github.com/gojaebeom/java_tutorial/blob/master/src/ch11_%EC%83%81%EC%86%8D/IS_A_%EC%98%88%EC%A0%9C.java)

## 상위 클래스의 참조변수가 참조할 수 있는 대상의 범위
```java
class Sartphone extends MobilePhone {...}
```
<br>

따라서 다음과 같이 문장을 구성할 수 있다.
```java
SmartPhone phone = new SmartPhone("010-555-777", "Nougat");
```
<br>

그런데 다음과 같이 MobilePhone형 참조변수가 SmartPhone 인스턴스를 참조하게 할 수도 있다.
```java
MobilePhone phone = new SmartPhone("010-555-777", "Nougat");
```
<br>

이렇듯 상위 클래스의 참조변수는 하위 클래스의 인스턴스를 참조할 수 있는데, 이 부분을 다음과 같이 이해하자.
- 모바일폰을 상속하는 스마트폰도 일종의 모바일폰이다.
    - Mobilephone을 상속하는 SmartPhone 인스턴스는 MobilePhone 인스턴스이기도 하다.
- 따라서 MobilePhone형 참조변수는 SmartPhone 인스턴스를 참조할 수 있다.

다음과 같이 상속 관계가 형성이 되면,
```java
class Sartphone extends MobilePhone {...}
```
<br>

다음 인스턴스는 Smartphone 인스턴스인 동시에 MobilePhone 인스턴스가 된다.<br>
(이는 스마트폰을 가리키며 모바일폰이다. 라고 말할 수 있는 것과 이치가 같다.)

```java
new SmartPhone("010-555-666","Nougat");
//스마트폰 인스턴스이면서 동시에 모바일폰 인스턴스
```
<br>

따라서 위에 말한것처럼
```java
SmartPhone phone = new SmartPhone("010-555-777", "Nougat");
MobilePhone phone = new SmartPhone("010-555-777", "Nougat");
```
SmartPhone 인스턴스를 참조하는 변수를 선언하는 두 가지 방법이 가능하다.

### _지금까지 설명한 것을 예제를 통해 알아보자_
```java
//Overriding_Exam01.class 

class MobilePhone{
	protected String number;// 전화번호
	
	public MobilePhone(String number) {
		this.number  = number;
	}
	
	public void answers() {
		System.out.println("Hi ~ from " + number);
	}
}

//모바일폰을 상속받는 하위클래스 스마트폰
class SmartPhone extends MobilePhone{
	private String androidVer;// 안드로이드 운영체제 네임(버전)

	public SmartPhone(String number, String ver) {
		super(number);
		this.androidVer = ver;
	}
	public void playApp() {
		System.out.println("App is running in " + androidVer);
	}
}
class OverridingTest{
    public static void main(String[] args) {
		SmartPhone ph1 = new SmartPhone("010-111-222", "Andro01");
		MobilePhone ph2 = new SmartPhone("010-444-333", "Andro02");
		
		ph1.answers();
		ph1.playApp();
		
		ph2.answers();
		//ph2.playApp();
	}
}
```

위 예제에서는 다음과 같이 인스턴스를 생성하였다.
```java
MobilePhone phone = new SmartPhone("010-555-777", "Nougat");
```
<br>

그리고 다음과 같이 mobilePhone 클래스에 정의된 메소드를 호출하는데 이는 당연히 가능한 일이다.
```java
ph2.answer();
```
<br>

그러나 다음과 같이 SmartPhone 클래스에 정의된 메소드의 호출은 불가능하다. 참조변수 ph2가 실제 참조 하는 인스턴스가 SmartPhone 인스턴스이지만 불가능하다.
```java
ph2.playApp(); // 스마트폰 클래스에서 정의한 메소드
```
<br>

참조변수 ph2는 MobilePhone형 참조변수이다. 이러한 경우 ph2를 통해서 접근이 가능한 멤버는 MobilePhone 클래스에 정의되었거나 이 클래스가 상속하는 클래스의 멤버로 제한된다.(ph2가 참조하는 인스턴스가 무엇인지는 상관이 없다)

지금 설명한 이 내용이 비합리적이라고 생각할 수 있다. 참조변수의 형에 상관없이, 참조하는 인스턴스에 따라서 접근가능한 멤버가 결정되어야 한다고 생각할 수 있다. 그러나 그렇게 설계하지 않은 이유가 두 가지 있는데 그중 하나는 다음과 같다.
- _실행 시간을 늦추는 결과로 이어질 수 있습니다_

자바는 메소드 호출 시 참조변수의 형을 참조 하여 그 메소드 호출이 옳은 것인지 판단한다.예를 들면 다음과 같다.(다음과 같이 컴파일러가 판단하고 컴파일을 한다)

```java
ph2.answer();
//ph2가 MobilePhone형이므로 MobilePhone 클래스의 메소드 answer은 호출가능하다.
```
<br>

이러한 형태의 판단은 그 속도가 빠르다.(컴파일 단계에서 쉽게 판단 가능하다) 그러나 실제 참조하는 인스턴스를 대상으로 메소드의 호출 가능성을 판단하는 일은 간단하지 않다. 참조하는 인스턴스의 종류는 코드의 흐름에 따라 얼마든지 달라질 수 있기 때문이다.

그런데 이러한 단점도 감수할 만한 가치가 있다면 감수했을 것이다. 그러나 이어서 언급하는 두 번째 이유는 이러한 단점을 감수할 필요가 없다는 결론을 내리게 한다. 
- _참조변수의 타입을 기준으로 접근 가능한 멤버를 제한하는 것은 코드를 단순하게 한다._

단점이 많은 일부 기능을 제한함으로써 단순하고 명료한 코드의 작성을 유도하는 언어가 좋은 언어이다. 그런 측면에서 참조변수의 타입을 기준으로 접근 가능한 멤버를 제한한 것은 의미가 있는 일이다.
<br>

## 업캐스팅(Up Casting)
업캐스팅이란 서브 클래스의 객체가 수퍼 클래스 타입으로 형변환되는 것을 말한다.

다음과 같이 상속 관계를 맺은 세 클래스가 존재한다고 가정하자.
```java
class Cake{
    public void sweet(){...}
}

class CheeseCake extends Cake{
    public void milky(){...}
}

class StrawberryCheeseCake extends CheeseCake{
    public void sour(){...}
}
```
<br>
이때 StrawberryCheeseCake 인스턴스는 다음과 같이 말할 수 있다.
- _StrawberryCheeseCake 인스턴스는 CheeseCake 인스턴스이면서 Cake 인스턴스 이다._

따라서 다음과 같이 인스턴스를 참조할 수 있다. 
```java
Cake cake1 = new StrawberryCheeseCake();//업캐스팅
CheeseCake cake2 = new StrawberryCheeseCake();//업캐스팅
```
<br>
그러나 Cake형 참조변수 cake1을 통해서 호출할 수 있는 메소드는 다음 한 가지이다.

```java
cake1.sweet();
//Cake에 정의된 메소드 호출
```
<br>
그리고 CheeseCake형 참조변수 cake2를 통해서 호출할 수 있는 메소드는 다음 두 가지이다.

```java
cake2.sweet();
//Cake에 정의된 메소드 호출
cake2.milky();
//CheeseCake에 정의된 메소드 호출
```
<br>
이렇듯 참조변수가 참조하는 인스턴스의 종류에 상관없이, 참조변수의 타입에 해당하는 클래스와 그 클래스가 
상속하는 상위 클래스에 정의된 메소드들만 호출이 가능하다.