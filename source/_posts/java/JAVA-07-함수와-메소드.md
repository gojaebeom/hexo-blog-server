---
title: JAVA - 07. 함수와 메소드
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/java-thumbnail.jpg?raw=true
author: JaeBeom Go
date: 2020-04-27 19:10:00
tags:
  - 자바
  - 함수
  - 메소드
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
## 함수(Function)란?
프로그래밍에서 함수는 하나의 기능을 수행하는 코드의 단위이다.
<!-- more -->

이전의 객체지향 프로그래밍이 무엇인가 다루었을 때 객체의 속성은 변수, 기능은 메소드라고 하였다. 메소드와 함수는 무슨 차이일까? 

## 메소드(Method)란?
클래스 내부에서 클래스의 기능을 갖는 함수를 `메소드` 라 한다. 즉 함수가 좀더 포괄적인 개념이다. 하지만 서로 기능적인 차이는 거의 없다. 단지 자바 프로그래밍을 할 때 우리는 function 보다 method라는 단어를 더 많이 접하게 될 것이다.

### 메소드 정의하기
클래스를 정의할 때는 앞의 문자를 대문자로 하는 것이 일반적인 관례였다. 반대로 변수와 메소드명을 정의할 때는 소문자로 시작하고, 두 단어 이상이 사용되면 카멜케이스를 사용하는 것이 일반적인 관례이다. 

```java
//메소드 정의하기
반환형 메소드명 (매개변수){몸통}
        ˇˇˇ
void func(int x){...}
```
메소드는 위와 같이 반환형, 메소드명, 매개변수, 그리고 구현부로 이루어져있다. void는 반환값이 없을때 사용하는 키워드이다. 그리고 매개변수는 사용함에 따라 선언 유무는 상관이 없고, 다수의 변수를 선언해도 상관 없다. 

다음 예제를 보자. 
```java
//반환값이 없고 매개변수가 없는 메소드 정의
void func1(){...}

//반환값이 없고 매개변수가 하나 있는 메소드 정의
void func2(int a){...}

//반환값이 없고 매개변수가 두개 있는 메소드의 정의
void func3(int a, int b){...}

//물론 매개변수는 두개이상도 가능하다.
void func4(int a, int b, int c, int d){...}

//매개변수의 타입은 필요에 따라 원하는 타입으로 선언할 수 있다.
void func5(int a, String str, double d){...}
```

그리고 메소드의 기능을 실행한뒤에 결과 값을 다른곳으로 반환하고 싶다면 아래와 같이 할 수 있다.
```java
int addNum(){
  int num = 10;
  return num;
}
```
반환형에 int를 명시해줬기 때문에 return되는 값은 int형이여야 한다. 물론 다른형으로도 명시가 가능하다.

### 메소드의 return 
메소드의 return은 값을 반환함과 동시에 메소드를 종료시킴을 의미한다.

다음으로 매개변수를 받아 가공하여 반환 하는 메소드의 예제를 보자.
```java
int addNum(int a, int b){
	return a + b;
}
```
위 메소드는 매개변수로 두 정수 값을 받아 더해서 반환하는 함수이다. 그리고 위 예제들의 모든 함수들은 정의만 하였고 사용되지 않았다.

### 메소드 사용하기
메소드는 메소드의 이름으로 호출 할 수 있다.
```java
public static int addNum(int a, int b){
	return a + b;
}

public static void helloWorld(){
	System.out.println("Hello~ world");
}

public static void main(String[] args){
    helloWorld();
    
    int result = addNum(10, 20);
    System.out.println(result);
}
```
메소드의 반환형 앞에 붙은 public과 static은 신경쓰지말자. 이것은 이후에 배울 접근 제어자와, static을 통해 알 수 있다. 

이전에 클래스를 사용할 때도 main 메소드 내부에서 실행한 것을 알 수 있다. 이는 자바 프로그램이 main 이라는 이름의 메소드에서부터 시작하는것을 약속으로 한다.

위의 `addNum` 그리고 `helloworld` 메소드는 메인 메소드에서 호출하였다.

helloworld 메소드의 경우 내부적으로 println를 통해 문자열을 출력하는 일을 한다. 

addNum의 경우 int형 인자값을 두개 받기로 약속하였기 때문에 정수값 두개를 넘겨주고 내부에서 사칙연산을 수행 이후 값을 반환하고 있다. 그리고 반환값이 int형이기 때문에 int 타입의 변수에 값으로 할당할 수 있게 된다. 이후 그 값을 잘 출력하는 것을 볼 수 있다.

## 메소드와 메모리 스택(Stack)
이전 클래스의 인스턴트 부분에서 메모리 구조에 대해 간략하게 소개한 적이 있다. 인스턴스는 메모리의 힙이라는 곳에 생성된다고 하였다. 반대로 메소드나, 메소드 내부에서 사용되는 변수(지역변수)들은 스택이라는 곳에 저장된다.

### Last In First Out (LIFO)
*스택은 후입선출의 방법으로 메모리를 관리한다. 즉 나중에 들어온 값이 가장 먼저 나가게 되는 것 이다.*

예를 들어보자.
```java
public static void main(String[] args){
	func1();
    func2();
}

public static void func1(){...}

public static void func2(){...}
```

위 예제는 메인함수가 먼저 실행이되고 메인 함수에서 `func1` 과 `func2`함수를 차례대로 호출하고 있다. 

먼저 메인 메소드가 실행이 되면 다음과 같이 스택에 메인함수가 생성이 된다.
![스택 1](https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/%EC%8A%A4%ED%83%9D3.png?raw=true)

그리고 메인메서드가 func1 메소드를 호출한다.

![스택 2](https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/%EC%8A%A4%ED%83%9D1.png?raw=true)

위의 메소드는 내부적으로 기능을 완료하고 종료한다. 
![스택 1](https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/%EC%8A%A4%ED%83%9D3.png?raw=true)
그 이후 func2 메소드를 호출한다.
![스택 2](https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/%EC%8A%A4%ED%83%9D2.png?raw=true) 

메소드는 이와같이 후입선출의 개념으로 스택영역에 저장되고, 소멸하게 된다.