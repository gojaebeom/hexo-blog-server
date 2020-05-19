---
title: JAVA - 04. 연산자
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/thumbnail.png?raw=true
date: 2020-04-22 17:16:00
tags: 
- java
- 연산자
- 자바 연산자
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
## 연산자란?
어떠한 기능 또는 어떤 대상체에 계산과 같은 처리를 수행하는 문자 또는 기호를 연산자라 한다. Java에서의 연산자는 크게 단항, 이항, 삼항, 대입 연산자로 나뉘며, 이항 연산자는 산술, 비교, 논리 연산자로 나뉠 수 있다.<!-- more -->

- 연산자(operator) : 어떠한 기능을 수행하는 기호 (+, -, *, / 등)
- 피연산자(operand) : 연산자의 작업 대상 (변수, 상수, 수식 등)

## 연산자의 종류
### 산술 연산자 (+, -, *, /, %)
우리가 평소에 자주 사용하는 연산이다.
```java
//사용 예제
int a = 10, b =20;
System.out.println(a + b); //더하기
System.out.println(a - b); //빼기
System.out.println(a * b); //곱하기
System.out.println(a / b); //나누기
System.out.println(a % b); //나눈 나머지
```

### 대입 연산자(=)
- 오른쪽에서 왼쪽으로 할당
- 변수끼리 할당 가능
- 변수에 값이 존재하더라도 다른 값을 할당하면 마지막 할당된 값이 할당
- 연산자중에 우선순위가 제일 낮다

```java
int a = 0, b = 1;
a = b; // 변수의 자료형이 같다면 할당 가능 : a 값이 1로 update
a = 20; // 당연히 자료형에 맞는 타입의 값이면 할당 가능
```

### 복합 대입 연산자(+=, -=, *=, /=, %=)
연산자와 대입 연산자를 결합한 연산 후 대입 연산

```java
//복합 대입 연산자

// +=
a += b; // a = a+b

// -=
a -= b; // a = a-b

// *=
a *= b; // a = a*b

// /=
a /= b; // a = a/b

// %=
a %= b; // a = a%b;

// &=
a &= b; // a = a&b;

// |=
a |= b; // a = a | b;

// ^=
a ^= b; // a = a ^ b;
```

### 형변환 연산자(`(DataType)`)
자동형변환의 경우 알아서 형변환이 일어나지만, 명시적으로 형변환을 필요로 할 때 사용가능하다.
```java
int iNum = 20;
short sNum = (short)iNum;

double dNum = 5.5;
float fNum = (float)dNum;
```

### 증감 연산자(++, - -)
- 증가 연산자(++) : 피연산자의 값을 1 증가시킨다.
- 감소 연산자(-­ -­) : 피연산자의 값을 1 감소시킨다.

증감연산자는 피연산자의 앞 또는 뒤에 붙일 수 있는데 그에따라 차이점을 보인다.
```java

//전위 형 : 값이 참조되기 전에 증가시키거나 감소시킨다.
int a = 0;
System.out.println(++a); //1

//후위 형 : 값이 참조되고 난 이후 증가시키거나 감소시킨다.
int b = 0;
System.out.println(b++); //0

//이 이후에 값이 증가 된상태
System.out.println(b); //1
```

### 비교 연산자(>, >=, <, <=, ==, !=, instanceof)
비교 연산자는 제어문의 조건문이나 반복문에 자주 쓰인다.
```java
//사용 예시
int a = 0 , b = 1;
if(a < b) // a 보다 b가 크다 : 참
if(a <= b) // a 보다 b가 크거나 같다 : 참
if(a > b) // a 가 b보다 크다 : 거짓
if(a >= b) // a 가 b보다 크거나 같다 : 거짓
if(a == b) // a 와 b가 같다 : 거짓

Person p = new Person();
System.out.println(p instanceof Person); // p가 Person의 객체인지 참, 거짓으로 구분 : 참
```


### 비트 연산자(&, |, ^, ~)
데이터를 비트단위로 연산할 수 있는 연산자로 정수형또는 논리형에만 사용할 수 있다.
```java
System.out.println(0&1); // 비트 단위의 논리곱(AND)
System.out.println(5|1); // 비트 단위의 논리합(OR)
System.out.println(0^1); // 비트 단위의 배타적 논리합(AND)
System.out.println(~1); // 비트 단위의 보수(부정)
System.out.println(0>>2); // 0을 2 만큼 오른쪽으로 이동시킴. 이동한 만큼의 왼쪽 비트는 부호 확장이 발생
System.out.println(0>>>1); // 부호 확장이 없고 이동한 만큼의 왼쪽 비트는 항상 0 으로 채운다

System.out.println(true&true);
System.out.println(true^false);
```

### 논리 연산자(&&, ||, !)
비트 논리 연산자의 경우 연산 대상이 정수형과 논리형에 모두 가능하지만, 논리 연산자의 경우 논리형에만 적용할 수 있다.
```java
System.out.println(true && true);  //true
System.out.println(true && false); //false
System.out.println(true || true);  //true
System.out.println(true || false); //true
System.out.println(false || false);//false
System.out.println(!true);//false
System.out.println(!false;//true
```

### 삼항 연산자( ? : )
조건을 평가해서 소괄호 값이 참, 거짓이냐에 따라 수식1, 수식2 값을 대입한다.
```java
//조건 연산자 예제
int num1 = 10;
int num2 = 20;
int result = (false) ? num1 : num2;
System.out.println("결과 : "+ result);
```

## 연산자 우선순위
| 우선순위|  연산자   |
|:-------:|:-------- :|
| 1       | ()   []   .     
| 2       | ++ , - - , ~ , ! 
| 3       | * ,  / ,  %     
| 4       |  + ,  -         
| 5       | >> ,  >>> ,  << 
| 6       |  > ,  >= ,  < ,  <=      
| 7       | == , !=       
| 8       |   &     
| 9       |   ^     
| 10      |   ｜   
| 11      |   &&     
| 12      |   ｜｜     
| 13      |  a ? b : c    
| 14      |    =    


*tip. 우선순위에 상관 없이 ()를 사용하여 우선순위를 지정할 수 있다*