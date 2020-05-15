---
title: JAVA - 02. 변수와 자료형
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/java-thumbnail.jpg?raw=true
date: 2020-04-21 19:25:00
tags: 
- java
- java 변수
- 식별자
- 자료형
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
## 변수(Variable)란?
- 변수란 데이터의 저장과 참조를 위해 '할당된 메모리 공간' 에 붙인 이름을 말한다. <!-- more -->
- 변하는 값을 프로그램에서 나타내는 방법

## 변수 선언
변수를 선언하는 것은 해당 자료형의 크기만큼의 메모리를 사용하겠다는 뜻 이다. 메모리의 위치를 변수명으로 참조한다.

변수는 다음과 같은 방식으로 선언할 수 있다.

```java
[자료형] [변수명];
//example
int number;

// tip.선언 이후 값을 할당하는 방법은 다음과 같이 할 수 있다.
number = 10;

// tip.선언과 동시에 값을 할당할 수 있는데, 이것을 `선언 및 초기화` 라고 한다.
int age = 26; 

// tip.선언 되어있는 변수 이름과 이름이 중복될 수 없다.(변수의 스코프에 한함)
int age; // 에러

// tip.만약 변수를 선언만 하고 값을 할당하지 않았다면 사용될 수 없다.
int testNum;
System.out.println(testNum); // 에러

// tip.동일한 자료형에 한해서 다수의 선언이 가능하다.
int number1, number2, number3;

// tip.다수의 선언과 동시에 값의 할당도 가능하다.
int number4 = 10, number5 = 20;
```

### 식별자 규칙
자바는 대소문자를 구분한다. 따라서 Num1 과 num1은 서로 다른 이름으로 인식된다. 때문에 자료형 int를 대신하여 INT를 사용할 수 없고 변수의 이름을 짓는데 다음과 같은 제약사항이 존재한다.

- 영문자나 숫자를 사용한다. 단 숫자로 시작할 수 없다.
- 특수문자중에서는 _와 $를 사용할 수 있다.(보통 사용할 경우 변수명 앞에 붙인다)
- 예약어는 사용할 수 없다.(ex> int, double, char..)
- 변수는 그 쓰임에 맞는 이름으로 만드는 것이 가독성에 좋다.

### 일반적인 관례
- 변수는 소문자의 명사를 사용
- 클래스 이름은 대문자의 명사를 사용
- 메서드 이름은 소문자의 동사를 사용
- 두단어 이상 사용할 경우 카멜 케이스(Camel Case)로 표기(ex> helloWorld, intNum..)
- 상수는 대문자의 명사(두 단어 이상 사용할 경우 _(언더바)로 연결)

## 자료형
앞서 int 라는 키워드를 사용하여 변수를 만들었는데, 이러한 키워드를 가리켜 **자료형** 이라고 한다. 그리고 자바에서는 다양한 자료형을 제공한다. 자바의 자료형은 크게 기본형(primitive type)과 참조형(referene type)으로 나뉜다.

**기본형(primitive type)**
- 자바언어에서 기본적으로 제공해주는 자료형
- 메모리의 크기가 정해져있다.
- 정수, 실수, 문자, 논리 형이 있다.

**참조형(referene type)**
- JDK(java development kit)에서 제공되는 클래스와 프로그래머가 정의하는 클래스
- 클래스에 따라 사용되는 크기가 다르다.
- String, 그리고 사용자가 만든 클래스 등이 포함된다.

### 기본 자료형 종류
|  자료형 |  데이터   |  크기   | 표현 가능 범위 |
|---------|:-------- :|-------:|:-------------:|
| boolean | 참과 거짓 | 1바이트 | true, false
| char    | 문자      | 2바이트 | 유니코드 문자
| byte    | 정수      | 1바이트 | -128~127
| short   | 정수      | 2바이트 | -32,768~32,767
| int     | 정수      | 4바이트 | -2,147,483,648 ~ 2,147,483,647
| long    | 정수      | 8바이트 | -9,223,372,036,854,775,808 ~ 엄청크다..
| float   | 실수      | 4바이트 | 단정도 실수형 (유효 자리는 7 정도임)
| double  | 실수      | 8바이트 | 배정도 실수형 (유효 자리는 15정도)
<br> 

### 정수 자료형 
자바는 정수형 연산을 진행할 때 int형(4 byte)을 기본으로 한다.
```java
// IntegerTest.java
public static void main(String[] args){
  int iNum = 2147483648; //에러 , 2147483647까지 표현 가능
  long lNum = 2147483648;//에러
}
```
위의 예제의 두 코드들은 에러가 난다. int 형 변수 `iNum` 은 4byte에 초과되는 값을 담았기 때문에 에러가 나는것은 이해할 수 있다. 하지만 int형에 담을 수 없는 값이기에 long형 변수에 할당했는데도 오류가 나고있다.

위에 설명했듯이 자바는 정수형 연산을 4byte를 기본으로 하기때문에 위의 `long lNum = 2147483648` 코드의 숫자들을 4byte에 담으려고 하니 에러가 나는 것 이다. 이럴때 형변환 이라는 것을 해주어야 하는데 다음과 같이 해결할 수 있다.
```java
// IntegerTest.java
public static void main(String[] args){
  long num = 2147483648L;
}
```
뒤에 l 또는 L 을 붙여줌으로써 형변환할 수 있다. 형변환은 다른글에서 자세히 다루도록 하겠다.

### 실수 자료형
실수 자료형은 연산을 진행할 때 double형(8 byte)을 기본으로 한다.
```java
//DoubleTest.java
public static void main(String[] args){
  
  float fNum1 = 0.1; // 에러
  float fNum2 = 0.1F;
}
```
위의 경우와 비슷한 예제이다. 실수는 double을 기본으로 연산을 하기때문에 double보다 낮은 float에 값을 할당 시 위 예제와 같이 f 또는 F를 값 뒤에 붙여 주어야 한다.

*자바에서 정수형은 주로 int가 많이 사용이되고 실수형은 double이 많이 사용된다.*

### 문자 자료형
- 내부적으로는 비트의 조합으로 표현된다.
- 인코딩 -> 각 문자에 따른 특징인 숫자 값(코드 값)을 부여
- 디코딩 -> 숫자값을 원래 문자로 반환

```java
// CharacterTest.java
public static void main(String[] srg) {
  char ch = 'A';
  System.out.println(ch); //A
  System.out.println((int)ch); //65

  int iCh = 66;
  System.out.println(iCh); //66
  System.out.println((char)iCh); //B

  //char ch2 = -66; 음수값은 들어갈 수 없음

  char hangle1 = '\uAC00'; //유니코드 넣는 방법
  System.out.println(hangle1);

  char hangle2 = '가'; //물론 이렇게 표현할 수 있다.
  System.out.println(hangle2);
}
```
문자의 표현에 대한 약속을 가리켜 ‘문자셋(Character Set)’ 이라고 한다. 이러한 문자 셋의 설계는 지역 및 국가별로 각각 이루어져 그 수가 다양하다. 때문에 데이터를 주고받거나 여러 국가의 언어를 동시에 표현하는 상황에서는 문제가 되는데, 그래서 모든 나라의 문자를 수용하여 전 세계적으로 사용할 수 있는 문자 셋을 설계하게 되었다. 이를 가리켜 ‘유니코드(Unicode)’라고 한다.

**문자 세트**
- 아스키 : 1byte로 영문자, 숫자, 특수문자등을 표현
- 유니코드 : 한글과 같은 복잡한 언어를 표현하기 위한 표준 인코딩 (UTF-8, UTF-16이 대표적이다)

### 논리 자료형
논리 자료형은 boolean이라는 키워드를 사용하여 선언한다. 1byte의 크기를 사용하며 보통 참과 거짓을 구분할 때 많이 사용된다.

```java
//BooleanTest.java
public static void main(String[] args){
  boolean isMarried = false;	
	System.out.println(isMarried);// fasle
}
```

