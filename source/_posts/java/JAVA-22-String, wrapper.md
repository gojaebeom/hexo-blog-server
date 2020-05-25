---
title: JAVA - 22. String, Wrapper 클래스
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/thumbnail.png?raw=true
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
  - type: bgm
    position: right
sidebar:
  right:
    sticky: true
---

## String 클래스
자바에서 문자열을 사용하기 위해 기본적으로 String 클래스라는 것을 재공한다. 선언 방법은 다음과 같다.<!-- more -->

### String 사용하기
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

  String str3 = "hello"; // 상수 풀에 있는 문자열을 가리킴
  String str4 = "hello"; // 상수 풀에 있는 문자열을 가리킴

  System.out.println(str1 == str2); //false
  System.out.println(str3 == str4); //true
}
```
위의 `str1`,`str2`은 서로 다른 인스턴스를 참조하기때문에 `false`라는 값이 출력되고 `str3`,`str4`는 상수 풀에 있는 같은 값을 가리키기 때문에 `true`가 출력되었다. 상수풀은 [상수와 형변환](https://gojaebeom.github.io/2020/04/22/java/JAVA-03-%EC%83%81%EC%88%98%EC%99%80%20%ED%98%95%EB%B3%80%ED%99%98/) 편에서 한번 다룬적이 있다.

위의 코드는 다음과 같은 이미지로 비유될 수 있다.

![이미지](https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/string.png?raw=true)

### String의 불변성
String 객체가 하나 생성되면, 그 값은 길어지거나 줄어들 수 없으며, 그 문자들 중 어떤 것도 바뀔 수 없다. 그래서 String 객체는 변경불능(immutable)이라고 한다. 예제를 보자.

```java
public static void main(String[] args){
  String hello = new String("hello");
  String world = new String("world");

  System.out.println(System.identityHashCode(hello)); //2036958521
  hello = hello.concat(world);
  System.out.println(System.identityHashCode(hello)); //1945604815
}
```
처음 참조변수 `hello`의 주소값을 출력할때와 이후 `concat` 메소드를 통해 참조변수 `world`를 연결하고 주소값을 출력할때의 값이 각각 다르다.(여기서 `identityHashCode`라는 System클래스의 메소드는 객체가 메모리에서 가진 해쉬 주소값을 출력한다)

String 클래스는 처음 생성한 값의 변경이 불가능하다. 대신 `concat`이나 `+`로 연결하는 등 변화를 주게 되면 그 문자열은 다른 공간에 새로 생성이되고 참조변수는 그 주소를 가리키게 되는 것 뿐이다. 

위의 방법은 메모리의 공간을 새로 참조하면서 낭비를 유발하기때문에 다음과 같은 상황에서는 자바에서 제공하는 `StringBuffer` 또는 `StringBuilder` 클래스를 사용하는 것이 좋다. 

### StringBuffer, StringBuilder
두 클래스의 차이는 다음과 같다.
- StringBuffer는 멀티 쓰레드프로그래밍에서 동기화가 보장된다.
- 단일 쓰레드 프로그래밍에서는 StringBuilder를 사용하는것이 더 좋다.

아직 쓰레드를 배우지 않았기에 이런 특징이 있다고만 이해하고 넘어가는게 좋을것 같다.

```java
//buffer 사용예제
public static void main(String[] args){
  StringBuffer buff = new StringBuffer("hello");
  buff.append(" world");
  System.out.println(buff); //hello world
}
```

## Wrapper 클래스
프로그램에 따라 기본 타입의 데이터를 객체로 취급해야 하는 경우가 있다. 예를 들어, 메소드의 인수로 객체 타입만이 요구되면, 기본 타입의 데이터를 그대로 사용할 수는 없다. 이때에는 기본 타입의 데이터를 먼저 객체로 변환한 후 작업을 수행해야 한다.

 
이렇게 8개의 기본 타입에 해당하는 데이터를 객체로 포장해 주는 클래스를 래퍼 클래스(Wrapper class)라고 한다. 래퍼 클래스는 각각의 타입에 해당하는 데이터를 인수로 전달받아, 해당 값을 가지는 객체로 만들어 준다. 이러한 래퍼 클래스는 모두 java.lang 패키지에 포함되어 제공이된다.

자바의 기본 타입에 대응하여 제공하고 있는 래퍼 클래스는 다음과 같다.

|기본형 타입|wrapper class| 
|---------|:-------- :|
| boolean | Boolean |
| char    | Charter |
| byte    | Byte    |
| short   | Short   |
| int     | Integer |
| long    | Long    |
| float   | Float   |
| double  | Double  | 
| void    | Void    | 

> void 클래스는 실체화될 수 없으며 단지 공 참조 개념을 나타낸다.
