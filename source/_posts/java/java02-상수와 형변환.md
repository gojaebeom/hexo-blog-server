---
title: JAVA - 02. 상수와 형변환
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
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

### 상수의 특징 
자바의 일반적인 상수는 변수를 선언할 때 final이라는 선언을 추가하면 그 변수는 '상수'가 된다. 그리고 상수는 다음과 같은 특징이 있다. 
- 값을 딱 한 번만 할당할 수 있다.
- 한 번 할당된 값은 변경이 불가능하다.
<!-- more -->

다음 예제를 보자
```java
public static void mina(String[] args) {
    
    final int MAX_SIZE = 100;
    final char CONST_CHAR = '상';
    final int CONST_ASSIGNED; 
    CONST_ASSIGNED = 12; //할당하지 않았던 상수의 값 할당.
    
    System.out.println(MAX_SIZE);
    System.out.println(CONST_CHAR);
    System.out.println(CONST_ASSIGNED);
}
```
위의 예제에서는 다음과 같이 변수의 선언에 final을 추가하였다. 따라서 이 변수는 값의 변경이 불가능한 상수가 된다. CONST_ASSIGNED처럼 선언만해놓았다면 딱 한번 값을 할당할 수 있다. 물론 그이후로는 불가능 하다.

**상수의_관례**
그리고 위와같이 관례상 상수의 이름은 다음 두가지 사항을 지켜서 짓는다.
- 상수의 이름은 모두 대문자로 짓는다.
- 이름이 둘 이상의 단어로 이뤄질 경우 단어 사이에 언더바를 넣는다.
		
## 리터럴 상수에 대한 이해
다음 예제를 보자
```java
int num = 157;
```
대입연산자의 오른편에 위치한 숫자 157을 리터럴 또는 리터럴 상수 라고한다. 컴파일러는 위 변수에 대입한 숫자 157을 무엇으로 인식할까?   결론은 int형 정수로 인식한다. 다음 예제를 통해 좀더 이해를 도와보겠다.
```java
public static void main(String[] args){
    long num = 3146234266;
}
```
에러처리가 나서 주석처리를 하였다. 

_The literal 3146234266 of type int is out of range_

라는  에러가 뜨는 것을 확인하였다. 숫자 3146234266 는 int형 정수여야하는데 값이 너무크다라고 한다. 이게 이해가 가지 않는다 당연히 큰숫자인것을 알고있기때문에 일부러 int가 아닌 long자료형의 변수에 값을 할당했는데 이런 오류가 나다니..

위에서도 언급하지만, 왼편에 있는 변수의 자료형에 상관없이 정수는 int형으로 표현하기로 약속되어있다. 그래서 위와같은 오류 메시지가 발생하는 것이다. 그렇다면 long형 변수에 다음과같은 큰 값을 어떻게 저장할 수 있을까?

### 형 변환
**자동 형변환**
다음 예제를 보자
```java
public static void main(String[] args) {
	int num1 = 50;
	long num2 = 3147483647L;
	System.out.println(num1 + num2);
}
```
위의 상황에서는 int형 변수에 담긴 값을 long형으로 변환해야 데이터의 손실 없이 연산이 가능하다. 따라서 다음의 과정을 거쳐서 연산을 마무리한다.
- 변수 num1에 저장된 값을 long형으로 변환하여 메모리에 임시 저장한다.
- 이어서 이 변환된 값과 num2에 저장된 값을 대상으로 덧셈을 진행한다.

이러한 일련의 과정을 가리켜 '자료형 변환' 또는 줄여서 '형 변환' 이라고 한다. 그리고 위의 예제의 특징으로 자동 형 변환 이라고 한다.  프로그래머가 명시한 형 변환이 아니고 필요한 상황에서 자동으로 형 변환이 일어났기 때문이다. 이렇듯 형 변환이 필요한 상황에서는 다음 두 규칙에 근거하여 자동으로 형 변환이 일어난다.

**자동 형변환 규칙**
1. 자료형의 크기가 큰 방향으로 형 변환이 일어난다.
2. 자료형의 크기에 상관없이 정수 자료형보다 실수 자료형이 우선한다.
 
byte -> short -> int && char -> long -> float -> double
 		 	       
**자동 형변환의 예**
```java
double num3 = 30; //int형 정수 30은 double형으로 자동 형 변환 한다.
System.out.println(60L + 34.5); //long형 정수 60L은 double형으로 자동 형 변환 한다.
```

**명시적 형변환**
자동형변환의 특징을 봤을땐 

byte -> short -> int && char -> long -> float -> double

의 특징을 가지고있었다. 그럼 거꾸로 실수에서 정수형으로 형변환을 하려고하는 예제를 보자.
```java
public static void main(String[] args) {
		
    double pi = 3.1415;
    //int wholeNumber = pi; double형의 pi를 int형 wholeNumer에 할당하려 하자 에러가난다. 이것을 명시적으로 형변환하면 아래와 같다.
    int wholeNumer = (int)pi; 
    
    //이전 예제였던 short의 합 명시적 형변환으로 해결
    short num1 = 10;
    short num2 = 20;
    short num3 = (short) (num1+ num2);
}
```
위의 문장에 10번째 줄에 소괄호가 두번 등장하였다. 하나는 num1과 num2의 덧셈연산을 묶을 목적으로, 또 하나는 형 변환을 목적으로 등장하였다.      이중에서 형 변환에서 사용된 소괄호는 연산자로 분류한다. 반면에 묶거나 구분하는 목적으로 사용이 되는 소괄호는 '구분자'라 하여 그 성격이 연산자와 다르다.

> 본 문서는 책의 일부 내용을 발췌한 것으로서 온오프라인 상의 무단 배포를 금합니다.


