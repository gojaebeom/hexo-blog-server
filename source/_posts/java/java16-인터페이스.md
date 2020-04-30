---
title: JAVA - 16. 인터페이스 01
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
date: 2020-04-29 22:56:00
tags: 
- java
- 인터페이스
- interface
- 추상 메소드
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
클래스가 인터페이스를 상속하는 행위는 **상속** 이아닌 **구현(Implementation)** 이라 한다. 문법 관계는 상속과 동일하지만 본질은 구현이기 때문이다. 위의 예제에 클래스에서 인터페이스를 상속할때 extends 라는 키워드 대신 implements가 사용되어진 것을 볼 수 있다.

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
위와 같이 ExampleClass 의 인스턴스를 생성하고 참조변수에 할당하려고한다. 그렇다면 참조변수의 타입은 ExampleClass의 인스턴스(객체) 이기때문에 당연히 ExampleClass가 될 것 이다. 그리고 ExampleClass가 상속한 SuperExampleClass도 ExampleClass의 부모클래스이기때문에 ExampleClass의 참조변수 타입으로써 인스턴스 할당이 가능 한 것이다. (물론 자식 클래스에서 새로 구현된 메소드는 부모클래스형인 참조변수에서는 사용할 수 없다)

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

> 본 문서는 책의 일부 내용을 발췌한 것으로서 온오프라인 상의 무단 배포를 금합니다.
