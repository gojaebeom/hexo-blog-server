---
title: JAVA - 03. 상수와 형변환
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/java-thumbnail.jpg?raw=true
date: 2020-04-22 16:22:00
tags: 
- java
- 상수
- 형변환
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

## 상수(Constant)란?
- 변하지 않는 수를 말한다. <!-- more -->

## 상수 선언
자바의 일반적인 상수는 변수를 선언할 때 final이라는 선언을 추가하면 그 변수는 '상수'가 된다. 그리고 상수는 다음과 같은 특징이 있다. 
- 값을 딱 한 번만 할당할 수 있다.
- 한 번 할당된 값은 변경이 불가능하다.

```java
// tip.상수의 선언
final int NUM;

// tip.선언된 상수에 값 할당
NUM = 10;

// tip.그 이후로 값의 변경은 불가능하다
NUM = 5; // 에러

// tip.변수와 마찬가지로 선언과 동시에 초기화가 가능하다.
final int FINAL_NUMBER = 10;
```

**상수의 관례**
그리고 위와같이 관례상 상수의 이름은 다음 두가지 사항을 지켜서 짓는다.
- 상수의 이름은 모두 대문자로 짓는다.
- 이름이 둘 이상의 단어로 이뤄질 경우 단어 사이에 언더바를 넣는다.

## 리터럴(literal)
프로그램에서 사용하는 모든 숫자, 문자, 논리 값 등을 가리켜 리터럴이라고 한다. 모든 리터럴(리터럴 상수라고도 한다)들은 상수 풀(Constant Pool)이라는 곳에 저장되어 있다.
```java
int num = 100; //right value에 해당하는 100이 리터럴이다.
char ch = 'A'; //마찬가지로 A도 리터럴 이다.
```

**리터럴(숫자, 문자, 논리 값) --로딩--> Constant Pool(10, 'A', true) --대입, 복사--> 변수**

## 형변환
서로 다른 자료형의 값이 대입이 되는 경우 형변환이 일어난다.

**byte -> short -> int && char -> long -> float -> double**

일반적으로 위와 같이 화살표의 방향대로 대입이 되면 묵시적인 형변환이 일어나고 아닐 경우 직접 명시적인 형변환을 해주어야 한다.

### 묵시적 형 변환(Implicit Type Conversion)
- 작은 수에서 큰 수로 대입
- 덜 정밀한 수에서 더 정밀한 수로 대입(정수에서 실수)

```java
//ImplicitConterSionTest.java
public static void main(String[] args) {
  //정수
  byte bNum = 10;
  short sNum = bNum;
  int iNum = sNum;
  long lNum = iNum;

  //실수
  float fNum = lNum;
  double dNum = fNum;
}
```
위의 예제처럼 크기가 작은 수에서 큰 타입 순서로 대입을 할경우 자동적인 형변환이 일어난다.

### 명시적 형 변환(Explicit Type Conversion)
- 변환되는 자료형을 명시(타입 캐스팅)
  - 이에 따른 자료의 손실이 발생할 수 있다.

```java
//ExplicitConterSionTest.java
public static void main(String[] args) {
  // 예제 1
  int iNum = 1000;
  byte bNum = (byte)iNum;
  //형변환을 억지로 하면 데이터 손실을 불러올 수 있다.
  System.out.println(bNum);//-24

  // 예제 2
  double dNum = 1.2;
  float fNum = 0.9F;

  int iNum1 = (int)dNum + (int)fNum; //1
  int iNum2 = (int)(dNum + fNum); //2

  System.out.println(iNum1);
  System.out.println(iNum2);
}
```
예제 1은 int형 변수에 1000의 값을 할당하였다. 그리고 byte에게 대입하려고 한다. 하지만 byte는 int보다 크기가 작음으로 `(byte)` 와같이 프로그래머가 직접 byte형으로 변환 하겠다고 명시해주어야한다. 그리고 명시적인 형변환을 하게 되면 데이터가 손실될 수 도 있다. 예제 1의 경우 byte가 담을 수 있는 크기를 초과하여 값이 잘려 -24가 출력 되는 것을 알 수 있다.

예제 2의 핵심은 두개의 실수를 더하여 정수형 변수에 대입하려고 하는 것 이다. `iNum1`의 경우엔 각 `dNum`, `fNum` 의 값을 형변환 하고 연산을 진행한다. 즉 각자의 값은 소숫점이 잘려나가 1, 0이된다. 결국 1+0의 연산을 통해 1이라는 값이 `iNum1`에 대입이 된다. `iNum2`의 경우 먼저 변수의 값이 연산을 진행 한 이후 타입캐스팅이 일어난다 1.2 + 0.9 = 2.1이 되고 그 이후 소숫점이 잘려 2라는 값이 대입이 되는 것을 알 수 있다. 이것은 이 다음에 다룰 연산자에서 연산 우선순위를 통해 알 수 있다.

> 본 문서는 책의 일부 내용을 발췌한 것으로서 온오프라인 상의 무단 배포를 금합니다.


