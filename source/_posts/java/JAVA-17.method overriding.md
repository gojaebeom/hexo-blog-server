---
title: JAVA - 17. 메소드 오버라이딩
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/thumbnail.png?raw=true
author: JaeBeom Go
date: 2020-05-02 21:20:00
tags:
  - 자바
  - 상속
  - 메소드 오버라이딩
  - method overriding
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

## 메소드 오버라이딩(Method Overriding)이란?
상위 클래스에 정의된 메소드를 하위 클래스에서 다시 정의하는 행위를 가리켜 '메소드 오버라이딩' 이라 하는데, 여기서 말하는 오버라이딩은 '무효화 시키다'의 뜻으로 해석이 된다. <!-- more -->

다음 예제를 통해 메소드 오버라이딩의 결과를 확인해보자.
```java
class Cake{
	public void yummy() {
		System.out.println("Yummy Cake");
	}
}

class CheeseCake extends Cake{
	public void yummy() {// Cake의 Yummy 메소드를 오버라이딩 함
		System.out.println("Yummy Cheese Cake");
	}
}

public class YummyCakeOverriding {
	public static void main(String[] args) {
		Cake c1 = new CheeseCake();
		CheeseCake c2 = new CheeseCake();
		
		c1.yummy(); //오버라이딩 한 CheeseCake의 Yummy 메소드가 호출됨
		c2.yummy(); //오버라이딩 한 CheeseCake의 Yummy 메소드가 호출됨
	}
}
```
  실행 결과 : Yummy Cheese Cake가 두번 출력 되는 것을 알 수 있다.

위의 CheeseCake 클래스는 Cake를 상속하면서, Cake에 정의된 yummy메소드와 다음 세 가지가 같은 메소드를 정의하였다.
- 메소드의 이름
- 메소드의 반환형
- 메소드의 매개변수 선언

위의 세가지가 같아야 메소드 오버라이딩이 성립한다.

즉 Cake의 yummy 메소드를 CheeseCake의 Yummy 메소드가 오버라이딩 하였다. 그리고 오버라이딩을 하면, 참조변수의 형에 상관없이 오버라이딩 한 메소드가 오버라이딩된 메소드를 대신하게 된다. 

위의 예제의 main 메소드에서 다음과 같이 Cake 형 참조변수로 CheeseCake 인스턴스를 참조하였다.
```java
Cake c1 = new CheeseCake();//업캐스팅
```

그리고 다음과 같이 yummy 메소드를 호출하였다.
```java
c1.yummy();
```

앞서 설명한 바에 의하면 c1은 Cake형 참조변수이니, 위 문장의 경우 Cake의 yummy 메소드가 호출되어야 한다. CheeseCake 인스턴스를 참조하고 있는 상황이라도 말이다. 그러나 Cake의 yummy 메소드는 오버라이딩 되었다(무효화 되었다). 따라서 이 경우에는 CheeseCake의 yummy 메소드가 대신 호출이 된다.

## 메소드 오버라이딩의 일반화
앞서 설명한 메소드 오버라이딩을 문법적으로 정리하기 위해서 클래스를 다음과 같이 정의하였다.
```java
class Cake{
  public void yummy(){...}
}
class CheeseCake extends Cake{
  public void yummy(){...}
}
class StrawberryCheeseCake extends CheeseCake{
  public void yummy(){...}
}
```

위와 같이 클래스를 정의한 경우 CheeseCake의 참조변수와 인스턴스의 생성문을 다음과 같이 구성할 수 있다.
```java
Cake c1 = new StrawberryCheeseCake();
CheeseCake c2 = new StrawberryCheeseCake();
StrawberryCheeseCake c3 = new StrawberryCheeseCake();
```

그리고 다음 세 문장이 실행되었을 때 호출되는 메소드는 StrawberryCheeseCake의 yummy 메소드이다.
```java
c1.yummy(); //StrawberryCheeseCake의 yummy 메소드 호출
c2.yummy(); //StrawberryCheeseCake의 yummy 메소드 호출
c3.yummy(); //StrawberryCheeseCake의 yummy 메소드 호출
```

## 오버라이딩된 메소드를 호출하는 방법
위의 예제들에서도 알 수 있듯이 Cake, CheeseCake에 정의된 yummy 메소드들을 위의 방법처럼 호출하는 것은 불가능하다.

하지만 클래스 외부가 아닌 내부에서 Cake의 yummy 메소드를 호출하는 방법은 있다. 다음 예제를 살펴보자.

```java
package ch11_상속;
//오버라이딩 된 메소드를 호출하는 방법 예제

class Cake{
	public void yummy() {
		System.out.println("Yummy Cake");
	}
}

class CheeseCake extends Cake{
	public void yummy() {
		super.yummy();
		System.out.println("Yummy CheeseCake");
	}
}

public class YummyCakeSuper {
	public static void main(String[] args) {
		CheeseCake cake = new CheeseCake();
		cake.yummy();
	}
}
```
지금까지는 상위 클래스의 생성자를 호출할 목적으로 키워드 super를 사용하였다. 그런데 위의 예제에서 보이듯이 상위 클래스에 정의된, 오버라이딩 된 메소드의 호출을 목적으로도 super가 사용될 수 있다.

## Object 클래스
클래스를 정의할 때 어떤 클래스도 상속하지 않으면 해당 클래스는 java.lang 패키지에 묶여 있는 Object 클래스를 상속하게 된다.
```java
class MyClass {...}

class MyClass extends Object {...}
```
두 클래스의 정의는 동일하다.

물론 위의 설명에도 언급했듯이 상속하는 클래스가 있는 경우에는 Object 클래스를 상속하지 않는다.
```java
class MyClass extends OtherClass {...} 
```

그러나 이 경우에도 OtherClass 또는 OtherClass가 상속하는 클래스가 Object 클래스를 상속한다. 결국 자바의 모든 클래스는 Object 클래스를 직접 혹은 간접적으로 상속하게 되어있다. 그렇다면 자바의 모든 클래스는 Object 클래스를 상속하도록 한 이유는 무엇일까?

이는 자바의 모든 인스턴스에 공통된 기준 및 규약을 적용하기 위함이다. 한 예로 자바의 모든 인스턴스는 다음 메소드의 인자로 전달될 수 있다.

```java
public void println(Object x) // System.out.println 메소드
```
위 메소드의 매개변수 형이 Object이다. 따라서 자바의 모든 인스턴스는 위 메소드의 인자가 될 수 있다. 그리고 위의 메소드는 인자로 전달된 인스턴스의 다음 메소드를 호출한다. 이 메소드는 Object 클래스에 정의되어 있는 메소드이므로 모든 인스턴스를 대상으로 호출이 가능하다.

이 블로그엔 포스팅하지 않았지만 글쓴이의 github 에 [String 클래스 예제](https://github.com/gojaebeom/java_tutorial)에 대해 다루었다.(목차에서 String 클래스 부분의 글들을 찾아보면 된다) 

이 예제에서 클래스를 정의하면서 toString 메소드를 정의한 바 있다. 그런데 사실 이것은 Object 클래스의 toString 메소드를 오버라이딩 한 것 이다. 이와 관련해서 다음 예제를 살펴보자.

```java
class Bread{
	
	//오브젝트 클래스의 toString 메소드를 오버라이딩
	public String toString() {
		System.out.println(super.toString());
		return "My Bread";
	}
}

class CreamBread extends Bread{
	
	//Bread 클래스의 toString 메소드를 오버라이딩
	public String toString() {
		
		return "my CreamBread";
	}
}

public class OverridingToString {
	public static void main(String[] args) {
		Bread b1 = new Bread();
		Bread b2 = new CreamBread();
		
		//b1이 참조하는 인스턴스의 toString 메소드 호출로 이어짐
		System.out.println(b1);
		
		//b2가 참조하는 인스턴스의 toString 메소드 호출로 이어짐
		System.out.println(b2);
	}
}
```

## 클래스와 메소드의 final 선언
클래스를 정의하는데 있어서 해당 클래스를 다른 클래스가 상속하는 것을 원치 않는다면, 다음과 같이 final 선언을 추가하면 된다.
```java
public final class MyClass{...} //MyClass 는 다른 클래스가 상속 할 수 없음
```

대표적인 final 클래스로 String 클래스가 있다. 따라서 우리는 String 클래스를 상속할 수 없다. 또한 다음과 같이 메소드의 정의에 final 선언을 추가하여 해당 메소드의 오버라이딩을 허용하지 않을 수 도 있다.

```java
public final void func(){...}
```

## @Override
자바 5에서 '어노테이션(Annotations)'이라는 것이 소개되었다. 그리고 이와 관련하여 이후에 별도로 설명을 하겠다. 그러나 상속, 정확히는 메소드 오버라이딩과 관련 있는 내용이 있어 이에 대한 부분만 먼저 소개하고자 한다. 다음 예제를 보자. 이 예제는 컴파일도 되고 실행도 잘 된다. 그러나 프로그래머의 실수가 일부 포함되어 있다. 그 실수가 무엇인지찾아보자.

```java
class ParentAdder{
	public int add(int a, int b) {
		
		return a + b;
	}
}

class ChildAdder extends ParentAdder{
	
	// 상위 클래스의 add를 오버라이딩 하려고 합니다.
	public double add(double a, double b) {
		return a + b;
	}
}

public class OverrideMistake {
	public static void main(String[] args) {
		ParentAdder adder = new ChildAdder();
		System.out.println(adder.add(3, 4));
	}
}
```

클래스 ChildAdder 는 ParentAdder를 상속한다. 그리고 ParentAdder의 add를 오버라이딩 할 의도였음을 주석을 통해 알 수 있다. 그러나 부모 메소드와 매개변수 타입과 반환형이 달랐기 때문이다. 이러한 유형의 실수는 매우 흔하다. 그럼에도 불구하고 발견이 쉽지 않기 때문에 치명적인 실수가 될 수 있다. 제일 좋은 것은 컴파일 과정에서 실수가 확인되는 것이다. 그러나 이 경우 문법적으로는 오류가 없기 때문에 컴파일도 되고 실행도 된다.

이러한 상황을 방지하기 위해서 '어노테이션' 이라는 것을 사용할 수 있다. 어노테이션은 일종의 메모이다. 그것도 '자바 컴파일러에게 메시지를 전달하는 목적의 메모'이다. ChildAdder 클래스를 설계하는 과정에서 add 메소드가 ParentAdder의 add 메소드를 오버라이딩 할 의도였다면 다음과 같이 메모를 달아준다.

```java 
class ChildAdder extends ParentAdder{
	
	// 상위 클래스의 add를 오버라이딩 하려고 합니다.
    @Override
	public double add(double a, double b) {
		return a + b;
	}
}
```

위와같이 어노테이션을 정의하면 컴파일러는 오버라이딩이 제대로 되었는지 확인을 하고, 프로그래머의 의도대로 오버라이딩이 되지 않았다면 컴파일 단계에서 에러를 전달해준다.

메소드를 오버라이딩 해야 한다면, 이렇듯 어노테이션을 사용하여 컴파일 과정에서 확인되지 않는 오류의 발생을 차단하는 것이 좋다.